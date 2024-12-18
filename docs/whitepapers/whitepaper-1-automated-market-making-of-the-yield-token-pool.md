# 📃 Whitepaper (1): Automated Market Making of the Yield Token Pool

## Whitepaper (1): **Automated Market Making of the Yield Token Pool**

## **Abstract**

ALEX aims to provide fixed rate borrowing and lending services with pre-determined maturity in the world of decentralized finance (DeFi). We’ve included forward contracts in our trading pool, with an Automated Market Making (AMM) engine utilizing Generalized Mean. We have formalized the trading practice of swapping forward contracts on the underlying asset, and we’ve incorporated the latest innovation in DeFi — concentrated liquidity. Consequently, liquidity providers on ALEX are able to save significant capital by market making on a selected range of interest rates.

## **Introduction**

ALEX stands for **A**utomated **L**iquidity **EX**change. It is a hybrid of automated market making and on-chain loan-able fund built on Bitcoin via Stacks. While lenders and borrowers can minimize uncertainty by securing loans with fixed rate and tenor, liquidity providers are able to take advantage of our capital efficiency mechanism by imposing a cap and floor on the interest rate. This allows liquidity to be offered on parts of the curve that contains the majority of trading activity and leads to efficient capital management.

On ALEX, lending and borrowing activities are facilitated by a forward contract based token “ayToken”. It is similar to an OTC bilateral forward contract in the conventional financial market, which specifies underlying asset “Token” and expiry date. This paper assumes ayToken is minted and ready to be exchanged. Lenders purchase ayToken at a discount to the spot Token price when the contract is initiated and reclaim the underlying asset upon expiration when forward price converges to spot price. Borrowers sell ayToken in return for Token on day one and return Token upon expiration. The implied interest rate depends on how discounted the forward price is to the spot price at the time of transaction, which is executed on the AMM.

Last but not least, ALEX hopes to bridge the gap between Defi and conventional finance by applying an AMM protocol derived from one of the basic instruments in the fixed income market — the zero coupon bond first proposed by [Yield Space](https://yield.is/YieldSpace.pdf). This empowers ALEX to both learn from the fiat world and offer more decentralized financial products in the future.

This paper focuses on technical aspects of the AMM and is the first of a series of ALEX papers unveiling all the exciting features and applications ALEX is developing.

## **AMM and Invariant Function**

ALEX AMM is built on three beliefs: (i) it is mathematically neat and reflects economic demand and supply; (ii) it is a type of mean, like other AMMs; and (iii) it is derived and can be interpreted in terms of yield and can be connected to conventional finance, where research has been conducted for decades.

We will first review some desirable features of the AMM that ALEX hopes to exhibit.

## **Properties of AMM**

![https://miro.medium.com/max/1400/1\*3YqkqWB-v4ItOamoGNwocQ.png](https://miro.medium.com/max/1400/1*3YqkqWB-v4ItOamoGNwocQ.png)

Meanwhile, _f_ can usually be interpreted as a form of mean, for example, [mStable](https://docs.mstable.org/) relates to arithmetic mean, where _&#x78;_&#x2081;+_&#x78;_&#x2082;=L (constant sum formula); one of the most popular platforms [Uniswap](https://uniswap.org/whitepaper-v3.pdf) relates to geometric mean, where _&#x78;_&#x2081;_&#x78;_&#x2082;=L (constant product formula); [Balancer](https://balancer.fi/whitepaper.pdf), which our collateral rebalancing pool employs, applies weighted geometric mean. Its AMM is:

![https://miro.medium.com/max/338/1\*PJRDEL52vRfvHKI7mjNYsA.png](https://miro.medium.com/max/338/1*PJRDEL52vRfvHKI7mjNYsA.png)

where _&#x77;_&#x2081; and _&#x77;_&#x2082; are fixed weights. However, none of these three protocols consider time to maturity, which is essential in modern interest rate theory.

## **ALEX AMM**

After extensive research, we consider it possible for ALEX AMM to be connected to generalised mean defined as:

![https://miro.medium.com/max/1400/1\*uui14K4E2efhu7QA7v2SKw.png](https://miro.medium.com/max/1400/1*uui14K4E2efhu7QA7v2SKw.png)

![https://miro.medium.com/max/1400/1\*6ZBbIERf5zMOd4lHgQl\_0A.png](https://miro.medium.com/max/1400/1*6ZBbIERf5zMOd4lHgQl_0A.png)

In the benchmark research piece by [Yield Space](https://yield.is/YieldSpace.pdf), the invariant function above is formalized from the perspective of zero coupon bond. _p_ is replaced by 1−_t_ where _t_ is time to maturity and _L_ is a function of _t_, so that

![https://miro.medium.com/max/1400/1\*IUsRchNH0bS3j93YG7Vsaw.png](https://miro.medium.com/max/1400/1*IUsRchNH0bS3j93YG7Vsaw.png)

In the rest of the paper, to be consistent with [Yield Space](https://yield.is/YieldSpace.pdf), we employ notations below

* _x_ : balance of the underlying Token
* _y_ : balance of ayToken
* _r_ : implied interest rate, defined as the natural logarithm of balance of ayToken and Token

![https://miro.medium.com/max/1400/1\*rJFBOIh\_J-RuH8OI68mCBA.png](https://miro.medium.com/max/1400/1*rJFBOIh_J-RuH8OI68mCBA.png)

![https://miro.medium.com/max/1400/1\*Gvu2JnE2aNKjpscVID-6NA.png](https://miro.medium.com/max/1400/1*Gvu2JnE2aNKjpscVID-6NA.png)

Though purely theoretical at this stage, [Appendix 2](https://medium.com/whitepaper/automated-market-making-of-alex#appendix-2-liquidity-mapping-to-uniswap-v3) maps _L_ to the liquidity distribution of [Uniswap V3](https://uniswap.org/whitepaper-v3.pdf). This is motivated by an independent research from [Paradigm](https://www.paradigm.xyz/2021/06/uniswap-v3-the-universal-amm/).

## **Trading Formulae**

Market transactions, which involves exchange of Token and ayToken, satisfies the invariant function. While fee is deposited back to the liquidity pool in some protocols, such as _Uniswap V2_, resulting in slight increase of _L_ after each transaction, ALEX counts the fee separately. This is consistent with [Uniswap V3](https://uniswap.org/whitepaper-v3.pdf). Hence _L_ remains constant.

## **Out-Given-In**

![https://miro.medium.com/max/1400/1\*8WMeCR7XkOhMFfBbOREQ-Q.png](https://miro.medium.com/max/1400/1*8WMeCR7XkOhMFfBbOREQ-Q.png)

![https://miro.medium.com/max/1400/1\*WrwxJAhbY2baGGHE3xguiw.png](https://miro.medium.com/max/1400/1*WrwxJAhbY2baGGHE3xguiw.png)

![https://miro.medium.com/max/1400/1\*r5JHkckZev3K9N9Sa5pSfw.png](https://miro.medium.com/max/1400/1*r5JHkckZev3K9N9Sa5pSfw.png)

![https://miro.medium.com/max/1400/1\*04K06US94bsXUAy4I5d6kg.png](https://miro.medium.com/max/1400/1*04K06US94bsXUAy4I5d6kg.png)

![https://miro.medium.com/max/1400/1\*wwJMeWllkefYct7oi-G5Ig.png](https://miro.medium.com/max/1400/1*wwJMeWllkefYct7oi-G5Ig.png)

![https://miro.medium.com/max/1400/1\*5ViCy9rX05OJBCSRlYK3pw.png](https://miro.medium.com/max/1400/1*5ViCy9rX05OJBCSRlYK3pw.png)

[https://miro.medium.com/max/820/0\*io5bXLFMARJOxplP](https://miro.medium.com/max/820/0*io5bXLFMARJOxplP)

Figure 1

![https://miro.medium.com/max/1400/1\*oHNB8jZmKW5R8iNC1x-LYQ.png](https://miro.medium.com/max/1400/1*oHNB8jZmKW5R8iNC1x-LYQ.png)

![https://miro.medium.com/max/1400/1\*qcXdKb7xpc\_rumRAM3dWTw.png](https://miro.medium.com/max/1400/1*qcXdKb7xpc_rumRAM3dWTw.png)

![https://miro.medium.com/max/1400/1\*EugLUkC1QWy0bsFmTIk59Q.png](https://miro.medium.com/max/1400/1*EugLUkC1QWy0bsFmTIk59Q.png)

![https://miro.medium.com/max/1400/1\*PLKTpDZuCLliU1ykDGIv0w.png](https://miro.medium.com/max/1400/1*PLKTpDZuCLliU1ykDGIv0w.png)

![https://miro.medium.com/max/1400/1\*knOe6WwHMlRKP9Wklg6S8g.png](https://miro.medium.com/max/1400/1*knOe6WwHMlRKP9Wklg6S8g.png)

![https://miro.medium.com/max/1400/1\*VpA4DEJXfl3OH1RhW8xMxQ.png](https://miro.medium.com/max/1400/1*VpA4DEJXfl3OH1RhW8xMxQ.png)

![https://miro.medium.com/max/1400/1\*NkE8mAW8LsHQWY9nbHcApw.png](https://miro.medium.com/max/1400/1*NkE8mAW8LsHQWY9nbHcApw.png)

[https://miro.medium.com/max/1104/0\*wKYLoNXy2EaX-fpL](https://miro.medium.com/max/1104/0*wKYLoNXy2EaX-fpL)

Figure 2

![https://miro.medium.com/max/1400/1\*oaYS5hBSITx1C79rpT1Mpw.png](https://miro.medium.com/max/1400/1*oaYS5hBSITx1C79rpT1Mpw.png)

![https://miro.medium.com/max/1400/1\*E4rkTP8zXBuB1fK9-GMQSQ.png](https://miro.medium.com/max/1400/1*E4rkTP8zXBuB1fK9-GMQSQ.png)

![https://miro.medium.com/max/1400/1\*7WJPUmndF9AOgmsPlfN6uw.png](https://miro.medium.com/max/1400/1*7WJPUmndF9AOgmsPlfN6uw.png)

![https://miro.medium.com/max/1400/1\*IE9uG1WxODh7w3ynTC0ybA.png](https://miro.medium.com/max/1400/1*IE9uG1WxODh7w3ynTC0ybA.png)

![https://miro.medium.com/max/1400/1\*FwND\_W14vRbt05pFiyTNdg.png](https://miro.medium.com/max/1400/1*FwND_W14vRbt05pFiyTNdg.png)

![https://miro.medium.com/max/1400/1\*LroQGwF17qftskZ-FeO5hg.png](https://miro.medium.com/max/1400/1*LroQGwF17qftskZ-FeO5hg.png)

![https://miro.medium.com/max/1400/1\*wbIXxhBDwY\_cobmf-Y5LCA.png](https://miro.medium.com/max/1400/1*wbIXxhBDwY_cobmf-Y5LCA.png)

[https://miro.medium.com/max/970/0\*dt0RxVxz0DKLxnIu](https://miro.medium.com/max/970/0*dt0RxVxz0DKLxnIu)

Figure 3
