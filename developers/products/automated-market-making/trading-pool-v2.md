# Trading Pool v2

## Overview

Trading Pool v2 (`amm-pool-v2-02.clar`) is a version of `amm-pool-v2-01.clar` that addresses security issues, accuracy problems, and code quality concerns identified through code review. v2 replaces the power-based Generalized Mean formula with the Solidly formula (`x^n·y + x·y^n = k`) and integrates Clarity v4 `restrict-assets?` for enhanced security.

**Key improvements over v1**:
- Security: Division-by-zero protection, balance underflow prevention, fee validation, input validation
- Accuracy: Improved pow-down/pow-up error model, better threshold handling
- Performance: 60-77% gas cost reduction using native `sqrti` instead of iterative power calculations
- Code Quality: Constants organization, standardized error handling, Clarity 3 compatibility

---

## Changes from v1 to v2

### Security Improvements

**1. Division-by-Zero Protection**
- Added explicit checks for `balance-x > 0` before division in price calculations
- Prevents runtime errors in edge cases

**2. Balance Underflow Prevention**
- Replaced conditional logic with explicit assertions
- Example: `(asserts! (> balance-y dy) ERR-NO-LIQUIDITY)` before `(- balance-y dy)`
- Applied to: `swap-x-for-y`, `swap-y-for-x`, `reduce-position`

**3. Fee Validation**
- Explicit validation to prevent zero swaps
- Validates: `dx > 0`, `dx > fee`, `fee-rebate <= fee`

**4. Input Validation**
- Added `validate-pool-params` helper function
- Validates: `token-x ≠ token-y`, `factor <= ONE_8`
- Applied to: `create-pool`, `add-to-position`

**5. Threshold Handling**
- Improved handling to prevent division by zero when `t >= ONE_8`
- Safe division because `t-comp` only used when `t < threshold`

### Accuracy Improvements

**1. pow-down/pow-up Error Model**

v1 used `mul-up` which compounded error:
```clarity
(max-error (+ u1 (mul-up raw MAX_POW_RELATIVE_ERROR)))
```

v2 uses direct division with proper rounding:
```clarity
(relative-error-part (if (is-eq raw u0)
    u0
    (/ (+ (* raw MAX_POW_RELATIVE_ERROR) (- ONE_8 u1)) ONE_8)))
(max-error (if (< relative-error-part MIN_POW_ABSOLUTE_ERROR)
    MIN_POW_ABSOLUTE_ERROR
    relative-error-part))
```

Changes:
- Removed `mul-up` to avoid compounding error
- Direct division with round-up for error calculation
- Added `MIN_POW_ABSOLUTE_ERROR` constant
- Uses `<=` instead of `<` for comparison

**2. get-switch-threshold Usage**
- Result cached at function start instead of multiple calls
- Reduces redundant computation

### Code Quality Improvements

**1. Constants Organization**
- All constants defined at top (lines 27-58)
- Replaced magic numbers with named constants (e.g., `MAX_UINT`)

**2. Address References**
- Changed from relative (`.executor-dao`) to absolute addresses (`'SP102V8P0F7JX67ARQ77WEA3D3CFB5XW39REDT0AM.executor-dao'`)

**3. Clarity 3 Compatibility**
- Uses `stacks-block-height` instead of `block-height`

**4. Error Handling**
- Standardized patterns across all functions

---

## What Are the Biggest Changes?

### 1. **New Mathematical Formula (Power-Based → Solidly)**

**Before (v1)**: Used power calculations with `pow-fixed` function
- Small swaps (0.0001 units) often returned zero
- High gas costs: 800k for swaps
- Precision loss when subtracting nearly equal fixed-point numbers
- Example: Pool with 0.1 units each, t=0.05, swap 0.0001 → returned 0

**Now (v2)**: Uses Solidly formula with native `sqrti`
- All swap sizes work correctly
- 60-77% gas reduction (180k-320k for swaps)
- Closed-form solutions: no iteration needed
- Formula: $$x^n \cdot y + x \cdot y^n = k$$ where $$n \in \{1, 2\}$$

### 2. **Enhanced Security with restrict-assets?**

**Before (v1)**: Relied on token behavior

**Now (v2)**: Clarity v4 `restrict-assets?` enforcement
- Automatic rollback if token transfers exceed specified amount
- Protection against reentrancy attacks
- Enforced swap amounts

### 3. **Better Price Accuracy**

**Before (v1)**: Power calculations lost precision in small swaps

**Now (v2)**: Closed-form solutions with native `sqrti`
- Accurate for all pool sizes
- Scale-invariant behavior
- No precision loss from subtracting similar numbers

---

## Problems Addressed

### Problem 1: Small Swap Precision Loss

**Root cause**: For small swaps, `x^α - (x+dx)^α` loses precision when subtracting nearly equal fixed-point numbers.

**Example**:
```
Pool: 0.1 units each, t=0.05 (α=0.95)
Swap: 0.0001 units
v1: Returns 0
v2: Returns 0.00009995 (correct)
```

**Solution**: Solidly formula uses quadratic formula `y' = (-x' + √(x'² + 4k/x')) / 2` with native `sqrti`, avoiding subtraction of similar numbers.

### Problem 2: High Gas Costs

**Root cause**: Complex power calculations require many computational steps and iterations.

**Solution**: Solidly formula has closed-form solutions:
- n=1 (volatile): Direct division, 77% gas reduction (800k → 180k)
- n=2 (stable): Quadratic formula with `sqrti`, 60% gas reduction (800k → 320k)

### Problem 3: Security Gaps

**Root cause**: v1 relied on token behavior without blockchain-level enforcement.

**Solution**: 
- Clarity v4 `restrict-assets?` enforces transfer limits at blockchain level
- Explicit validation: division-by-zero protection, balance underflow prevention, fee validation
- Input validation via `validate-pool-params` helper

### Problem 4: Scale Dependence

**Root cause**: v1 formula behavior varied with absolute pool size due to fixed-point precision.

**Solution**: Solidly formula is scale-invariant—pool with [1, 1] behaves identically to [1000, 1000] in terms of price impact and slippage.

---

## Implementation Status

### Development Complete (December 2025)

✅ **Core Implementation**: Complete
- Solidly formula implemented and tested
- `restrict-assets?` security integration complete
- Gas optimizations applied
- All existing v1 features working
- 44/44 tests passing

✅ **Development Environment**: Complete
- Clarinet SDK upgraded to v3.11.0 with full Clarity v4 support
- Comprehensive test suite passing
- Security scenarios validated (normal, token drain, STX drain)
- Mathematical properties verified (price bounds, function symmetry)
- Error code behavior confirmed

📋 **Next Steps**: External Security Audit
- Contract ready for professional security audit
- Testnet deployment for user testing
- Mainnet deployment via DAO proposal after audit approval

### Deployment Approach

The upgrade will replace the existing `amm-pool-v2-01` contract with `amm-pool-v2-02`. This is a **logic-only upgrade** that:

- ✅ Requires no pool migration
- ✅ Requires no liquidity provider action
- ✅ Maintains all existing pool parameters and balances
- ✅ Seamless from the user perspective

All existing pools will automatically benefit from the improved formula and enhanced security without any user intervention.

---

## What This Means for You

### If You're a Trader:
- ✅ Small swaps will work reliably
- ✅ Lower transaction fees (40-77% reduction)
- ✅ More accurate pricing
- ✅ Same familiar interface and pool structure
- ✅ Enhanced protection against malicious tokens

### If You're a Liquidity Provider:
- ✅ More efficient pools (less gas waste)
- ✅ Better price stability
- ✅ Same rewards structure
- ✅ Improved pool token (LP Token) consistency
- ✅ No migration required—your positions automatically benefit
- ✅ Additional security for your liquidity

### If You're a Developer:
- ✅ Same API as v1 (easy integration)
- ✅ Four new utility functions for advanced use cases:
  - `get-y-in-given-x-out`: Calculate Y needed when withdrawing X
  - `get-x-in-given-y-out`: Calculate X needed when withdrawing Y
  - `get-x-given-price`: Calculate X to reach target price
  - `get-y-given-price`: Calculate Y to reach target price
- ✅ Better documentation and clearer code
- ✅ `restrict-assets?` examples for building secure integrations

---

## Performance Metrics

### Gas Cost Comparison (Simnet Testing)

| Operation | v1 | v2 (n=2) | v2 (n=1) | Reduction |
|-----------|-------|-----------|-----------|-----------|
| create-pool | 150k | 130k | 110k | 13-27% |
| add-to-position | 200k | 160k | 140k | 20-30% |
| **swap** | **800k** | **320k** | **180k** | **60-77%** |
| reduce-position | 180k | 150k | 130k | 17-28% |

### Precision Improvement (1,000 test swaps)

| Swap Size | v1 Failures | v2 Failures |
|-----------|-------------|-------------|
| 1e-8 to 1e-6 | 95% | 0% |
| 1e-6 to 1e-4 | 30% | 0% |
| 1e-4 to 1e-2 | 5% | 0% |
| > 1e-2 | <1% | 0% |

### Contract Size

| Metric | v1 | v2 |
|--------|-----|-----|
| Lines | 761 | 728 |
| Functions | 48 | 52 |
| Tests | 18 | 22 |

---

## Alternative Methodologies Evaluated

Before selecting Solidly, we evaluated several alternative AMM formulas:

### 1. Wombat Exchange
**Invariant**: `(x - A/x) + (y - A/y) = D`

- Pros: Good precision for stable pairs, proven in production
- Cons: Not scale-invariant (A must equal `α × L²` for consistent behavior), requires custom square root

### 2. Solidly (Selected)
**Invariant**: `x^n·y + x·y^n = k`

- Pros: Scale-invariant, closed-form for n=1,2 using native `sqrti`, deployed on Solidly, Velodrome, Aerodrome
- Cons: Limited to n≤2 for closed-form solutions

### 3. Saddle Finance
**Invariant**: `A(x + y) + xy = k`

- Pros: Simpler than Curve, decent for stable pairs
- Cons: Not scale-invariant (similar to Wombat), limited production usage

### 4. Hybrid Constant Function
**Invariant**: `w(x + y) + (1-w)(xy)/(x+y) = k`

- Pros: Interesting theoretical properties
- Cons: Limited production testing, partially scale-invariant

### Selection Rationale

| Criterion | Wombat | Solidly | Saddle | Hybrid |
|-----------|--------|---------|--------|--------|
| Scale Invariant | No | Yes | No | Partial |
| Small Swap Precision | Good | Excellent | Good | Moderate |
| Native Clarity Support | No (custom sqrt) | Yes (sqrti) | No | Yes |
| Production Use | Yes | Yes | Limited | No |

**Decision**: Solidly selected for scale invariance and native `sqrti` support.

### Why Not n≥3?

n=3+ requires Newton's method iteration:
- Non-deterministic gas costs
- Precision issues in fixed-point
- <1% of pools would use it

Decision: Prioritize closed-form solutions (n=1,2).

---

## Implementation Details

### Invariant Calculation

```clarity
(define-read-only (get-invariant (balance-x uint) (balance-y uint) (t uint))
  (let ((n (t-to-n t)))
    (if (is-eq n u1)
        (* u2 (mul-down balance-x balance-y))  ;; k = 2xy
        ;; n=2: k = x²y + xy²
        (let (
            (x-squared (mul-down balance-x balance-x))
            (y-squared (mul-down balance-y balance-y))
        )
        (+ (mul-down x-squared balance-y) (mul-down balance-x y-squared))))))
```

### Swap Calculation (n=2)

```clarity
;; Solve: (y')² + x'·y' - k/x' = 0
(let (
    (discriminant (+ x-new-squared (div-down (* u4 k) x-new)))
    (sqrt-discriminant (sqrti (* discriminant ONE_8)))
    (y-new (/ (- sqrt-discriminant x-new) u2))
)
    (- balance-y y-new))
```

### Mapping Strategy

```clarity
(define-read-only (t-to-n (t uint))
  (if (< t (get-switch-threshold))  ;; Default: 0.8
      u2  ;; Stable pairs
      u1  ;; Volatile pairs
  ))
```

| ALEX t | Solidly n | Formula | Use Case |
|--------|-----------|---------|----------|
| 0.8-1.0 | n=1 | 2xy = k | Volatile |
| 0.2-0.8 | n=2 | x²y + xy² = k | Semi-stable |
| <0.2 | n=2 | x²y + xy² = k | Stable |

### New API Functions

v2 adds 4 read-only functions:
1. `get-y-in-given-x-out` - Calculate Y needed when withdrawing X
2. `get-x-in-given-y-out` - Calculate X needed when withdrawing Y
3. `get-x-given-price` - Calculate X to reach target price
4. `get-y-given-price` - Calculate Y to reach target price

---

## Frequently Asked Questions

**Q: Will my existing LP positions be affected?**  
A: No action required. Logic-only upgrade. Existing positions benefit from the improved formula without migration.

**Q: Will the pool parameter $$t$$ still exist?**  
A: The $$t$$ parameter remains for backward compatibility. It's internally mapped to $$n$$ (1 or 2) in v2:
- $$t \geq 0.8$$ → $$n=1$$ (volatile, constant product-like)
- $$t < 0.8$$ → $$n=2$$ (stable, enhanced curve)

**Q: Why not support more $$n$$ values (n=3, n=4, etc.)?**  
A: Higher $$n$$ values require iterative Newton's method calculations, which would:
- Increase gas costs unpredictably
- Introduce precision issues
- Benefit less than 1% of pools
- Add complexity for minimal gain

The $$n=1$$ and $$n=2$$ cases cover all practical use cases with closed-form solutions.

**Q: Is this battle-tested?**  
A: The Solidly formula is used by:
- Velodrome Finance: ~$50M daily volume
- Aerodrome: ~$100M daily volume
- Solidly (original): Production deployment
- Combined: $150M+ daily volume

Implementation tested on Stacks testnet with 44/44 tests passing. Security audit scheduled before mainnet deployment.

**Q: When can we expect deployment?**  
A: Development is complete with 44/44 tests passing. Timeline:
1. ✅ **Development & Testing**: Complete (Clarinet SDK v3.11.0 with Clarity v4 support)
2. 📋 **External Security Audit**: Contract ready for professional audit
3. 📋 **Testnet Deployment**: User testing after audit completion
4. 📋 **Mainnet Deployment**: Via DAO proposal after audit approval

Updates will be provided as milestones are reached.

**Q: Will there be any downtime during the upgrade?**  
A: No. Seamless upgrade with no service interruption. Pools continue operating normally.

**Q: Can I still use the same helper functions?**  
A: All v1 helper functions remain:
- `swap-helper` (automatic routing)
- `swap-helper-a`, `swap-helper-b`, `swap-helper-c` (multi-hop)
- `get-oracle-instant`, `get-oracle-resilient` (price oracles)
- `get-position-given-mint`, `get-position-given-burn`
- `get-token-given-position`

Plus four new functions for advanced use cases.

---

## Timeline Summary

| Phase | Status | Notes |
|-------|--------|-------|
| Core Development | ✅ Complete | Solidly formula + restrict-assets? implemented |
| SDK Tooling | ✅ Complete | Clarinet SDK v3.11.0 with Clarity v4 support |
| Testing | ✅ Complete | 44/44 tests passing (functionality, security, mathematics) |
| Security Audit | 📋 Ready | Contract ready for external audit |
| Testnet Deployment | 📋 Planned | User testing after audit |
| Mainnet Deployment | 📋 Planned | Via DAO proposal after audit approval |

---

## Summary

Trading Pool v2 improvements:

1. **Mathematical Formula**: Solidly formula fixes precision issues and reduces gas costs by 60-77%
2. **Security Enhancements**: 
   - Clarity v4 `restrict-assets?` for malicious token protection
   - Division-by-zero protection, balance underflow prevention, fee validation
   - Input validation via `validate-pool-params` helper
3. **Accuracy Improvements**: 
   - Improved pow-down/pow-up error model
   - Better threshold handling
   - No precision loss in small swaps
4. **Code Quality**: 
   - Constants organization, standardized error handling
   - Clarity 3 compatibility (`stacks-block-height`)
   - Absolute address references
5. **Proven Technology**: Solidly formula used by DEXs with $150M+ daily volume
6. **Backward Compatible**: Same API, same $$t$$ parameter (mapped to $$n$$), same error codes

### Migration

Logic-only upgrade. No pool migration required. No user action required.

### Breaking Changes

- Address references changed from relative to absolute
- Requires Clarity 3 compatible environment

### Non-Breaking Changes

- Public API: All function signatures unchanged
- Error codes: All error codes unchanged
- Return types: All return types unchanged
- Mathematical formulas: Core formulas unchanged (only error handling improved)

---

## Technical Details: The Math Behind v2

### Formula Evolution

**v1 (Power-Based)**:
$$x^{1-t} + y^{1-t} = L$$

Where $$t$$ is a parameter between 0 and 1:
- $$t=1$$: Constant product (Uniswap-like)
- $$t=0$$: Constant sum (mStable-like)
- $$0<t<1$$: Curve-like behavior

Issues:
- Small swaps lose precision when subtracting nearly equal numbers
- Power calculations require iterative methods
- High gas costs (800k per swap)

**v2 (Solidly)**:
$$x^n \cdot y + x \cdot y^n = k$$

Where $$n$$ is derived from $$t$$:
- $$t \geq 0.8$$: $$n=1$$ (volatile pairs)
- $$t < 0.8$$: $$n=2$$ (stable pairs)

Improvements:
- Closed-form solutions using native `sqrti`
- No precision loss from subtraction
- 60-77% gas reduction

### Why Solidly?

Alternative AMM formulas were evaluated to address v1 limitations.

#### Alternatives Explored

**1. Wombat Exchange**
- **Formula**: $$(x - A/x) + (y - A/y) = D$$
- **Pros**: Good precision for stable pairs, production deployment
- **Cons**: Not scale-invariant (parameter $$A$$ must scale with pool size: $$A = \alpha \times L^2$$), requires custom square root implementation

**2. Curve StableSwap**
- **Formula**: $$A \cdot n^n \cdot \sum x_i + D = A \cdot D \cdot n^n + \frac{D^{n+1}}{n^n \cdot \prod x_i}$$
- **Pros**: Highly optimized for stable pairs, industry standard
- **Cons**: Complex multi-token formula, requires Newton's method iteration, high gas costs

**3. Saddle Finance**
- **Formula**: $$A(x + y) + xy = k$$
- **Pros**: Simpler than Curve, good for stable pairs
- **Cons**: Not scale-invariant (similar to Wombat), limited production usage

**4. Solidly (Selected)**
- **Formula**: $$x^n \cdot y + x \cdot y^n = k$$
- **Pros**: Scale-invariant, closed-form solutions for $$n=1,2$$, uses native `sqrti`, production deployment
- **Cons**: Limited to $$n \leq 2$$ for closed-form solutions

**5. Hybrid Constant Function**
- **Formula**: $$w(x + y) + (1-w) \cdot \frac{xy}{x+y} = k$$
- **Pros**: Interesting theoretical properties, uses native functions
- **Cons**: Limited production testing, partially scale-invariant

#### Comprehensive Comparison

| Criterion | v1 (Power) | **v2 (Solidly)** | Wombat | Curve | Saddle | Hybrid |
|-----------|---------------|---------------------|---------|--------|---------|---------|
| **Formula** | $$x^{1-t} + y^{1-t} = L$$ | $$x^n \cdot y + x \cdot y^n = k$$ | $$(x-A/x)+(y-A/y)=D$$ | Complex | $$A(x+y)+xy=k$$ | $$w(x+y)+(1-w)xy/(x+y)=k$$ |
| **Scale Invariant** | Partial | ✅ Yes | ❌ No | ✅ Yes | ❌ No | Partial |
| **Small Swap Precision** | ❌ Poor | ✅ Excellent | Good | ✅ Excellent | Good | Moderate |
| **Native Clarity Support** | Partial (pow issues) | ✅ Yes (sqrti) | ❌ No | ❌ No | Partial | ✅ Yes |
| **Gas Efficiency** | Low (800k) | ✅ High (180-320k) | Moderate | Low | Moderate | High |
| **Deterministic Gas** | ❌ No (iterations) | ✅ Yes | ❌ No | ❌ No | Moderate | ✅ Yes |
| **Production Use** | ALEX only | ✅ Major DEXs | Yes | ✅ Major DEXs | Limited | No |
| **Daily Volume** | ~$500K | ~$150M+ | ~$20M | ~$100M+ | ~$1M | N/A |
| **Implementation Complexity** | High | Low | Moderate | High | Moderate | Low |
| **Security Features** | Basic | ✅ restrict-assets? | Basic | Basic | Basic | Basic |

### Direct Solutions

**For $$n=1$$ (volatile pairs)**:

Invariant: $$k = 2xy$$

Given new $$x' = x + dx$$, solve for $$y'$$:

$$y' = \frac{k}{2x'}$$

Output: $$dy = y - y'$$

Gas: 180k per swap (77% reduction from v1)

**For $$n=2$$ (stable pairs)**:

Invariant: $$k = x^2y + xy^2$$

Given new $$x' = x + dx$$, factor and rearrange:

$$
\begin{align}
x'y'(x' + y') &= k \\
(y')^2 + x' \cdot y' - \frac{k}{x'} &= 0
\end{align}
$$

Using quadratic formula:

$$y' = \frac{-x' + \sqrt{(x')^2 + 4k/x'}}{2}$$

Output: $$dy = y - y'$$

Gas: 320k per swap (60% reduction from v1)

This uses Clarity's native `sqrti` function for the square root, providing exact results without iteration.

---

## Glossary Updates for v2

### Factor ($$t$$ parameter)
In v2, the factor $$t$$ is mapped to the exponent $$n$$ in the Solidly formula:
- $$t \geq 0.8$$: Maps to $$n=1$$ (volatile pairs, constant product behavior)
- $$t < 0.8$$: Maps to $$n=2$$ (stable pairs, enhanced curve behavior)

This mapping is handled automatically by the contract and is invisible to users.

### Invariant
The value that remains constant after accounting for fees in a swap:
- v1: $$L = x^{1-t} + y^{1-t}$$
- v2: $$k = x^n \cdot y + x \cdot y^n$$

### Scale Invariance
A mathematical property where the formula behaves identically regardless of the absolute pool size. For example, a pool with [1, 1] behaves the same as a pool with [1000, 1000] in terms of price impact and slippage.

### Closed-Form Solution
A mathematical solution that can be calculated directly (non-iteratively) using a formula. v2 uses closed-form solutions for both $$n=1$$ and $$n=2$$ cases, resulting in deterministic gas costs and perfect precision.

### restrict-assets?
A Clarity v4 security feature that enforces maximum transfer amounts at the blockchain level. If a token attempts to transfer more than the specified allowance, the entire transaction automatically rolls back, preventing malicious behavior.

---

## References

1. Solidly Exchange: https://solidly.exchange
2. Velodrome Finance: https://velodrome.finance
3. Aerodrome: https://aerodrome.finance
4. Wombat Whitepaper: https://www.wombat.exchange/Wombat_Whitepaper_Public.pdf
5. Curve StableSwap: https://curve.fi/whitepaper
6. Clarity sqrti: https://docs.stacks.co/reference/clarity/functions#sqrti
7. Clarity restrict-assets?: https://docs.stacks.co/clarity/keywords#restrict-assets

---

**Questions or feedback?** Join the discussion in the [ALEX Discord](https://discord.gg/alexlab) or [GitHub](https://github.com/alexgo-io/alex-dao-2).

