# 🔖 The Openbook Protocol

A protocol featuring a high-frequency off-chain order book with on-chain settlement, enabling capital-efficient peer-to-peer markets.

The Openbook Protocol is essentially defined as a major product that brings together other modules into a single platform. Put simply, it can be described as a core layer open to developing different concepts of products.

The Openbook Protocol provides a platform where all public/private orders from the OTC portal, all orders managed by the limit order protocol, and even instant orders executed by Piteas can be managed in a single portal.

### The Orderbook Protocol Process <a href="#the-orderbook-protocol-flow" id="the-orderbook-protocol-flow"></a>

* A market participant creates a limit order specifying the assets they offer and the assets they expect to receive, and signs this message. Another participant, known as the taker, can then choose to fulfill the order by signing a mirrored version of the maker's original order.
* The taker's signature is then sent back to the maker, who settles the transaction on-chain using the Order settlement contract. The maker receives both the maker and taker order signatures, along with an additional server signature.
* This signature from the taker is propagated back to the maker for the market maker to settle on-chain by a call to the Order settlement contract. The market maker will be given both order signatures (the maker and the taker order) plus an additional server signature.
* If the maker does not execute the order by the set block deadline time N, the taker gains the ability to execute the order, preventing censorship by the maker.
* If neither party executes the order, it is removed from the order book after N blocks (i.e., T + 2N).

***

### Order Creation and Execution <a href="#order-creation-and-execution" id="order-creation-and-execution"></a>

**Maker Orders and Signatures:** On Pday, a maker's order is represented by a signature containing order details, allowing a taker to execute based on those parameters. This approach enables makers to place and cancel orders without gas fees or losing custody of assets until execution.

**Taker Execution:** When a taker fulfills an order, it is removed from the order book upon receiving the API call, even before on-chain confirmation. A server signature is then generated, allowing a set number of blocks for order execution. If not executed within this timeframe, the order returns to the order book. To prevent potential DDOS attacks, takers have a limit on the number of orders they can take without on-chain confirmation.

***

### Limit Orders as Intentions <a href="#limit-orders-as-intents" id="limit-orders-as-intents"></a>

Various initiatives have introduced new types of intentions for consumers. While some teams work on creating generalized languages for intentions, others focus on novel DSLs for their ecosystem. In traditional finance, limit orders have been the foundation of markets. By porting this concept to on-chain trading, we benefit from simplicity, granularity, and fixed pricing, reducing attack vectors and providing a seamless experience for traditional institutions.

Utilizing a static price limit order offers several advantages over alternative methods:

* The simplicity and granularity of a limit order make it easy to analyze, transmit, and aggregate.
* With a constant price, there is no slippage, eliminating most attack vectors such as sandwiching or single block censorship. This ensures a fairer environment for market makers and liquidity providers.
* Traditional market making models can be seamlessly applied, providing a familiar experience for institutions seeking to access on-chain liquidity.

***

### Solver Ecosystem <a href="#solvers-upon-solvers" id="solvers-upon-solvers"></a>

The term "solver" refers to programs specialized in solving specific problems, akin to searchers, keepers, and fillers ensuring protocol health on-chain. These entities utilize domain-specific knowledge for optimization and decision-making.

MEV searchers are increasingly seen as creating positive externalities for users, with order flow auctions and RFQ-like platforms driving narratives of payment for order flow. As technical skills for writing solvers evolve, modularization of solver functionalities must keep pace, allowing multiple solvers to work in tandem across different contexts.

We aim to manage relationships with MEV searchers, institutional market makers, and high-frequency trading firms, channeling liquidity into user-facing solutions.
