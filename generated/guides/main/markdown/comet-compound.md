## Comet Protocol


## Introduction

## Compound III Updates
Updates to Compound III can be suggested, but caution must be taken as changes may decrease the program's security. Developers should create tests to ensure that any modifications work properly and do not introduce vulnerabilities. To help ensure safety, companies such as OpenZeppelin, ChainSecurity, and Certora also offer support.

To make changes safely to Compound III, this guide provides detailed instructions on code-level updates and safety measures. The guide covers topics such as creating tests for new code, running tests to confirm functionality, and using GitHub Actions to aid in testing. It also outlines the program's architecture, how to make changes to it, and how to ensure changes are safe before integrating them into the program.

## Architecture
The lending, borrowing, and market creation functions in Compound III are all contained within the "comet" smart contracts. 

#### Tests
The code base undergoes testing using various frameworks, including Solidity unit tests using Mocha.js written in JavaScript, and "scenarios" acting as integration tests.

#### Configurator
The Configurator is a unique contract that manages all the settings for the Compound III protocol. As even minor changes can have significant consequences, caution must be exercised. Developers must write tests, scenarios, and migration scripts to make changes safely.

#### Github Actions
The Compound III repository offers a range of Github Actions that developers can utilize. Some actions, such as testing, are executed automatically upon code commit, while others can be triggered via the Github UI, such as enacting migrations


    


---
## Evaluation





##### What is the purpose of the Configurator in Compound III?  
     
- [x]  To manage and apply all the updates for the Compound III protocol
- [ ]  To contain the lending, borrowing, and market creation functions
- [ ]  To execute Github Actions automatically upon code commit
- [ ]  To make it easy for developer to add solidity configurations





##### Which testing frameworks are used to test the Compound III code base?  
     
- [ ]  Java unit tests using JUnit
- [ ]  Python unit tests using pytest
- [x]  Unit tests using Mocha.js written in JavaScript
- [ ]  Ruby unit tests using RSpec

    


---
## Governor Bravo - Proposals

## About Governor Bravo
Governor Bravo is a governance mechanism that facilitates incremental changes to infrastructure without causing disruption. It is administered by Compound Governance and allows users to provide a string explaining their vote along with their vote receipt. The governance process can be customized through adjustable parameters, such as voting period, voting delay, and proposal threshold, which eliminates the need for deploying new contracts to enable governance changes.

In case of an error, the proposer of a proposal has the option to cancel their proposal at any time. The admin, governed by the Compound timelock, manages the configurable parameters and implementation.

## Compound III Updates
Updates to Compound III can be made through two methods:
1. Configuration updates from Governor Bravo UI
2. Code changes that utilize migration to generate a Governor Bravo proposal

Although these methods have slightly different starting points, both culminate in a Governor Bravo Proposal, which is voted on by the community to determine whether the changes should be implemented.

![](https://d31h13bdjwgzxs.cloudfront.net/academy/compound-eth-1/Guide/comet-compound/screenshot_2023-03-08%20at%2009.42.26.png)

## Create proposal from Governor Bravo UI
To propose a governance proposal, an individual must have 1% of COMP delegated to their address. 

![](https://d31h13bdjwgzxs.cloudfront.net/academy/compound-eth-1/Guide/comet-compound/create_proposal.jpeg)


## Update code and then create proposal
The process for updating the code and using the migration script to create a proposal that will implement those changes is outlined in the following steps.

    


---
## Evaluation





##### What is Governor Bravo?  
     
- [ ]  A solidity library that governs the number of functions
- [x]  A governance framework that facilitates incremental changes to Compound III
- [ ]  A testing framework for Solidity code
- [ ]  Title of the person who manages all the governance updates 





##### How much COMP must be delegated to an individual's address to propose a governance proposal?  
     
- [ ]  10%
- [ ]  5%
- [x]  1%
- [ ]  0.1%

    


---
## Contracts and Tests

## Comet Contracts
The Comet protocol is made up of different contracts that work together to create a system for exchanging a digital asset called Comet.

The main contract, `Comet.sol`, is responsible for most of Comet's core functionalities. It uses another contract, `CometExt.sol`, for functions that don't fit within Comet.sol.

`CometInterface.sol` is an abstract contract that contains all the functions and events for `Comet.sol` and `CometExt.sol` and is compatible with ERC-20.

The `Configurator` contracts manage Comet's configurations and deploy new implementations of Comet.

There are some supplementary contracts like `Bulker.sol`, which allows multiple Comet functions to be called in a single transaction, and CometRewards.sol, which allows users to claim rewards based on their protocol participation.

Finally, there are Vendor contracts like `ConfiguratorProxy.sol` and `CometProxyAdmin.sol`, which inherit from OZ proxies and are used to deploy and upgrade Comet.

## Scenario Tests

Scenarios are tests that check if Comet protocol is working correctly. To run these tests, you use a tool called Hardhat. You can run different scenarios against different versions of the Comet protocol. You can also change the number of workers, which can make the tests run faster.

To run the scenarios, Hardhat plugin is used. The command `npx hardhat scenario` is used to run the tests. You can also run scenarios against different versions of the Comet protocol using the `--bases` option. Additionally, the `--workers` option can be used to change the number of workers to speed up the testing process. Before we can run all the tests, we need to set some environment variables will be used to fetch existing data from supported blockchains.

`npx hardhat scenario --bases development,goerli,fuji`

To add a new test, you create a new file in a folder called "scenario". You then write the test in the file using a programming language called TypeScript. The test checks that a specific feature of the Comet protocol works correctly.

All the steps are explained in detail [here](https://github.com/compound-finance/comet/blob/main/SCENARIO.md)

Sometimes, a scenario requires the most recent version of the Comet contract. In this case, you add a "constraint" to the scenario that says it needs to use the most recent version. This makes sure that the scenario can run on any network, even if some features are not available.

    


---
## Migrations

Migrations are scripts that are used to deploy or modify contracts in a systematic way. The purpose of migration scripts is to make sure that users can see potential changes that are run prior to creating a governance proposal. In other words, it's a way to prepare for governance changes by showing everyone what changes will be made to the code before actually implementing them.

To create a migration, you can use the command `yarn hardhat gen:migration` followed by the network and deployment options. There are two methods that needs to be implemented in a migration script: 
1. `prepare` - which creates artifacts like new on-chain contracts
2. `enact` - which makes these artifacts current, such as upgrading the proxy to the address from the previous step.

```javascript
enact: async (deploymentManager: DeploymentManager) => {
    const trace = deploymentManager.tracer();
    const ethers = deploymentManager.hre.ethers;

    const {
      governor,
      comet,
      configurator,
      cometAdmin,
      WETH,
    } = await deploymentManager.getContracts();

    const actions = [
      // 1. Increase supply cap for WETH
      {
        contract: configurator,
        signature: "updateAssetSupplyCap(address,address,uint128)",
        args: [comet.address, WETH.address, exp(150_000, 18)],
      },

      // 2. Deploy and upgrade to a new version of Comet
      {
        contract: cometAdmin,
        signature: "deployAndUpgradeTo(address,address)",
        args: [configurator.address, comet.address],
      },
    ];
    const description = "# Increase WETH Supply Cap in cUSDCv3\n"
    const txn = await deploymentManager.retry(
      async () => trace((await governor.propose(...await proposal(actions, description))))
    );

    const event = txn.events.find(event => event.event === 'ProposalCreated');
    const [proposalId] = event.args;

    trace(`Created proposal ${proposalId}.`);
  }
```

You can run a migration locally using `yarn hardhat migrate` and specifying the network, deployment, and whether to prepare or enact the migration. You can also simulate either of the previous steps without actually modifying the on-chain state.

If you look carefully you will see the following line towards end of `enact` function, that creates the Governor Bravo proposal

`await governor.propose(...await proposal(actions, description))`


The preferred way to run a migration is in GitHub, via manual workflow dispatch, which allows everyone to see the exact code that was deployed or run. After preparation, a migration stores some artifacts which can be loaded and referenced in the enact step of that migration.

Once a migration has been created, the next step is to create a pull request on GitHub and get it reviewed, approved, and enacted before merging it. If the migration creates a governance proposal on-chain, then wait until the proposal either executes or fails before merging the pull request.

    


---
## Evaluation





##### What is the purpose of migration scripts in contract deployment?  
     
- [ ]  To make DB updates
- [ ]  To make sure that package.json version is updated properly upon deployment
- [x]  To make sure that users can see potential changes that are run prior to creating a governance proposal
- [ ]  Migrate data from testnet to mainnet





##### What are the two methods that must be implemented in a migration script?  
     
- [ ]  Propose and enact
- [x]  Prepare and enact
- [ ]  Deploy and update
- [ ]  Upgrade and review

    


---
## Github Actions

## Enable Workflows and Add Secrets
After we update the code and add the tests, the first thing we need to do is run our scenarios in our CI workflow. To do this, we need to commit our code and push it to GitHub. For the forked comet repo we need to first enable the workflows. The workflows in the forked repository run independently from the official repository.

We will also need to add the same environment variables as Actions secrets in the repository.

After adding all the keys, we can run the workflows in our fork. It's a good idea to run tests in our fork CI before opening a pull request on the official Comet repository. If our branch is up to date, all passing tests in the fork CI will result in passing tests in the pull request to main.

## Run workflow
We can click the Actions tab in forked github repo and select the Run Scenarios workflow on the left. We click the Run workflow button on the right, select our branch in the dropdown menu, and then click the green Run workflow button. It will take several minutes to run. 

![](https://d31h13bdjwgzxs.cloudfront.net/academy/compound-eth-1/Guide/comet-compound/comet_workflow.png)

After you execute the enact action, it will create a Governor Bravo Proposal which can be voted upon by the community.  

    


---
## Your Info





| Label | Type | Required |
| ----------- | ----------- | ---- |
| Nickname        | PublicShortInput   |  true    |


    

