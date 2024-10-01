---
coverY: 0
layout:
  cover:
    visible: false
    size: full
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 📝 Self-Service Listing

## Self-Service Listing Procedure

Step 1: Submit the token information & deposit the anchor token (Token Y)

Step 2: Waiting for the pool contract creation (around 24-48 hours)

Step 3: Deposit the listing token (Token X)

Step 4: Open Pool

Step 5: Provide additional token information

***

## Example: Self-service listing for “STX-PEPE” pool

### Step1：Submit the token information & deposit the anchor token

#### **Step 1.1 Input the SIP-10 token contract address**

(e.g. Token PEPE： SP1Z92MPDQEWZXW36VX71Q25HKF5K2EPCJ304F275.tokensoft-token-v4k68639zxz)

<figure><img src="../.gitbook/assets/image (8).png" alt="" width="375"><figcaption></figcaption></figure>

#### **Step 1.2 Confirm token information provided by the contract**

*   Example:

    Token name: Pepe Coin

    Token symbol: PEPE

    Description: Greetings, Earthlings! I grant you the opportunity to join my intergalactic economy by embracing Pepe Coin (PEPE).

    Token contract address： SP1Z92MPDQEWZXW36VX71Q25HKF5K2EPCJ304F275

    Token logo

#### **Step 1.3 Confirm the initial liquidity**

*   Example

    Token X: 1,000,000 PEPE

    Token Y: 1,800 STX

    Initial exchange rate：

    1 Pepe Coin =0.0018STX

\*Once the AMM pool opens, the exchange rate of the AMM pool will automatically re-balance as users buy or sell the token.

#### **Step 1.4 Advanced pool settings（you can keep the default settings）**

*   Example

    STX-PEPE pool setting：

    STX-PEPE swap fee rate = 0.3% （fee-rate-x,fee-rate-y）

    Threshold of a single transaction = pool size\*10% （max-in-ratio, max-out-ratio）

    Start block: on finalization （trading will commence once the creation process is finalized）

#### **Step 1.5 Submit**

Click to submit Pool information and deposit the initial liquidity of the Anchor Token.

*   Example

    PEPE deposit 1,800 STX

### Step 2：Waiting for pool contract creation

* Once the pool contract is created, 'Contract Ready' status will display 'Ready'.

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

### Step3：Deposit Token X

* After creating the contract, click on 'Deposit' to add an amount of Token X matching the amount you previously submitted.
  *   Example

      ```
       PEPE needs to deposit 1,000,000 $PEPE token
      ```

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

### Step4：Open Pool

Once the 'Open Pool' status appears as "Succeeded," it indicates that the pool has been launched and is listed under ALEX Pool -> self-service pool ([https://app.alexlab.co/pool](https://app.alexlab.co/pool) ). You can now proceed with trading your token on the ALEX DEX.

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

### **Step5：Provide additional token information**

Click “Contact Us” or "Customer Support" in the Self-Service Listing guide, to add social media information such as Twitter, Official website, etc.

ALEX requires a “Coingecko” or “CoinMarketcap” token listing to verify the provided social media information.

The token's social media information will be displayed on the ALEX Token List: [https://app.alexlab.co/token-list](https://app.alexlab.co/token-list).
