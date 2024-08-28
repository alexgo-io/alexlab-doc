---
description: >-
  Learn the basics of liquidity pools and providers, their role in DEXs and
  AMMs, and their function within the ALEX decentralized exchange.
---

# Key concepts

## What are Liquidity Pools?

Liquidity pools are crowdfunded collections of crypto assets held in a smart contract, designed to provide liquidity for decentralized exchanges (DEXs) and support various decentralized finance (DeFi) protocols.

While their applications are diverse, ranging from lending and borrowing platforms to algorithmic protocols for stablecoins, their primary use is on DEXs. In this case, liquidity pools enable users to trade crypto assets without the need for a centralized intermediary, serving as reserves of assets that users can trade against.

## Their role in Automated Market Makers (AMMs)

Automated Market Makers (AMMs) are the predominant type of decentralized exchange (DEX). While other DEX designs exist, AMM-based DEXs have become extremely popular. These exchanges operate using liquidity pools and algorithmic mechanisms to determine prices and facilitate the trading of crypto assets between peers.

Smart contracts manage all trades executed within the AMM, including aspects such as fees, prices, and minimum target token amounts. In AMM-based DEXs, there is no need for direct counterparties as in traditional order book trading. Instead, liquidity pools act as the counterparties, providing instant liquidity when needed.

## ALEX Liquidity Pools

The ALEX decentralized exchange is AMM-based and consists of a set of smart contracts built on top of the Stacks network. Each liquidity pool is composed of funds from a specific pair of cryptocurrencies, vwhich are locked into a smart contract by voluntary depositors. These pools enable users to perform trustless swaps between the token pairs.

For example, if a user wants to trade Stacks' native currency (STX) for ALEX's governance token (ALEX), they would interact with the STX - ALEX liquidity pool on ALEX's smart contracts. For more details on how to execute such swaps, refer to the [Token Swaps](../token-swaps/) section.

The users who deposit their assets into these pools are known as liquidity providers (LPs). To incentivize participation, the ALEX AMM protocol rewards LPs with a portion of the trading fees collected on each swap. These fees are accrued every time a transaction occurs within the pool.

## Liquidity Providers (LPs)

In exchange for providing funds to a pool, liquidity providers receive an amount of LP tokens that represent their share of assets within that pool. LP token holders earn a proportional share of all transaction fees charged to traders who perform swaps within the pool. Liquidity can be removed at any time, and the earnings associated with those LP tokens are also withdrawn at this point.

For example, if a user holds 5% of the pool’s total funds, they will earn 5% of the transaction fees allocated to liquidity providers. These earnings are withdrawn when the liquidity is removed.

{% hint style="info" %}
**Note:** The initials "LP" are used both to abbreviate "liquidity provider" and to refer to the tokens these users receive, which represent their share of the contributed funds in the pool.
{% endhint %}
