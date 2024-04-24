#       Party Protocol Smart Contracts Analysis
####  1. Party Protocol: A Comprehensive Overview

DYAD protocol, aims at creating a truly capital efficient decentralize stablecoin, reducing the cost of excess collateral and DEX liquidity through the kerosine token. Users are minted NOTES which are erc-712 NFTs which forms a base for the creation of vaults into which approved erc-20 tokens can be deposited, the currently approved tokens are; wstETH, wETH, as well as kerosine.
The protocol is deployed in the Ethereum Mainnet.

####   2. Main Contracts and Their Analysis

###  Dyad Protocol in Scope: 
Kerosine Denominator - This contract is for calculating the denominator that will be used in the assetPrice() function in vault.kerosine.unbounded.

VaultManagerV2 - The vault manager is a core contract for controlling vaults in the protocol actions like adding and removing of vaults, depositing and withdrawing as well as redeeming of assets are done in the manager contract.

Vault.Kerosine - This is the kerosine vault contract that is used for depositing and moving assets between users.

KerosineManager - The kerosine manager is used for adding and removing kerosine vaults in the protocol.

Vault.Kerosine.bounded - This contract is aligned with the kerosine vault contract and used for for withdrawing kerosine from the kerosine vault and for calculating the assetprice of the kerosine token 

Vault.Kerosine.unbounded - This contract is also used for for withdrawing kerosine and for calculating the assetprice of the kerosine using the denominator from the KerosineDenominator contract.

DeployV2 - This is the deployment script which depicts the other inwhich the contracts in scope are to be deployed.

####  3. Approach taken in evaluating the codebase
High-level overview: I analyzed the overall codebase in one iteration, going through the codebase once to get a high-level understanding of the code structure and functionality.

Documentation review: i read through the docs to understand the general intent of the protocol and to understand how contracts are related to each other

Literature review: I read the bot races findings in order to get more context.

Testing setup: I set up my testing environment and ran the tests to ensure that all tests passed. Used foundry to test this protocol.

Detailed analysis: I started with the detailed analysis of the code base, line by line. I took the necessary notes to ask and read the answers from sponsors to my asked questions and those asked by other auditors.
#### 4. Party Protocol: Architecture 
The protocol is structured to provide an avenue for users who have dNFT minted to be able to borrow stablecoin from the protocol.
Though there is always room for improving and optimizing the architectural design of the protocol;

Monitoring and Analytics: Implement monitoring and analytics tools to better understand protocol behavior and provide valuable insights for decision-making.

User-Friendliness: The architecture should be as intuitive as possible for end-users. This might involve a more user-friendly user interface or the automation of processes that currently require manual action.

Education and Outreach: Ensuring that users fully understand how the architecture works and how they can get the most out of it, is essential. This could include educational resources and a robust documentation base.
####  5. Systemic and Centralization Risks
The protocol lacks proper documentation as the available documentation does not detail the whole protocol for more context and insight into how each contract is supposed to behave. The codebase also lacks inline comments and natspec, for easier auditing of the codebase.
There are no centralization risk in the protocol.
####  6. Security Approach of the Project
What the project can add in the understanding of Security:

Deploying to Testnet - By distributing the project to testnets, protocols behavior can be determined to a certain extent.
Pause Mechanism - Adding a pause mechanism will increase the safety of the protocol in case any thing goes wrong. Although this can be thought of as a choice between decentralization and security.
Add On-Chain Monitoring System - Adding on-chain monitoring systems such as Forta  can increase the security of the protocol.













### Time spent:
15 hours