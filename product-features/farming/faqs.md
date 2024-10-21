---
description: Common questions you may have when dealing with farms.
---

# FAQs

<details>

<summary>How is farming related to staking?</summary>

Yield farming is a specific type of staking. In farming, you stake **LP tokens**, the tokens received in exchange for providing liquidity to a trading pool. This means that farmers are also [liquidity providers](../liquidity-providers/) (LPs). So while both farming and staking involve locking up tokens to earn rewards, farming always requires participation in a liquidity pool first.

</details>

<details>

<summary>What is harvesting?</summary>

Harvesting refers to the act of **claiming your farming rewards**. Similar to how you claim staking rewards, in farming, you "harvest" the rewards earned from staking your LP tokens in a farm.

</details>

<details>

<summary>Do farming rewards accumulate?</summary>

Yes, farming rewards accumulate over time. It is not mandatory to harvest your rewards at the end of each cycle, you can claim them whenever you choose. Also, when you withdraw (unstake) your LP tokens, any unharvested rewards will automatically be withdrawn as well.

</details>

<details>

<summary>What is the cooldown period?</summary>

The cooldown period refers to the time between when your LP tokens are staked into the farm and when a new farming cycle begins. Essentially, it is the remaining time (measured in Stacks blocks) of the current staking cycle. This implies that your staked tokens won't start generating reward immediately but in next upcoming cycle. For more details, check the [Cycles and Cooldown Period](key-concepts.md#cycles-and-cooldown-period) section of the Key concepts page.

</details>

<details>

<summary>Why is it more convenient to stake for longer periods?</summary>

Because of the cooldown period. If you plan to stake for multiple cycles, it is more efficient to stake for the entire period upfront rather than withdrawing and restaking repeatedly.

For example, if you want to farm for 12 cycles and choose to stake three times for 4-cycle periods, you will miss out on rewards for 3 cycles. This happens because each time you withdraw and restake, you enter a cooldown period. In contrast, if you stake directly for the full 12 cycles, you will only miss rewards for 1 cycle, the very first one.

</details>

<details>

<summary>What can I do with my rewards?</summary>

You have several options for your rewards: you can hold them, trade them, or generate compound interest. Compound interest occurs when your rewards generate more rewards. Here are some ways to achieve this within the ALEX Lab Platform:

* Stake the rewards on [ALEX Staking](../stake.md). You can even buy LiALEX for auto-compounding rewards, maximizing your long-term yield.
* Provide liquidity to a pool to earn a share of the trading fees. To further enhance your yield, stake the LP tokens in a farm.

</details>

<details>

<summary>How can I restake my rewards in the farm?</summary>

Restaking your rewards in the farm is an effective strategy for generating compound interest, but not as straight forward. To restake, you will need to transform your rewards into LP tokens first. There are two scenarios to consider:

* **Case 1:** The reward token is one of the trading pair tokens.&#x20;
* **Case 2:** The reward token is none of the trading pair tokens.

Here are the steps to "re-farm" your rewards:

1. [Swap](https://app.alexlab.co/swap) the rewards in order to obtain the liquidity pool trading pair tokens. This may involve one swap for Case 1 and two swaps for Case 2.
2. [Provide liquidity](https://app.alexlab.co/pool) to the pool associated with the trading pair to receive LP tokens.
3. Finally, stake the new LP tokens into the farm.

</details>

<details>

<summary>What is APower?</summary>

ALEX Staking Power, or APower, is a non-transferrable and non-tradable token. It is a special incentive that you can earn through staking on the ALEX Lab Platform, either by:

1. **Stake $ALEX (1x Multiplier)**
2. **Stake LP tokens through Yield Farming (0.3x Multiplier)**

APower is the lottery ticket that allows you to take part in any future IDO rounds on our [Launchpad](https://app.alexlab.co/launchpad). There is no maximum amount of APower an address can earn over a period of time. If you are interested in frequently participating in IDOs, staking $ALEX would generate APower fastest.

Every IDO is unique, however, and may have a cap on the amount of APower that can be allocated. This is to prevent IDOs dominated by a small group of "whale" members.

Full Medium post [here](https://medium.com/alexgobtc/what-is-alex-staking-power-and-how-do-i-use-it-1b3de3797fa2).

</details>

<details>

<summary>What happens to my LP tokens when I stake them?</summary>

When you stake your LP tokens in a yield farm, they are technically not in your possession anymore. During farming, LP tokens are locked in the ALEX smart contract. Although they belong to you and you are the only one authorized to withdraw them, they are not held in your wallet during the lock-up period.

</details>

<details>

<summary>Why can't I see my LP tokens in the My Liquidity panel?</summary>

Since LP tokens are held by the ALEX smart contract during farming, you must first unstake them from the farm for them to appear in the **My Liquidity** panel. To access this panel, navigate to the **Swap** > **Pool** tab. Once you select the desired pool from the list, it will appear just above the **Pool Info** panel.

</details>

<details>

<summary>Why does farming come with the risk of Impermanent Loss?</summary>

The risk of Impermanent Loss is associated with providing liquidity. To farm, you must be a liquidity provider (LP), which inherently carries this risk.

When you provide liquidity, you add assets to a liquidity pool. The market prices of those assets can fluctuate. Impermanent Loss occurs when the prices of the assets change unfavorably compared to their value at the time of deposit. This loss is termed "impermanent" because it only becomes permanent if the LP withdraws their funds when prices have diverged significantly.

For further information, please refer to the [Impermanent Loss subsection](../liquidity-providers/key-concepts.md#impermanent-loss) on the Liquidity Providers page.

</details>
