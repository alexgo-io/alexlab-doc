---
description: >-
  In these two guides, you'll find the required steps to provide liquidity and
  to withdraw liquidity from ALEX DEX pools.
---

# How to add/remove liquidity

## :palm\_up\_hand: :moneybag: Adding Liquidity

### Step 1

Go to [https://app.alexlab.co/](https://app.alexlab.co/) and click on navbar's Swap -> Pool tab.

<figure><img src="../../.gitbook/assets/liquidity-providers/adding-liquidity-1-pool-tab.png" alt="" width="375"><figcaption></figcaption></figure>

All available pools will be displayed including information such as:

* **Trading Pair:** The token pair that constitute liquidity pools to which you can add liquidity.
* **Liquidity:** The total liquidity in the pool, expressed in USD value.
* **Volume:** The trading volume between the token pair over the last 7 days.
* **Fee Rebate:** Potential LP earnings from swap fees over a year, based on the last week's average. This metric, also known as Pool APR, reflects the potential profitability of participating in a pool over a year, assuming similar trading activity continues.&#x20;

### Step 2

Select the token pair to which you want to add liquidity from the displayed list. Note you can sort by pool metrics.

<figure><img src="../../.gitbook/assets/liquidity-providers/adding-liquidity-2-select-pool.png" alt=""><figcaption><p>Selected STX - ALEX liquidity pool as example.</p></figcaption></figure>

### Step 3

After selecting a pool, you will be taken to a control panel for that specific liquidity pool, where you can add liquidity to the token pair and view more detailed metrics.&#x20;

When you set the amount for one token, the corresponding amount for the other token is automatically calculated, as liquidity must be provided in equal value for both tokens.

<figure><img src="../../.gitbook/assets/liquidity-providers/adding-liquidity-3-pool-control-panel.png" alt=""><figcaption><p>Control panel example for STX - ALEX liquidity pool. Amount is set to 4 STX and ALEX token amount is automatically determined.</p></figcaption></figure>

### Step 4

If you want to adjust slippage, select the "Settings" icon to open the Transaction Settings panel and set your desired tolerance. The default slippage tolerance is set to 4%, meaning your transaction will revert if the price changes unfavourably by more than this percentage. The displayed number of LP tokens you will receive is approximate due to this potential variation.

<figure><img src="../../.gitbook/assets/liquidity-providers/adding-liquidity-4-settings-icon.png" alt="" width="375"><figcaption><p>Transaction Settings icon.</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/liquidity-providers/adding-liquidity-4-adjust-slippage.png" alt="" width="375"><figcaption><p>Transaction Settings panel example, with slippage tolerance set to 3%.</p></figcaption></figure>

### Step 5

One you decide the amount, click the "Add" button. Confirmation panel will appear. Here you can double check balances, slippage and LP tokens. If everything it's okay, click "Confirm" :sunglasses:

<figure><img src="../../.gitbook/assets/liquidity-providers/adding-liquidity-5-confirm-add-liquidity.png" alt="" width="375"><figcaption></figcaption></figure>

### Step 6

After clicking "Confirm", you will need to confirm the transaction in your wallet. Here, your Stacks wallet is interacting with ALEX smart contract and is asking you for approval. Scroll through the wallet transaction window, review it and confirm the transaction. By doing this, you are allowing the wallet to sign and broadcast the transaction.

{% hint style="info" %}
To be completely sure, you can check:

* Transaction is requested by **"Alex app" (app.alexlab.co)**
* The amounts you will transfer to the smart contract, covered by [Stacks post conditions](https://docs.stacks.co/stacks-101/post-conditions). Note that one transfer amount is exactly determined (STX in the example) while the other's is less than or equal to. This is because the potential slippage variation, and here we can see the exact upper bound. If this conditions are not met, the transaction will abort.
{% endhint %}

<div>

<figure><img src="../../.gitbook/assets/liquidity-providers/adding-liquidity-6-add-to-position-post-con.png" alt="" width="375"><figcaption><p>Amounts to transfer and post conditions.</p></figcaption></figure>

 

<figure><img src="../../.gitbook/assets/liquidity-providers/adding-liquidity-6-add-to-position-function-args.png" alt="" width="375"><figcaption><p>Function arguments and confirmation button.</p></figcaption></figure>

</div>

### Step 7

Wait for the transaction to be confirmed on the network.&#x20;

<figure><img src="../../.gitbook/assets/liquidity-providers/adding-liquidity-7-tx-broadcasted.png" alt="" width="375"><figcaption></figcaption></figure>

{% hint style="info" %}
Recommended to track transaction status:

* Turn on Telegram notifications, you will get notified when the transaction is confirmed.&#x20;
* Searching for the transaction on [explorer](https://explorer.hiro.so/txid/0x588d949ea697b325237eb20d5d3a6af5f6f496668cf0c7428ba79068573efba9?chain=mainnet). &#x20;
* Check your address activity on the wallet.
{% endhint %}

<div>

<figure><img src="../../.gitbook/assets/liquidity-providers/adding-liquidity-7-tg-tx-pending.png" alt="" width="348"><figcaption><p>Telegram message with transaction pending status.</p></figcaption></figure>

 

<figure><img src="../../.gitbook/assets/liquidity-providers/adding-liquidity-7-tg-tx-success.png" alt="" width="349"><figcaption><p>Telegram message with transaction success status.</p></figcaption></figure>

</div>

<div>

<figure><img src="../../.gitbook/assets/liquidity-providers/adding-liquidity-7-leather-tx-pending.png" alt="" width="375"><figcaption><p>Transaction pending displayed on Leather wallet.</p></figcaption></figure>

 

<figure><img src="../../.gitbook/assets/liquidity-providers/adding-liquidity-7-leather-tx-success.png" alt="" width="375"><figcaption><p>Transaction completed, token transfers are visible.</p></figcaption></figure>

</div>

### Step 8

After successfully adding liquidity, you will be able to see your LP tokens and further information in "My Liquidity" panel.

* **My LP** are your LP token holdings for the pool. Note LP tokens are specific por each pool.
* The **Pooled** amount represents the total token holdings of the liquidity pool.
* The **My Pool Share** reflects your contribution, as a percentage, to the pool’s liquidity for reference.
* The **Indicative Value** changes depending on the price action of both assets, which may result in changing values.

<figure><img src="../../.gitbook/assets/liquidity-providers/adding-liquidity-8-my-liquidity.png" alt=""><figcaption><p>"My Liquidity" panel. You can also find it in <a href="https://app.alexlab.co/pool">https://app.alexlab.co/pool</a>. </p></figcaption></figure>

## :palm\_down\_hand: :moneybag: Removing liquidity

### Step 1

As when adding liquidity, go to [https://app.alexlab.co/](https://app.alexlab.co/) and click on navbar's Swap -> Pool tab.

<figure><img src="../../.gitbook/assets/liquidity-providers/adding-liquidity-1-pool-tab.png" alt="" width="375"><figcaption></figcaption></figure>

You will be able to see your liquidity in the main "Pool" panel.

<figure><img src="../../.gitbook/assets/liquidity-providers/removing-liquidity-1-my-liquidity-main-panel.png" alt=""><figcaption><p>The pools where you are providing liquidity are displayed here.</p></figcaption></figure>

### Step 2

Select the pool you would like to remove liquidity from.

<figure><img src="../../.gitbook/assets/liquidity-providers/removing-liquidity-2-select-pool.png" alt=""><figcaption><p>STX - ALEX pool selection.</p></figcaption></figure>

### Step 3

Once in the panel of the pool, select the "Remove Liquidity" tab.

<figure><img src="../../.gitbook/assets/liquidity-providers/removing-liquidity-3-remove-tab.png" alt="" width="375"><figcaption></figcaption></figure>

### Step 4

Enter the amount of LP tokens you would like to withdraw and hit the "Remove" button.

<figure><img src="../../.gitbook/assets/liquidity-providers/removing-liquidity-4-enter-amount.png" alt="" width="375"><figcaption></figcaption></figure>

### Step 5

A confirmation panel will appear where you can double check the amount. If everything looks correct, click "Confirm" :sunglasses:

<figure><img src="../../.gitbook/assets/liquidity-providers/removing-liquidity-5-confirm-remove-liquidity.png" alt="" width="375"><figcaption></figcaption></figure>

### Step 6

After clicking "Confirm", you will need to confirm the transaction in your wallet. Here, your Stacks wallet is interacting with ALEX smart contract and is asking you for approval. Scroll through the wallet transaction window, review it and confirm the transaction. By doing this, you are allowing the wallet to sign and broadcast the transaction.

<figure><img src="../../.gitbook/assets/liquidity-providers/removing-liquidity-6-reduce-position-function-args.png" alt="" width="375"><figcaption><p>Function arguments and confirmation button.</p></figcaption></figure>

### Step 7

Wait for the transaction to be confirmed on the network.&#x20;

<figure><img src="../../.gitbook/assets/liquidity-providers/adding-liquidity-7-tx-broadcasted.png" alt="" width="375"><figcaption></figcaption></figure>

{% hint style="info" %}
Recommended to track transaction status:

* Turn on Telegram notifications, you will get notified when the transaction is confirmed.&#x20;
* Searching for the transaction on [explorer](https://explorer.hiro.so/txid/0xd34372393d5467dc5a0e161beeb3d376222690d24ab964edbd7f5bc80835559b). &#x20;
* Check your address activity on the wallet.
{% endhint %}

<div>

<figure><img src="../../.gitbook/assets/liquidity-providers/removing-liquidity-7-tg-tx-pending.png" alt="" width="344"><figcaption><p>Telegram message with transaction pending status.</p></figcaption></figure>

 

<figure><img src="../../.gitbook/assets/liquidity-providers/removing-liquidity-7-tg-tx-success.png" alt="" width="361"><figcaption><p>Telegram message with transaction success status.</p></figcaption></figure>

</div>

<div>

<figure><img src="../../.gitbook/assets/liquidity-providers/removing-liquidity-7-leather-tx-pending.png" alt="" width="375"><figcaption><p>Transaction pending displayed on Leather wallet.</p></figcaption></figure>

 

<figure><img src="../../.gitbook/assets/liquidity-providers/removing-liquidity-7-leather-tx-success.png" alt="" width="375"><figcaption><p>Transaction completed, token transfers are visible.</p></figcaption></figure>

</div>

### Step 8

Once the transaction is completed, you will see the changes reflected in the "My Liquidity" panel, and the updated token balances should appear in your wallet.

<figure><img src="../../.gitbook/assets/liquidity-providers/removing-liquidity-8-my-liquidity.png" alt=""><figcaption></figcaption></figure>
