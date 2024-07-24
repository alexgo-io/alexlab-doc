# ALEX’s Automated Market Maker (AMM)

## **ALEX’s Automated Market Maker (AMM) — Short Version**

_ALEX’s_ core product is essentially a zero-coupon bond in conventional finance. A key benefit of this product is reduced uncertainty about a loan’s interest rate, resulting in better financial planning. Specifically, prior to entering a loan contract, borrowers and lenders secure the loan’s interest rate and tenor on _ALEX_.

## **1. Lending and Borrowing Process**

Let’s start with a concrete example:

Rachel has 100 USD. She wants to increase her 100 USD and thus chooses to lend her assets out. She decides to lend out her 100 USD for a fixed term of three months. Rachel goes to _ALEX’s_ interface and there she sees that “three-month ayUSD” is currently priced at 0.9 vs USD. Put simply, this means that 1 ayUSD gets her 0.9 USD. She takes her 100 USD and exchanges it for ayUSD. Given the current exchange rate, Rachel gets about 110 ayUSD. Now that three months have passed, Rachel can exchange her 110 ayUSD for USD again. The rate is 1 ayUSD to 1 USD. So Rachel gets 110 USD — that’s a gain of 10 USD over 3 months. Pretty sweet!

Here is the general story:

Borrowers and lenders enter a loan contract. Specifically, they swap a forward contract-based token called “ayToken” with “Token” — the underlying asset. For example, borrowers and lenders could swap ayUSD with USD but more generally, the lender lends out “Tokens” and obtains “ayToken” in return. The price of “Token” is lower than its par value. The contract starts when a lender deposits “Token” in an _ALEX_ pool. Then, upon expiration, the lender redeems the underlying asset, “Token”, at par value. Because the lender lent out their “Token” at a discounted price some time ago, and now redeems “Token” for par value, there is a profit.

In mathematical terms, interest rate _r_ is calculated as \*pₜ =\*1/_eʳᵗ_ where _pₜ_ is the spot price of ayToken and the interest rate is assumed to be compound. The formula utilizes one of the most fundamental concepts in asset pricing in that the present value is the discounted future value. In our example, _t =_ 1 and _r_ = \*\*log 1/0.9 ≈ 10%.

## **2. Automated Market Making (AMM) Protocol**

When designing AMM, _ALEX_ believes in the following:

(i) AMMs are mathematically neat and reflect economic supply and demand. For example, price should increase when supply is low or when demand is high;

(ii) AMMs are a type of mean which remains constant during trading activities. This approach is adopted by popular platforms, such as _Uniswap_, which employ algorithmic means; and

(iii) AMM can be interpreted through the lens of modern finance theory. Doing so enables _ALEX_ to grow and draw comparisons with conventional finance.

After extensive research, our beliefs led us to the AMM first proposed by _YieldSpace_. While we appreciate the mathematical beauty of their derivation, we adapt it in several ways with _ALEX_. For example, we replace a simple interest rate with a compounding interest rate. This change is in line with standard uses in financial pricing and modeling since the adoption of the Black-Scholes model. We also introduce a new capital efficiency scheme, as explained below.

In mathematical terms, our AMM can be expressed as:

_x ¹⁻ ᵗ + y ¹⁻ ᵗ = L_

where _x, y, t,_ and _L_ are, respectively, the balance of “Token”, the balance of “ayToken”, time to maturity, and a constant term when _t_ is fixed. Interest rate _r_ is defined as _r =_ log\*(y/x)\*, i.e. natural logarithm of the ratio of balance between “ayToken” and “Token”, while the price of “ayToken” with respect to “Token” is _(y/x)ᵗ._

Our design depicts an AMM in the form of a generalized mean. It makes economic sense because the shape of the curve is decreasing and convex. It incorporates time to maturity _t_, which is explicitly built-in to derive ayToken’s spot price. &#x20;

## **3. Liquidity Providers (LP) and Capital Efficiency**

LPs deposit both ayToken and Token in a pool to facilitate trading activities. LPs are typically ready to market-make on all possible scenarios of interest rate movements ranging from _−∞_ to _+∞._ However\*,\* part of the interest rates curve or movements will never be considered by market participants. One example of this occurs when the interest rate is negative. Although negative rates can be introduced in the fiat world by central bankers as a monetary policy tool, yield farmers in the crypto world are still longing everything to be positive. In _ALEX_, a positive rate refers to the spot price of ayToken not exceeding 1 and ayToken reserve being larger than Token.

Inspired by _Uniswap v3_, _ALEX_ employs virtual tokens — part of the assets that will never be touched, hence they are not required to be held by LPs.

![https://miro.medium.com/max/1400/1\*h06s2YnEFXi6L97lAlP2\_Q.png](https://miro.medium.com/max/1400/1\*h06s2YnEFXi6L97lAlP2\_Q.png)

Figure 1: _t =_ 0.5 and _L =_ 20. Blue line (IFC) satisfies _x ¹⁻ ᵗ + y ¹⁻ ᵗ = L,_ whereas red line (CEC) satisfies _x ¹⁻ ᵗ + (y+yᵥ) ¹⁻ ᵗ = L_. Virtual reserve _yᵥ_ = 100.

Figure 1 illustrates an example of adopting virtual tokens in the event of a positive interest rate. The blue line is the standard AMM. The blue dot marks an equal balance of Token and ayToken of _yᵥ_, meaning there is no (or a 0%) interest rate. _yᵥ_ is the boundary amount, as any amount lower than it will never be touched by an LP to avoid a negative rate, which is represented by the blue dashed line. Thus, _yᵥ_ is the virtual token reserve. Effectively, LP is market-making on the red line, which shifts the blue line lower by _yᵥ_. When ayToken is depleted as shown by the red dashed line, trading activities are suspended.

A numerical example provided in Table 1 shows capital efficiency with respect to various interest rates, assuming _t =_ 0.5 and _L =_ 20 for illustration’s sake. When the current interest rate _r =_ 10%, LPs are required to deposit 95 Token and 105 ayToken according to standard AMM. However, if the interest rate is floored at 0%, LPs only need to contribute 5 ayToken, as the rest 100 ayToken would be virtual. This is a decent saving of more than 90%.

![https://miro.medium.com/max/1400/1\*1donSHtKYaEUb3Y7d9ZwbA.png](https://miro.medium.com/max/1400/1\*1donSHtKYaEUb3Y7d9ZwbA.png)

## **4. Yield Curve and Yield Farming**

By expressing interest rate as _pₜ =1/eʳᵗ_, i.e. r = (-1/_t)_ log _pₜ_, we can obtain a series of interest rates from trading pool prices with respect to various maturities based on which we are able to build a yield curve. The yield curve is the benchmark tool for modeling risk-free rates in conventional finance. The shape of the curve dictates the expectation of future interest rate paths, which helps market participants understand market behaviors and trends. Currently, we might be able to build a Bitcoin yield curve from Bitcoin futures listed on Chicago Mercantile Exchange (CME). However, not only is the exchange heavily regulated, its trading volume is skewed to the very short-dated front-end contracts lasting several months only. _ALEX_ aims to offer futures contracts up to 1y when the platform goes live. Should markets mature, _ALEX_ may extend to longer tenors.

Yield farmers can benefit from understanding the yield curve by purchasing ayToken whose tenor corresponds to high interest rates and selling ayToken whose tenor associates with low interest rates. This is a typical “carry” strategy.

Last but certainly not least, based on the development of a yield curve and the solid design work of our AMM, _ALEX_ is able to provide more products. Specifically, _ALEX_ will be able to offer derivatives, including options and structured products, building on and extending a large number of influential works of literature and applications in conventional finance.
