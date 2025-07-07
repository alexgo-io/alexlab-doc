---
description: >-
  ALEX AMM v3, also known as the Discrete Automated Market Maker (DAMM), is coming soon! 
---

# ALEX AMM v3

## Abstract

The ALEX AMM v3 contract is an enhanced version of the Automated Market Making (AMM), optimized for concentrated liquidity. It utilizes the invariant function $(Vx + x) * (Vy + y) = K$, which, with appropriately chosen virtual liquidity values $Vx$ and $Vy$, allows the AMM to focus liquidity within a specific price range $[P_{start}, P_{end}]$.

## Math

The invariant function is:

$$
(Vx + x) * (Vy + y) = K
$$

Where $Vx$ and $Vy$ ensure the pair is traded in the price range $[P_{start}, P_{end}]$.

$$
Vx = f_x(P_{start}, P_{end}, x, y)
$$

$$
Vy = f_y(P_{start}, P_{end}, x, y)
$$

In order to simply the math, we segregate the price range $(0, \infty)$ by introducing an integer parameter $tick$ and bin size $bs$, where for each $tick$ we have a price range $P_{start} = (1 + 0.01 * bs)^{tick}$ and $P_{end} = (1 + 0.01 * bs)^{tick + 1}$.

We define $t = \sqrt{1 + 0.01 * bs}$ and $p = P_{start}$, then we have:

$$
P_{end} = t^2 * P_{start} = pt^2
$$

The price of the pair is $P_{start}$ when balance x is swapped out (i.e. $\Delta x = -x$), and is $P_{end}$ when balance y is swapped out (i.e. $\Delta y = -y$). Hence:

$$
p = \frac{Vx}{Vy + y + \Delta y} = \frac{Vx^2}{Vx * (Vy + y + \Delta y)} = \frac{Vx^2}{K}
$$

$$
pt^2 = \frac{Vx + x + \Delta x}{Vy} = \frac{Vy * (Vx + x + \Delta x)}{Vy ^ 2} = \frac{K}{Vy^2}
$$

Hence:

$$
p^2t^2 = \frac{Vx^2}{Vy^2}
$$

$$
Vx = ptVy
$$

So:

$$
pt^2 = \frac{K}{Vy^2} = \frac{(Vx + x)(Vy + y)}{Vy^2} = \frac{(ptVy + x)(Vy + y)}{Vy^2}
$$

$$
p(t^2 - t)Vy^2 - (x + pty)Vy - xy = 0
$$

$$
Vy = \frac{x + pty + \sqrt{(x + pty)^2 + 4p(t^2 - t)xy}}{2p(t^2 - t)}
$$

$$
Vx = \frac{x + pty + \sqrt{(x + pty)^2 + 4p(t^2 - t)xy}}{2(t - 1)}
$$

## Swap x for y util price hit $P_{max}$

This is similar to Immediate or Cancel (IOC) order in orderbook, given $\Delta x$, swap as much as possible until the price hit $P_{max}$, where $P_{max}$ is within the price range $[P_{start}, P_{end}]$.

$$
P_{max} = \frac{Vx + x + \Delta x_{max}}{Vy + y - \Delta y}
$$

$$
K * P_{max} = (Vx + x + \Delta x_{max})^2
$$

$$
\Delta x_{max} = \sqrt{K * P_{max}} - (Vx + x)
$$

$$
\Delta x_{swappable} = min(max(0, \Delta x_{max}), \Delta x)
$$

$$
\Delta y = (Vy + y) - \frac{K}{Vx + x + \Delta x_{swappable}}
$$

## Swap y for x util price hit $P_{min}$

Likewise, given $\Delta y$, swap as much as possible until the price hit $P_{min}$, where $P_{min}$ is within the price range $[P_{start}, P_{end}]$.

$$
P_{min} = \frac{Vx + x - \Delta x}{Vy + y + \Delta y_{max}}
$$

$$
\frac{K}{P_{min}} = (Vy + y + \Delta y_{max})^2
$$

$$
\Delta y_{max} = \sqrt{\frac{K}{P_{min}}} - (Vy + y)
$$

$$
\Delta y_{swappable} = min(max(0, \Delta y_{max}), \Delta y)
$$

$$
\Delta x = (Vx + x) - \frac{K}{Vy + y + \Delta y_{swappable}}
$$

## Add liquidity

After adding $\Delta x$ and $\Delta y$ to the pool, the pool size (i.e. liquidity token balance) and token pair price will both be affected.

$$
Price = \frac{V_x' + x + \Delta x}{V_y' + y + \Delta y}
$$

The price should be checked to prevent unexpected deviation from other markets.

And the pool size increase proportionally to the virtual balances.

$$
L_p' = L_p * \frac{V_x'}{V_x} = L_p * \frac{V_y'}{V_y}
$$

This is based on the fact that swapping does not change $V_x$, $V_y$, and the pool size. So when token y is depleted, i.e. $y = 0$, the balance of token x represents the total value of the pool:

$$
V_x = \frac{x + pty + \sqrt{(x + pty)^2 + 4p(t^2 - t)xy}}{2(t - 1)} = \frac{x}{t-1}
$$

$$
x = (t-1)*V_x
$$

$$
L_p' = L_p * \frac{x'}{x} = L_p * \frac{(t-1)*V_x'}{(t-1)*V_x}= L_p * \frac{V_x'}{V_x}
$$

The same when token x is depleted, i.e. $x = 0$, the balance of token y represents the total value of the pool:

$$
Vy = \frac{x + pty + \sqrt{(x + pty)^2 + 4p(t^2 - t)xy}}{2p(t^2 - t)} = \frac{y}{t-1}
$$

$$
y = (t-1)*V_y
$$

$$
L_p' = L_p * \frac{y'}{y} = L_p * \frac{(t-1)*V_y'}{(t-1)*V_y}= L_p * \frac{V_y'}{V_y}
$$

## Reduce liquidity

If we change the existing pool balance proportionally, we get the new invariant function:

$$
(\sigma Vx + \sigma x) * (\sigma Vy + \sigma y) = \sigma ^2 K
$$

$$
Price = \frac{\sigma Vx + \sigma x}{\sigma Vy + \sigma y} = \frac{Vx + x}{Vy + y}
$$

Hence changing the existing pool balance proportionally does not affect the price of the pair. So when adjusting the liquidity, for a given $\Delta x$ we have:

$$
\frac{y - \Delta y}{x - \Delta x} = \frac{y}{x}
$$

$$
\Delta y = \frac{y}{x} * \Delta x
$$

## Appendix

### Implement pow-fixed in Clarity

The pow-fixed function needed for AMM v3 is defined as:

$$
pow(x, n) = x ^ n
$$

Where x is a fixed point number with precision $10^8$, and n is an integer.

To simplify the calculation in Clarity, we assume only a limited set of bin sizes are supported (e.g. 5%, 10%, and 20%), and the price range falls between 0.00000001 and 100000000. And then we can pre-calculate the result for $(1 + bs) ^ {(2 ^ n)}$.

```clarity
(define-constant PRICES_5 (list u26574222192236 u51550191262 u2270466719 u476494146 u218287458 u147745544 u121550625 u110250000 u105000000))
(define-constant PRICES_10 (list u19873012250342 u44579156845 u2111377674 u459497298 u214358881 u146410000 u121000000 u110000000))
(define-constant PRICES_20 (list u11684220576272 u34182189187 u1848842588 u429981695 u207360000 u144000000 u120000000))
```

So that for a given tick, we have:

$$
tick = \sum_{i=n}^{0} (abs(tick \& (2^i)) * (2^i))
$$

$$
Price = \prod_{i=n}^{0} (1 + 0.01 * bs)^{abs(tick \& (2^i)) * (2^i)}
$$

This mathematical optimization reduce the calculation complexity exponentially.

## Calculate Virtual Balances in Clarity

Since there's no float point numbers in clarity, we use fixed decimal to calculate values, specifically using uint128 to represent a decimal with 8 fixed decimal places. So the calculations should be handled very cautiously in order to prevent precision loss (with error rate less than roughly 1e-8) and arithmetic overflow.

This is how it looks like after we translate the formula of the virtual balances into code using float point numbers:

```javascript
const ts = 1 + 0.01 * bin;
const t = Math.sqrt(ts);
const price = ts ** tick;
// x + pty
const x_pty = balanceX + price * t * balanceY;
const denominator_vx = 2 * (t - 1);
const denominator_vy = 2 * (price * (ts - t));
const numerator =
  x_pty +
  Math.sqrt(x_pty ** 2 + 2 * denominator_vy * balanceX * balanceY);
const vx = numerator / denominator_vx;
const vy = numerator / denominator_vy;
```

Then we translate it into code using fixed decimal with 8 decimal places:

```javascript
const ONE_8 = 10n ** 8n;
const ONE_16 = 10n ** 16n;
// bin: 1n, 5n, 10n or 20n
const ts = ONE_8 + (10n ** 6n) * bin;
const t = Math.sqrt(ts * ONE_8);
const price = pow_fixed(ts, tick);
// x + pty
const x_pty = balanceX + price * t * balanceY / ONE_16;
const denominator_vx = 2n * (t - ONE_8);
const denominator_vy = 2n * (price * (ts - t) / ONE_8);
const numerator =
  x_pty +
  Math.sqrt(x_pty ** 2n + 2n * denominator_vy * balanceX * balanceY / ONE_8);
const vx = numerator * ONE_8 / denominator_vx;
const vy = numerator * ONE_8 / denominator_vy;
```

Now we consider the value ranges of the input:

+ balanceX, balanceY cap at 1000T=$10^{15}$: `[0n, 10n ** (8n + 15n)]`
+ Allowed price range: `[10n ** 4n, 10n ** (8n + 7n)]`
+ U128_MAX: `2n ** 128n - 1n` = `340282366920938463463374607431768211455n`, approximately `3.4e38`

When the values are small, there might be precision loss, for example:

+ When price and balanceY are small, e.g. price=1e4, balanceX=0, balanceY=1e3, `x_pty = 1e4 * 1e8 * 1e3 / 1e16 = 0` which should be `1e-9` in float point number, in this case `numerator = 2 * x_pty = 0` which should be `2e-9` in float point number, resulting `vx = 0` which should be `1e-9 / (1.01 ** 0.5 - 1) = 20.0498756211e-8` when `bin = 1`
+ When price is small, e.g. price=1e4, `denominator_vy = 2 * 1e4 * (1.01 - 1.01 ** 0.5) = 100`, which should be `100.2487577582`

And when values are huge, there might be overflow, for example when `balanceX > 2e19` then `x_pty > 2e19`, `x_pty ** 2n > U128_MAX`

To remediate that, we can scale balanceX and balanceY, to make max(balanceX, balanceY) be around `1e16`. This is based on the fact that virtual balances and balances scale proportionally, which is proved before. And do not divide by 1e8 so fast when getting `denominator_vy`.

So we get the first revised version:

```javascript
const ONE_8 = 10n ** 8n;
const ONE_16 = 10n ** 16n;
// bin: 1n, 5n, 10n or 20n
const ts = ONE_8 + (10n ** 6n) * bin;
const t = Math.sqrt(ts * ONE_8);
const price = pow_fixed(ts, tick);
// scale balances
const amplify_factor = max(1n, ONE_16 / (max(balanceX, balanceY) + 1n));
const shrink_factor = max(max(balanceX, balanceY) / ONE_16, 1n);
const bx_scaled = balanceX * amplify_factor / shrink_factor;
const by_scaled = balanceY * amplify_factor / shrink_factor;
// x + pty
const x_pty = bx_scaled + (t * by_scaled / ONE_8) * price / ONE_8;
const denominator_vx = 2n * (t - ONE_8);
const denominator_vy_e8 = 2n * price * (ts - t);
const numerator =
  x_pty +
  Math.sqrt(x_pty ** 2n + 2n * denominator_vy_e8 * bx_scaled * by_scaled / ONE_16);
const vx_scaled = numerator * ONE_8 / denominator_vx;
const vy_scaled = numerator * ONE_16 / denominator_vy_e8;
const vx = vx_scaled * shrink_factor / amplify_factor;
const vy = vy_scaled * shrink_factor / amplify_factor;
```

There are 2 issues with the first revision:

1. The max value of `x_pty` can be roughly `1e16 + 1e8 * 1e16 * 1e15 / 1e16`, which is `1e23`, this will cause `x_pty ** 2` to overflow when calculating the numerator
2. `denominator_vy_e8 * bx_scaled * by_scaled / ONE_16` should be handled cautiously to prevent precision loss

For the first issue we use the same scaling method:

```javascript
const x_pty = bx_scaled + (t * by_scaled / ONE_8) * price / ONE_8;
const x_pty_shrink_factor = max(x_pty / ONE_16, 1n);
const x_pty_scaled = x_pty / x_pty_shrink_factor;
const denominator_vx = 2n * (t - ONE_8);
const denominator_vy_e8 = 2n * price * (ts - t);
// numerator is also scaled accordingly (numerator_scaled = numerator / x_pty_shrink_factor) to avoid overflow in the following calculations, and is approximately between 1e16 and 1e17
const numerator_scaled =
  x_pty_scaled +
  Math.sqrt(
    x_pty_scaled ** 2n +
    2n * denominator_vy_e8 * bx_scaled * by_scaled / ONE_16 / (x_pty_shrink_factor ** 2)
  );
const vx_scaled = numerator_scaled * ONE_8 / denominator_vx;
const vy_scaled = numerator_scaled * ONE_16 / denominator_vy_e8;
const vx = vx_scaled * shrink_factor * x_pty_shrink_factor / amplify_factor;
const vy = vy_scaled * shrink_factor * x_pty_shrink_factor / amplify_factor;
```

Since both `denominator_vy_e8` and `x_pty_shrink_factor` scale proportionally to price, and `x_pty_shrink_factor` is greater than 1 when `price` is greater than approximately `1e8`, hence `denominator_vy_e8 / x_pty_shrink_factor` is greater than `1e12`. And also `x_pty_shrink_factor` cap at approximately `1e7` when `by_scaled` and `price` are with the maximum value.

Base on those, we can rewrite `2n * denominator_vy_e8 * bx_scaled * by_scaled / ONE_16 / (x_pty_shrink_factor ** 2)` into `2n * (denominator_vy_e8 / x_pty_shrink_factor) * (bx_scaled * by_scaled / ONE_16 / x_pty_shrink_factor)` to prevent precision loss.

Now we get final revision:

```javascript
const ONE_8 = 10n ** 8n;
const ONE_16 = 10n ** 16n;
// bin: 1n, 5n, 10n or 20n
const ts = ONE_8 + (10n ** 6n) * bin;
const t = Math.sqrt(ts * ONE_8);
const price = pow_fixed(ts, tick);
// scale balances
const amplify_factor = max(1n, ONE_16 / (max(balanceX, balanceY) + 1n));
const shrink_factor = max(max(balanceX, balanceY) / ONE_16, 1n);
const bx_scaled = balanceX * amplify_factor / shrink_factor;
const by_scaled = balanceY * amplify_factor / shrink_factor;
// x + pty
const x_pty = bx_scaled + (t * by_scaled / ONE_8) * price / ONE_8;
const x_pty_shrink_factor = max(x_pty / ONE_16, 1n);
const x_pty_scaled = x_pty / x_pty_shrink_factor;
const denominator_vx = 2n * (t - ONE_8);
const denominator_vy_e8 = 2n * price * (ts - t);
// numerator is also scaled accordingly (numerator_scaled = numerator / x_pty_shrink_factor) to avoid overflow in the following calculations, and is approximately between 1e16 and 1e17
const numerator_scaled =
  x_pty_scaled +
  Math.sqrt(
    x_pty_scaled ** 2n +
    2n * (denominator_vy_e8 / x_pty_shrink_factor) * (bx_scaled * by_scaled / ONE_16 / x_pty_shrink_factor)
  );
const vx_scaled = numerator_scaled * ONE_8 / denominator_vx;
const vy_scaled = numerator_scaled * ONE_16 / denominator_vy_e8;
const vx = vx_scaled * shrink_factor * x_pty_shrink_factor / amplify_factor;
const vy = vy_scaled * shrink_factor * x_pty_shrink_factor / amplify_factor;
```
