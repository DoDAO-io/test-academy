## Supply & Borrow Interest Calcu.


## Introduction


The supply and borrow interest rates are determined by the utilization rate of the base asset. Each model has a utilization rate "kink" above which the interest rate increases more rapidly. Interest is calculated every second using the block timestamp. Collateral assets, however, do not earn or pay interest.
        

    


---
## Introduction Evaluation

When utilization is less than or equal to the supplyKink:

`supply rate = interestRateBase + interestRateSlopeLow * utilization`

    


---
## Step 3

When utilization is greater than the supplyKink:

`supply rate = interestRateBase + interestRateSlopeLow * kink + interestRateSlopeHigh * (utilization - kink)`

    


---
## Step 7





##### What is the formula for calculating supply rate when utilization is greater than the supplyKink?  
     
- [ ]  supply rate = interestRateBase + interestRateSlopeLow * utilization
- [ ]  supply rate = interestRateBase + interestRateSlopeLow * kink
- [x]  supply rate = interestRateBase + interestRateSlopeLow * kink + interestRateSlopeHigh * (utilization - kink)
- [ ]   None of the above

    


---
## Step 4

When utilization is less than or equal to the borrowKink:

`borrow rate = interestRateBase + interestRateSlopeLow * utilization`

    


---
## Step 5

When utilization is greater than the borrowKink:

`borrow rate = interestRateBase + interestRateSlopeLow * kink + interestRateSlopeHigh * (utilization - kink)`

    


---
## Step 6





##### What is the formula for calculating borrow rate when utilization is less than or equal to the borrowKink?  
     
- [x]  borrow rate = interestRateBase + interestRateSlopeLow * utilization
- [ ]   borrow rate = interestRateBase + interestRateSlopeLow * kink
- [ ]  borrow rate = interestRateBase + interestRateSlopeHigh * (utilization - kink)
- [ ]  None of the above

    
   