## Compound - Internals


## Introduction

To achieve greater capital efficiency, including reduced gas costs, Compound III allows users to supply volatile crypto assets and borrow a single asset(often a stable coin). 

This approach is in contrast to the current trend in DeFi where most borrowing involves supplying volatile crypto assets and borrowing a single borrowable base token. Compound III offers more value by providing fine-grained access controls for managing accounts, internalizing liquidation and profits, and optimizing for common usage with crypto collateral and borrows. 

Interest is earned by users who have a positive balance of the base asset, and it's denominated in the base asset. The interest rate is determined by a supply rate model, which is set by governance. On the other hand, users with a negative balance of the base asset have to pay interest based on a borrow rate model, which is also set by governance. These are two separate interest rate models.

The supply and borrow interest rates are determined by the utilization rate of the base asset. Each model has a utilization rate "kink" above which the interest rate increases more rapidly. Interest is calculated every second using the block timestamp. Collateral assets, however, do not earn or pay interest.



    


---
## Evaluation





##### How is the interest rate determined for users who have a positive balance of the base asset?  
     
- [ ]  It is denominated by borrow rate of the banks
- [x]  It is determined by a borrow rate model
- [ ]  It is set by governance and is static
- [ ]   It is determined for all the users at the time of market creation





##### How are the supply and borrow interest rates affected by the utilization rate of the base asset?
  
     
- [ ]  They remain constant regardless of the utilization rate
- [ ]  They decrease as the utilization rate increases.
- [x]  They increase more rapidly above a certain utilization rate "kink"

    


---
## Variables

The most significant configuration variables for Compound III that impact the lend and borrow rates are as follows:

`utilization` - The formula for producing the utilization is: `Utilization = TotalBorrows / TotalSupply`

`supplyKink` - This represents the point in the supply rates where the low interest rate slope meets the high interest rate slope, and is measured in factors.

`borrowKink` - This represents the point in the borrow rate where the low interest rate slope meets the high interest rate slope, and is measured in factors.

`supplyPerSecondInterestRateBase` - This is the base interest rate for supply per second, measured in factors.

`supplyPerSecondInterestRateSlopeLow` - This is the interest rate slope for supply per second when the utilization is below the kink point, measured in factors.

`supplyPerSecondInterestRateSlopeHigh` - This is the interest rate slope for supply per second when the utilization is above the kink point, measured in factors.

`borrowPerSecondInterestRateSlopeLow` - This is the interest rate slope for borrow per second when the utilization is below the kink point, measured in factors.

`borrowPerSecondInterestRateSlopeHigh` - This is the interest rate slope for borrow per second when the utilization is above the kink point, measured in factors.

`borrowPerSecondInterestRateBase` - This is the base interest rate for borrow per second, measured in factors.

    


---
## Evaluation





##### How is the utilization of Compound III calculated?  
     
- [x]  Utilization = TotalBorrows / TotalSupply
- [ ]  Utilization = supplyPerSecondInterestRateSlopeHigh / borrowPerSecondInterestRateSlopeHigh
- [ ]  Utilization = supplyKink / borrowKink
- [ ]  Utilization = borrowPerSecondInterestRateBase / supplyPerSecondInterestRateBase





##### What is the purpose of the supplyKink variable in Compound III?  
     
- [ ]  It determines the base interest rate for supply per second
- [ ]  It represents the point where the low interest rate slope meets the high interest rate slope for supply rates
- [ ]  It calculates the utilization of Compound III
- [x]   It determines the interest rate slope for supply per second when the utilization is above the kink point

    


---
## Calculations

The interest rates for supply and borrow can be calculated using the following formulas:

### Supply Rate:

* When utilization is less than or equal to the supplyKink:

  `supply rate = interestRateBase + interestRateSlopeLow * utilization`
* When utilization is greater than the supplyKink:

  `supply rate = interestRateBase + interestRateSlopeLow * kink + interestRateSlopeHigh * (utilization - kink)`

### Borrow Rate:
* When utilization is less than or equal to the borrowKink:

  `borrow rate = interestRateBase + interestRateSlopeLow * utilization`
* When utilization is greater than the borrowKink:

  `borrow rate = interestRateBase + interestRateSlopeLow * kink + interestRateSlopeHigh * (utilization - kink)`

    


---
## Evaluation





##### What is the formula for calculating supply rate when utilization is greater than the supplyKink?  
     
- [ ]  supply rate = interestRateBase + interestRateSlopeLow * utilization
- [ ]  supply rate = interestRateBase + interestRateSlopeLow * kink
- [x]  supply rate = interestRateBase + interestRateSlopeHigh * (utilization - kink)
- [ ]   None of the above





##### What is the formula for calculating borrow rate when utilization is less than or equal to the borrowKink?  
     
- [x]  borrow rate = interestRateBase + interestRateSlopeLow * utilization
- [ ]   borrow rate = interestRateBase + interestRateSlopeLow * kink
- [ ]  borrow rate = interestRateBase + interestRateSlopeHigh * (utilization - kink)
- [ ]  None of the above

    


---
## Market Updates

The initialization of variables that affect the calculation of borrow and supply rates occurs when a market is deployed on a blockchain. These variables can be modified through governance proposals even after the market has been created and deployed. The text below illustrates some of these variables.

```
borrowKink = 900000000000000000
borrowPerSecondInterestRateBase = 157680000
borrowPerSecondInterestRateSlopeHigh = 19552320000
borrowPerSecondInterestRateSlopeLow = 1639871893

supplyKink = 900000000000000000
supplyPerSecondInterestRateBase = 0
supplyPerSecondInterestRateSlopeHigh = 9460800000
supplyPerSecondInterestRateSlopeLow = 1356048000
```
Based on these variables we can plot how the borrow and interest rates look like with utilization.

![](https://d31h13bdjwgzxs.cloudfront.net/academy/compound-eth-1/Guide/compound-working-internals-compound/compund_3_eth_3.jpeg)


    


---
## Your Info





| Label | Type | Required |
| ----------- | ----------- | ---- |
| Nickname        | PublicShortInput   |  true    |


    

