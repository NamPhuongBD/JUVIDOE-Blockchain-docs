# JSON RPC Commands

### eth

#### eth\_chainId

Returns the currently configured chain id, a value used in replay-protected transaction signing as introduced by EIP-155.

***

_**Parameters:**_

* None

_**Returns:**_

* QUANTITY - big integer of the current chain id.

_**Example:**_

Run the command and see live results from our testnet.

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_chainId","params":[],"id":1}'
```

Run command

#### eth\_syncing

Returns information about the sync status of the node

***

_**Parameters:**_

* None

_**Returns:**_

\* Boolean (FALSE) - if the node isn't syncing (which means it has fully synced)

\* Object - an object with sync status data if the node is syncing

* startingBlock: QUANTITY - The block at which the import started (will only be reset, after the sync reached his head)
* currentBlock: QUANTITY - The current block, same as eth\_blockNumber
* highestBlock: QUANTITY - The estimated highest block

_**Example:**_

Run the command and see live results from our testnet.

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_syncing","params":[],"id":1}'
```

Run command

#### eth\_getBlockByNumber

Returns block information by number.

***

_**Parameters:**_

* QUANTITY|TAG - integer of a block number, or the string "latest"
* Boolean - If true it returns the full transaction objects, if false only the hashes of the transactions.

_**Returns:**_

Object - A block object, or null when no block was found:

* number: QUANTITY - the block number.
* hash: DATA, 32 Bytes - hash of the block.
* parentHash: DATA, 32 Bytes - hash of the parent block.
* nonce: DATA, 8 Bytes - hash of the generated proof-of-work.
* sha3Uncles: DATA, 32 Bytes - SHA3 of the uncles data in the block.
* logsBloom: DATA, 256 Bytes - the bloom filter for the logs of the block.
* transactionsRoot: DATA, 32 Bytes - the root of the transaction trie of the block.
* stateRoot: DATA, 32 Bytes - the root of the final state trie of the block.
* receiptsRoot: DATA, 32 Bytes - the root of the receipts trie of the block.
* miner: DATA, 20 Bytes - the address of the beneficiary to whom the mining rewards were given.
* difficulty: QUANTITY - integer of the difficulty for this block.
* totalDifficulty: QUANTITY - integer of the total difficulty of the chain until this block.
* extraData: DATA - the “extra data” field of this block.
* size: QUANTITY - integer the size of this block in bytes.
* gasLimit: QUANTITY - the maximum gas allowed in this block.
* gasUsed: QUANTITY - the total used gas by all transactions in this block.
* timestamp: QUANTITY - the unix timestamp for when the block was collated.
* transactions: Array - Array of transaction objects, or 32 Bytes transaction hashes depending on the last given parameter.
* uncles: Array - Array of uncle hashes.

_**Example:**_

Run the command and see live results from our testnet.

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getBlockByNumber","params":["latest", true],"id":1}'
```

Run command

#### eth\_getBlockByHash

Returns block information by hash.

***

_**Parameters:**_

* DATA , 32 Bytes - Hash of a block.
* Boolean - If true it returns the full transaction objects, if false only the hashes of the transactions.

_**Returns:**_

Object - A block object, or null when no block was found:

* number: QUANTITY - the block number.
* hash: DATA, 32 Bytes - hash of the block.
* parentHash: DATA, 32 Bytes - hash of the parent block.
* nonce: DATA, 8 Bytes - hash of the generated proof-of-work.
* sha3Uncles: DATA, 32 Bytes - SHA3 of the uncles data in the block.
* logsBloom: DATA, 256 Bytes - the bloom filter for the logs of the block.
* transactionsRoot: DATA, 32 Bytes - the root of the transaction trie of the block.
* stateRoot: DATA, 32 Bytes - the root of the final state trie of the block.
* receiptsRoot: DATA, 32 Bytes - the root of the receipts trie of the block.
* miner: DATA, 20 Bytes - the address of the beneficiary to whom the mining rewards were given.
* difficulty: QUANTITY - integer of the difficulty for this block.
* totalDifficulty: QUANTITY - integer of the total difficulty of the chain until this block.
* extraData: DATA - the “extra data” field of this block.
* size: QUANTITY - integer the size of this block in bytes.
* gasLimit: QUANTITY - the maximum gas allowed in this block.
* gasUsed: QUANTITY - the total used gas by all transactions in this block.
* timestamp: QUANTITY - the unix timestamp for when the block was collated.
* transactions: Array - Array of transaction objects, or 32 Bytes transaction hashes depending on the last given parameter.
* uncles: Array - Array of uncle hashes.

_**Example:**_

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getBlockByHash","params":["0xdc0818cf78f21a8e70579cb46a43643f78291264dda342ae31049421c82d21ae",false],"id":1}'
```

#### eth\_blockNumber

Returns the number of the most recent block.

***

_**Parameters:**_

None

_**Returns:**_

* QUANTITY - integer of the current block number the client is on.

_**Example:**_

Run the command and see live results from our testnet.

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}'
```

Run command

#### eth\_gasPrice[​](https://polygon-edge-v063.evmbuilder.com/docs/get-started/json-rpc-commands#eth_gasprice) <a href="#eth_gasprice" id="eth_gasprice"></a>

Returns the current price of gas in wei. If minimum gas price is enforced by setting the `--price-limit` flag, this endpoint will return the value defined by this flag as minimum gas price.

***

_**Parameters:**_

None

_**Returns:**_

* QUANTITY - integer of the current gas price in wei.

_**Example:**_

Run the command and see live results from our testnet.

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_gasPrice","params":[],"id":1}'
```

Run command

#### eth\_getBalance[​](https://polygon-edge-v063.evmbuilder.com/docs/get-started/json-rpc-commands#eth_getbalance) <a href="#eth_getbalance" id="eth_getbalance"></a>

Returns the balance of the account of the given address.

***

_**Parameters:**_

* DATA, 20 Bytes - address to check for balance.
* QUANTITY|TAG - integer block number, or the string "latest"

_**Returns:**_

* QUANTITY - integer of the current balance in wei.

_**Example:**_

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getBalance","params":["0x407d73d8a49eeb85d32cf465507dd71d507100c1", "latest"],"id":1}'
```

#### eth\_sendRawTransaction[​](https://polygon-edge-v063.evmbuilder.com/docs/get-started/json-rpc-commands#eth_sendrawtransaction) <a href="#eth_sendrawtransaction" id="eth_sendrawtransaction"></a>

Creates new message call transaction or a contract creation for signed transactions.

***

_**Parameters:**_

* DATA - The signed transaction data.

_**Returns:**_

* DATA, 32 Bytes - the transaction hash, or the zero hash if the transaction is not yet available.

_**Example:**_

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_sendRawTransaction","params":["0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675"],"id":1}'
```

Returns the information about a transaction requested by transaction hash.

***

_**Parameters:**_

* DATA, 32 Bytes - hash of a transaction

_**Returns:**_

Object - A transaction object, or null when no transaction was found:

* blockHash: DATA, 32 Bytes - hash of the block where this transaction was in.
* blockNumber: QUANTITY - block number where this transaction was in.
* from: DATA, 20 Bytes - address of the sender.
* gas: QUANTITY - gas provided by the sender.
* gasPrice: QUANTITY - gas price provided by the sender in Wei.
* hash: DATA, 32 Bytes - hash of the transaction.
* input: DATA - the data send along with the transaction.
* nonce: QUANTITY - the number of transactions made by the sender prior to this one.
* to: DATA, 20 Bytes - address of the receiver. null when its a contract creation transaction.
* transactionIndex: QUANTITY - integer of the transactions index position in the block.
* value: QUANTITY - value transferred in Wei.
* v: QUANTITY - ECDSA recovery id
* r: DATA, 32 Bytes - ECDSA signature r
* s: DATA, 32 Bytes - ECDSA signature s

_**Example:**_

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getTransactionByHash","params":["0x88df016429689c079f3b2f6ad39fa052532c56795b733da78a91ebe6a713944b"],"id":1}'
```

#### eth\_getTransactionReceipt

Returns the receipt of a transaction by transaction hash.

Note That the receipt is not available for pending transactions.

***

_**Parameters:**_

* DATA, 32 Bytes - hash of a transaction

_**Returns:**_

Object - A transaction receipt object, or null when no receipt was found:

* transactionHash : DATA, 32 Bytes - hash of the transaction.
* transactionIndex: QUANTITY - integer of the transactions index position in the block.
* blockHash: DATA, 32 Bytes - hash of the block where this transaction was in.
* blockNumber: QUANTITY - block number where this transaction was in.
* from: DATA, 20 Bytes - address of the sender.
* to: DATA, 20 Bytes - address of the receiver. null when its a contract creation transaction.
* cumulativeGasUsed : QUANTITY - The total amount of gas used when this transaction was executed in the block.
* gasUsed : QUANTITY - The amount of gas used by this specific transaction alone.
* contractAddress : DATA, 20 Bytes - The contract address created, if the transaction was a contract creation, otherwise null.
* logs: Array - Array of log objects, which this transaction generated.
* logsBloom: DATA, 256 Bytes - Bloom filter for light clients to quickly retrieve related logs.

It also returns either :

* root : DATA 32 bytes - post-transaction stateroot (pre Byzantium)
* status: QUANTITY - either 1 (success) or 0 (failure)

_**Example:**_

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getTransactionReceipt","params":["0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238"],"id":1}'
```

#### eth\_getTransactionCount

Returns the number of transactions sent from an address.

***

_**Parameters:**_

* DATA, 20 Bytes - address.
* QUANTITY|TAG - integer block number, or the string "latest"

_**Returns:**_

* QUANTITY - integer of the number of transactions send from this address.

_**Example:**_

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getTransactionCount","params":["0x407d73d8a49eeb85d32cf465507dd71d507100c1","latest"],"id":1}'
```

#### eth\_getBlockTransactionCountByNumber

Returns the number of transactions in a block matching the given block number.

***

_**Parameters:**_

* QUANTITY|TAG - integer of a block number, or the string "latest"

_**Returns:**_

* QUANTITY - integer of the number of transactions in this block.

_**Example:**_

Run the command and see live results from our testnet.

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getBlockTransactionCountByNumber","params":["latest"],"id":1}'
```

Run command

#### eth\_getLogs

Returns an array of all logs matching a given filter object.

***

_**Parameters:**_

Object - The filter options:

* fromBlock: QUANTITY|TAG - (optional, default: "latest") Integer block number, or "latest" for the last mined block
* toBlock: QUANTITY|TAG - (optional, default: "latest") Integer block number, or "latest" for the last mined block
* address: DATA|Array, 20 Bytes - (optional) Contract address or a list of addresses from which logs should originate.
* topics: Array of DATA - (optional) Array of 32 Bytes DATA topics. Topics are order-dependent. Each topic can also be an array of DATA with “or” options.
* blockhash: DATA, 32 Bytes - (optional, future) With the addition of EIP-234, blockHash will be a new filter option which restricts the logs returned to the single block with the 32-byte hash blockHash. Using blockHash is equivalent to fromBlock = toBlock = the block number with hash blockHash. If blockHash is present in the filter criteria, then neither fromBlock nor toBlock is allowed.

_**Returns:**_

* QUANTITY - integer of the number of transactions send from this address.

_**Example:**_

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getLogs","params":[{"topics": ["0x000000000000000000000000a94f5374fce5edbc8e2a8697c15331677e6ebf0b"]}],"id":1}'
```

#### eth\_getCode

Returns code at a given address.

***

_**Parameters:**_

* DATA, 20 Bytes - address
* QUANTITY|TAG - integer block number, or the string "latest"

_**Returns:**_

* DATA - the code from the given address.

_**Example:**_

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getCode","params":["0xa94f5374fce5edbc8e2a8697c15331677e6ebf0b", "0x2"],"id":1}'
```

#### eth\_call

Executes a new message call immediately without creating a transaction on the blockchain.

***

_**Parameters:**_

Object - The transaction call object

* from: DATA, 20 Bytes - (optional) The address the transaction is sent from.
* to: DATA, 20 Bytes - The address the transaction is directed to.
* gas: QUANTITY - (optional) Integer of the gas provided for the transaction execution. eth\_call consumes zero gas, but this parameter may be needed by some executions.
* gasPrice: QUANTITY - (optional) Integer of the gasPrice used for each paid gas
* value: QUANTITY - (optional) Integer of the value sent with this transaction
* data: DATA - (optional) Hash of the method signature and encoded parameters. For details see Ethereum Contract ABI in the Solidity documentation
* QUANTITY|TAG - integer block number, or the string "latest", see the default block paramete

_**Returns:**_

* DATA - the return value of executed contract.

_**Example:**_

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_call","params":[{see above}],"id":1}'
```

#### eth\_getStorageAt

Returns the value from a storage position at a given address.

***

_**Parameters:**_

* DATA, 20 Bytes - address of the storage.
* QUANTITY - integer of the position in the storage.
* QUANTITY|TAG - integer block number, or the string "latest"

_**Returns:**_

* DATA - the value at this storage position.

_**Example:**_

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getStorageAt","params":["0x295a70b2de5e3953354a6a8344e616ed314d7251", "0x0", "latest"],"id":1}'
```

#### eth\_estimateGas

Generates and returns an estimate of how much gas is necessary to allow the transaction to complete. The transaction will not be added to the blockchain. Note that the estimate may be significantly more than the amount of gas actually used by the transaction, for a variety of reasons including EVM mechanics and node performance.

***

_**Parameters:**_

Expect that all properties are optional.

Object - The transaction call object

* from: DATA, 20 Bytes - The address the transaction is sent from.
* to: DATA, 20 Bytes - The address the transaction is directed to.
* gas: QUANTITY - Integer of the gas provided for the transaction execution. eth\_call consumes zero gas, but this parameter may be needed by some executions.
* gasPrice: QUANTITY - Integer of the gasPrice used for each paid gas
* value: QUANTITY - Integer of the value sent with this transaction
* data: DATA - Hash of the method signature and encoded parameters. For details see Ethereum Contract ABI in the Solidity documentation
* QUANTITY|TAG - integer block number, or the string "latest", see the default block paramete

_**Returns:**_

* QUANTITY - the amount of gas used.

_**Example:**_

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_estimateGas","params":[{see above}],"id":1}'
```

#### eth\_newFilter

Creates a filter object, based on filter options. To get all matching logs for specific filter, call eth\_getFilterLogs. To check if the state has changed, call eth\_getFilterChanges.

***

_**Parameters:**_

Object - The filter options:

* fromBlock: QUANTITY|TAG - (optional, default: "latest") Integer block number, or "latest" for the last mined block
* toBlock: QUANTITY|TAG - (optional, default: "latest") Integer block number, or "latest" for the last mined block
* address: DATA|Array, 20 Bytes - (optional) Contract address or a list of addresses from which logs should originate.
* topics: Array of DATA - (optional) Array of 32 Bytes DATA topics. Topics are order-dependent. Each topic can also be an array of DATA with “or” options.

_**Returns:**_

* QUANTITY - A filter id.

_**Example:**_

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_newFilter","params":[{"topics":["0x12341234"]}],"id":1}'
```

#### eth\_newBlockFilter

Creates a filter in the node, to notify when a new block arrives. To check if the state has changed, call eth\_getFilterChanges.

***

_**Parameters:**_

None

_**Returns:**_

1. QUANTITY - A filter id.

_**Example:**_

Run the command and see live results from our testnet.

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_newBlockFilter","params":[],"id":1}'
```

Run command

eth\_getFilterLogs

Returns an array of all logs matching filter with given id.

{% hint style="danger" %}
**ETH\_GETLOGS VS. ETH\_GETFILTERLOGS**

These 2 methods will return the same results for same filter options:

1. eth\_getLogs with params \[options]
2. eth\_newFilter with params \[options], getting a \[filterId] back, then calling eth\_getFilterLogs with \[filterId]
{% endhint %}

_**Parameters:**_

* QUANTITY - the filter id.

_**Returns:**_

Array - Array of log objects, or an empty array

* For filters created with eth\_newFilter logs are objects with the following params:
  * removed: TAG - true when the log was removed, due to a chain reorganization. false if its a valid log.
  * logIndex: QUANTITY - integer of the log index position in the block. null when its pending log.
  * transactionIndex: QUANTITY - integer of the transactions index position log was created from. null when its pending log.
  * transactionHash: DATA, 32 Bytes - hash of the transactions this log was created from. null when its pending log.
  * blockHash: DATA, 32 Bytes - hash of the block where this log was in. null when its pending log.
  * blockNumber: QUANTITY - the block number where this log was in. null when its pending log.
  * address: DATA, 20 Bytes - address from which this log originated.
  * data: DATA - contains one or more 32 Bytes non-indexed arguments of the log.
  * topics: Array of DATA - Array of 0 to 4 32 Bytes DATA of indexed log arguments. (In solidity: The first topic is the hash of the signature of the event (e.g. Deposit(address,bytes32,uint256)), except you declared the event with the anonymous specifier.)

_**Example:**_

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getFilterLogs","params":["0x16"],"id":1}'
```

Polling method for a filter, which returns an array of logs that occurred since the last poll.

***

_**Parameters:**_

* QUANTITY - the filter id.

_**Returns:**_

Array - Array of log objects, or an empty array if nothing has changed since last poll.

* For filters created with eth\_newBlockFilter the return are block hashes (DATA, 32 Bytes), e.g. \["0x3454645634534..."].
* For filters created with eth\_newFilter logs are objects with the following params:
  * removed: TAG - true when the log was removed, due to a chain reorganization. false if its a valid log.
  * logIndex: QUANTITY - integer of the log index position in the block. null when its pending log.
  * transactionIndex: QUANTITY - integer of the transactions index position log was created from. null when its pending log.
  * transactionHash: DATA, 32 Bytes - hash of the transactions this log was created from. null when its pending log.
  * blockHash: DATA, 32 Bytes - hash of the block where this log was in. null when its pending log.
  * blockNumber: QUANTITY - the block number where this log was in. null when its pending log.
  * address: DATA, 20 Bytes - address from which this log originated.
  * data: DATA - contains one or more 32 Bytes non-indexed arguments of the log.
  * topics: Array of DATA - Array of 0 to 4 32 Bytes DATA of indexed log arguments. (In solidity: The first topic is the hash of the signature of the event (e.g. Deposit(address,bytes32,uint256)), except you declared the event with the anonymous specifier.)

_**Example:**_

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getFilterChanges","params":["0x16"],"id":1}'
```

#### eth\_uninstallFilter

Uninstalls a filter with a given id. Should always be called when a watch is no longer needed. Additionally, filters timeout when they aren’t requested with eth\_getFilterChanges for some time.

***

_**Parameters:**_

* QUANTITY - The filter id.

_**Returns:**_

* Boolean - true if the filter was successfully uninstalled, otherwise false.

_**Example:**_

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_uninstallFilter","params":["0xb"],"id":1}'
```

#### eth\_unsubscribe

Subscriptions are cancelled with a regular RPC call with eth\_unsubscribe as a method and the subscription id as the first parameter. It returns a bool indicating if the subscription was cancelled successfully.

***

_**Parameters:**_

* SUBSCRIPTION ID

_**Returns:**_

* UNSUBSCRIBED FLAG - true if the subscription was cancelled successful.

_**Example:**_

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_unsubscribe","params":["0x9cef478923ff08bf67fde6c64013158d"],"id":1}'
```

### net

#### net\_version

Returns the current network id.

***

_**Parameters:**_

None

_**Returns:**_

* String - The current network id.

_**Example:**_

Run the command and see live results from our testnet.

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"net_version","params":[],"id":83}'
```

Run command

#### net\_listening

Returns true if a client is actively listening for network connections.

***

_**Parameters:**_

None

_**Returns:**_

* Boolean - true when listening, otherwise false.

_**Example:**_

Run the command and see live results from our testnet.

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"net_listening","params":[],"id":83}'
```

Run command

#### net\_peerCount

Returns number of peers currently connected to the client.

***

_**Parameters:**_

None

_**Returns:**_

* QUANTITY - integer of the number of connected peers.

_**Example:**_

Run the command and see live results from our testnet.

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"net_peerCount","params":[],"id":1}'
```

Run command

### web3

#### web3\_clientVersion

Returns the current client version.

***

_**Parameters:**_

None

_**Returns:**_

* String - The current client version

_**Example:**_

Run the command and see live results from our testnet.

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"web3_clientVersion","params":[],"id":1}'
```

Run command

#### web3\_sha3

Returns Keccak-256 (not the standardized SHA3-256) of the given data.

***

_**Parameters:**_

* DATA - the data to convert into a SHA3 hash

_**Returns:**_

* DATA - The SHA3 result of the given string.

_**Example:**_

Run the command and see live results from our testnet.

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"web3_sha3","params":["0x68656c6c6f20776f726c64"],"id":1}'
```

Run command

### TxPool

#### txpool\_content

Returns a list with the exact details of all the transactions currently pending for inclusion in the next block(s), as well as the ones that are being scheduled for future execution only.

***

_**Parameters:**_

None

_**Example:**_

Run the command and see live results from our testnet.

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"txpool_content","params":[],"id":1}'
```

Run command

txpool\_inspect

Returns a list with a textual summary of all the transactions currently pending for inclusion in the next block(s), as well as the ones that are being scheduled for future execution only. This is a method specifically tailored to developers to quickly see the transactions in the pool and find any potential issues.

***

_**Parameters:**_

None

_**Example:**_

Run the command and see live results from our testnet.

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"txpool_inspect","params":[],"id":1}'
```

Run command

#### txpool\_status

Returns the number of transactions currently pending for inclusion in the next block(s), as well as the ones that are being scheduled for future execution only.

***

_**Parameters:**_

None

_**Example:**_

Run the command and see live results from our testnet.

```
curl  https://rpc.poa.psdk.io:8545 -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"txpool_status","params":[],"id":1}'
```

Run command
