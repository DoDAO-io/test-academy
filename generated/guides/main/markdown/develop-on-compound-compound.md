## Develop on Compound


## Introduction

## Compound III
Compound III is a specialized protocol that aims to achieve greater capital efficiency in DeFi by allowing users to supply volatile assets and borrow a single stable asset. This approach is intended to reduce gas costs and increase capital efficiency. The Compound III Smart Contracts or Coment repository uses a business source license, which Compound governance can grant usage to, as it sees fit, by making changes to compound-community-licenses.eth, a new ENS domain owned by the community.

## Compound Grants Program (CGP)
Compound is encouraging developers to collaborate and build on top of the new Compound III code base through the Compound Grants Program. This program is designed to promote composability and facilitate the development of new features and functionality related to Compound III. The primary objectives of the program are to expand Compound's grant program, delegate capital allocation to members of the community, and strengthen the builder community during bear market conditions.

## CGP 2.0 Details
CGP 2.0 is a specific program within the Compound Grants Program that focuses on getting the community to participate in the process of delegating capital allocation. The program disburses $800K (22087.24 COMP) through 4 domain allocators, who are experts in their specific domains and involved in the Compound community. Each domain allocator runs their respective grants program on-chain for full transparency using Questbook. The disbursement of the grant happens on-chain from a multi-sig wallet controlled by the program manager & the domain allocator. The program manager will coordinate with the compound community to ensure that the application is aligned with the Compound growth before signing the disbursal, while the domain allocator approves or rejects the application based on their evaluation.

    


---
## Evaluation





##### What is the main objective of the Compound Grants Program?  
     
- [x]  To encourage developers to collaborate and build on top of the new Compound III code base.
- [ ]  To allow users to supply volatile assets and borrow a single stable asset.
- [ ]  To reduce gas costs and increase capital efficiency.
- [ ]  To strengthen the builder community during bear market conditions.





##### How does CGP 2.0 allocate grants?
  
     
- [ ]  Through a centralized authority
- [ ]  Core team decides
- [x]  Through 4 domain allocators who are experts in their specific domains
- [ ]  Through on-chain voting

    


---
## Code Examples

These straightforward examples demonstrate the simplicity of working with Comet Smart Contracts for supplying and borrowing.

## Supply
The below code block supplies WETH as collateral, approves Comet to move WETH collateral, sends initial supply to Compound, and then prints the current WETH collateral balance. It uses JavaScript to interact with the Comet protocol.


```javascript
    const provider = new ethers.providers.JsonRpcProvider(jsonRpcUrl);
    const signer = provider.getSigner(me);
    const comet = new ethers.Contract(cometAddress, cometAbi, signer);
    const weth = new ethers.Contract(wethAddress, wethAbi, signer);
    const wethMantissa = 1e18; // WETH and ETH have 18 decimal places

    let tx = await weth.deposit({ value: ethers.utils.parseEther('10') });
    await tx.wait(1);

    console.log('\tApproving Comet to move WETH collateral...');
    tx = await weth.approve(cometAddress, ethers.constants.MaxUint256);
    await tx.wait(1);

    console.log('\tSending initial supply to Compound...');
    tx = await comet.supply(wethAddress, ethers.utils.parseEther('10'));
    await tx.wait(1);

    let collateralBalance = await comet.callStatic.collateralBalanceOf(me, wethAddress);
    console.log('\tMy current WETH collateral balance:', +collateralBalance.toString() / wethMantissa);
```

## Borrow
The below code borrows a specific amount of base assets from the Compound platform using JS. It starts by defining the user account, provider, and signer. It also sets up the contracts for Comet, WETH, and USDC. The user then deposits WETH collateral, approves Comet to move it, and supplies it to the Compound platform. After that, the user borrows a specified amount of USDC from Compound and checks their current balance of base assets.

```javascript
    const provider = new ethers.providers.JsonRpcProvider(jsonRpcUrl);
    const signer = provider.getSigner(me);
    const comet = new ethers.Contract(cometAddress, cometAbi, signer);
    const weth = new ethers.Contract(wethAddress, wethAbi, signer);
    const wethMantissa = 1e18; // WETH and ETH have 18 decimal places
    const usdc = new ethers.Contract(baseAssetAddress, stdErc20Abi, signer);
    const baseAssetMantissa = 1e6; // USDC has 6 decimal places

    let tx = await weth.deposit({ value: ethers.utils.parseEther('10') });
    await tx.wait(1);

    console.log('\tApproving Comet to move WETH collateral...');
    tx = await weth.approve(cometAddress, ethers.constants.MaxUint256);
    await tx.wait(1);

    console.log('\tSending initial WETH supply of collateral to Compound...');
    tx = await comet.supply(wethAddress, ethers.utils.parseEther('10'));
    await tx.wait(1);

    // Accounts cannot hold a borrow smaller than baseBorrowMin (100 USDC).
    const borrowSize = 1000;
    console.log('\tExecuting initial borrow of the base asset from Compound...');
    console.log('\tBorrow size:', borrowSize);

    tx = await comet.withdraw(usdcAddress, (borrowSize * baseAssetMantissa).toString());
    await tx.wait(1);

    let bal = await usdc.callStatic.balanceOf(me);
    console.log('\tMy current base asset balance:', +bal.toString() / baseAssetMantissa);
```

    


---
## Next Steps

The Compound team wants developers to collaborate in any capacity. Some of the many several ways to collaborate are:

1. You can extend or update the Comet contracts.
2. You can develop an analytics dashboard.
3. You can create educational content, similar to this one.
4. You can build applications on top of the Comet smart contracts.
5. Alternatively, you can come up with your own idea - all ideas are welcome.

To get involved, please join the #development room in the Compound community Discord server and the forums at comp.xyz. Compound Labs and the community members are eager to help you build an application on top of Compound III. If you have any questions or can't find what you're looking for, don't hesitate to ask. Your feedback helps us improve.

For documentation on the Compound III Protocol, please visit https://docs.compound.finance.

    


---
## Evaluation





##### What are some ways developers can collaborate with the Compound team?
  
     
- [ ]  They can extend or update the Comet contracts.
- [ ]  They can create educational content, similar to this one.
- [ ]  They can develop an analytics dashboard.
- [x]  All of the above

    


---
## Your Info





| Label | Type | Required |
| ----------- | ----------- | ---- |
| Nickname        | PublicShortInput   |  true    |


    

