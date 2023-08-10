

**New POC Proposal**

DCA.Monster: Modular DeFi 2.0 Components for Cartesi

 
**Core Concept and purpose statement**

The [DCA.Monster](https://ethglobal.com/showcase/dca-monster-b8157) project, an Automated Market Maker (AMM) previously distinguished at ETH Global Paris 2023, laid the groundwork for utilizing ERC20 streams for precise on-chain dollar-cost averaging (DCA). This Proof of Concept aims to extend its technical boundaries, improving both the power and flexibility of on-chain DCA mechanisms.

The crux of this POC centers around the development and optimization of Python-based Dockerized components, specifically crafted for compatibility with Cartesi's DeFi applications. While they're instrumental to the further advancement of DCA.Monster, these components have been architected to be modular and standalone building blocks, potentially contributing to other applications within the Cartesi ecosystem.

Key technical objectives for this POC include:

1.  **Streamable tokens:** Implementing Streamable token mechanics designed for efficient management of large-scale ongoing streams and accurate real-time balance computations.
2.  **Cartesi Subgraphs:** Implementing a dedicated Graph API mechanism, fine-tuned for indexing Cartesi-specific "Notices".
3.  **Cartesi Automated Market Maker:** Port the AMM model of Uniswap V2 to Cartesi, facilitating algorithmic token transfers without relying on an order book.
4.  **AMM & StreamableTokens:** Adapting the Uniswap V2 structure for Cartesi to integrate fluidly with StreamableTokens, facilitating stream swaps.
5.  **Gasless Transactions:** Adapting EIP-4337's gasless transaction framework for Cartesi DApps, keeping in mind Cartesi's unique architecture.

The underlying assumption driving this POC is that these individual modules, when cohesively integrated, can effectively elevate DCA.Monster's functionalities. Each module is also engineered to be operationally independent, allowing for immediate deployment within the Cartesi framework upon finalization. The primary success criterion is the realization of a fully functional version of DCA.Monster and the individual operational readiness of each distinct module post-development of each deliverable (Detailed descriptions below).
  
**How will you use Cartesi, specifically?**

DCA.Monster's implementation and each of it's components hinges on Cartesi's technology to enable its intricate functionalities on-chain. For this POC, Cartesi will be integrated in the following key areas:

1.  **Streamable tokens**: Cartesi will provide the scalable environment for efficient handling of large-scale streams and precise real-time balance computations. This would be impossible to implement in classic EVM smart contracts.
    
2.  **Cartesi Subgraphs**: A wrapper of Cartesi's graph API specifically targeting "Notices" generated in the rollup to index them with custom business logic to simplify data retrieval.
    
3.  **Cartesi AMM**: Porting Uniswap V2's AMM to Cartesi to allow token transfer operations, leveraging Cartesi's efficient computing environment.
    
4.  **Cartesi AMM with Streamable tokens**: Cartesi's modular computing will be used to adjust Uniswap V2's structure for compatibility with StreamableTokens featuring "stream swaps", and advance new kind of swap only possible with Cartesi's computation.
    
5.  **Gasless Transaction**: The EIP-4337 model will be adapted using Cartesi's off-chain computations, aiming for optimised transactional efficiency within DApps.
    
In summary, Cartesi's capabilities will be crucial for the technical execution of each module, ensuring both the enhancement of DCA.Monster and standalone functionality for the wider Cartesi ecosystem.

For a clearer understanding, reference to the sections detailing the specific technical objectives (such as Streamable token mechanics and Graph API mechanism) would provide an in-depth view of how Cartesi's features are intricately woven into the POC's architecture.

**Technical details**

Our outlined deliverables aim to introduce robust functionalities tailored specifically for Cartesi DeFi applications and other Cartesi DApps. Crafted using the Cartesi custom app starter kit, each modular component is structured for easy Docker deployment in Python, ensuring adaptability and reusability. Consistent quality assurance is maintained with a target of 90-95% test coverage.

1. **Streamable Tokens (Cartesi Streamable Tokens on-steroids)**

	-   **Description**: A python standardised implementation of a Cartesi Streamable token based on [SuperfluidToken](https://github.com/superfluid-finance/protocol-monorepo/blob/dev/packages/ethereum-contracts/contracts/superfluid/SuperfluidToken.sol) on-steroids that can handle a very high (almost infinite) number of ongoing streams and realtime balances. (See [realtimeBalanceOf](https://github.com/superfluid-finance/protocol-monorepo/blob/4e0833900fa51d2dd82cc1be55d97e43d64451f7/packages/ethereum-contracts/contracts/superfluid/SuperfluidToken.sol#L72C6-L72C6))
	-   **Features**:
		-  Standardised interface C-SERC-20 (Cartesi Streamable ERC-20) to have high composability with Cartesi DApps
		-   Work seamlessly with Cartesi's InputBox & Vouchers
	    -   Infinite (or extremely high) open streams that working graciously to allow building more sophisticated applications with them.
	-   **Benchmarking**:
	    -   Objective: Performance evaluation with high demand this number should support for a DEX operating at peak demand. Support at least [TODO] number of simultaneous token streams.
	-   **Use Cases**:
		-   Programmable transfers (e.g. send X tokens at specific time during X seconds)
	    -   Subscription Services: Manage ongoing subscription payments.
	    -   DEX
	-   **Deliverable duration**: [x weeks/months]
	-   **Funds request (USD) for the deliverable**: [$x USD]

2.  **Cartesi Subgraphs: Standardised Notices Subgraph Indexing Mechanism**

	-   **Description**: A Graph API tailored for Cartesi indexing "Notices" equipped with customisable parsers and Graph schemas. This mechanism mirrors the functionalities of [Subgraph](https://thegraph.com/docs/en/developing/creating-a-subgraph/) and is termed "Cartesi Subgraph." While its primary design targets indexing ongoing streams for DCA.Monster, its modular architecture ensures adaptability across diverse use cases. Within the Cartesi Subgraph framework, notices are parsed based on dedicated business logic, facilitating streamlined data provisioning for frontend applications via a Graph API, consistent with industry best practices.
	-   **Features**:
	    -   Flexible graph schema with configurable parsers, facilitating adaptability to diverse data structures and reusability in any context.
	    -   Seamless integration into the Cartesi Docker compose infrastructure.
	-   **Benchmarking**:
    
	    -   Prioritizes minimal indexation latency, ensuring its viability in frontend applications without compromising user experience.
	-   **Use Cases**:
    
	    -   Offloads data querying responsibilities from the Cartesi Inspect DApp Rest API, promoting performance efficiency.
	    -   Simplifies frontend business logic by presenting a ready-to-consume Graph API, streamlining data access and presentation.
	-   **Deliverable duration**: [x weeks/months]
	-   **Funds request (USD) for the deliverable**: [$x USD]

3.  **AMM: Uniswap V2 Port for Cartesi**
    
    -   **Description**: A meticulous port of the Uniswap V2 architecture to the Cartesi platform using Python, focusing on traditional transfer operations as found in a [Constant Function Market Maker (CFMM)](https://en.wikipedia.org/wiki/Constant_function_market_maker).
        
    -   **Features**:
        
        -   Adheres to the constant product formula, integral to the Uniswap V2 model.
        -   Supports standard transfer operations for straightforward token exchanges.
    -   **Design**:
        
        -   An exacting port of the Uniswap V2 system, adapted for Cartesi's unique environment.
    -   **Use Cases**:
        
        -   Decentralized token exchanges on the Cartesi platform.
        -   Facilitates token swaps.
	-   **Deliverable duration**: [x weeks/months]
	-   **Funds request (USD) for the deliverable**: [$x USD]
        
4.  **StreamableToken AMM: Advanced Market Maker for StreamableTokens**
    
    -   **Description**: Building upon the base Uniswap V2 AMM ported to Cartesi, this AMM is optimized to work effortlessly with StreamableTokens. It not only manages regular swaps but also extends support for advanced stream swaps, utilizing the computational advantages of the Cartesi Dapp and pushing the boundaries toward DeFi 2.0.
        
    -   **Features**:
        
        -   Seamless integration with StreamableTokens, permitting advanced stream swaps.
        -   Inherits the foundational features of the Uniswap V2 port but enhanced for token streams.
    -   **Design**:
        
        -   An evolution of the Uniswap V2 port on Cartesi, specifically honed for StreamableTokens' operations.
    -   **Use Cases**:
        
        -   Progressive decentralized token swaps with streaming capabilities.
        -   Dynamic DeFi operations leveraging token stream features.
	-   **Deliverable duration**: [x weeks/months]
	-   **Funds request (USD) for the deliverable**: [$x USD]
5. **EIP 4337: Gasless Transactions with Transaction Sponsors for Cartesi DApps**

	- **Description:**  
A Python light adaptation of the [EIP-4337](https://eips.ethereum.org/EIPS/eip-4337) upgrade tailored for Cartesi DApps, facilitating gasless transactions within the Cartesi ecosystem. This enhancement offers a seamless transaction experience, eliminating the need for individual users to pay gas fees. Transaction sponsors, such as Paymasters, assume these costs, making the process especially friendly for newcomers unfamiliar with the intricacies of the gas system. This is meant to be a simple reusable implementation port of the EIP 4337 to be used by DCA.Monster to offer gas-less swaps but allowing upgrades to implement all the remaining features of the EIP 4337.

	- **Features:**

		 1.  **Gasless Transactions for Cartesi:** Specifically designed to empower any Cartesi DApp with the ability to fund transactions not just with ETH but also with Cartesi bridged ERC-20 tokens.
    
		2.  **Paymaster Integration:** The backbone of the gasless transaction system, these Cartesi python smart contract accounts sponsor transactions, reducing the friction for DApp users. It's responsible for compensating the entity that fronts the gas cost for the transaction.
    
		3.  **Python Implementation:** Built using Python, this adaptation ensures a flexible and efficient approach to integrate gasless transactions within the Cartesi framework.
    

	- **Design:**
    
		1.  **Aggregator:** The Aggregator collects multiple such Cartesi user operations. It is responsible for bundling these operations and validating the aggregated signatures. Once bundled, the Aggregator submits these operations to the Cartesi rollup. Implemented as a Docker service, they process off-chain signed messages and upload to IPFS. However, these Aggregator are run by Cartesi node runners. As a result, users must trust that these runners aren't censoring or vetoing specific transactions. This introduces an element of trust in the decentralised system.
		2.  **Paymaster:** Python smart contract, assuring Cartesi DApp users can transact without gas fee concerns. Handles the logic to repay the sponsor for the gas upfront if needed.
    
	- **Use Cases:**

		1.  **Generalised Gasless transactions:** In the context of DCA.Monster, this adaptation enables users to perform swaps without worrying about gas fees, thus streamlining the user experience and reducing friction. However this implementation will be generalised to work in any DApp to offer transaction sponsoring out of the box.
    
		2.  **Mass Adoption within Cartesi:** By providing this feature, Cartesi DApps can cater to a broader audience, thus fostering the wider adoption of Cartesi's unique offerings.
    

	-   **Deliverable duration**: [x weeks/months]
	-   **Funds request (USD) for the deliverable**: [$x USD]
    

By housing all these modular deliverables within a single GitHub repository, we aim to simplify integration, ensuring Cartesi DApps can easily leverage them for varied use cases. Each module is constructed with a minimalistic approach, focusing on core functionalities while maintaining the flexibility for broader applications.


**Value Proposition**

This POC fortifies Cartesi's developer ecosystem by delivering modular DeFi components tailored for both specific and general purposes. The areas of value are:

1.  **Advanced Financial Tools**: With the refined DCA.Monster, developers have access to sophisticated on-chain dollar-cost averaging tools, expanding DeFi potential and enabling precise financial operations.
    
2. **Modular DeFi Components**: The POC emphasizes modularity. Each component functions independently, facilitating easier integration into various Cartesi DApps. This approach promotes innovation while decreasing development time and barriers for newcomers to Cartesi.
    
3.  **General-Purpose Modules**: By introducing versatile tools such as Cartesi Subgraphs and Gasless Transactions, the POC broadens the toolkit available for developers, allowing for a wide array of applications beyond just DeFi.

In sum, the POC's execution fosters agility in Cartesi's DeFi landscape and beyond, enabling developers to deploy faster, cut overheads, and smoothly integrate an array of cutting-edge modules. It's a significant stride towards a richer and more diversified development environment within Cartesi.

**Estimated Duration and Funds Requested**

Duration: [x weeks/months]

Funds request (USD) for the POC: [$x USD]

  
**Subsequent Vision and Extensibility**

  With the successful validation of the POC, we're paving the way for transformative projects within Cartesi.

**Vision**: DCA.Monster exemplifies the pinnacle of what's achievable, leveraging all the introduced modules to their full extent. It would stand as a testament to how comprehensive toolkits can lead to sophisticated DeFi platforms, offering advanced financial operations and granular controls. Beyond DCA.Monster, envision a Cartesi landscape flourishing with diverse DApps—each benefiting from the universally applicable modules—spanning areas from DeFi to gaming .

**Immediate Next Steps Post-POC**:

1.  **DCA.Monster Enhancement & Expansion**: Drawing on the POC, accelerate the development and deployment of advanced features in DCA.Monster, solidifying its place as a premier DeFi platform in Cartesi.
    
2.  **Feedback Integration**: Actively engage with DCA.Monster users and the broader Cartesi developer community to refine and optimize the modules, ensuring they meet real-world demands.
    
3.  **Broadened Cartesi Subgraphs Utility**: Amplify the utility of the Cartesi Subgraphs tool, supporting more diverse data structures and sources, expanding its reach.
    
4.  **Augmented Gasless Transaction Capabilities**: Further the gasless transaction module to embrace a broader array of tokens, broadening its appeal and use-case scenarios.
    
5.  **Educational Outreach**: Roll out detailed documentation, workshops, and tutorials, facilitating developers in harnessing the new modules, and integrating them into varied DApps.
    
6.  **Community-Centric Initiatives**: Spearhead events like hackathons, fostering innovation and possibly uncovering unanticipated applications of the new tools.
    

In sum, post-POC, the objective is twofold: bolstering DCA.Monster's capabilities and stature, and simultaneously promoting the broader adoption and innovative use of the modules by the diverse Cartesi developer community. The POC isn't just a foundation; it's a launchpad for a more dynamic and capable Cartesi ecosystem.


**Reusability and Other Use Cases**

This POC, presents a modular design that is ripe for a plethora of applications within the Cartesi ecosystem.

**Potential Uses**:

1.  **Streamable Tokens**: These can be employed beyond DeFi, finding applications in gaming for in-game assets, or for continuous subscription models in service platforms.
    
2.  **Cartesi Subgraphs**: Mimicking the EVM subgraph pattern, Cartesi Subgraphs preprocess on-chain data (Cartesi Notices), tailoring it with specific business logic, rendering it ready-to-consume for frontends and user queries. This streamlining can drastically enhance DApp efficiency and user experience.
    
3.  **AMM Module**: Projects aiming to facilitate programmatic tradable tokens can integrate this module, simplifying token trading mechanics.
    
4.  **Advanced AMM with Streams**: This showcases the future of AMMs — ones that can operate with streamable tokens and potentially intricate rules. This becomes feasible given the expanded capabilities enabled by Cartesi.
    
5.  **Gasless Transactions**: As Ethereum trends towards mainstreaming gasless interactions with concepts like EIP-4337, it’s essential for Cartesi to adopt this model. The module doesn't just eliminate transactional friction but sets the stage for EIP-4337's future incorporation within Cartesi.
    
In a nutshell, the POC's modules are versatile, ready-to-use components. Whether assimilated into expansive endeavors like DCA.Monster or integrated into smaller projects, they stand poised to redefine Cartesi-based developments, driving innovation and enhancing user-centric experiences.
  

**Risks and Contingency Plans**

 1.  **Performance Benchmark with Simultaneous Streams** :
		-   **Risk** : There's a possibility that we might not achieve the desired benchmarks when handling simultaneous on-going streams.
		-   **Contingency**: Should we encounter this performance hurdle, we can introduce design constraints to reduce complexity or refactor using a more performant low-level language, enhancing both speed and efficiency.

2.  **Bundled Transaction Size in Aggregator**:
    
    -   **Risk**: The aggregator might face constraints on the size of bundled transactions, limiting throughput.
    -   **Contingency**: Utilizing Cartesi's Linux environment, we can adopt advanced data compression techniques. By leveraging algorithms like LZ77 or Brotli, which are efficient for blockchain transaction data, we can drastically reduce transaction sizes, circumventing the limitation.
3.  **Integration with Existing Cartesi Infrastructure**:
    -   **Risk**: Interoperability challenges may arise when trying to fuse our modules with Cartesi's existing infrastructure.
    -   **Contingency**: Proactively engaging with Cartesi's core development community can facilitate smoother integration. If unforeseen incompatibilities emerge, we'll collaborate with Cartesi's team for potential workarounds or adjustments in our POC design.

In each case, constant monitoring, performance testing, and community feedback will be instrumental in detecting issues early. Such proactive measures will allow us to pivot or adjust our approach swiftly, ensuring the POC's successful realization.
  
**Success criteria**

1.  **Performance Benchmarks**:
    -   **Criteria**: Achieve optimized handling of simultaneous on-going streams without significant lag or processing delays. Our goal is for the system to gracefully handle a predefined number of streams without noticeable performance degradation.
    -   **Verification**: Detailed performance testing logs highlighting latency, throughput, and resource utilization.
2.  **Aggregator Transaction Bundling**:
	-   **Criteria**: Ensure efficient management of concurrent streams without prominent delays. The system should manage a set number of streams without evident performance drops.
	-   **Verification**: Performance summary showcasing latency and throughput metrics.
3.  **Module Integration and Interoperability**:
	-   **Criteria**: Efficient module integration with Cartesi infrastructure, ensuring each component functions as intended.
	-   **Verification**: A demonstration on DCA.Monster highlighting the cohesiveness and functionality of all integrated modules within the Cartesi platform.
4.  **Deliverables**:
    
	-   **Criteria**: Provide concise, well-documented code for each module, with user guidelines and sample applications to illustrate module utility.
	-   **Verification**: Direct links to repositories, documentation briefs, and sample use cases.
5.  **Community Feedback and Adjustments**:
    
	-   **Criteria**: Obtain constructive feedback from Cartesi's developer community or developer team to validate the modules' utility and effectiveness.
	-   **Verification**: Summaries from feedback sessions and consolidated survey insights.

The POC will be deemed complete when the outlined criteria are satisfied, supported by tangible evidence showcased on DCA.Monster.

**Deliverables:**

The detailed technicalities of each deliverable have been elucidated in the technical details section. Presented below is a brief list of the key deliverables for easy reference:

1.  **Streamable Tokens**:
    
    -   Python Implementation of a Cartesi Streamable token based on SuperfluidToken with capabilities to handle an extensive number of ongoing streams and realtime balances.
    -   Standardized C-SERC-20 interface, Cartesi's InputBox & Vouchers compatibility, and high-demand performance benchmarks.
2.  **Cartesi Subgraphs**:
    
    -   Graph API for Cartesi indexing "Notices", mirroring functionalities of Subgraph.
    -   Adaptable framework targeting indexing of ongoing streams for DCA.Monster.
3.  **AMM: Uniswap V2 Port for Cartesi**:
    
    -   Precise python port of Uniswap V2 for the Cartesi platform.
    -   Integration of the constant product formula and token exchange operations.
4.  **StreamableToken AMM**:
    
    -   Advanced Market Maker tailored for StreamableTokens.
    -   Enhancement of the Uniswap V2 port for Cartesi, honed for StreamableTokens' features.
5.  **EIP 4337: Gasless Transactions**:
    
    -   Python Implementation of the EIP-4337 tailored for Cartesi DApps.
    -   Integration of gasless transactions and paymaster mechanism.

Each deliverable will be accessible within a consolidated GitHub repository, ensuring streamlined access and integration.

  

**Final report**

Upon a failure of the POC, the Grants Council may still issue prorated payment if the applicant provides a written debriefing that sufficiently details the approaches used, why they failed, and what next steps would be if someone else were to resume the project. This will be shared with the community. Do you agree to provide this?
  
YES

  

**About Your Development team**
Pablo

Role: Pablo will lead the entire project, overseeing the technical development, integration, testing and documentation of each module.

  
 
**ERC-20 Payee address**

[TODO]