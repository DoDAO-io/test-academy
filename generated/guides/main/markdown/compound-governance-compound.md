## Compound Governance


## Introduction

The goal of Compound is to create a sturdy financial infrastructure for developers and applications to rely on. To achieve this, the Compound protocol must be fully decentralized, eliminating the risk of a single point of failure (the team) and creating a robust, unbreakable system that can grow in new directions. The Compound protocol has established a governance structure that enables voters to make changes to the protocol through proposals, discussions, and executions, all without relying on or requiring a centralized team. Community governance takes the lead in this system as the administrator of the Compound protocol.

With the help of the COMP token, governance module (Governor Bravo), and Timelock, COMP token-holders govern and upgrade the Compound protocol. These three components work together to provide the community with the ability to propose, vote, and implement changes through the cToken's administrative functions or the Comptroller. These proposals can change system parameters, introduce new markets, or add new features to the protocol.

This system guarantees that the Compound protocol remains adaptive to the needs of its users and gives every COMP token holder a voice in determining the direction of the platform. If you are seeking a lending platform that places control in your hands, Compound is the perfect choice for you.


This "Compound Governance" guide serves as a comprehensive guide for those who want to contribute to the Compound DAO.  This document outlines the different responsibilities, procedures, and opportunities for all parties involved in the Compound DAO. It brings together essential information in a single, easy-to-use source.

    


---
## Evaluation





##### Who is responsible for compound governance?  
     
- [ ]  Management team
- [x]  COMP token holders
- [ ]  Developers
- [ ]  Director

    


---
## Proposal Types

## Compound Governor Proposals
Compound Governor Proposals are utilized to authorize various executions of smart contracts, such as the adjustment of risk parameters, distribution parameters, primary modular contracts, and administrative functions (such as reducing reserves or transferring ERC-20 tokens).

The lifecycle of a Compound Governor Proposal involves three stages:

1. Idea stage: Post the proposal in the "Proposal" category on the Compound Forum and provide enough information to demonstrate its impact on Compound.
2. Community Feedback stage: Use the community's feedback to make any necessary changes to the proposal.
3. Compound Governor stage: After the proposal is approved by the community and has a high chance of success, it is recommended to move it to an on-chain vote.

Any individual with more than 1% of COMP can propose a proposal to Compound Governance. If they don't have enough COMP, they can request someone else to post the proposal on their behalf. The Compound multisig can also temporarily white-list proposers.

## Compound Improvement Proposals
The Compound Improvement Proposals (CIPs) outline the standards, procedures, and upgrades aimed at enhancing the governance protocol. Their objective is to refine both on-chain and off-chain governance of the Compound.

CIPs come in three different forms, each with its distinct methodology, which are detailed below.

1. Meta Process: Any process to be introduced or altered that enhances the coordination of Compound's governance, development, or community initiatives.
2. Protocol Enhancement: This encompasses any alterations to the smart contracts involved in the Compound Protocol and Governor.
3. Tooling & Support: This encompasses any new additions or modifications to off-chain infrastructure, tools, documentation, or other supportive components for the use of Compound Protocol.

    


---
## Evaluation





##### Select the two correct proposal types in Compound Governance.  
     
- [ ]  Compound Management Proposals
- [x]  Compound Governor Proposals
- [ ]  Compound Developers Proposals
- [x]  Compound Improvement Proposals





##### Which of these types of proposals qualify for Compound Governor Proposals?  
     
- [ ]  Proposals that outline the standards, procedures, and upgrades aimed at enhancing the governance protocol
- [ ]  Proposals that govern service providers
- [x]  Proposals that are used to approve different smart contract executions and administrative tasks.
- [ ]  Proposals that are used to update the Compound DAO size.

    


---
## CIP Lifecycle

The authors of CIPs will initiate the process by conceiving an idea, converting it into a CIP document, seeking a peer review, and then undergoing an approval procedure with the Compound Working Group.

To initiate a review, the CIP document should be posted in the #governance channel on Compound's Discord platform.

Potential ideas can be submitted as issues on a shared GitHub repository, similar to Ethereum PM. CIPs can be drafted as pull requests and then request for a review to be scheduled for discussion at the bi-weekly Working Group meetings.

![](https://d31h13bdjwgzxs.cloudfront.net/academy/compound-eth-1/Guide/compound-governance-compound/cip_appproval_process.png)


CIP editors will provide feedback on CIPs. If objections are raised during its first meeting, the CIP must address the feedback and request another review at a future meeting. If there are no objections or a majority of editors support the CIP, it will be approved during its second meeting and remain in the Last Call stage for 14 days before the implementation process commences.

![](https://d31h13bdjwgzxs.cloudfront.net/academy/compound-eth-1/Guide/compound-governance-compound/cip_implementation_process.png)


Once the Working Group approves a CIP, its implementation path will vary based on its type:

1. Meta Process CIPs will be adopted officially through a majority Signal vote by COMP holders without the need for a quorum.
2. Protocol Enhancements must pass through a Compound Governance vote, just like any other change to the smart contract.
3. Other CIPs are left to the community to implement, which may include funding approved by a Grant Committee or any other entity willing to support them.

More Details about CIPs can be found [here](https://github.com/compound-finance/cip-pm/pull/1/files)

    


---
## Evaluation





##### Which of these types of proposals qualify for Compound Improvement Proposals?  
     
- [ ]  Proposals that are used for governance changes
- [ ]  Proposal that govern service providers
- [ ]  Proposals that outline the standards, procedures, and upgrades aimed at enhancing the governance protocol
- [x]  Proposals that are used to approve different smart contract executions and administrative tasks.





##### Which of these is not a valid step in Compound Improvement Proposal approval process?  
     
- [ ]  Authors of CIPs will initiate the process by conceiving an idea, converting it into a CIP document
- [x]  Organize a twitter spaces to collect feeback from broader DeFi comunity
- [ ]  After the draft a peer review is the next step
- [ ]  If objections are raised during its first meeting, the CIP must address the feedback and request another review at a future meeting

    


---
## Governance Roles

There are three main roles in the Compound governance process:

### Delegates
Delegates have acquired voting power through delegation from other community members or self-delegation. The addresses are ranked by voting weight and only the top 100 delegates are displayed. Any individual holding more than 1% of COMP is eligible to propose a governance action.

Becoming a delegate is open to everyone and does not require any applications. Delegates can access their voting history by visiting their profile.

### Delegators
Delegators are community members who own COMP but have assigned their voting power to another individual, referred to as a delegate.

### Contributors
Contributors are members of the Compound DAO who actively contribute their time and effort to the organization. They participate by developing on top of the Compound Protocol or supporting the DAO through grants or partnerships, all while working towards common goals.


In Compound DAO, there are no established working groups, and no templates exist for creating such groups. Compound DAO has entered into service provider agreements with Open Zeppelin and Gauntlet.

To streamline the process for individuals or teams to participate in the DAO, a standardized "Service Provider" template should be established.

    


---
## Evaluation





##### Which of these is not a valid role in the Compound governance process?  
     
- [x]  Director
- [ ]  Delegates
- [ ]  Delegators
- [ ]  Contributors





##### Which of these is a requirement to be able to propose a governance action?  
     
- [ ]  Only the developing team can propose proposals
- [ ]  Only the management team can propose governance actions
- [x]  Any individual holding more than 1% of COMP is eligible to propose a governance action
- [ ]  An individual needs to be a director to propose governance actions

    


---
## Funding

Compound DAO has two sources of funding:

### 1. Direct funding through governance
- Service providers can enter into agreements with Compound DAO in exchange for payment. This option is currently not frequently used within Compound DAO, but it may become more prevalent in the future as service providers become more common.
- Open Zeppelin serves as an example of a service provider for Compound DAO.

### 2. Compound Grants Program 2.0
- The Compound Grants Program focuses on four areas: Multichain strategy, Developer Tooling, Security Tooling, and New Protocol Ideas & Dapps. Applicants can apply directly for funding through the program.
- If your proposal does not fall within the specified domains, or if you have any questions about the grants program, please reach out to the team in the #grants channel on the Compound Discord.

    


---
## Evaluation





##### How can other organizations get funding from Compound DAO?  
     
- [ ]  By selling their shares
- [ ]  Donations from Voters
- [ ]  Raising funds through VCs
- [x]  Other organizations or individuals can enter into Service providers agreements with Compound DAO in exchange for payment





##### What is the primary purpose of the Compound Grants Program?  
     
- [ ]  Providing technical support and advice on Discord
- [x]  Finance initiatives, plans, and activities that benefit Compound and its stakeholders
- [ ]  Create proposals for governance
- [ ]  Delegate voting rights

    


---
## Voting

All protocol modifications in Compound DAO are executed through Compound Governor. Proposals are actual executable code, not just suggestions for the team or foundation to execute.

After a proposal has been submitted, it goes through a 3-day voting period. For a proposal to be approved, it must receive a minimum of 400,000 votes and achieve a majority. Once the proposal has been approved, it is immediately scheduled in the timelock and will be put into effect after a 2-day waiting period.

![](https://d31h13bdjwgzxs.cloudfront.net/academy/compound-eth-1/Guide/compound-governance-compound/voting.jpeg)


    


---
## Evaluation





##### What is a minimal vote requirement to achieve a majority for implementation?  
     
- [x]  A proposal needs at least 400,000 votes and a majority in order to be approved
- [ ]  A proposal needs at least 4000 votes and a majority in order to be approved
- [ ]  A proposal needs at least 100,000 votes
- [ ]  Voting is not required to approve a proposal

    

