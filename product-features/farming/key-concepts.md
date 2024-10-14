---
description: >-
  All you need to know for successfully farming on ALEX Lab, from farm basics to
  dashboard metrics!
---

# Key concepts

## Farm basics

Yield farming works very similar to standard staking, with the key difference being that the tokens you stake are LP tokens. As in traditional staking, you lock up your tokens for a certain period (measured in cycles) and earn rewards over time. After each cycle, you will have rewards available to harvest.

### What are LP tokens?

LP tokens are the tokens you receive when you provide funds to a liquidity pool. These tokens represent your share of the pool's assets. As a liquidity provider, you earn a portion of the fees charged to users who perform swaps within the pool. For a deeper understanding of these concepts, check out the [Liquidity Providers](../liquidity-providers/) section of the docs.

{% hint style="warning" %}
You may notice that farming often yields higher rewards than regular staking. Well, farming involves liquidity provision and comes with the risk of Impermanent Loss. It's not as scary as it sounds, but it is worth learning about the concept before you get started. Learn more in the [Impermanent Loss subsection](../liquidity-providers/key-concepts.md#impermanent-loss) from the Liquidity Providers page.
{% endhint %}

### What exactly is a farm?

A farm is a staking pool for a specific LP token. Each liquidity pool has their specific native LP tokens. There are different LP tokens corresponding to each liquidity pool on the ALEX Lab Platform.

Farms are identified by these two attributes.

* **Trading Pair:** The specific LP token that the farm accepts. To obtain these LP tokens, you will have to provide liquidity to the pool associated with the same trading pair.
* **Token Rewards:** The token in which the farm rewards the stakers at the end of each cycle. This token is predefined by the farm.

Farms only accept LP tokens of one kind. For example, the STX-ALEX farm only accepts STX-ALEX LP tokens, which you receive in exchange for providing liquidity to the STX-ALEX pool.

### Cycles and cooldown period

Farming is measured in cycles. **One cycle** is 525 Stacks blocks, which is approximately **3.5 days**. This means that when you stake tokens in a farm, you need to specify the number of cycles you want to lock up your tokens in the farm. Rewards are distributed after a cycle ends.

Your staked tokens will start generating yield in the next upcoming cycle, which means there will be no reward during the time gap between when you stake and when the upcoming cycle starts. To maximize your earnings, it's best to stake for longer cycle periods, avoiding gaps in rewards due to the cooldown. That's why 32-cycle staking is recommended.

Let's use an example. Assume you stake for one cycle at a time. When that cycle ends, you can claim the rewards associated with that cycle. To continue generating rewards, you will have to withdraw your LP tokens and restake them. However, when you restake them, the current cycle will not be eligible for you to earn rewards. Therefore, you will have to wait until the next cycle to acquire rewards. Over 100 cycles, this method would cause you to miss rewards for about 50 cycles. In contrast, if you stake for 32 cycles, you will only miss rewards for 3 cycles.

### Reward distribution

Farms may offer different types of reward tokens, and each farm has a predetermined amount of rewards. For simplicity, we can assume that the total rewards distributed to stakers during each cycle remains constant. At the end of each cycle, the rewards are available to be harvested by the farmers (stakers).

Rewards are distributed proportionally to each farmer based on their staked amount. This can be represented by the following equation:

$$
\begin{equation} \textrm{Farmer Reward} = \frac{\textrm{Farmer Staked Amount}}{\textrm{Total Staked Amount}} \; \cdot \; \textrm{Total Rewards}. \end{equation}
$$

Each value in the equation applies to a specific cycle.

When there are two reward tokens (e.g. $ALEX and APower), the formula is applied separately for each token, resulting in two Farmer Reward amounts, one for each reward token.

### Farm APR

The Farm APR metric reflects your potential annual earnings from farming, based on the most recent cycle yields. It represents the potential profitability of participating in a farm over a year, assuming the total staked tokens remain similar to the last cycle.

The Farm APR is calculated based on the rewards distributed in the current cycle:

$$
\begin{equation} \textrm{Farm APR} = \frac{\textrm{Total Rewards}}{\textrm{Total Staked Amount}} \; \cdot \; \textrm{Annual Factor} \; \cdot \; 100. \end{equation}
$$

Where

* Total Rewards refers to the rewards distributed in the cycle (including $ALEX and potentially other tokens) converted to USD value;
* Total Staked Amount is the total value of staked LP tokens in USD;
* Annual Factor is 100.15 (\~ 100 cycles per year);
* 100 factor is used to express the APR as a percentage.

## My Farming Dashboard

Once you have staked LP tokens into a farm, it's important to familiarize yourself with this dashboard. You can access it by clicking on a farm from the [ALEX Lab Farms page](https://app.alexlab.co/farm). Let's walk through all the farming metrics.

<figure><img src="../../.gitbook/assets/farming/my-farming-dashboard-example.png" alt=""><figcaption><p>My Farming dashboard example for ALEX - LiALEX farm. This user has accumulated rewards from previous cycles that are available to claim. Also, there are no LP tokens that have completed their staking period and are ready for withdrawal (LP to claim).</p></figcaption></figure>

### Active farming LP

The tokens you have staked in the farm. When your staking period ends for a certain amount, those tokens will move from here to the [LP to claim](key-concepts.md#lp-to-claim) section of the dashborad. If you staked multiple times at different cycles, the lock periods apply to each amount separately.

### Average APR

This metric represents the average of all your farming cycle APRs (both current and upcoming).

### Rewards to claim

The rewards available for you to harvest. If you don't harvest, these rewards will accumulate over time. However, to maximize your returns, we recommend harvesting your rewards after every cycle ends. This way, you can stake them or buy more LP tokens to generate compound interest.

### LP to claim

The tokens that have completed their staking period. These tokens are no longer in a farming state. To make them generate farming rewards again, you will have to withdraw and restake them.

### Cycles

Your active farming cycles. Here, there will be shown all the cycles during which you have LP tokens locked and earning rewards. For each cycle, you will find:

* The **Cycle Number**, with a "current" or "upcoming" tag.
* The **Farming Amount**, which indicates the amount you have staked in that cycle.
* The **Farm APR**, calculated based on equation (2).
* Your **Estimated Earnings**, derived from equation (1).

For the **current cycle**, all metrics are exact, as the staked tokens are already defined. For the **upcoming cycles**, all metrics are estimates since we cannot predict how many LP tokens will be staked; we can only say how many LP tokens are commited so far for that cycle. This explains why the APR percentage appears higher for more distant cycles, due to the estimated total staked amount.
