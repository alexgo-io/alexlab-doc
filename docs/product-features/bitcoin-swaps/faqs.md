---
description: Common questions you may have when dealing with the Bitcoin Native Swap.
---

# ❓ FAQs

<details>

<summary>Will my fees be lower or higher?</summary>

Fees depend on many variables, such as transaction size and pool liquidity. The Bitcoin Native Swap performs the same operations as you would in a manual operation, so fees should be roughly equal. They may be slightly higher than in a manual operation if, for example, the fees drop in the extra minutes it takes you to complete the steps yourself. However, the difference is negligible. If anything, fees may be slightly lower since Bitcoin Native Swap finds the most optimal route for your transaction.

</details>

<details>

<summary>Why should I use the ALEX Bitcoin Native Swap instead of performing the operations myself?</summary>

The main benefit of the **Bitcoin Native Swap** on ALEX is that it ensures you won't miss the chance to execute a transaction at your desired exchange rate. Since the swap is performed automatically, you don't have to worry about price fluctuations that may occur if you perform the operation manually. 
The Bitcoin Native Swap also makes transactions simpler and more atomized. It performs the swap in just one operation instead of requiring you to interact with multiple wallets, networks, or contracts. Should any error occur in any of the intermediate steps, the whole process will revert, allowing you control over the entire swap.

</details>

<details>

<summary>Why are my tokens being converted to other tokens before being swapped for my target token?</summary>

The ALEX Bitcoin Native Swap may use intermediate tokens to complete the exchange because it is designed to find the most optimal route for the swap. Sometimes, there may not be a liquidity pool trading both the base and the target token, so the **Bitcoin Native Swap** must use other liquidity pools to complete the exchange. The route, as well as the fee, will always be displayed before your transaction is confirmed.

</details>

<details>

<summary>How are swaps and liquidity pools related?</summary>

When you perform a swap on ALEX, you are interacting with liquidity pools. Each pool contains two tokens, which makes it possible to exchange one for the other. Besides, the exchange rate of the swap is determined by the price of the tokens in the pool via an Automated Market Maker (AMM). 

</details>

<details>

<summary>What is the difference between a swap fee and a liquidity provider fee?</summary>

The liquidity provider fee is the amount paid by the user to the Liquidity Providers of the pool that is being used for the swap. The swap fee, in this case, refers to the fee that is being distributed to the ALEX Lab Platform for facillitating the exchange.

</details>