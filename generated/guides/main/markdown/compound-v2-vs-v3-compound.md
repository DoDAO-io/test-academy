## Compound V2 vs V3


## Compound V3 Launch

Compound III is a refined version of the protocol that prioritizes security, capital efficiency, and user experience. Its design focuses on simplification rather than complexity, resulting in the most effective borrowing tool in DeFi.

The most significant improvement was moving away from the pooled-risk model, which allowed users to borrow any asset but constantly rehypothecated collateral. This model was vulnerable to a single bad asset or oracle update draining all assets from the protocol.

In Compound III, each market deployment offers a single borrowable asset, and the supplied collateral remains the property of the borrower, except during liquidation. This new approach increases capital efficiency and reduces risk since the collateral is more "useful" when the borrower knows the specific asset being borrowed in advance.

The first release of Compound III allows borrowing of USDC using ETH, WBTC, LINK, UNI, and COMP as collateral. Although borrowers will not earn interest on their collateral, they will be able to borrow more with lower risks of liquidation and penalties while spending less on gas fees.

wETH market is also live now, with `Coinbase Wrapped Staked ETH(cbETH)` and `Lido Staked ETH(stETH)` as collateral.

The repository uses a business source license, which Compound governance can grant usage to, as it sees fit.

    


---
## Evaluation





##### What is the focus of Compound III's design?  
     
- [ ]  Complexity
- [x]   Security, capital efficiency, and user experience
- [ ]  KYC/AML
- [ ]  Support at least top 200 assets





##### What was the problem with the pooled-risk model in the previous protocol?
  
     
- [ ]  Borrowers couldn't earn interest on their collateral.
- [ ]  The collateral remained the property of the borrower, except during liquidation.
- [x]  The model was vulnerable to a single bad asset or oracle update.
- [ ]  Borrowers could borrow any asset without collateral.

    


---
## Features and Advantages of V3

## New Features of Compound V3
The major changes to the existing protocol in Compound III can be summarized as follows:

1. Each Compound III deployment features a single interest-earning base asset, with all other assets serving as collateral. This simplifies the protocol, reduces risk, and potentially improves capital efficiency.
2. Collateral size limits, or supply caps, can be set for each collateral asset.
3. Borrowing collateral factors and liquidation collateral factors are separate, protecting borrowers from early liquidation and improving risk management.
4. The risk management and liquidation engine has been redesigned to increase the safety of the protocol while maintaining liquidator incentives.
5. The price feed is designed to use Chainlink directly, without requiring a custom price oracle, making it portable to EVM chains beyond Ethereum. Governance retains the ability to modify this decision in the future.
6. Supply and borrow interest rate models can be decoupled, giving governance full control over economic policy.
7. Advanced account management tools enable new user experience patterns and applications to be built on top of the protocol.
8. An abstract incentive metric is natively built into the core contract to reward user activity from the protocol's inception. A rewards system is also added on top to provide flexible incentives that can be extended by governance.
9. A code repository includes sophisticated tooling for managing and testing deployments, based on years of experience and feedback from prior versions of the protocol.





    


---
## Evaluation





##### What is the major benefit of each Compound III deployment featuring a single interest-earning base asset?  
     
- [x]  Reduced risk, and potentially improved capital efficiency
- [ ]  Allows for unlimited borrowing
- [ ]  Eliminates the need for collateral
- [ ]  Minimal risk of liquidation





##### How have borrowing collateral factors and liquidation collateral factors been separated in Compound III?  
     
- [ ]  They are no longer used in the protocol.
- [ ]  They have been combined into a single factor for simplicity
- [ ]  They are now separate, protecting liquidators from taking too much collateral
- [x]  They are now separate, protecting borrowers from early liquidation

    


---
## V2 vs V3



| Compound II | Compound III |
| - | - |
| Uses pools for assets with no separation  | Each market has a base asset  and no assets are shared between the markets |
| There is a single deployment of the protocol contracts on a blockchain | Each market is a separate instance of new Comet contracts|
| Risk Level of some hack draining all the funds is relatively high | Risk Level of some hack draining all the funds is relatively low as the markets are completely isolated |
| Lender earns interest on all the assets that lent to the protocol | Only the base asset earns interest, while all other assets in the market act as collateral |

    


---
## Your Info





| Label | Type | Required |
| ----------- | ----------- | ---- |
| Nickname        | PublicShortInput   |  true    |


    

