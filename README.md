# Overview

### Z Chain <a href="#credit-smart-chain" id="credit-smart-chain"></a>

Z Chain is a modular and extensible framework for building Ethereum-compatible blockchain networks, sidechains, and general scaling solutions.

Its primary use is to bootstrap a new blockchain network while providing full compatibility with Ethereum smart contracts and transactions. It uses IBFT (Istanbul Byzantine Fault Tolerant) consensus mechanism, supported in one flavour as [PoS (proof of stake)](https://tuoitresoft-1.gitbook.io/untitled/consensus/proof-of-stake).

Z Chain also supports communication with multiple blockchain networks, enabling transfers of both [ERC-20](https://ethereum.org/en/developers/docs/standards/tokens/erc-20/) and [ERC-721](https://ethereum.org/en/developers/docs/standards/tokens/erc-721) tokens, by utilising the centralised bridge solution.

Industry standard wallets can be used to interact with Z Chain through the [JSON-RPC](https://tuoitresoft-1.gitbook.io/untitled/architecture/modules/json-rpc) endpoints and node operators can perform various actions on the nodes through the [gRPC](https://tuoitresoft-1.gitbook.io/untitled/working-with-a-node/query-operator-information) protocol.

To find out more about Z Chain, visit the [official website](https://github.com/ZChain-168168).

[**GitHub repository**](https://github.com/ZChain-168168)

{% hint style="danger" %}
**CAUTION**

This is a work in progress so architectural changes may happen in the future, so please contact the Z team if you would like to use it in production.
{% endhint %}

To get started by running a`z-edge` network locally, please read: [Installation](https://tuoitresoft-1.gitbook.io/untitled/get-started/installation) and [Local Setup](https://tuoitresoft-1.gitbook.io/untitled/get-started/local-setup).
