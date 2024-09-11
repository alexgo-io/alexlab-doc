# 🐋 Liquidity Pool

## Getting Started

### What are Liquidity Pools?

Liquidity pools are crowdfunded collections of crypto assets held in a smart contract, designed to provide liquidity for decentralized exchanges (DEXs) and support various decentralized finance (DeFi) protocols.

While their applications are diverse, ranging from lending and borrowing platforms to algorithmic protocols for stablecoins, their primary use is on DEXs. In this case, liquidity pools enable users to trade crypto assets without the need for a centralized intermediary, serving as reserves of assets that users can trade against.

### Their role in Automated Market Makers (AMMs)

Automated Market Makers (AMMs) are the predominant type of decentralized exchange (DEX). While other DEX designs exist, AMM-based DEXs have become extremely popular. These exchanges operate using liquidity pools and algorithmic mechanisms to determine prices and facilitate the trading of crypto assets between peers.

Smart contracts manage all trades executed within the AMM, including aspects such as fees, prices, and minimum target token amounts. In AMM-based DEXs, there is no need for direct counterparties as in traditional order book trading. Instead, liquidity pools act as the counterparties, providing instant liquidity when needed.

### ALEX Liquidity Pools

The ALEX decentralized exchange is AMM-based and consists of a set of smart contracts built on top of the Stacks network. Each liquidity pool represents a collection of funds locked into a smart contract by voluntary depositors.

Each liquidity pool contains a specific pair of cryptocurrencies for users to perform swaps on. For instance, a user looking to trade Stacks' native currency (STX) for ALEX's governance token (ALEX) will interact with the STX/ALEX liquidity pool on ALEX's smart contracts. Check the [Swap](../swap.md) section if you are interested in this feature.

The users who deposit their assets into the pools are known as liquidity providers (LPs). To incentivize liquidity providers, the ALEX AMM protocol rewards them with a fraction of the trading fees. These fees are the ones charged by the AMM exchange on every swap.

### Liquidity Providers (LPs)

In exchange for providing funds to a pool, liquidity providers receive an amount of LP tokens that represent their share of assets within that pool. LP token holders earn a proportional share of all transaction fees charged to traders who perform swaps within the pool. Liquidity can be removed at any time, and the earnings associated with those LP tokens are also withdrawn at this point.

For example, if a user holds 5% of the pool’s total funds, they will earn 5% of the transaction fees allocated to liquidity providers (the other portion goes to the platform). These earnings are withdrawn when the liquidity is removed.

{% hint style="info" %}
**How is this related to farming?** Liquidity providers can stake or lock up LP tokens to earn additional rewards. These rewards are separate from the earnings of liquidity provision. This process is referred to as [Yield Farming](../farm.md).
{% endhint %}

{% hint style="info" %}
**Note:** The initials "LP" are used both to abbreviate "liquidity provider" and to refer to the tokens these users receive, which represent their share of the contributed funds in the pool.
{% endhint %}

## 🫴💰 Provide Liquidity

You can become a liquidity provider on ALEX by submitting two tokens to a liquidity pool, which allows you to **earn a share of the trading fees**. Note that these two tokens are the ones that constitute the pool. The trading fee rate is 0.5% per transaction, with 50% allocated to liquidity providers and the remaining 50% going to the ALEX platform.

### Example

* **Becoming a Liquidity Provider:** Suppose you want to provide liquidity for the STX/ALEX pool. If each token is valued at $1, you would add 10 ALEX and 10 STX to the pool, since liquidity is added in equal parts.
* **Getting LP Tokens in return:** Let's say you receive 100 LP tokens in representation of your share of the pool's funds. These 100 LP tokens also represent a total value of $20 (10 ALEX + 10 STX, each valued at $1).
* **Earnings from trades:** As other users trade within the pool, the pool collects a 0.5% fee per transaction. Of this, 50% is reinvested into the pool.
* **Removing Liquidity:** You can remove your liquidity at any time. When you decide to do so, you can reduce your position by redeeming your LP tokens. If you return your 100 LP tokens, you will receive a greater amount of ALEX and STX than you initially provided, reflecting your earnings. These earning are proportional to the LP token amount redeemed and thus proportional your share of the pool’s funds; meaning the more liquidiy you provide, the greater the earnings.

{% hint style="info" %}
If you want to potentially earn higher returns as a liquidity provider, you can opt for [Yield Farming](../farm.md). This involves staking or locking up your LP tokens for a fixed period to earn additional yield rewards. Alongside trading fees, you’ll receive ALEX platform incentive tokens. However, during farming, you cannot withdraw your LP tokens until the staking period ends.
{% endhint %}

{% hint style="success" %}
Check out the [STX/ALEX Liquidity Pool](https://app.alexlab.co/pool/token-amm-pool-v2-01:token-wstx,age000-governance-token,1e8) on the ALEX Lab platform to explore real-time information and stats. You should be able to understand displayed info after this section.
{% endhint %}

### 🙋 First time as liquidity provider?

Visit our how-to sections for a step-by-step guide on [How to Add/Remove Liquidity](https://docs.alexlab.co/how-to/how-to-add-remove-liquidity).
