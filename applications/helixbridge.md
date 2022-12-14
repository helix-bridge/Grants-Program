# HelixBridge

- **Team Name:** Helix
- **Payment Address:** FsyQNF17naZjZMutC8DAYEhxgGTgKB1dZcjumqDN4uKct8r (KSM)
- **[Level](https://github.com/w3f/Grants-Program/tree/master#level_slider-levels):** 2

## Project Overview :page_facing_up:

### Overview

Helix focuses on asset interoperability between chains.
After researching and working with a large number of asset cross-chain bridge projects, we found that each cross-chain bridge supports a limited number of chains and assets, and all have their own user portal.
We are more interested in integrating the best asset bridges in the market and providing a unified user portal.
Polkadot xcm is a good solution for asset interoperability between parachains, but due to the flexibility of xcm command, there are differences in the interfaces implemented by each parachain. HelixBridge provides users with a unified cross-chain portal for assets and shield users from the differences in cross-chain interfaces between each parachain.
In the future, we will also implement cross-chain asset transfer services between parachain EVMs based on general messaging services (e.g. Polkadot XCM).

### Project Details

- **Designs(UI)**:

1. Transfer
![image](https://github.com/helix-bridge/docs/blob/main/static/img/demo-transfer.jpeg)

The user can easily select the source chain, target chain and token through this page, the system will estimate and display the time and cost of the transfer, the user performs the transfer operation by calling the wallet plugin (Polkadot.js or metamask) to initiate the signature operation.

2. Records
![image](https://github.com/helix-bridge/docs/blob/main/static/img/demo-record.png)
![image](https://github.com/helix-bridge/docs/blob/main/static/img/demo-detail.png)

Through this page, all transfer transactions are displayed and information such as the address of the sending and receiving accounts can be retrieved.

- **Indexer Architecture**

The back-end uses a two-tier indexing structure, with the first tier indexing the transfer-related events or transactions of each chain and saving them independently, while the second tier will do correlation and sorting based on the indexed data of the first tier, and provide query and filtering interfaces for the front-end to call

- **Token Mapping Protocol**

In addition to aggregating existing protocols on chains such as xcm, Helix will also provide asset registration and mapping services between some chains, as described in [Helix Docs](https://docs.helixbridge.app/how-it-works/token_protocol)

### Ecosystem Fit

Most of parachains with xcmp channel will be included
For parachains like moonriver with evm module, our asset registration protocol will be deployed to complete the cross-chaining of assets between evm modules.

## Team :busts_in_silhouette:

### Team members

- Head of product: [HackFisher](https://github.com/HackFisher)
- Product design: [ZolaxZola](https://github.com/ZolaxZola)/[ranji](https://github.com/1022ranji)
- DevOps: [fewensa](https://github.com/fewensa)
- Frontend: [sxlwar](https://github.com/sxlwar)
- Tech lead, backend: [xiaoch05](https://github.com/xiaoch05)

### Contact

- **Contact Name:** Cheng Xiao
- **Contact Email:** hello@helixbridge.app
- **Website:** https://helixbridge.app/

### Legal Structure

Individual

### Team's experience

For several years, our team has been contributing to different projects on blockchain, especially in the area of cross-chain bridges, where we have accumulated a wealth of experience. We hope to provide users with a more user-friendly and easy-to-use cross-chain interaction experience in the Polkadot ecosystem.

### Team Code Repos

- https://github.com/helix-bridge/helix-ui
- https://github.com/helix-bridge/indexer
- https://github.com/helix-bridge/dao
- https://github.com/helix-bridge/contracts
- https://github.com/helix-bridge/docs

Please also provide the GitHub accounts of all team members. If they contain no activity, references to projects hosted elsewhere or live are also fine.

- https://github.com/HackFisher
- https://github.com/ZolaxZola
- https://github.com/1022ranji
- https://github.com/fewensa
- https://github.com/sxlwar
- https://github.com/xiaoch05

## Development Status :open_book:

The source code repository for the Helix application is located at [Github](https://github.com/helix-bridge).
It includes the [indexing service](https://github.com/helix-bridge/indexer) which monitors events on the chain and records transaction history, the [front-end](https://github.com/helix-bridge/helix-ui) which is responsible for user interaction and record presentation, the [docs](https://github.com/helix-bridge/docs), and the [contract](https://github.com/helix-bridge/contracts). In the initial version, we will encompass most of the xcm token transfers between parachains. In the future, Helix app will also use its own token mapping protocol based on xcm to complete token transfers between parachains evm and handle atomic operations for user asset transfers.

## Development Roadmap :nut_and_bolt:

### Overview

- **Total Estimated Duration:** 6 months
- **Full-Time Equivalent (FTE):**  5
- **Total Costs:** 30,000 USD

### Milestone 1 — The Indexer For Cross-Chain Transfer Records

- **Estimated duration:** 3 month
- **FTE:**  5
- **Costs:** 15,000 USD

We use the industry's best indexing services (e.g. thegraph, subql, etc.) to index the xcm events on each parachain. and store them in association with the sent and received information, providing a unified record access interface for the front-end. For parachains that support evm, we use contracts to call xcm to do cross-chain asset transfers to ensure atomicity of transfer transactions.

| Number | Deliverable | Specification |
| -----: | ----------- | ------------- |
| **0a.** | License | MIT |
| **0b.** | Documentation | We will provide both **inline documentation** of the code and a basic **tutorial** that explains how to build the service to index data from the chain and aggregate the indexed data into a data format that can be queried by the front-end, how to deploy the service and the detailed usage of the API. |
| **0c.** | Testing and Testing Guide | The core functions will be fully covered by unit tests, we will use ci to run the test automatically each time the project updated. |
| **0d.** | Docker | We will provide a Dockerfile(s) that can be used to test all the functionality delivered with this milestone. |
| 0e. | Article | We will publish an **article**/workshop that explains explain how transaction events are related and aggregated together, and describe the process of interaction between that service and the chain, and the details of interaction with the front end.  |
| 1. | Subql Module | We will use subql to index cross-chain transaction events and transaction parameters from pallet on the chain. |
| 2. | Subgraph Module | We will use subgraph to index cross-chain transaction events and transaction parameters from contracts on the chain. |
| 3. | Reindexer Service | We will use the re-indexing service to correlate indexed data across chains, and aggregate filtering and sorting. |
| 4. | Smart Contracts: Backing | For helix-hosted asset bridges, we use backing to manage users' native assets, supporting locking and unlocking. |
| 5. | Smart Contracts: Issuing | For helix-hosted asset bridges, we use issuing to manage users' mapping assets, supporting minting and burning. |

### Milestone 2 — Front-End Development

- **Estimated Duration:** 3 month
- **FTE:**  5
- **Costs:** 15,000 USD

Encapsulate the cross-chain interface of parachains to provide users with a unified transfer operation page and display operation records and details.

| Number | Deliverable | Specification |
| -----: | ----------- | ------------- |
| **0a.** | License | MIT |
| **0b.** | Documentation | We will provide both **inline documentation** of the code and a basic **tutorial** that explains how a user can use helix bridge to send a cross-chain transaction, query or search the transaction history and how user's token transfer from one chain to another. |
| **0c.** | Testing and Testing Guide | The core functions will be fully covered by unit tests and e2e test, we will use ci to run the test automatically each time the project updated. And also we provide some testnet for users to experience the cross-chain process. |
| **0d.** | Docker | We will provide a Dockerfile(s) that can be used to test all the functionality delivered with this milestone. |
| 0e. | Article | We will publish an **article**/workshop that explain how to use the service to interact with the wallet and how to view historical behavior. |
| 1. | Shared Components | We will provide a public library to encapsulate the wallet interface (including polkadot.js and metamask, etc.), as well as encapsulate the basic bridge configuration and base components. |
| 2. | Transfer Components | We will provide trading components to help users choose the correct chain and token, and display key parameters such as fees and transaction times. The most important call to the wallet interface to send cross-chain transactions. |
| 3. | History & Transaction Detail | We provide historical transaction records and transaction details display page, providing query, filtering and correlation of transaction history. |

## Future Plans

1. Support ERC20 and NFT transfers between parachains.
2. Support cross-chain pooling model.
3. Work with the Ethereum Asset Bridge project to aggregate its assets across linking ports and connect Ethereum to parachains.

## Additional Information :heavy_plus_sign:

We have already implemented asset interoperability between some of the parachains on Kusuma via xcm, moonriver, shiden, karura and other networks, and the basic software architecture is built and has a dapp page that can be accessed and operated. With the help of web3 Foundation, we hope to build a convenient, secure and fast multi-chain asset transfer portal for our users.
