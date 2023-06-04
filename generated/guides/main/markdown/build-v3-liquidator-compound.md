## Compound III Liquidator


## Intro to Liquidation

## Liquidation
Liquidation refers to the process of seizing and selling collateral in DeFi lending and borrowing platforms when its value drops below a specific threshold known as the liquidation ratio. 

This ratio is set by the lending platform to ensure that there is enough collateral to cover the outstanding loan, and it represents the minimum ratio of the collateral's value to the loan value. To avoid liquidation, borrowers must usually provide collateral that exceeds the loan amount, which is called over-collateralization. 

The degree of over-collateralization required varies depending on the lending platform and the cryptocurrency used as collateral. Over-collateralization helps to mitigate the risk of default or a decrease in collateral value, ensuring there is enough collateral to cover outstanding debt and minimizing risk for lenders and the lending platform.

## Liquidation Process
When a borrower places cryptocurrency as collateral and borrows another cryptocurrency, the lending platform constantly monitors the value of the collateral. If the value falls below the liquidation ratio, the loan is considered undercollateralized, and liquidation can occur.

The liquidation process involves a liquidator purchasing the collateral at a discounted price to cover the outstanding loan. The liquidator receives a discount on the collateral to compensate for the risk they are taking on. The discount is determined by the lending platform and is designed to incentivize liquidators to participate in the liquidation process.

The proceeds from the sale of the collateral are then used to repay the outstanding loan. If the proceeds are greater than the outstanding loan, the excess is returned to the borrower. However, if the proceeds are not enough to cover the outstanding loan, the borrower is responsible for the difference. In some cases, the lending platform may absorb some of the losses.

It's important for borrowers to be aware of the liquidation process and the risks involved. They should also make sure to maintain their collateral above the liquidation ratio to avoid liquidation. On the other hand, liquidators can benefit from the discounted collateral prices, but they also take on the risk of the collateral value decreasing further after the purchase. Overall, the liquidation process is designed to protect the lending platform and its users from significant losses due to undercollateralized loans.

    


---
## Evaluation





##### What is the liquidation ratio in DeFi lending and borrowing platforms?  
     
- [ ]  The minimum ratio of the collateral's value to the loan value
- [ ]  The maximum ratio of the collateral's value to the loan value
- [x]  The minimum ratio of the loan value to the collateral's value
- [ ]  The maximum ratio of the loan value to the collateral's value





##### What happens if the proceeds from the sale of the collateral are not enough to cover the outstanding loan in a liquidation?  
     
- [ ]  The borrower is not responsible for the difference
- [ ]  The liquidator is responsible for the difference
- [ ]  The lending platform absorbs all the losses
- [x]  The borrower is responsible for the difference, and the lending platform may absorb some of the losses

    


---
## Liquidation in Compound III

## Changes to the liquidation system in Compound III
The latest version of the Compound protocol has undergone changes in its liquidation system. To ensure the system's solvency, the protocol takes over borrower accounts that violate the collateral requirements. Underwater borrowers are repaid using the protocol's reserves. However, if the protocol reserves fall below a governance-selected threshold, anyone can extract value after the account is absorbed.

## Liquidation criteria in Compound III
Like other DeFi projects, Compound III demands that borrowers maintain a greater value of collateral locked in the protocol than the total value of their borrow at all times, a process called over-collateralization. When a borrower accrues excessive interest on their borrow, or the USD value of their collateral decreases too much, or the USD value of their borrow rises too much, the account becomes liquidatable.

## Incentives for liquidators in Compound III
During the liquidation process, any account can extract value through an arbitrage opportunity. When the protocol absorbs an account, it repays its open borrow of the base asset using the protocol reserves and seizes the entire collateral assets of the account. Using the protocol's price feed, the seized collateral's discounted price is determined and then publicly sold. Any account can purchase the discounted collateral using the base asset. A liquidator can purchase the discounted collateral asset, trade it on a DEX at a higher price, and earn the difference in a single EVM transaction.

## Blockchains for Liquidation
Liquidations can occur on any blockchain where Compound III is deployed, and the protocol is written in Solidity and can be deployed to any EVM chain that has a price feed, sufficient liquidity, and a means for on-chain governance. However, running the liquidator bot contract example in the Comet repository is not recommended as it only serves as an educational tool, and running it may result in reverted transactions and EVM gas wasted as a result of losing the battle to better running searchers.


    


---
## Evaluation





##### What happens to the collateral assets of a liquidated borrower's account in Compound III?  
     
- [ ]  They are returned to the borrower
- [ ]  They are burned and removed from the protocol
- [x]  They are sold at a discounted price
- [ ]  They are locked in the protocol indefinitely





##### What is the incentive for liquidators in Compound III?  
     
- [ ]  They receive a percentage of the borrower's collateral assets
- [x]  They can purchase the discounted collateral assets and sell them at a higher price
- [ ]  They can liquidate accounts without penalty
- [ ]  They can manipulate the protocol's price feed to their advantage.

    


---
## V3 Liquidation Process

Liquidation is determined based on liquidation collateral factors, which are distinct and higher than borrow collateral factors used for determining initial borrowing capacity. This mechanism safeguards both borrowers and the protocol by ensuring a price buffer for all new positions. Additionally, this system enables governance to decrease borrow collateral factors without initiating the liquidation of existing positions.

When an account's borrowing balance surpasses the limits set by liquidation collateral factors, it becomes qualified for liquidation. The absorb function can be activated by a liquidator (a bot, contract, or user), which transfers ownership of the account's collateral and refunds the user the value of the collateral minus a penalty (liquidationFactor) in the base asset. Following liquidation, the user has no outstanding debt and will usually have an excess balance of the base asset, which can earn interest.

The protocol's reserves of the base asset fund each absorption. In exchange, the protocol gains ownership of the collateral assets. If the remaining reserves are lower than a governance-set target, liquidators can purchase the collateral at a discount using the base asset, which boosts the protocol's reserves of the base asset.

    


---
## Evaluation





##### What safeguards both borrowers and the protocol by ensuring a price buffer for all new positions in liquidation?
  
     
- [ ]  Governance-set liquidation amount
- [ ]  Initial borrowing capacity
- [ ]  Liquidation collateral factors that is less than Borrow collateral factors
- [x]  Liquidation collateral factors that is more than Borrow collateral factors

    


---
## Step by Step Process

This is an example of how Compound III handles liquidations

1. If a borrower doesn't have enough collateral to cover their loan or the value of their collateral drops too much, their account can be liquidated. This can be checked at any time programmatically using the Comet `isLiquidatable` function, which returns a boolean.

2. A person who notices the liquidation creates a transaction to make money through arbitrage.

3. The first step in the process is for the protocol to move the borrower's collateral to the protocol balance sheet to cover the loan. This is done by invoking the `absorb` function on the Comet smart contract. 

4. The absorb function guarantees that the current reserves value is lower than targetReserves. Once targetReserves is achieved, the v3 contracts retain the collateral assets and provide compensation to the liquidator through rewards. However, reaching the high value of targetReserves is unlikely.

4. The person then figures out how much of the borrower's collateral they can buy with the base asset. To ascertain the payment for the base asset, the searcher should inspect the `collateralBalanceOf` for each associated collateral asset. After obtaining the asset's price through the price feed, they can utilize the `quoteCollateral` function to determine the discounted rate.

5. They can pay for this with their own money or by using another protocol to borrow the base asset. This can be done by calling `buyCollateral` to purchase as much of the discounted collateral as they can.

6. Once they have the collateral, they can sell it at a higher price on a DEX like Uniswap.

7. They use the profits to repay any borrowed base asset and keep the remaining balance for themselves.

    


---
## Your Info





| Label | Type | Required |
| ----------- | ----------- | ---- |
| Nickname        | PublicShortInput   |  true    |


    

