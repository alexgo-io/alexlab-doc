---
description: Create your own pool and make your token tradeable on ALEX decentralized exchange in simple steps!
---

# 📝 Self-Service Listing

{% hint style="warning" %}
**Supported Tokens:** ALEX Self-Service Listing currently supports Stacks Chain Tokens (SIP-010 Standard Token).
{% endhint %}

## 🚀 Getting Started

### How Does It Work?

Self-Service Listing allows you to **create your own liquidity pool** on the ALEX DEX, enabling the **permissionless trade** of the **listed token** with an **anchor token** within the exchange. The anchor token is typically one with a stable value, providing a reliable reference point for defining the price of the newly listed token.

Pool creation usually takes between 24 to 48 hours. Once the pool is created and live, the price discovery phase begins: users can start trading the listed token against the anchor token and viceversa. Users interested in providing liquidity can contribute to the pool like any other ALEX pool.

The pool owner is the initial liquidity provider and will receive the corresponding LP tokens upon successful pool creation. Once the pool is live and operational, the owner can withdraw funds just like any other liquidity provider.

{% hint style="info" %}
Avaiblable Anchor Tokens: Native STX token, ALEX token and aBTC token.
{% endhint %}

The trading pool operates under the [ALEX Automated Market Maker (AMM)](../../detailed-information/alexs-automated-market-maker-amm.md) algorithm, which dynamically determines the exchange rate (price) based on the trades.

### Minimum Requirements

👉 **Token Deployment.** Ensure your token is deployed on the Stacks blockchain, as you will need to provide the token contract.

👉 **Select an Anchor Token.** Choose an anchor token from the available options: Stacks native token STX, ALEX token, or aBTC token. Ensure you have at least 1,800 STX or an equivalent value in $ALEX or aBTC token to create the pool—this is the minimum anchor token liquidity.

👉 **Determine Initial Price.** Decide the initial price for your listing token in terms of anchor token units. This should answer the question: how many anchor tokens do users need to buy one listed token?

👉 **Calculate Initial Liquidity.** Once the initial price is determined, you can set the initial liquidity amounts for both tokens in the pool. You may calculate this manually or use the ALEX Lab UI for assistance. If you're planning to [add farming to the pool](self-service-farming.md), make sure to reserve enough tokens for farm rewards.

<details>

<summary>Manual Calculation Example (Price, Ratio & Initial Amounts)</summary>

Let's suppose you choose STX as the anchor token and want to provide 4,000 STX as the initial anchor token liquidity.

To determine the price, you will need to decide how many STX equals 1 of your listing token. In other words, decide how many STX users will need to buy 1 listed token. Let's say you set the price of your token at 0.5 STX.

To calculate the initial liquidity for the listed token, you need to divide the anchor token amount by the price. This is `4,000 STX / 0.5 STX = 8,000`, resulting in the initial amount for the listed token.

The liquidity pool for the pair **Listed Token :rocket: - Anchor Token :anchor:** will have an initial ratio of 2:1. This ratio is calculated as the minimal expression of the fraction `8,000 / 4,000` (initial listed token amount slash initial anchor token amount).

</details>

🔎 For more details, check the [FAQs](./liquidity-pools/faqs.md#self-service-listing) section.

With that said, let's get hands-on!

## 🛠️  Procedure

### Step 0: Go to the Self-Service Listing Page

Head to the [Self-Service Listing page](https://app.alexlab.co/self-service-listing) at the ALEX Lab App. Alternatively, you can access it via the [app.alexlab.co](https://app.alexlab.co) homepage by navigating to the `Swap` -> `Pool` tab. Once on the Pool main page, hit the `+ Create` button and select the `Creating a new pool` option.

<figure><img src="../.gitbook/assets/self-service-listing/main-page.png" alt="Self-Service Listing page" width=""><figcaption></figcaption></figure>

### Step 1: Submit Token Information & Deposit the Anchor Token

In this step, you will set up the pool trading pair and configuration parameters. As part of this same transaction, you will transfer the anchor token's initial liquidity :moneybag: :anchor:.

<figure><img src="../.gitbook/assets/self-service-listing/step-1-submit.png" alt="Self-Service Listing page" width=""><figcaption></figcaption></figure>

<details>

<summary>Step 1.1: Input the SIP-10 Token Contract Address</summary>

Provide the listed token contract address. Ensure it complies with the [SIP-010 Fungible Token Standard](https://github.com/stacksgov/sips/blob/main/sips/sip-010/sip-010-fungible-token-standard.md) trait. In the example, the contract address is `SP108J6F4C7JD93BGJ91TEB5D3CFB5XW39QHDJ3MV.rabby-token`.

</details>

<details>

<summary>Step 1.2: Confirm Token Information Provided by the Contract</summary>

Verify that the token information retrieved from the contract is correct. In the example:

- **Token name** -> `RABBY Token`
- **Token symbol** -> `RABBY`
- **Description** -> Unlock the potential of programmable adventures within Bitcoin's rabbit holes.
- **Token deployment address** -> `SP108J6F4C7JD93BGJ91TEB5D3CFB5XW39QHDJ3MV`
- **Token logo**

</details>

<details>

<summary>Step 1.3: Set the Initial Liquidity & Price</summary>

Enter the initial balances for both tokens. You can experiment with different amounts to observe how the exchange rate changes, though we recommend calculating these values beforehand.

In the screenshot example, this is:

- **Anchor Token ⚓** (a.k.a `token-x`) -> `4,000 STX ($7,200)`
- **Listing Token 🚀** (a.k.a `token-y`) -> `200,000 RABBY`
- **Exchange Rate ⚖️** -> `1 RABBY = 0.02 STX ($0.03)`

Once the pool opens, the AMM algorithm will automatically rebalance the exchange rate as users trade the tokens.

</details>

<details>

<summary>Step 1.4: Advanced Pool Settings (Optional)</summary>

This step is optional, as the default settings are usually sufficient.

However, we recommend consulting the [ALEXGo Technical documentation](https://docs.alexgo.io/automated-market-making/trading-pool) before making customizations. If you have questions to ask before customization, reach out via [Discord](https://discord.com/invite/alexlab) or [Telegram](https://t.me/AlexCommunity).

</details>

<details>

<summary>Step 1.5: Submit Transaction</summary>

Keep in mind that as part of this same transaction, you will transfer the anchor token's initial liquidity. By confirming the transaction, you are accepting the transfer of specific amount of anchor tokens from your wallet to the ALEX smart contract.

Click `Submit` and scroll through the wallet transaction window, ensuring the parameters and transfer amount are correct. If everything looks good, confirm the transaction on your wallet. This will allow your wallet to sign and broadcast the transaction.

{% hint style="info" %}
Recommended to track transaction status:

* Turn on [Telegram notifications](https://t.me/stacks\_tx\_notification\_bot), you will get notified when the transaction is confirmed.
* Search for the transaction on the [ALEX Explorer](https://app.alexlab.co/explorer).
* Check your address activity on the wallet.
{% endhint %}

</details>

### Step 2: Contract Creation

After submitting the Self-Service Listing Pool, a pop-up will appear, allowing the creator to choose whether to lock or burn the initial LP tokens, or to leave the liquidity pool unlocked. By default, the Self-Service Listing Pool is set to be locked for 6 months, as it is the recommended option. Users are prompted to select one of three settings:

- **Do not lock LP 🔓**: There will be no lock-up period and the initial liquidity provider (the pool creator) will receive the corresponding LP tokens once the pool is live and operational. Since the pool is unlocked, the owner will be able to withdraw liquidity at any time. 

- **LP is locked for 6 months 🔒** : This is the default option. It locks liquidity within decentralized smart contracts for a 6 month period, requiring a manual LP claim upon maturity. When the period concludes, the pool owner can withdraw liquidity as any other provider. This prevents unexpected withdrawals and protects liquidity providers from rug pulls.

- **Burn LP 🔥** : Permanently burns a portion of tokens, ensuring that they can never be recovered or withdrawn. Since the initial liquidity vanishes, this option protects future liquidity providers from rug pulls and enhances trust and transparency.

<figure><img src="../.gitbook/assets/self-service-listing/lock-lp-1.png" alt="LP Lock Settings labels" width=""><figcaption></figcaption></figure>

In case of locking or burning tokens, there will be a highlighted banner that displays the setting selected by the pool creator. This way, liquidity providers will know if the initial LP tokens have been locked or burnt, or if neither option has been applied.

### Step 3: Contract creation

Once the transaction you executed in Step 1 is completed, you will see the checkbox labeled `Deposit Anchor Token ✅` marked as done. The ALEX team will review the submitted information and create a specific contract (a wrapped version) for your token to interact with the AMM DEX. This process may take between 24 and 48 hours.

### Step 4: Deposit Listing Token

Once the `Contract ready ✅` checkbox is marked as done, you're ready to deposit the listing token balance. This step involves interacting with a smart contract, so be sure to review the transaction details, paying particular attention to the amount to transfer. By accepting this transaction, you agree to transfer the initial liquidity of the listing token from your wallet to the ALEX smart contract.

### Step 5: Pool Creation Success

Once the `Deposit Listing Token ✅` transaction is completed and the `Open pool ✅` checkbox is marked as done, your pool will be automatically ready for use. The new pool will appear as an ALEX Pool under the `Self Listed` tab on [app.alexlab.co/pool](https://app.alexlab.co/pool).

🤝 After completing this step, you (and everyone) can start trading the token pair on ALEX DEX 🤝

<figure><img src="../.gitbook/assets/self-service-listing/pool-creation-successful.jpg" alt="Pool creation successful" width=""><figcaption><p>Pool creation successful.</p></figcaption></figure>

{% hint style="warning" %}
If you have added a custom `start-block` configuration, the pool will be unavailabe until that block is reached.
{% endhint %}

### Step 6: Provide Additional Token Information (Optional)

To make your token visible on the ALEX Token List at [app.alexlab.co/token-list](https://app.alexlab.co/token-list), provide additional token information. Click on `Customer Support` on the [Self-Service Listing page](https://app.alexlab.co/self-service-listing) or contact us via Telegram at [t.me/ALEXselfservice ](https://t.me/ALEXselfservice) to submit the information (e.g. X accont, Discord, official website).

<figure><img src="../.gitbook/assets/self-service-listing/token-list.png" alt="Token List example" width=""><figcaption><p>Token List example.</p></figcaption></figure>

ALEX requires a [Coingecko](https://www.coingecko.com/) or [CoinMarketCap](https://coinmarketcap.com/) token listing to verify the provided social media information before uploading it to the official list at [app.alexlab.co/token-list](https://app.alexlab.co/token-list).

Thanks for creating your pool on the ALEX DEX 🎉 📈 

<!-- 
Summarized Steps:

1) User submits token information, balances and config params. Within this same transaction, transfers the anchor token balance.

2) User selects LP Lock settings

3) User waits for token confirmation from ALEX

4) User deposits the listed token balance.

5) Once this tx is confirmed, the pool is automatically created and available (if start-block is configured "On finalization").

-->