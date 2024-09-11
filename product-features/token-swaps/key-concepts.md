---
description: >-
  Learn the key terms involved in ALEX swap operations.
---

# Key concepts

### Token Swap

A Token Swap is the exchange or trade of a certain amount of one crypto asset for another. In ALEX Lab Platform, swaps are performed on the ALEX's decentralized exchange (DEX) and are facilitated by liquidity pools.

### Swap Transaction

The ALEX DEX operates through smart contracts built on the Stacks blockchain, so all interactions, including swaps, are carried out through blockchain transactions. When you confirm a swap transaction on the ALEX Lab Platform, you are submitting it to the Stacks network to interact with the ALEX DEX smart contract. Once the transaction confirmed, it means the swap was executed successfully. If the transaction is reverted, no funds will be lost.

### Base Token

The token you currently hold and want to exchange. Is the token you will transfer to ALEX smart contract during the swap transaction.

### Target Token

Also know as the "quoted token", this is the token you will receive in the swap transaction in exchange for the base token.

### Exchange Rate

The exchange rate determines how many target tokens you would receive for one base token. On ALEX DEX, this rate is algoritmically determined by the ALEX Automated Market Maker (AMM) protocol and is updated after each swap.

### Swap Fee

Is the cost associated with performing a swap. It is deducted from the base token amount and is tipically set at 0.5%, though it can vary depending on the token pair (liquidity pool) involved.

### Swap Route

If a direct swap between your desired token pair isn't possible, ALEX DEX may use intermediate tokens to complete the exchange. For example, swapping Token-A to Token-C might require an intermediate swap through Token-B. This process is known as a multi-hop or multi-step swap. In this case, the swap route would be Token-A -> Token-B -> Token-C, where Token-B is the intermediate token. Routes on ALEX DEX can involve up to three intermediate tokens.

### Slippage

Since the exchange rate fluctuates due to ongoing trades and blockchain transactions are not instantaneous, the price at the moment of the swap transaction execution may differ from the price at the moment of submitting the transaction. This difference is called slippage and occurs when traders have to accept a different price than what they initially requested.

### Slippage tolerance

ALEX Lab Platform allows you to set a maximum percentage for slippage, which is the maximum price movement youare willing to accept between submission and execution of the swap transaction. The default slippage tolerance is 4%, but you can adjust this setting. If the price movement exceeds the slippage tolerance, the transaction will be canceled.

### Price Impact

The price impact refers to how much a swap affects the exhange rate. You might encounter it expressed as a percentage. For small swaps, price impact is typically negligible. However, for larger swaps, the price impact increases as the trade size approaches the pool's liquidity. This is why having a slippage tolerance is so important.
