---
description: >-
  In this guide, you'll find the required steps to withdraw liquidity from ALEX DEX pools.
---

# 🧑‍🏫 How to remove liquidity

When **removing liquidity**, you will transfer your LP tokens back to the ALEX smart contract and withdraw an equivalent value of the token pair plus any fees accrued while holding those LP tokens. Since the relative balance of the tokens in the liquidity pool may have changed since your initial deposit, you could experience what's known as [Impermanent Loss](key-concepts.md#impermanent-loss).

Ready to start? Let's get hands-on!

### Step 1

As when adding liquidity, go to [https://app.alexlab.co/](https://app.alexlab.co/) and click on navbar's Swap -> Pool tab.

<figure><img src="../../.gitbook/assets/liquidity-pools/adding-liquidity-1-pool-tab.png" alt="" width="375"><figcaption></figcaption></figure>

Once you're on the Pool page, you'll find the "My Liquidity" panel at the top of the pool list. This panel provides a summary of all your pool contributions.

<figure><img src="../../.gitbook/assets/liquidity-pools/removing-liquidity-1-my-liquidity-main-panel.png" alt=""><figcaption><p>The pools where you are providing liquidity are displayed here. There is only one in this example.</p></figcaption></figure>

### Step 2

Select the pool you would like to remove liquidity from, either through the "My Liquidity" panel or directly from the pool list.

<figure><img src="../../.gitbook/assets/liquidity-pools/removing-liquidity-2-select-pool.png" alt=""><figcaption><p>STX-ALEX pool selection.</p></figcaption></figure>

### Step 3

Once in the panel of the pool, select the "Remove Liquidity" tab.

<figure><img src="../../.gitbook/assets/liquidity-pools/removing-liquidity-3-remove-tab.png" alt="" width="375"><figcaption></figcaption></figure>

### Step 4

For this step, it's important to have in mind that the LP tokens you hold represent your share of the pool's funds. By entering the LP token amount, you're specifying the portion of the pooled funds you want to withdraw. Clicking the "Max" button sets your entire LP token balance, indicating you want to remove all liquidity from the pool.

When you enter the amount of LP tokens, you are specifiyng amount you will transfer to ALEX smart contract in order to receive your funds and any accrued fees in return. These fees are the ones accrued while holding those LP tokens.

Once you have decided the LP token amount, click the "Remove" button.

<figure><img src="../../.gitbook/assets/liquidity-pools/removing-liquidity-4-enter-amount.png" alt="" width="375"><figcaption><p>Example of removing all liquidity; the amount matches the LP token balance.</p></figcaption></figure>

### Step 5

A confirmation panel will appear where you can double check the amount. If everything looks correct, click "Confirm" :sunglasses:

<figure><img src="../../.gitbook/assets/liquidity-pools/removing-liquidity-5-confirm-remove-liquidity.png" alt="" width="375"><figcaption></figcaption></figure>

### Step 6

After clicking "Confirm", you will need to confirm the transaction in your wallet. Here, your Stacks wallet is interacting with ALEX smart contract and is asking you for approval. Scroll through the wallet transaction window, review it and confirm the transaction. By doing this, you are allowing the wallet to sign and broadcast the transaction.

<figure><img src="../../.gitbook/assets/liquidity-pools/removing-liquidity-6-reduce-position-function-args.png" alt="" width="375"><figcaption><p>Function arguments and confirmation button.</p></figcaption></figure>

### Step 7

Wait for the transaction to be confirmed on the network.

<figure><img src="../../.gitbook/assets/liquidity-pools/adding-liquidity-7-tx-broadcasted.png" alt="" width="375"><figcaption></figcaption></figure>

{% hint style="info" %}
Recommended to track transaction status:

* Turn on [Telegram notifications](https://t.me/stacks_tx_notification_bot), you will get notified when the transaction is confirmed.
* Search for the transaction on the [ALEX Explorer](https://app.alexlab.co/explorer).
* Check your address activity on the wallet.
{% endhint %}

<div><figure><img src="../../.gitbook/assets/liquidity-pools/removing-liquidity-7-tg-tx-pending.png" alt="" width="344"><figcaption><p>Telegram message with transaction pending status.</p></figcaption></figure> <figure><img src="../../.gitbook/assets/liquidity-pools/removing-liquidity-7-tg-tx-success.png" alt="" width="361"><figcaption><p>Telegram message with transaction success status.</p></figcaption></figure></div>

<div><figure><img src="../../.gitbook/assets/liquidity-pools/removing-liquidity-7-leather-tx-pending.png" alt="" width="375"><figcaption><p>Transaction pending displayed on Leather wallet.</p></figcaption></figure> <figure><img src="../../.gitbook/assets/liquidity-pools/removing-liquidity-7-leather-tx-success.png" alt="" width="375"><figcaption><p>Transaction completed, token transfers are visible.</p></figcaption></figure></div>

### Step 8

Once the transaction is completed, you will see the changes reflected in the "My Liquidity" panel, and the updated token balances should appear in your wallet.

<figure><img src="../../.gitbook/assets/liquidity-pools/removing-liquidity-8-my-liquidity.png" alt=""><figcaption></figcaption></figure>

[^1]: The APR metric is the same as the displayed in the Fee Rebate column on the previous step.
