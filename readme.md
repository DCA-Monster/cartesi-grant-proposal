

**New POC Proposal**

DCA.Monster: Modular DeFi 2.0 Components for Cartesi

 
**Core Concept and purpose statement**

The [DCA.Monster](https://ethglobal.com/showcase/dca-monster-b8157) project, an Automated Market Maker (AMM) previously distinguished at ETH Global Paris 2023, laid the groundwork for utilizing ERC20 streams for precise on-chain dollar-cost averaging (DCA). This Proof of Concept aims to extend its technical boundaries, improving both the power and flexibility of on-chain DCA mechanisms.

The crux of this POC centers around the development and optimization of Python-based Dockerized components, specifically crafted for compatibility with Cartesi's DeFi applications. While they're instrumental to the further advancement of DCA.Monster, these components have been architected to be modular and standalone building blocks, potentially contributing to other applications within the Cartesi ecosystem.

Key technical objectives for this POC include:

1.  **Streamable tokens:** Implementing Streamable token mechanics designed for efficient management of large-scale ongoing streams and accurate real-time balance computations.
2. **Cartesi Subgraphs:** Introducing a GraphQL API built atop Cartesi Node's native Postgres DB, emulating the utility and functionality of EVM's Subgraph, to streamline the processing of Cartesi-specific contract data for optimal frontend consumption.
3. **Cartesi Automated Market Maker & StreamableTokens Integration:** Port the AMM model of Uniswap V2 to Cartesi, facilitating algorithmic token transfers without relying on an order book. Further, adapt this structure to integrate seamlessly with StreamableTokens, enabling advanced stream swaps. Unlike traditional Order Book-based exchanges that require users to manually set buy or sell orders and often await matching trades, an AMM provides instant, automated swaps by leveraging a liquidity pool. This ensures more efficient trades, reduced user intervention, and a smoother overall trading experience.
4.  **Gasless Transactions:** Adapting EIP-4337's gasless transaction framework for Cartesi DApps, keeping in mind Cartesi's unique architecture.

The underlying assumption driving this POC is that these individual modules, when cohesively integrated, can effectively elevate DCA.Monster's functionalities. Each module is also engineered to be operationally independent, allowing for immediate deployment within the Cartesi framework upon finalization. The primary success criterion is the realization of a fully functional version of DCA.Monster and the individual operational readiness of each distinct module post-development of each deliverable (Detailed descriptions below).
  
**How will you use Cartesi, specifically?**

DCA.Monster's implementation and each of it's components hinges on Cartesi's technology to enable its intricate functionalities on-chain. For this POC, Cartesi will be integrated in the following key areas:

1.  **Streamable tokens**: Cartesi will provide the scalable environment for efficient handling of large-scale streams and precise real-time balance computations. This would be impossible to implement in classic EVM smart contracts.
    
2. **Cartesi Subgraphss**: Implementing a GraphQL API that interfaces seamlessly with Cartesi's Postgres DB, focusing on the transformation of "Notices" and other relevant contract states into an easily consumable format. This approach, inspired by EVM's Subgraphs, mitigates the inefficiencies of the Inspect API and furnishes developers with a familiar and efficient toolset.
    
3. **Cartesi AMM & StreamableTokens Integration:** Port Uniswap V2's AMM to Cartesi, harnessing token transfer operations within Cartesi's optimized computing environment. Further refine this framework to seamlessly integrate with StreamableTokens, pioneering the concept of "stream swaps". Leveraging Cartesi's distinct computational strengths, these advanced swap modalities are introduced, which would be computationally infeasible without the capabilities provided by Cartesi.
    
4.  **Gasless Transaction**: The EIP-4337 gasless transactions model will be adapted using Cartesi's off-chain computations, aiming for optimised transactional efficiency within DApps.
    
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

2.  **Cartesi Subgraphs:  GraphQL API Integration with Postgres DB**

	- **Description**: A GraphQL API built on top of Cartesi Node's native Postgres DB, specifically designed to imitate the functionality of EVM's [Subgraph](https://thegraph.com/docs/en/developing/creating-a-subgraph/). This novel implementation introduces a plug-in-like interface for the Postgres DB, bringing the familiar toolset of The Graph subgraphs to developers working with Cartesi. By acting as a business logic layer, it processes contract state information into easily consumable data formats for frontends. A significant advantage of this approach is replacing the less efficient "Inspect API", ensuring that the GraphQL API remains up-to-date with the latest contract information, analogous to Subgraphs in EVM contracts. 
	- **Features**: 
		- Mimics the familiar toolset of EVM's Subgraphs, enabling a smoother transition for developers to Cartesi. 
		- Provides a high-performance alternative to the Cartesi Inspect API, resolving its inherent limitations. 
		- Seamless plug-in-like  interface  for Cartesi's native Postgres DB. 
	- **Benchmarking**: 
		- Addresses the performance limitations of the Cartesi Inspect API, offering enhanced scalability and real-time data updates. 
	- **Use Cases**: 
		 - Aims to serve as a direct replacement for the Cartesi Inspect API, circumventing its efficiency constraints. See Considerations from Cartesi Documentation below. 
		 - Offers frontends a consistently updated source of data, similar to how Subgraphs function  for EVM contracts. 
	- **Considerations from Cartesi Documentation**: 
		- **Inspect Server**: Currently suffers from serialization and scalability issues. Inspect API calls can impact application efficiency due to its design, which stops new input processing to handle inspect requests. 
		- **Recommendation for Developers**: While the Inspect API is valuable for loading the application state initially, frequent calls should be minimized. For regular status updates, the GraphQL API should be leveraged, polling at intervals of around 500ms to maintain frontend synchronization. 
	- **Deliverable Duration**: [x weeks/months] 
	- **Funds Request (USD) for the Deliverable**: [$x USD]

	**3. AMM: Combined Uniswap V2 Port & StreamableToken Enhancement for Cartesi**

	-   **Description**: An integrated approach to bringing the Uniswap V2 architecture to the Cartesi platform using Python, focusing on traditional transfer operations from [Constant Function Market Maker (CFMM)](https://en.wikipedia.org/wiki/Constant_function_market_maker). Building on this foundational structure, we further optimize for StreamableTokens, introducing advanced stream swaps that leverage the computational capabilities of the Cartesi Dapp.
		
	-   **Features**:
		
		-   **Uniswap V2 Base**:
			-   Adheres to the constant product formula inherent in the Uniswap V2 model.
			-   Facilitates standard token exchange operations.
		-   **StreamableToken Enhancement**:
			-   Seamless integration with StreamableTokens, allowing for advanced stream swaps.
			-   Inherits and builds upon the foundational features of the Uniswap V2 port.
	-   **Design**:
		
		-   **Uniswap V2 Base**: Meticulous adaptation of the Uniswap V2 system for Cartesi's environment.
		-   **StreamableToken Enhancement**: Evolves the Uniswap V2 port on Cartesi, honing in specifically for StreamableTokens' functionalities.
	-   **Use Cases**:
		
		-   **Uniswap V2 Base**:
			-   Decentralized token exchanges on the Cartesi platform.
			-   Enables straightforward token swaps.
		-   **StreamableToken Enhancement**:
			-   Progressive decentralized token swaps incorporating streaming capabilities.
			-   Pioneering DeFi operations that utilize token stream benefits like Dollar-Cost Averaging.
	-   **Deliverable Duration**: [x weeks/months]
		
	-   **Funds Request (USD) for the Deliverable**: [$x USD]

	**4. Off-chain Transactions Aggregator API based on EIP-4337 for Cartesi DApps**

	-   **Description:**
	An API inspired by [EIP-4337](https://eips.ethereum.org/EIPS/eip-4337) custom-built for Cartesi DApps. It aggregates off-chain signed messages, validates the signatures, and structures them into Merkle Directed Acyclic Graphs (DAG) for storage on IPFS. To reinforce decentralization and circumvent potential transaction vetoing, the latest Content Identifier (CID) of the DAG is broadcasted over the Libp2p network. Given the public nature of the messages, any entity, including Cartesi-based protocols seeking to improve user experience, can process them via Cartesi's InputBox for rollup. This design epitomizes transparency and promotes efficient, gasless transactions within the Cartesi ecosystem.

		
	-   **Features:**
		
		1.  **Gasless Transactions for Cartesi:** Allows users to conduct transactions without worrying about gas fees.
			
		2.  **Transparent Off-chain Transactions:** Transactions are bundled and stored publicly on IPFS and broadcasted over the Libp2p network, ensuring any participant can post them.
			
		3.  **Timestamp and ID Integrity:** Every message carries a signature, timestamp, and ID, ensuring each transaction's authenticity and preventing double-spending.

		4. **Optional Automatic Execution:** The API can be configured to autonomously enact messages using a designated private key after reaching a predetermined count of transactions or a specific time duration (e.g., every X transactions or seconds).
			
	-   **Design:**  
		**Aggregator:** An API that processes off-chain signed messages, structures them into Merkle DAGs, and saves them on IPFS. It also broadcasts the associated CID via the Libp2p protocol. Optionally the API allows to automatically execute messages using a private key either after a set number of transactions or a specific time interval (e.g., every X transactions or seconds).

	-   **Use Cases:**
		
		1.  **Gasless Transactions in Cartesi:** Provides an efficient and user-friendly way to execute transactions without gas costs.
			
		2.  **Versatility in Cartesi Ecosystem:** The feature promotes broader Cartesi adoption by offering DApps and protocols a tool to enhance their user experience.
			
	-   **Deliverable duration**: [x weeks/months]
		
	-   **Funds request (USD) for the deliverable**: [$x USD]
    

By housing all these modular deliverables within a single GitHub repository, we aim to simplify integration, ensuring Cartesi DApps can easily leverage them for varied use cases. Each module is constructed with a minimalistic approach, focusing on core functionalities while maintaining the flexibility for broader applications.


**Value Proposition**

This POC fortifies Cartesi's developer ecosystem by delivering modular DeFi components tailored for both specific and general purposes. The areas of value are:

1.  **Advanced Financial Tools**: With the refined DCA.Monster, developers have access to sophisticated on-chain dollar-cost averaging tools, expanding DeFi potential and enabling precise financial operations.
    
2. **Modular DeFi Components**: The POC emphasizes modularity. Each component functions independently, facilitating easier integration into various Cartesi DApps. This approach promotes innovation while decreasing development time and barriers for newcomers to Cartesi.
    
3.  **General-Purpose Modules**: The addition of versatile tools, like the GraphQL API for Cartesi Subgraphs and Gasless Transactions, provides developers with a broader toolkit.

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
    
3.  **Broadened Cartesi Subgraphs Utility**: Our ambition for Cartesi Subgraphs isn't confined to its present capabilities. We envision augmenting its utility, ensuring it's adaptable to a plethora of data structures and sources.
    
4.  **Augmented Gasless Transaction Capabilities**: Further the gasless transaction module to add transaction sponsor repayment in bridged tokens logic within the rollup, broadening its appeal and use-case scenarios.
    
5.  **Educational Outreach**: Roll out detailed documentation, workshops, and tutorials, facilitating developers in harnessing the new modules, and integrating them into varied DApps.
    
6.  **Community-Centric Initiatives**: Spearhead events like hackathons, fostering innovation and possibly uncovering unanticipated applications of the new tools.
    

In sum, post-POC, the objective is twofold: bolstering DCA.Monster's capabilities and stature, and simultaneously promoting the broader adoption and innovative use of the modules by the diverse Cartesi developer community. The POC isn't just a foundation; it's a launchpad for a more dynamic and capable Cartesi ecosystem.


**Reusability and Other Use Cases**

This POC, presents a modular design that is ripe for a plethora of applications within the Cartesi ecosystem.

**Potential Uses**:

1.  **Streamable Tokens**: These can be employed beyond DeFi, finding applications in gaming for in-game assets, or for continuous subscription models in service platforms.
    
2.  **Cartesi Subgraphs**: Drawing inspiration from the EVM subgraph, the Cartesi Subgraphs provide a GraphQL API integrated with Cartesi Node's Postgres DB. This unique configuration pre-processes on-chain data (like Cartesi Notices) in line with distinct business logic, ensuring it's primed for frontend consumption and user queries. This optimization can significantly elevate DApp performance and overall user experience.
    
3. **AMM Module with Advanced Stream Capabilities**: Projects aiming to simplify token trading mechanics can integrate this module. Beyond facilitating programmatic tradable tokens, it showcases the future of AMMs that can operate with streamable tokens and handle intricate rules, leveraging the enhanced capabilities provided by Cartesi.
    
4.  **Gasless Transactions**: As Ethereum trends towards mainstreaming gasless interactions with concepts like EIP-4337, it’s essential for Cartesi to adopt this model. The module doesn't just eliminate transactional friction but sets the stage for EIP-4337's future incorporation within Cartesi.
    
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
2.  **Aggregator Message Bundling**:
    -   **Criteria**: Ensure efficient management of concurrent off-chain signed messages without prominent delays. The system should manage a set number of messages without evident performance drops.
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
    
	-	A GraphQL API interfaced with Cartesi Node's native Postgres DB, emulating the functionality of EVM's Subgraph.
	-	A versatile framework geared towards indexing token streams, especially for DCA.Monster, while offering the flexibility for diverse applications.
3.  **AMM with StreamableToken Enhancement: Uniswap V2 Port for Cartesi**:
	-   Precise python port of Uniswap V2 for the Cartesi platform, integrated with the constant product formula and token exchange operations.
	-   Advanced Automated Market Maker tailored specifically for StreamableTokens, further enhancing the Uniswap V2 port for Cartesi to cater to StreamableTokens' unique requirements.
4.  **Gasless Transactions Based on EIP-4337**:

	-   Adapt a version of gasless transactions in a python API specifically designed for Cartesi DApps.
		
	-  Seamlessly incorporate the gasless transaction mechanism, drawing inspiration from the EIP-4337 structure, to enhance its functionality and usability within the Cartesi ecosystem.

Each deliverable will be accessible within a consolidated GitHub repository, ensuring streamlined access and integration.

  

**Final report**

Upon a failure of the POC, the Grants Council may still issue prorated payment if the applicant provides a written debriefing that sufficiently details the approaches used, why they failed, and what next steps would be if someone else were to resume the project. This will be shared with the community. Do you agree to provide this?
  
YES

  

**About Your Development team**
Pablo

Role: Pablo will lead the entire project, overseeing the technical development, integration, testing and documentation of each module.

  
 
**ERC-20 Payee address**

[TODO]
