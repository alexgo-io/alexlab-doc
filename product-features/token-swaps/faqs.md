---
description: Common questions that may arise when trading tokens.
---

# FAQs

<details>

<summary>Where does the swap fee go?</summary>

From the total fee charged during a swap operation, a portion is rebated to users who provide liquidity to the pool (liquidity providers) , while the remaining part goes to the ALEX Lab Foundation. By default, this split is 50/50, but it may vary depending on the specific liquidity pool settings.

You can view these percentages in the Pool Info panel by navigating to the Swap -> Pool tab from the navbar and selecting your pool of interest from the list.

</details>

<details>

<summary>In which cases is routing necessary?</summary>

Token swaps on ALEX are performed on a decentralized exchange (DEX) and powered by liquidity pools. This implies that if you want to trade STX for ALEX tokens, you are interacting with the STX-ALEX liquidity pool. Since this pool exists, a direct swap is possible.

Now, suppose you want to trade MEME1 for MEME2, but there isn't a specific MEME1-MEME2 liquidity pool. In this case, the platform will use intermediate pools. For example, if there are STX-MEME1 and ALEX-MEME2 liquidity pools, they will act as intermediaries. In this case, the swap route would be MEME1 -> STX -> ALEX -> MEME2. While MEME1 is still the base token and MEME2 the target token, the swap involves two intermediate tokens (STX and ALEX).

</details>

<details>

<summary>How do token swaps work?</summary>

Swaps on ALEX's decentralized exchange (DEX) operate through smart contracts built on the Stacks network. These smart contracts manage liquidity pools, which are collections of crypto assets deposited by users. When you perform a swap, you trade tokens with the liquidity pool, eliminating the need for a direct counterparty. For example, if a user wants to trade Stacks' native currency (STX) for ALEX's governance token (ALEX), they would interact with the STX-ALEX liquidity pool on ALEX's smart contracts.

The Automated Market Maker (AMM) protocol controls prices, fees, and token amounts. For further information on this topic please refer to the [ALEX Go Trading Pool documentation](https://docs.alexgo.io/trading-lending-and-borrowing/trading-pool).

</details>