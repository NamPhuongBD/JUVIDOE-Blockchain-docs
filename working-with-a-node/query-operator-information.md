# Query operator information

#### Prerequisites[​](https://polygon-edge-v063.evmbuilder.com/docs/working-with-node/query-operator-info#prerequisites) <a href="#prerequisites" id="prerequisites"></a>

This guide assumes you have followed the [Local Setup](../get-started/local-setup.md) or guide on how to set up an IBFT cluster on the cloud.

A functioning node is required in order to query any kind of operator information.

With the Z Smart Chain, node operators are in control and informed about what the node they're operating is doing. At any time, they can use the node information layer, built on top of gRPC, and get meaningful information - no log sifting required.

**NOTE**

If your node isn't running on `127.0.0.1:8545` you should add a flag `--grpc-address <address:port>` to the commands listed in this document.

#### Peer information[​](https://polygon-edge-v063.evmbuilder.com/docs/working-with-node/query-operator-info#peer-information) <a href="#peer-information" id="peer-information"></a>

**Peers list**[**​**](https://polygon-edge-v063.evmbuilder.com/docs/working-with-node/query-operator-info#peers-list)

To get a complete list of connected peers (including the running node itself), run the following command:

```
polygon-edge peers list
```

This will return a list of libp2p addresses that are currently peers of the running client.

**Peer status**[**​**](https://polygon-edge-v063.evmbuilder.com/docs/working-with-node/query-operator-info#peer-status)

For the status of a specific peer, run:

```
polygon-edge peers status --peer-id <address>
```

With the _address_ parameter being the libp2p address of the peer.

#### IBFT info[​](https://polygon-edge-v063.evmbuilder.com/docs/working-with-node/query-operator-info#ibft-info) <a href="#ibft-info" id="ibft-info"></a>

Lots of times, an operator might want to know about the state of the operating node in IBFT consensus.

Luckily, the Z Smart Chain provides an easy way to find this information.

**Snapshots**[**​**](https://polygon-edge-v063.evmbuilder.com/docs/working-with-node/query-operator-info#snapshots)

Running the following command returns the most recent snapshot.

Copy

```
polygon-edge ibft snapshot
```

To query the snapshot at a specific height (block number), the operator can run:

Copy

```
polygon-edge ibft snapshot --num <block-number>
```

**Candidates**[**​**](https://polygon-edge-v063.evmbuilder.com/docs/working-with-node/query-operator-info#candidates)

To get the latest info on candidates, the operator can run:

Copy

```
polygon-edge ibft candidates
```

This command queries the current set of proposed candidates, as well as candidates that have not been included yet

**Status**[**​**](https://polygon-edge-v063.evmbuilder.com/docs/working-with-node/query-operator-info#status)

The following command returns the current validator key of the running IBFT client:

Copy

```
polygon-edge ibft status
```

#### Transaction pool[​](https://polygon-edge-v063.evmbuilder.com/docs/working-with-node/query-operator-info#transaction-pool) <a href="#transaction-pool" id="transaction-pool"></a>

To find the current number of transactions in the transaction pool, the operator can run:

Copy

```
polygon-edge txpool status
```
