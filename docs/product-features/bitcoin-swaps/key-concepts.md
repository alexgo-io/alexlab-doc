---
description: Learn the key terms involved in swap operations.
---

# 💡 Key concepts

### Token Swap

A Token Swap is the exchange or trade of a certain amount of one crypto asset for another. In ALEX Lab Platform, swaps are performed on the ALEX's decentralized exchange (DEX) and are facilitated by liquidity pools. 

### Base Token

The token you currently hold and want to exchange. This is the token you will transfer to the ALEX smart contract during the swap transaction.

### Target Token

Also known as the "quoted token", this is the token you will receive in the swap transaction in exchange for the base token.

### Swap Transaction

All interactions on the ALEX DEX are carried out through smart contracts that operate on the Stacks blockchain. As you may know, it is not possible to deploy complex smart contracts on the Bitcoin blockchain, so ALEX uses Stacks to add a financial layer to Bitcoin. 

**Bitcoin Native Swaps** operate by bridging the **base token** on Bitcoin to Stacks, where the swap is performed. Afterwards, the token will be bridged from Stacks to the **target token** on Bitcoin. From a user standpoint, this operation is seamlessly handled by the ALEX DEX, since you will send and receive tokens from the same Bitcoin address. Once the transaction is confirmed, it means the swap was executed successfully. If the transaction is reverted, no funds will be lost.

The Bitcoing Native Swap eliminates the need for intermediate operations, saving time and protecting the user from fluctuations in prices. For more information on the benefits of the Bitcoin Native Swap, you can consult the [FAQs](./faqs.md).

### Exchange Rate

The exchange rate determines how many target tokens you would receive for one base token. On the ALEX DEX, this rate is algorithmically determined by the [ALEX Automated Market Maker (AMM)](../../detailed-information/alexs-automated-market-maker-amm.md) protocol and is updated after each swap.

### Swap Fee

This is the cost associated with performing a swap. It is deducted from the base token amount and is tipically set at 0.5%, though it can vary depending on the token pair (liquidity pool) involved. **Swap Fees** are distributed among Liquidity Providers and the ALEX Lab Platform.

The swap fees on the Bitcoin Native Swap are expressed in sat/vB, or satoshis per virtual bytes. Satoshis are the smallest units of Bitcoin and virtual Bytes are a measure of transaction size on the Bitcoin Network.

### Swap Route

If a direct swap between your desired token pair isn't possible, ALEX DEX may use intermediate tokens to complete the exchange. For example, swapping Token-A to Token-C might require an intermediate swap through Token-B. This process is known as a multi-hop or multi-step swap. In this case, the swap route would be Token-A -> Token-B -> Token-C, where Token-B is the intermediate token. Routes on ALEX DEX can involve up to three intermediate tokens.

### Slippage

Since blockchain transactions are not instantaneous, the price at the moment of executing a swap may differ from the price when the transaction was submitted. This occurs because ongoing trades cause fluctuations in the exchange rate between a token pair. This difference between the prices at the moment of submission and execution is known as slippage, and users may set it at whatever percentage they find most convenient.

### Slippage Tolerance

ALEX Lab Platform allows you to set a maximum percentage for slippage, which is the maximum price movement you are willing to accept between submission and execution of the swap transaction. The default slippage tolerance is 4%, but you can adjust this setting. If the price movement exceeds the slippage tolerance, the transaction will be reverted.

### Price Impact

The price impact refers to how much a swap affects the exchange rate. You might encounter it expressed as a percentage. For small swaps, price impact is typically negligible. However, for larger swaps, the price impact increases as the trade size approaches the pool's liquidity.