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

The ALEX decentralized exchange is AMM-based and consists of a set of smart contracts built on top of the Stacks network. Each liquidity pool is composed of funds from a specific pair of cryptocurrencies, which are locked into a smart contract by voluntary depositors. These pools enable users to perform trustless swaps between the token pairs.

For example, if a user wants to trade Stacks' native currency (STX) for ALEX's governance token (ALEX), they would interact with the STX - ALEX liquidity pool on ALEX's smart contracts. For more details on how to execute such swaps, refer to the [Token Swaps](../token-swaps/) section.

The users who deposit their assets into these pools are known as liquidity providers (LPs). To incentivize participation, the ALEX AMM protocol rewards LPs with a portion of the trading fees collected on each swap. These fees are accrued every time a transaction occurs within the pool.

## Liquidity Providers (LPs)

In exchange for providing funds to a pool, liquidity providers receive an amount of LP tokens that represent their share of assets within that pool. LP token holders earn a proportional share of all transaction fees charged to traders who perform swaps within the pool. Liquidity can be removed at any time, and the earnings associated with those LP tokens are also withdrawn at this point.

For example, if a user holds 5% of the pool’s total funds, they will earn 5% of the transaction fees allocated to liquidity providers. These earnings are withdrawn when the liquidity is removed.

{% hint style="info" %}
**Note:** The initials "LP" are used both to abbreviate "liquidity provider" and to refer to the tokens these users receive, which represent their share of the contributed funds in the pool.
{% endhint %}

## Impermanent Loss

Impermanent loss in decentralized finance (DeFi) occurs when a liquidity provider (LP) supplies assets to a liquidity pool and the price of those assets changes relative to when they were deposited. This loss is termed "impermanent" because it only becomes permanent if the LP withdraws their funds when prices have diverged significantly.

Here's how it works:

* In most DeFi protocols, LPs provide two assets (e.g., STX and a stablecoin) in equal value to a liquidity pool.

* If the price of one asset (e.g., STX) rises or falls relative to the other, arbitrage traders will trade against the pool, ensuring that the asset prices in the pool reflect current market conditions.

* These trades lead to a different balance of assets in the pool (ratio). When the LP eventually withdraws their funds, they may receive a different amount of each asset than what they initially provided.

* If the value of the assets in the pool has diverged significantly, the LP might have been better off simply holding the assets outside of the pool, resulting in a perceived **loss**.

* This loss is termed **impermanent** because it can be mitigated if the token prices return to their original values. Additionally, this loss can be offset by trading fees earned from the pool, meaning the LP might still come out ahead if the accumulated fees exceed the loss.

{% hint style="info" %}
You can check a complete walkthrough example in the FAQs: [**How does impermanent loss happen?**](faqs.md#how-does-impermanent-loss-happen)
{% endhint %}
