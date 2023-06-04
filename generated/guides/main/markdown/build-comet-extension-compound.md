## Build Comet Extension


## Introduction

## Extensions
Compound III, has launched a new feature called "Extensions". This feature is designed to allow community developers to create optional add-ons that can be used to enhance the Compound experience for users.

When a user enables an extension, it can leverage Compound III's advanced account management functionality to add new features to their account. These can include automation, position management, and composability with other DeFi protocols. Alternatively, an extension can run without requiring any permissions and simply provide useful information like liquidation alerts.

## Extension Types
There are two types of extensions: 
1. Web Extensions - Web extensions are like mini-websites that are embedded into the Compound III interface, allowing users to interact with the platform in new and different ways 
2. Operators - Operators, on the other hand, are smart contracts that allow users to do things like move positions from other DeFi platforms to Compound III. 

Some extensions have both a web extension and an operator, while others have only one or the other.

    


---
## Evaluation





##### What is the purpose of Compound III's "Extensions" feature?  
     
- [ ]  To provide additional information to users
- [x]  To allow community developers to create add-ons to enhance user experience
- [ ]  To restrict users from accessing certain features
- [ ]  To allow Compound III to manage user accounts more efficiently





##### What are the two types of extensions offered by Compound III?  
     
- [ ]  Web extensions and browser extensions
- [ ]  Web extensions and mobile extensions
- [ ]  Mobile extensions and desktop extensions
- [x]  Web extensions and operators

    


---
## Web Extensions

Web Extensions are used to expand the functionality of the Frontend by allowing users to perform actions or retrieve information related to their accounts. 

These extensions are incorporated into the main Compound III app as iframes, but the inner window of the iframe lacks access to the web3 context required for signing messages or transactions when interacting with smart contracts. To overcome this limitation, the Web Extension sends a message to the parent window, which then uses the context and forwards the message. `@compound-finance/comet-extension` provides all the glue code needed to interact with the parent window.

```javascript
let rpc: RPC = buildRPC();

// Send transaction request
let chainId = await sendWeb3(rpc, 'eth_chainId', []);

// Handle incoming messages
rpc.on({setTheme: ({theme}) => {
  console.log('theme', theme);
});
```
```javascript
let rpc: RPC = buildRPC();
let provider = new RPCWeb3Provider(rpc);

provider.sendTransaction(...);
```

Compound offers an extension template that includes all the necessary setup code and up-to-date frameworks for creating a frontend application.

https://github.com/compound-finance/comet-extension-template

To create a Comet Web Extension, developers should start by cloning the template repository's boilerplate to their local machine. With Foundry and Vite, they can then develop the Extension's frontend and smart contracts while utilizing a localhost development environment to verify that the code works correctly.

    


---
## Evaluate





##### How do Web Extensions interact with Compound III parent window UI?  
     
- [ ]  Web Extensions have direct access to the web3 context required for signing messages or transactions
- [x]   Web Extensions use window messaging system to send messages to parent window
- [ ]  Web Extensions are not able to interact with parent window
- [ ]  Web Extensions must be authorized by Compound III and user both before interacting with  parent window





#####  What is the purpose of the @compound-finance/comet-extension package?  
     
- [ ]  To provide a template for creating Web Extensions in Compound III
- [ ]   To provide a set of up-to-date frameworks for creating Web Extensions
- [ ]  To provide a development environment for testing Web Extensions
- [x]  To provide a messaging system for Web Extensions to interact with parent window

    


---
## Operator

Operators are smart contracts that have access to act on behalf of a user's Compound III position. For instance, the [Comet Migrator](https://github.com/compound-finance/comet-migrator) is a smart contract which moves a position from Compound II or other DeFi platforms, using a flash loan to move the position atomically.

Operator extensions are normal smart contracts and they are call extensions because they mostly extend comet's functionality. Here is a simplest smart contract structure that is included in the comet-extension-template

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.16;

import "./interfaces/CometInterface.sol";

/**
 * @title My Extension
 * @notice A Compound III operator to ...
 * @author Compound
 */
contract MyCometExtension {
  /// @notice The Comet contract
  Comet public immutable comet;

  /**
   * @notice Construct a new MyExtension operator.
   * @param comet_ The Comet contract.
   **/
  constructor(Comet comet_) payable {
    comet = comet_;
  }
}
``` 
[https://github.com/compound-finance/comet-extension-template](https://github.com/compound-finance/comet-extension-template) contains all the boilerplate code that is needed to compile and deploy the smart contracts. The operator code is built on [Foundry](https://book.getfoundry.sh/)

You can also choose you choice of frameworks for creating and deploying the operator smart contracts.



    


---
## Evaluation





##### What is the purpose of the Comet Migrator Extension?  
     
- [ ]  To deploy smart contracts on Compound III
- [ ]  To extend the borrow position of Comet
- [x]   To move a position from Compound II or other DeFi platforms
- [ ]  To compile and deploy the smart contracts needed for Comet extensions.

    


---
## Your Info





| Label | Type | Required |
| ----------- | ----------- | ---- |
| Nickname        | PublicShortInput   |  true    |


    

