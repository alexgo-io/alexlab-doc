# 📃 Whitepaper (2): Automated Market Making of the Collateral Rebalancing Pooltitled



## Whitepaper (2): **Automated Market Making of the Collateral Rebalancing Pool**

## **Abstract**

The collateral pools of many DeFi platforms are typically comprised of a single asset reflecting a borrower’s crypto ownership and risk appetite. While single asset pools benefit from asset appreciation, a pool’s value can diminish swiftly in volatile market conditions. The increasing chance of default and potential shortening of the loan term affect both borrowers and lenders who enter fixed-term and fixed-rate contracts hoping to remove uncertainties.

Unlike many DeFi platforms, ALEX uses diversified rather than single collateral pools. Diversified pools consist of a risky asset and risk-free asset. As a result, diversified pools reduce default risk while maintaining potential upside gains. Diversified pools are similar to portfolios with equity and government bonds, where the former represents the risky asset while the latter represents the risk-free asset. Importantly, diversified collateral pools are systematically managed. An algorithmic engine dynamically adjusts the split of the risky and risk-free asset in the diversified pool, based on Black-Scholes’ model.

ALEX’s algorithmic engine and diversified pools minimize the risk of a borrower defaulting. The result is a smoother lending and borrowing experience. Parties have more peace of mind, are interrupted less frequently, and achieve robust returns even in volatile market conditions. This represents a radical improvement over existing alternatives.

## **Introduction**

Protocols for loanable funds (PLF) enable borrowing and lending activities. Examples PLFs are Compound and Aave on Ethereum. The lender provides a token in need and earns interest in return. The borrower deposits collateral and gets access to a preferred asset. The borrower must pay back the borrowed asset in due time. Protocols enabling this borrowing and lending functionality are incredibly useful. Simply, they enable the present consumption on future earnings. This idea is powerful, and has been at the core of DeFi’s rise, including the rise of protocols such as Uniswap.

![https://miro.medium.com/max/1400/1\*Dj-HeVOc9nH1C7GNnbIBLw.gif](https://miro.medium.com/max/1400/1\*Dj-HeVOc9nH1C7GNnbIBLw.gif)

Simulation of ALEX’s AMM of Collateral Rebalancing Pool during high market volatility

However, one of the risks posed to market participants in existing PLFs is default risk. While each loan must be secured with collateral, the price of crypto collateral can fluctuate wildly and quickly. As a result, many PLFs ask borrows to significantly overcollateralise their positions. Overcollateralisation refers to value of collateralised assets being higher than the value of the loaned assets. The proportion of the collateral value to loaned value is often called “collateralisation ratio” (CR), the inverse of “loan to value” (LTV). For simplicity sake, we use the term LTV throughout the paper. The higher the LTV is, the more likely the default occurs. A LTV larger than 1 means the value of collateral cannot cover the value of the loaned asset.

In variable rate platforms, such as Aave, collateral in the form of more liquid assets tends to have a higher LTV. In fixed-rate fixed-term protocols, such as YieldSpace, using ETH as collateral to borrow Dai requires a LTV of 67%. In the event that the portfolio is underfunded, three scenarios could emerge in the existing protocols: (i) a borrower could top up the collateral asset to stay afloat; (ii) a borrower could return some of the borrowing asset to decrease the LTV; and (iii) the loan could be unwound by a third party such as liquidator if the borrower defaults. A third party unwinds a borrower’s position by paying back the loan, and in return earns certain fees. In cases when a collateral asset is illiquid, fees can be as high as 15% on Aave, representing a significant penalty to defaulting borrowers. This also poses disruption to borrowing/lending activity, as a pre-agreed loan is terminated early.

ALEX abolishes liquidation. ALEX keeps the loan active until maturity, regardless of market condition, solving problems plaguing many existing PLFs. The basis for ALEX’s superior solution is based on an innovative combination of asset management and collateral pools. This is how it works.

First, unlike many others, ALEX does not use a static collateral pool with a single asset. Instead, ALEX maintains robust performance in the collateral pool by splitting the deposited asset between a risky and a riskless asset. The collateral pool systematically rebalances the allocation of these two assets based on market conditions. Typically, the better the performance of one asset relative to the other asset, the higher its relative allocation. In mathematical terms, weight is calculated and modified from option delta derived from Black-Scholes model.

So the collateral pool consists of two assets. This opens up new opportunities. For example, ALEX can enable borrowers to gain additional income by engaging in automated market marking (AMM). Automated market making helps guarantee a constant proportion of assets in the collateral pool. The AMM takes the form a geometric mean, made popular by [Balancer](https://balancer.fi/whitepaper.pdf). The notion that users _get paid_ is different from much of conventional finance, where portfolio holders are typically required to pay fees to rebalance the portfolio.

Importantly, in market downturns, a risky asset may constantly depreciate. In these cases, ALEX’s relative allocation of a riskless asset will gradually increase by design. In the event of a loan close to being under-collateralized or defaulting, ALEX converts the remaining portion of the risky asset so that only the riskless asset remains. This ensures no interruption to borrowing/lending activities. Similarly, the agreed rate and maturity remains unaffected. This is different from liquidation. In other platforms, liquidations usually unwind the loan partially, or even fully, resulting in the early termination of a loan. ALEX’s design allows for borrowing and lending activity to unfold without the interruptions that plague many of ALEX’s alternatives.

## **Two-Asset Collateral Pool: Rationale**

Most loanable funds assume a single asset in the collateral pool. While this type of pool benefits when prices of collateral assets appreciate, a pool’s value can depreciate rapidly when volatility is large and prices of collateral assets plummet.

In conventional finance, whether or not to hold a risky asset depends on investors’ risk appetite and their perception of the market environment. A “risk on” market environment entices investors to purchase risky assets and to seek larger returns. In our view, collateral pools made up of single assets are more suitable during “risk on” environments. In these environments, “risk-seeking” borrowers worry less about defaulting and believe risky assets will rally further. This contrasts with “risk-off” environments, when market uncertainty increases. Investors become more risk-averse and tend to hold riskless assets which exhibit small volatility and smaller return.

Many investors would like to profit in both “risk on” and “risk off” periods by holding a diversified portfolio comprised of both risky and riskless assets. A typical example is a portfolio consisting of an S\&P 500 index and of US Treasury bonds. Diversification is essential to portfolio management. Diversification ensures portfolios are not overly exposed to one specific asset. Diversifications reduces unsystematic risk. Thus, diversification is a core reason why ALEX creates collateral pools with more than one asset: diversified collateral pools reduce pool volatility while enhancing returns.

## **AMM: Geometric Mean Market Maker**

AMMs are the key drivers behind many DeFi trading platforms. We discuss its general features in our [first white paper](https://docs.alexgo.io/whitepaper/automated-market-making-of-alex). Our AMM design adopts a “generalised mean market maker”. This design is powerful because it incorporates time to maturity features while aligning various AMM derivations with traditional financial pricing theory.

In the collateral pool, as weights of the underlying assets change regularly, we employ an AMM which has embedded weights in its expression: the geometric mean market maker (GMMM). Each weight of the GMMM corresponds to the proportion of a relevant asset’s value to the whole portfolio’s value. This is a desirable property for any portfolio manager who sets target weights for a portfolio’s assets.

GMMMs were first introduced by Balancer. A GMMM represents an extension to the AMM of the popular AMM platform Uniswap. Uniswap’s AMM is a special case of Balancer’s GMMM by imposing weights of 50% each on two assets in a given pool.

Mathematically, a GMMM consisting of two assets can be expressed as follows:

![https://miro.medium.com/max/1400/1\*EhhHu9KcyuSFrdqVY9Wc0A.png](https://miro.medium.com/max/1400/1\*EhhHu9KcyuSFrdqVY9Wc0A.png)

where _x(t)_ and _y(t)_ are the balance of the risky asset and the riskless asset respectively, whereas _w_ₓ\*(_t_)\* and _w_ᵧ\*(_t_)\* are the corresponding weights and _w_ₓ\*(_t_) + w_ᵧ_(_t_) =_1. L_(_t_)\* is the invariant constant, which remains unchanged when weights are fixed in between rebalancing time.

Prices _p_ₓ\*(_t_)\* and _p_c\*(_t_)\*, which share the same numeraire such as USD, satisfy the following no-arbitrage condition:

![https://miro.medium.com/max/1400/1\*qHqjeSZsCNNm9MAoJju7xQ.png](https://miro.medium.com/max/1400/1\*qHqjeSZsCNNm9MAoJju7xQ.png)

Denote the pool values as _v(t)=x(t)p_ₓ(t)+_y(t)pᵥ(t)._ Combining with a no-arbitrage condition, we can show that:

![https://miro.medium.com/max/1400/1\*S0o0Uy1ArP01mZEQUeX5sw.png](https://miro.medium.com/max/1400/1\*S0o0Uy1ArP01mZEQUeX5sw.png)

This means that a pool’s weight represents the underlying asset value in proportion to the pool’s value.

Lastly, GMMM is related to the generalized mean AMM employed in the Yield Token Pool by setting _w_ₓ(t)=_w_ᵧ(t)=0.5 because:

![https://miro.medium.com/max/1400/1\*lglIssQwvz2taKXnkT0H9A.png](https://miro.medium.com/max/1400/1\*lglIssQwvz2taKXnkT0H9A.png)

## **Rebalancing Set-up and Collateral Pool Valuation**

In conventional finance, rebalancing results in updated allocation of underlying assets without altering the portfolio value. However, this is not the case when an AMM is implemented in DeFi. The portfolio value changes reflecting the effort in preserving the price, while adjusting the invariant function with the newly calibrated weights.

Assume the loan is borrowed at time 0 and returned at time T. There are k-1 rebalancing events throughout the life time of the loan:

![https://miro.medium.com/max/1232/1\*iH5-4FbUQ\_5gz2yUKqCF5A.png](https://miro.medium.com/max/1232/1\*iH5-4FbUQ\_5gz2yUKqCF5A.png)

At the start of the contract _t_₀=0, initially deposited risky asset is split into _x(t_₀) and _y(t_₀). The split may occur using any trading platform, including our in-house DEX.

At rebalancing time _t_ᵢ(\*i=1,2,\*⋯,_k_-1), price will deviate from the market as soon as weights are updated. Our system relies on arbitrageurs to align the price with the market by trading in the pool. This subsequently impacts token balances, the invariant constant, and portfolio value.

The process is summarized below:

![https://miro.medium.com/max/1400/1\*e6RykjNfAVbXIasML\_9tiQ.png](https://miro.medium.com/max/1400/1\*e6RykjNfAVbXIasML\_9tiQ.png)

## **Dynamic Rebalancing**

ALEX’s rebalancing collateral pool is dynamic. It integrates the concept of asset management with collateral management. By holding and dynamically managing both a risky asset and a riskless asset, several benefits result. When the risky asset depreciates, the collateral pool increasingly holds more of the riskless rather than the risky asset, dynamically reducing the threat of undercollatisation. On the contrary, a higher weight is dynamically assigned to a risky asset when the its price surges, ensuring that the collateral pool captures most of the upside gains. This dynamic is similar to a call option, whose upside is protected whereas its downside is limited. With ALEX, no actual option is involved however, and thus the borrower is not required to pay any expensive option premiums. Options premiums are significant with many cryptoassets because many cryptoassets are very volatile.

In the current version, a collateral pool’s allocation mechanism has close ties with option delta. Option delta measures the sensitivity of the option’s valuation to the underlying asset price movement. The delta of a call option ranges between 0 and 1 depending on an asset’s spot price and the option’s strike price, as shown in Figure 1. The higher the spot price, the larger the delta. Therefore, the more weight would be assigned to risky asset. When the strike price is set to be the same as asset spot price (at-the-money option), the delta is around 0.5. In ALEX’s design, this means holding an equal amount of the risky and of the riskless assets.

[https://miro.medium.com/max/794/0\*mcJ5LmUNj\_xsGVm4](https://miro.medium.com/max/794/0\*mcJ5LmUNj\_xsGVm4)

In mathematical terms, option delta δ(t) is calculated from Black Scholes model as follows:

![https://miro.medium.com/max/1400/1\*oWEaop1P3M0ytfDz72JQbQ.png](https://miro.medium.com/max/1400/1\*oWEaop1P3M0ytfDz72JQbQ.png)

Ideally, the relative weights of the risky and riskless assets should be updated continuously to reflect spot price movements and delta changes. In practice, we are updating the weights periodically (e.g. daily). However as cryptoassets typically exhibit higher volatility than other asset classes, delta changes can be significantly different between time periods. Significant movements tend to imply considerable price deviations from the market after rebalancing. This leads to significant profits for arbitrageurs, but arbitrageurs’ gains are often a collateral pool losses. This is similar to impermanent loss. However, while impermanent loss is caused by token balances moving along an AMM curve, here it is caused by weight changes and the effort to preserve price.

[https://miro.medium.com/max/940/0\*P-d-Fo0\_g7QIgqjS](https://miro.medium.com/max/940/0\*P-d-Fo0\_g7QIgqjS)

To mitigate the impact of weight changes, ALEX smooths the delta using an exponential moving average. At rebalancing time _t_ᵢ, the holding of a risky asset is calculated as

![https://miro.medium.com/max/882/1\*4IbQoNYoKw5SSvGgvUbpcA.png](https://miro.medium.com/max/882/1\*4IbQoNYoKw5SSvGgvUbpcA.png)

where α is the smoothing factor. Allocation to the riskless asset is thus 1−_w_ₓ(_t_ᵢ). Figure 2 compares the risky asset weight and the option delta of a simulated bitcoin path over a three-month period.

In comparison with a collateral pool consisting of single asset, a collateral rebalancing pool could underperform when the market is risk-on and a risky asset exhibits strong upward price momentum. This is because holding a risky asset is a smoothed version of option delta, suggesting the asset’s weight hardly reaches 100%. However, when the market is tumbling and the risky asset depreciates, more weight is assigned to the riskless asset, reducing losses. This rebalancing slows down portfolio value depreciation. It also increases the chance of the loan staying afloat. Taken together, both these effects ensure robust performance with dynamic collateral pools across market conditions.

## **Flight to Quality**

Every effort is made to ensure the loan is overcollateralized by mimicking a call option whose downside is limited. However, the lack of an actual option means that the loan might still default, especially when the volatility of the risky asset increases or the market is in crisis.

If the collateral pool value drops below a pre-determined threshold, ALEX guarantees sustainability of the loan by converting the entire balance of the collateral pool’s risky asset to the collateral pool’s riskless asset. This ensures that borrowers can always cover the loan’s initial value. It also ensures no interruption of borrowing/lending activity more broadly.

These benefits are not possible by other protocols for loanable funds that use and enforce liquidation dynamics. Not only would the fixed term loan be interrupted due to early termination, but the price of liquidation might also not be known, adding an extra layer of uncertainty. Furthermore, liquidators can usually claim what is called a liquidation bonus, another source of loss to the borrower. For example, on Aave, liquidation bonuses range between 5% and 15%. On ALEX, borrowers are protected from these risks and losses.

ALEX’s protocol also faces less pressure should liquidity shrink amid turmoil. This is because ALEX’s design increases the holding of a riskless asset gradually when the market starts to shown signs of downturns. Although this is clearly an advantage compared to other platforms, the rare event of a mass market disruption might cause slow conversions and the collateral value dropping below the loan amount. To address such a black swan situation, ALEX also maintains a reserve fund. The fund is the protocol’s last resort for covering loans. It grows by way of collecting reserve premiums and is meant to secure the long term sustainability of ALEX as a whole.

In conventional finance, selling a risky asset to purchase a riskless asset is often called “flight to quality”. This often occurs during bear markets. In bear markets, investors endeavour to avoid economic losses, reduce risks, and thus seek “high quality” assets. ALEX incorporates this dynamic automatically and dynamically by rebalancing the assets in a collateral pool to contain more of the riskless than the risky asset.

To limit downside risks, once the collateral pool is rebalanced to only contain the riskless asset, all activities in the pool cease to function. This includes no more dynamic weights adjustments from price movements, even if the market rebounds.

## **Appendix**

## **Collateral Pool Key Parameters**

Most of the contents below are discussed in the main sections. Nonetheless, we list key parameters as they are essential to the collateral pool’s functioning, and for securing ALEX’s long term sustainability.

## **Contract Initialization**

* **Loan-to-Value (LTV)**: The ratio of the loan amount to the value of the collateral (“collateralize asset(s)”). For example, if LTV is set to be 80%, a loan amount equivalent to 80 BTC requires 100 BTC as collateral. There is generally no objectively correct LTV ratio; the LTV ratio depends on the quality of the collateralize asset, as well as the market condition when the loan is taken out. **Collateralization Ratio (CR)** is the inverse of LTV.
* **Tenor**: The length of time remaining before the loan expires.
* **Strike Price**: In the Black-Scholes model, strike price refers to the price at which the contract holder can purchase the underlying security when exercising a call option, or sell the underlying security when exercising a put option. In ALEX, the strike price determines the initial split of the risky and the riskless asset. For example, for an at-the-money option, in which strike price is set to be equal to the spot price, there would be an equal split of between two assets in the pool (i.e. \~50%).
* **Implied Volatility**: In the Black-Scholes model, implied volatility is the volatility estimate of an underlying security. A crude approximation of implied volatility is historical volatility. In practice, implied volatility is usually backed out from the observed option price.
* **Risk-free Interest Rate**: In the Black-Scholes model using risk-neutral valuation, the risk-free interest rate equals the expected return. The risk-free interest rate is usually assumed to be 0%, as future direction of the underlying security is unknown.

## **Pool Rebalancing**

* **Rebalancing Frequency**: Theoretically, continuous rebalancing is preferred for price continuity. In practice, ALEX updates the weights periodically to avoid over-calibration.
* **Smoothing Factor of Exponential Moving Average (EMA)**: EMA is an averaging method that places more weight on more recent observations. Assume y(t) is the observation value of y at time t, and that {y}(t) is the corresponding moving average, where α is the smoothing factor. Then:

![https://miro.medium.com/max/706/1\*fHHgHEoR2HEb7EdnI8sokA.png](https://miro.medium.com/max/706/1\*fHHgHEoR2HEb7EdnI8sokA.png)

## **Flight to Quality**

* **Conversion Threshold**: This is the LTV level when the risky asset in the collateral pool is completely converted to the riskless asset to prevent the loan from under-collateralization.
* **Reserve Premium**: The reserve premium is collected on behalf of a reserve fund. The reserve fund serves as the protocol’s last resort. In the extreme event that market turmoil dries up liquidity and ALEX cannot convert all risky assets quickly enough to cover the loan amount, the protocol would cover the difference. The reserve premium is thus another mechanism to guarantee continuity of borrowing and lending activity on ALEX.
