---
description: >-
  In this guide, you'll find the required steps to provide liquidity to ALEX DEX pools.
---

# 🧑‍🏫 How to add liquidity

When **adding liquidity**, you will deposit an equivalent value of both tokens into the pool. In return, you'll receive LP tokens, which represent your share of that specific liquidity pool.

Ready to start? Let's get hands-on!

### Step 1: Go to the Pool Page

Go to [https://app.alexlab.co/](https://app.alexlab.co/) and click on navbar's Swap -> Pool tab.

<figure><img src="../../.gitbook/assets/liquidity-pools/adding-liquidity-1-pool-tab.png" alt="" width="375"><figcaption></figcaption></figure>

### Step 2: Select Pool

All available pools will be displayed including information such as:

* **Trading Pair:** The token pair that constitute liquidity pools to which you can add liquidity.
* **Liquidity:** The total liquidity in the pool, expressed in USD value.
* **Volume:** The trading volume between the token pair over the last 7 days. By hovering on the trading volume for a specific row/pool, the 24-hour volume is also displayed.
* **Fee Rebate:** Potential LP earnings from swap fees over a year, based on the last week's average. This metric, also known as Pool APR, reflects the potential profitability of participating in a pool over a year, assuming similar trading activity continues.

Select the token pair to which you want to add liquidity from the displayed list. Note you can sort by pool metrics.

<figure><img src="../../.gitbook/assets/liquidity-pools/adding-liquidity-2-select-pool.png" alt=""><figcaption><p>Selected STX-ALEX liquidity pool as example.</p></figcaption></figure>

{% hint style="warning" %}
When hovering over a pool, you might notice a "+LP" button. This serves as a visual indicator for the selected pool. Clicking it will take you to the same screen as clicking anywhere on the pool's row.
{% endhint %}

### Step 3: Add Liquidity to Your Pool

After selecting a pool, you will be taken to a control panel for that specific liquidity pool, where you can add liquidity to the token pair and view more detailed metrics[^1].

When you set the amount for one token, the corresponding amount for the other token is automatically calculated, as liquidity must be provided in equal value for both tokens.

**Need tokens?** Visit the [Token Swaps](../stacks-swaps/) docs section and to learn how to exchange tokens on ALEX Lab platform.

<figure><img src="../../.gitbook/assets/liquidity-pools/adding-liquidity-3-pool-control-panel.png" alt=""><figcaption><p>Control panel example for STX-ALEX liquidity pool. Amount is set to 4 STX and ALEX token amount is automatically determined.</p></figcaption></figure>

{% hint style="warning" %}
Clicking the "Max" button will automatically set the amount to your total available balance.
{% endhint %}

### Step 4: Adjust Transaction Settings

If you want to adjust slippage, select the "Settings" icon to open the Transaction Settings panel and set your desired tolerance. The default slippage tolerance for non-stable swap token pairs is set to 4%, meaning your transaction will revert if the exchange rate changes unfavourably by more than this percentage. The displayed number of LP tokens you will receive is approximate due to this potential variation.

<figure><img src="../../.gitbook/assets/liquidity-pools/adding-liquidity-4-settings-icon.png" alt="" width="375"><figcaption><p>Transaction Settings icon.</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/liquidity-pools/adding-liquidity-4-adjust-slippage.png" alt="" width="375"><figcaption><p>Transaction Settings panel example, with slippage tolerance set to 3%.</p></figcaption></figure>

### Step 5: Confirm Added Liquidity

One you decide the amount, click the "Add" button. Confirmation panel will appear. Here you can double check balances, slippage and LP tokens. If everything it's okay, click "Confirm" :sunglasses:

<figure><img src="../../.gitbook/assets/liquidity-pools/adding-liquidity-5-confirm-add-liquidity.png" alt="" width="375"><figcaption></figcaption></figure>

### Step 6: Confirm the Transaction in Your Wallet

After clicking "Confirm", you will need to confirm the transaction in your wallet. Here, your Stacks wallet is interacting with ALEX smart contract and is asking you for approval. Scroll through the wallet transaction window, review it and confirm the transaction. By doing this, you are allowing the wallet to sign and broadcast the transaction.

{% hint style="info" %}
To be completely sure, you can check:

* Transaction is requested by **"Alex app" (app.alexlab.co)**
* The amounts you will transfer to the smart contract, covered by [Stacks post conditions](https://docs.stacks.co/stacks-101/post-conditions). Note that one transfer amount is exactly determined (STX in the example) while the other is subject to a "less than or equal to" condition. This accounts the potential slippage variation, and here you can see the exact upper bound. If these conditions are not met, the transaction will abort.
{% endhint %}

<div><figure><img src="../../.gitbook/assets/liquidity-pools/adding-liquidity-6-add-to-position-post-con.png" alt="" width="375"><figcaption><p>Amounts to transfer and post conditions.</p></figcaption></figure> <figure><img src="../../.gitbook/assets/liquidity-pools/adding-liquidity-6-add-to-position-function-args.png" alt="" width="375"><figcaption><p>Function arguments and confirmation button.</p></figcaption></figure></div>

### Step 7: Wait for Transaction Confirmation

Wait for the transaction to be confirmed on the network.

<figure><img src="../../.gitbook/assets/liquidity-pools/adding-liquidity-7-tx-broadcasted.png" alt="" width="375"><figcaption></figcaption></figure>

{% hint style="info" %}
Recommended to track transaction status:

* Turn on [Telegram notifications](https://t.me/stacks_tx_notification_bot), you will get notified when the transaction is confirmed.
* Search for the transaction on the [ALEX Explorer](https://app.alexlab.co/explorer).
* Check your address activity on the wallet.
{% endhint %}

<div><figure><img src="../../.gitbook/assets/liquidity-pools/adding-liquidity-7-tg-tx-pending.png" alt="" width="348"><figcaption><p>Telegram message with transaction pending status.</p></figcaption></figure> <figure><img src="../../.gitbook/assets/liquidity-pools/adding-liquidity-7-tg-tx-success.png" alt="" width="349"><figcaption><p>Telegram message with transaction success status.</p></figcaption></figure></div>

<div><figure><img src="../../.gitbook/assets/liquidity-pools/adding-liquidity-7-leather-tx-pending.png" alt="" width="375"><figcaption><p>Transaction pending displayed on Leather wallet.</p></figcaption></figure> <figure><img src="../../.gitbook/assets/liquidity-pools/adding-liquidity-7-leather-tx-success.png" alt="" width="375"><figcaption><p>Transaction completed, token transfers are visible.</p></figcaption></figure></div>

### Step 8: Check the Updated Liquidity

After successfully adding liquidity, you will be able to see your LP tokens and related details in "My Liquidity" panel.

* **My LP** are your LP token holdings specific to the pool you contributed to. Each pool issues its own unique LP tokens.
* The **Pooled** amount represents your total token holdings in the liquidity pool. Initially, reflects the amount you added and it increases over time due to accrued fees, showing your updated share of the pool's total liquidity.
* The **My Pool Share** shows how much of the overall pool you own, as a percentage.
* The **Indicative Value** reflects the value of your holdings in USD, which can change based on the price action of the underlying assets.

<figure><img src="../../.gitbook/assets/liquidity-pools/adding-liquidity-8-my-liquidity.png" alt=""><figcaption><p>"My Liquidity" panel.</p></figcaption></figure>

{% hint style="info" %}
You can find the "My Liquidity" panel above the Liquidity Pool control panel (shown in Step 3). A summarized version is also available under the Swap -> Pool tab or at https://app.alexlab.co/pool.
{% endhint %}