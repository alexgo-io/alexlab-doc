# 💸 How To Borrow

First， you’ll need to select the token you wish to borrow. Visit the[ ALEX DAPP](http://app.alexlab.co/), connect to Hiro wallet (upper right corner), go to the “LEND” tab on the top menu, and see a list of available tokens.

### Borrow <a href="#id-7b15" id="id-7b15"></a>

Having selected your preferred token:

1. Input the total amount you wish to borrow.
2. The maximum amount you can borrow will be capped by the amount of collateral token wallet and LTV (Loan-to-Value Ratio)
3. Confirm by selecting the “Borrow” button in the borrow panel and pop-up window.

After the borrow transaction proceeds, you will receive the borrowed tokens immediately in your wallet.

The borrow panel provides vital information for your borrowed tokens such as:

* Maturity: The maturity block when your borrow contract concludes. You may manually “rollover” your borrowed amount to extend its maturity to the next maturity block.
* Est. Interest: The interest paid upon borrowing the token.
* CRP Position: Borrowing on ALEX utilizes Collateral Rebalancing Pools (CRP) to manage your collateral and avert liquidation. CRP will dynamically allocate your collateral into both collaterals and borrow token pools. The CRP position provides borrowers a snapshot of the current pool weighting of the two tokens.
* Liquidity Provider Fee: The fee paid to the liquidity providers when borrowing.

![](https://miro.medium.com/max/1302/1\*j1jlqeZYTj\_XoeQjfNJZog.png)

The borrower can claim the collateral deposited upon maturity.

* The Collateral information is displayed in the “Borrowed” section, with the amount of both tokens as well as their estimated dollar value.

![](https://miro.medium.com/max/1400/1\*S4AqqWt\_sa5Ihj5ILFgrIA.png)

* Select the bar graph icon beside “Collateral” to display the collateral rebalancing details.

![](https://miro.medium.com/max/1400/1\*3WmOTXtxIQ4IBioiDiUtNg.png)

**Claim Collateral**

When the borrowing period gets to maturity, borrowers may claim their collateral by selecting the “Claim” button.

Borrowers do not need to manually repay the borrowed tokens when claiming their collateral, because Claim Value = Borrow Collateral Value — Borrowed Value.

![](https://miro.medium.com/max/1400/1\*ImTVSWIiJ0Jo1LA1LwsY5w.png)

Due to changing market conditions, borrowers may wish to extend the borrowing period.

**Roll Over**

Borrowers can manually roll over the borrowed contract to the next maturity block.

When doing so, the protocol will hold your collateral balance and roll it into the next borrowing period. This will help mitigate permanent losses due to shifting market conditions.

Once you’ve claimed your collateral, you will need to wait for the transaction to proceed to receive your remaining collateral value.

![](https://miro.medium.com/max/1400/1\*NHhh3KFqrAOz-TwLLaebvQ.png)
