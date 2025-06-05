# CLI Commands

This section details the present commands, command flags in the EVMBuilder Edge, and how they're used.

{% hint style="success" %}
**JSON OUTPUT SUPPORT**

The `--json` flag is supported on some commands. This flag instructs the command to print the output in JSON format
{% endhint %}

### Startup Commands

| **Command** | **Description**                                                                                                                                                 |
| ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| server      | The default command that starts the blockchain client, by bootstrapping all modules together                                                                    |
| genesis     | Generates a _genesis.json_ file, which is used to set a predefined chain state before starting the client. The structure of the genesis file is described below |

#### server flags

_**seal**_

{% tabs %}
{% tab title="Syntax" %}
`server [--seal SHOULD_SEAL]`
{% endtab %}

{% tab title="Example" %}
server --seal
{% endtab %}
{% endtabs %}

Sets the flag indicating that the client should seal blocks. Default: `true`.

***

_**data-dir**_

{% tabs %}
{% tab title="Syntax" %}
server \[--data-dir DATA\_DIRECTORY]
{% endtab %}

{% tab title="Example" %}
server --data-dir ./example-dir
{% endtab %}
{% endtabs %}

Used to specify the data directory used for storing EVMBuilder Edge client data. Default: `./test-chain`.

***

_**jsonrpc**_

{% tabs %}
{% tab title="Syntax" %}
server \[--jsonrpc JSONRPC\_ADDRESS]
{% endtab %}

{% tab title="Example" %}
server --jsonrpc 127.0.0.1:10000server \[--jsonrpc JSONRPC\_ADDRESS]server \[--jsonrpc JSONRPC\_ADDRESS]
{% endtab %}
{% endtabs %}

Sets the address and port for the JSON-RPC service `address:port`.\
If only port is defined `:10001` it will bind to all interfaces `0.0.0.0:10001`.\
If omitted the service will bind to the default `address:port`.\
Default address: `0.0.0.0:8545`.

***

_**grpc**_

{% tabs %}
{% tab title="Syntax" %}
server \[--grpc-address GRPC\_ADDRESS]
{% endtab %}

{% tab title="Example" %}
server --grpc-address 127.0.0.1:10001
{% endtab %}
{% endtabs %}

Sets the address and port for the gRPC service `address:port`. Default address: `127.0.0.1:9632`.

***

_**libp2p**_

{% tabs %}
{% tab title="Syntax" %}
server \[--libp2p LIBP2P\_ADDRESS]
{% endtab %}

{% tab title="Example" %}
server --libp2p 127.0.0.1:10002
{% endtab %}
{% endtabs %}

Sets the address and port for the libp2p service `address:port`. Default address: `127.0.0.1:1478`.

***

_**prometheus**_

{% tabs %}
{% tab title="Syntax" %}
server \[--prometheus PROMETHEUS\_ADDRESS]
{% endtab %}

{% tab title="Example" %}
server --prometheus 127.0.0.1:10004
{% endtab %}
{% endtabs %}

Sets the address and port for the prometheus server `address:port`.\
If only port is defined `:5001` the service will bind to all interfaces `0.0.0.0:5001`.\
If omitted the service will not be started.

***

_**block-gas-target**_

{% tabs %}
{% tab title="Syntax" %}
server \[--block-gas-target BLOCK\_GAS\_TARGET]
{% endtab %}

{% tab title=" Example" %}
server --block-gas-target 10000000
{% endtab %}
{% endtabs %}

Sets the target block gas limit for the chain. Default (not enforced): `0`.

A more detailed explanation on the block gas target can be found in the [TxPool section](../architecture/modules/txpool.md).

***

_**max-peers**_

{% tabs %}
{% tab title="Syntax" %}
server \[--max-peers PEER\_COUNT]
{% endtab %}

{% tab title="Example" %}
server --max-peers 40
{% endtab %}
{% endtabs %}

Sets the client's maximum peer count. Default: `40`.

Peer limit should be specified either by using `max-peers` or `max-inbound/outbound-peers` flag.

***

_**max-inbound-peers**_

{% tabs %}
{% tab title="Syntax" %}
server \[--max-inbound-peers PEER\_COUNT]
{% endtab %}

{% tab title="Example" %}
server --max-inbound-peers 32
{% endtab %}
{% endtabs %}

Sets the client's maximum inbound peer count. If `max-peers` is set, max-inbound-peer limit is calculated using the following formulae.

`max-inbound-peer = InboundRatio * max-peers`, where `InboundRatio` is `0.8`.

***

_**max-outbound-peers**_

{% tabs %}
{% tab title="Syntax" %}
server \[--max-outbound-peers PEER\_COUNT]
{% endtab %}

{% tab title="Example" %}
server --max-outbound-peers 8
{% endtab %}
{% endtabs %}

Sets the client's maximum outbound peer count. If `max-peers` is set, max-outbound-peer count is calculated using the following formulae.

`max-outbound-peer = OutboundRatio * max-peers`, where `OutboundRatio` is `0.2`.

***

_**log-level**_

{% tabs %}
{% tab title="Syntax" %}
server \[--log-level LOG\_LEVEL]
{% endtab %}

{% tab title=" Example" %}
server --log-level DEBUG
{% endtab %}
{% endtabs %}

Sets the log level for console output. Default: `INFO`.

***

_**log-to**_

{% tabs %}
{% tab title="Syntax" %}
server \[--log-to LOG\_FILE]
{% endtab %}

{% tab title="Example" %}
server --log-to node.log
{% endtab %}
{% endtabs %}

Defines log file name that will hold all log output from the server command. By default, all server logs will be outputted to console (stdout), but if the flag is set, there will be no output to the console when running server command.

***

_**chain**_

{% tabs %}
{% tab title="Syntax" %}
server \[--chain GENESIS\_FILE]
{% endtab %}

{% tab title="Example" %}
server --chain /home/ubuntu/genesis.json
{% endtab %}
{% endtabs %}

Specifies the genesis file used for starting the chain. Default: `./genesis.json`.

***

_**join**_

{% tabs %}
{% tab title="Syntax" %}
server \[--join JOIN\_ADDRESS]
{% endtab %}

{% tab title="Example" %}
server --join /ip4/127.0.0.1/tcp/10001/p2p/16Uiu2HAmJxxH1tScDX2rLGSU9exnuvZKNM9SoK3v315azp68DLPW
{% endtab %}
{% endtabs %}

Specifies the address of the peer that should be joined.

***

_**nat**_

{% tabs %}
{% tab title="Syntax" %}
server \[--nat NAT\_ADDRESS]
{% endtab %}

{% tab title="Example" %}
server --nat 192.0.2.1
{% endtab %}
{% endtabs %}

Sets the external IP address without the port, as it can be seen by peers.

***

_**dns**_

{% tabs %}
{% tab title="Syntax" %}
server \[--dns DNS\_ADDRESS]
{% endtab %}

{% tab title=" Example" %}


```
server --dns dns4/example.io
```

Copy\

{% endtab %}
{% endtabs %}

Sets the host DNS address. This can be used to advertise an external DNS. Supports `dns`,`dns4`,`dns6`.

***

_**price-limit**_

{% tabs %}
{% tab title="Syntax" %}
server \[--price-limit PRICE\_LIMIT]
{% endtab %}

{% tab title="Example" %}
server --price-limit 10000
{% endtab %}
{% endtabs %}

Sets minimum gas price limit to enforce for acceptance into the pool. Default: `1`.

***

_**max-slots**_

{% tabs %}
{% tab title="Syntax" %}
server \[--max-slots MAX\_SLOTS]
{% endtab %}

{% tab title="Example" %}
server --max-slots 1024
{% endtab %}
{% endtabs %}

Sets maximum slots in the pool. Default: `4096`.

***

_**config**_

{% tabs %}
{% tab title="Syntax" %}
server \[--config CLI\_CONFIG\_PATH]
{% endtab %}

{% tab title=" Example" %}
server --config ./myConfig.json
{% endtab %}
{% endtabs %}

Specifies the path to the CLI config. Supports `.json`.

***

_**secrets-config**_

{% tabs %}
{% tab title="Syntax" %}
server \[--secrets-config SECRETS\_CONFIG]
{% endtab %}

{% tab title="Second Tab" %}
server --secrets-config ./secretsManagerConfig.json
{% endtab %}
{% endtabs %}

Sets the path to the SecretsManager config file. Used for Hashicorp Vault, AWS SSM and GCP Secrets Manager. If omitted, the local FS secrets manager is used.

***

_**dev**_

{% tabs %}
{% tab title="Syntax" %}
server \[--dev DEV\_MODE]
{% endtab %}

{% tab title="Example" %}
server --dev
{% endtab %}
{% endtabs %}

Sets the client to dev mode. Default: `false`.

***

_**dev-interval**_

{% tabs %}
{% tab title="Syntax" %}
server \[--dev-interval DEV\_INTERVAL]
{% endtab %}

{% tab title="Example" %}
server --dev-interval 20
{% endtab %}
{% endtabs %}

Sets the client's dev notification interval in seconds. Default: `0`.

***

_**no-discover**_

{% tabs %}
{% tab title="Syntax" %}
server \[--no-discover NO\_DISCOVER]
{% endtab %}

{% tab title="Example" %}
server --no-discover
{% endtab %}
{% endtabs %}

Prevents the client from discovering other peers. Default: `false`.

***

_**restore**_

{% tabs %}
{% tab title="Syntax" %}
server \[--restore RESTORE]
{% endtab %}

{% tab title=" Example" %}
server --restore backup.dat
{% endtab %}
{% endtabs %}

Restore blocks from the specified archive file

***

_**block-time**_

{% tabs %}
{% tab title="Syntax" %}
server \[--block-time BLOCK\_TIME]
{% endtab %}

{% tab title="Example" %}
server --block-time 1000
{% endtab %}
{% endtabs %}

Sets block production time in seconds. Default: `2`

***

_**ibft-base-timeout**_

{% tabs %}
{% tab title="Syntax" %}
server \[--ibft-base-timeout IBFT\_BASE\_TIMEOUT]
{% endtab %}

{% tab title="Example" %}
server --ibft-base-timeout 10
{% endtab %}
{% endtabs %}

Sets the base value of timeout on IBFT consensus.\
IBFT consensus timeout is calculated by `BaseTimeout + 2^(round)`, or `BaseTimeout * 30` where round exceeds 8.\
It needs to be larger than block time and `BlockTime * 5` is set if it's not specified.

***

_**access-control-allow-origins**_

{% tabs %}
{% tab title="Syntax" %}
server \[--access-control-allow-origins ACCESS\_CONTROL\_ALLOW\_ORIGINS]
{% endtab %}

{% tab title="Example" %}
server --access-control-allow-origins
{% endtab %}
{% endtabs %}

Sets the authorized domains to be able to share responses from JSON-RPC requests.\
Add multiple flags `--access-control-allow-origins "https://example1.com" --access-control-allow-origins "https://example2.com"` to authorize multiple domains.\
If omitted Access-Control-Allow-Origins header will be set to `*` and all domains will be authorized.

***

#### genesis flags

_**dir**_

{% tabs %}
{% tab title="Syntax" %}
genesis \[--dir DIRECTORY]
{% endtab %}

{% tab title="Example" %}
genesis --dir ./genesis.json
{% endtab %}
{% endtabs %}

Sets the directory for the EVMBuilder Edge genesis data. Default: `./genesis.json`.

***

_**name**_

{% tabs %}
{% tab title="Syntax" %}
genesis \[--name NAME]
{% endtab %}

{% tab title="Example" %}
genesis --name test-chain
{% endtab %}
{% endtabs %}

Sets the name for the chain. Default: `polyton-edge`.

***

_**pos**_

{% tabs %}
{% tab title="Syntax" %}
genesis \[--pos IS\_POS]
{% endtab %}

{% tab title="Example" %}
genesis --pos
{% endtab %}
{% endtabs %}

Sets the flag indicating that the client should use Proof of Stake IBFT. Defaults to Proof of Authority if flag is not provided or `false`.

***

_**epoch-size**_

{% tabs %}
{% tab title="Syntax" %}
genesis \[--epoch-size EPOCH\_SIZE]
{% endtab %}

{% tab title="Example" %}
genesis --epoch-size 50
{% endtab %}
{% endtabs %}

Sets the epoch size for the chain. Default `100000`.

***

_**premine**_

{% tabs %}
{% tab title="Syntax" %}
genesis \[--premine ADDRESS:VALUE]
{% endtab %}

{% tab title="Example" %}
genesis --premine 0x3956E90e632AEbBF34DEB49b71c28A83Bc029862:1000000000000000000000
{% endtab %}
{% endtabs %}

Sets the premined accounts and balances in the format `address:amount`. The amount can be in either decimal or hex. Default premined balance: `0x3635C9ADC5DEA00000`.

***

_**chainid**_

{% tabs %}
{% tab title="Syntax" %}
genesis \[--chain-id CHAIN\_ID]
{% endtab %}

{% tab title="Example" %}
genesis --chain-id 200
{% endtab %}
{% endtabs %}

Sets the ID of the chain. Default: `100`.

***

_**ibft-validators-prefix-path**_

{% tabs %}
{% tab title="Syntax" %}
genesis \[--ibft-validators-prefix-path IBFT\_VALIDATORS\_PREFIX\_PATH]
{% endtab %}

{% tab title="Example" %}
genesis --ibft-validators-prefix-path test-chain-
{% endtab %}
{% endtabs %}

Prefix path for validator folder directory. Needs to be present if the flag `ibft-validator` is omitted.

***

_**ibft-validator**_

{% tabs %}
{% tab title="Syntax" %}
genesis \[--ibft-validator IBFT\_VALIDATOR\_LIST]
{% endtab %}

{% tab title="Example" %}
genesis --ibft-validator 0xC12bB5d97A35c6919aC77C709d55F6aa60436900
{% endtab %}
{% endtabs %}

Sets passed in addresses as IBFT validators. Needs to be present if the flag `ibft-validators-prefix-path` is omitted.

***

_**block-gas-limit**_

{% tabs %}
{% tab title="Syntax" %}
genesis \[--block-gas-limit BLOCK\_GAS\_LIMIT]
{% endtab %}

{% tab title="Example" %}
genesis --block-gas-limit 5000000
{% endtab %}
{% endtabs %}

Refers to the maximum amount of gas used by all operations in a block. Default: `5242880`.

***

_**consensus**_

{% tabs %}
{% tab title="Syntax" %}
genesis \[--consensus CONSENSUS\_PROTOCOL]
{% endtab %}

{% tab title="Example" %}
genesis --consensus ibft
{% endtab %}
{% endtabs %}

Sets consensus protocol. Default: `pow`.

***

_**bootnode**_

{% tabs %}
{% tab title="Syntax" %}
genesis \[--bootnode BOOTNODE\_URL]
{% endtab %}

{% tab title="Example" %}
genesis --bootnode /ip4/127.0.0.1/tcp/10001/p2p/16Uiu2HAmJxxH1tScDX2rLGSU9exnuvZKNM9SoK3v315azp68DLPW
{% endtab %}
{% endtabs %}

Multiaddr URL for p2p discovery bootstrap. This flag can be used multiple times. Instead of an IP address, the DNS address of the bootnode can be provided.

***

_**max-validator-count**_

{% tabs %}
{% tab title="Syntax" %}
genesis \[--max-validator-count MAX\_VALIDATOR\_COUNT]
{% endtab %}

{% tab title="Example" %}
genesis --max-validator-count 42
{% endtab %}
{% endtabs %}

The maximum number of stakers able to join the validator set in a PoS consensus. This number cannot exceed the value of MAX\_SAFE\_INTEGER (2^53 - 2).

***

_**min-validator-count**_

{% tabs %}
{% tab title="Syntax" %}
genesis \[--min-validator-count MIN\_VALIDATOR\_COUNT]
{% endtab %}

{% tab title="Example" %}
genesis --min-validator-count 4
{% endtab %}
{% endtabs %}

The minimum number of stakers needed to join the validator set in a PoS consensus. This number cannot exceed the value of max-validator-count. Defaults to 1.

***

### Operator Commands

#### Peer Commands

| **Command**  | **Description**                                                                     |
| ------------ | ----------------------------------------------------------------------------------- |
| peers add    | Adds a new peer using their libp2p address                                          |
| peers list   | Lists all the peers the client is connected to through libp2p                       |
| peers status | Returns the status of a specific peer from the peers list, using the libp2p address |

#### peers add flags

_**addr**_

{% tabs %}
{% tab title="Syntax" %}
peers add --addr PEER\_ADDRESS
{% endtab %}

{% tab title="Example" %}
peers add --addr /ip4/127.0.0.1/tcp/10001/p2p/16Uiu2HAmJxxH1tScDX2rLGSU9exnuvZKNM9SoK3v315azp68DLPW
{% endtab %}
{% endtabs %}

Peer's libp2p address in the multiaddr format.

***

_**grpc-address**_

{% tabs %}
{% tab title="Syntax" %}
peers add \[--grpc-address GRPC\_ADDRESS]
{% endtab %}

{% tab title="Example" %}
peers add --grpc-address 127.0.0.1:10003
{% endtab %}
{% endtabs %}

Address of the gRPC API. Default: `127.0.0.1:9632`.

#### peers list flags

_**grpc-address**_

{% tabs %}
{% tab title="Syntax" %}
peers list \[--grpc-address GRPC\_ADDRESS]
{% endtab %}

{% tab title="Example" %}
peers list --grpc-address 127.0.0.1:10003
{% endtab %}
{% endtabs %}

Address of the gRPC API. Default: `127.0.0.1:9632`.

#### peers status flags

_**peer-id**_

{% tabs %}
{% tab title="Syntax" %}
peers status --peer-id PEER\_ID
{% endtab %}

{% tab title="Example" %}
peers status --peer-id 16Uiu2HAmJxxH1tScDX2rLGSU9exnuvZKNM9SoK3v315azp68DLPW
{% endtab %}
{% endtabs %}

Libp2p node ID of a specific peer within p2p network.

***

_**grpc-address**_

{% tabs %}
{% tab title="Syntax" %}
peers status \[--grpc-address GRPC\_ADDRESS]
{% endtab %}

{% tab title="Example" %}
peers status --grpc-address 127.0.0.1:10003
{% endtab %}
{% endtabs %}

Address of the gRPC API. Default: `127.0.0.1:9632`.

#### IBFT Commands

| **Command**     | **Description**                                                                                       |
| --------------- | ----------------------------------------------------------------------------------------------------- |
| ibft snapshot   | Returns the IBFT snapshot                                                                             |
| ibft candidates | Queries the current set of proposed candidates, as well as candidates that have not been included yet |
| ibft propose    | Proposes a new candidate to be added/removed from the validator set                                   |
| ibft status     | Returns the overall status of the IBFT client                                                         |
| ibft switch     | Add fork configurations into genesis.json file to switch IBFT type                                    |

#### ibft snapshot flags

_**number**_

{% tabs %}
{% tab title="Syntax" %}
ibft snapshot \[--number BLOCK\_NUMBER]
{% endtab %}

{% tab title=" Example" %}
ibft snapshot --number 100
{% endtab %}
{% endtabs %}

The block height (number) for the snapshot.

***

_**grpc-address**_

{% tabs %}
{% tab title="Syntax" %}
ibft snapshot \[--grpc-address GRPC\_ADDRESS]
{% endtab %}

{% tab title="Example" %}
ibft snapshot --grpc-address 127.0.0.1:10003
{% endtab %}
{% endtabs %}

Address of the gRPC API. Default: `127.0.0.1:9632`.

#### ibft candidates flags

_**grpc-address**_

{% tabs %}
{% tab title="Syntax" %}
ibft candidates \[--grpc-address GRPC\_ADDRESS]
{% endtab %}

{% tab title="Example" %}
ibft candidates --grpc-address 127.0.0.1:10003
{% endtab %}
{% endtabs %}

Address of the gRPC API. Default: `127.0.0.1:9632`.

#### ibft propose flags

_**vote**_

{% tabs %}
{% tab title="Syntax" %}
ibft propose --vote VOTE
{% endtab %}

{% tab title="Example" %}
ibft propose --vote auth
{% endtab %}
{% endtabs %}

Proposes a change to the validator set. Possible values: `[auth, drop]`.

***

_**addr**_

{% tabs %}
{% tab title="Syntax" %}
ibft propose --addr ETH\_ADDRESS
{% endtab %}

{% tab title="Example" %}
ibft propose --addr 0x89205A3A3b2A69De6Dbf7f01ED13B2108B2c43e7
{% endtab %}
{% endtabs %}

Address of the account to be voted for.

***

_**grpc-address**_

{% tabs %}
{% tab title="Syntax" %}
peers add \[--grpc-address GRPC\_ADDRESS]
{% endtab %}

{% tab title="Example" %}
peers add --grpc-address 127.0.0.1:10003
{% endtab %}
{% endtabs %}

Address of the gRPC API. Default: `127.0.0.1:9632`.

#### ibft status flags

_**grpc-address**_

{% tabs %}
{% tab title="Syntax" %}
peers list \[--grpc-address GRPC\_ADDRESS]
{% endtab %}

{% tab title="Example" %}
ibft status --grpc-address 127.0.0.1:10003
{% endtab %}
{% endtabs %}

Address of the gRPC API. Default: `127.0.0.1:9632`.

#### ibft switch flags

_**chain**_

{% tabs %}
{% tab title="Syntax" %}
ibft switch \[--chain GENESIS\_FILE]
{% endtab %}

{% tab title="Example" %}
ibft switch --chain genesis.json
{% endtab %}
{% endtabs %}

Specifies the genesis file to update. Default: `test`.

***

_**type**_

{% tabs %}
{% tab title="Syntax" %}
ibft switch \[--type TYPE]
{% endtab %}

{% tab title="Example" %}
ibft switch --type PoS
{% endtab %}
{% endtabs %}

Specifies the IBFT type to switch. Possible values: `[PoS]`.

***

_**deployment**_

{% tabs %}
{% tab title="Syntax" %}
ibft switch \[--deployment DEPLOYMENT]
{% endtab %}

{% tab title=" Example" %}
ibft switch --deployment 100
{% endtab %}
{% endtabs %}

Specifies the height of contract deployment. Only available with PoS.

***

_**from**_

{% tabs %}
{% tab title="Syntax" %}
ibft switch \[--from FROM]
{% endtab %}

{% tab title="Example" %}
ibft switch --from 200
{% endtab %}
{% endtabs %}

***

_**max-validator-count**_

{% tabs %}
{% tab title="Syntax" %}
ibft switch \[--max-validator-count MAX\_VALIDATOR\_COUNT]
{% endtab %}

{% tab title=" Example" %}
ibft switch --max-validator-count 42
{% endtab %}
{% endtabs %}

The maximum number of stakers able to join the validator set in a PoS consensus. This number cannot exceed the value of MAX\_SAFE\_INTEGER (2^53 - 2).

***

_**min-validator-count**_

{% tabs %}
{% tab title="Syntax" %}
ibft switch \[--min-validator-count MIN\_VALIDATOR\_COUNT]
{% endtab %}

{% tab title="Example" %}
bft switch --min-validator-count 4
{% endtab %}
{% endtabs %}

The minimum number of stakers needed to join the validator set in a PoS consensus. This number cannot exceed the value of max-validator-count. Defaults to 1.

Specifies the beginning height of the fork.

#### Transaction Pool Commands

| **Command**      | **Description**                                |
| ---------------- | ---------------------------------------------- |
| txpool status    | Returns the number of transactions in the pool |
| txpool subscribe | Subscribes for events in the transaction pool  |

#### txpool status flags

_**grpc-address**_

{% tabs %}
{% tab title="Syntax" %}
txpool status \[--grpc-address GRPC\_ADDRESS]
{% endtab %}

{% tab title="Example" %}
txpool status --grpc-address 127.0.0.1:10003
{% endtab %}
{% endtabs %}

Address of the gRPC API. Default: `127.0.0.1:9632`.

#### txpool subscribe flags

_**grpc-address**_

{% tabs %}
{% tab title="Syntax" %}
txpool subscribe \[--grpc-address GRPC\_ADDRESS]
{% endtab %}

{% tab title="Example" %}
txpool subscribe --grpc-address 127.0.0.1:10003
{% endtab %}
{% endtabs %}

Address of the gRPC API. Default: `127.0.0.1:9632`.

***

_**promoted**_

{% tabs %}
{% tab title="Syntax" %}
txpool subscribe \[--promoted LISTEN\_PROMOTED]
{% endtab %}

{% tab title="Example" %}
txpool subscribe --promoted
{% endtab %}
{% endtabs %}

Subscribes for promoted tx events in the TxPool.

***

_**dropped**_

{% tabs %}
{% tab title="Syntax" %}
txpool subscribe \[--dropped LISTEN\_DROPPED]
{% endtab %}

{% tab title="Example" %}
txpool subscribe --dropped
{% endtab %}
{% endtabs %}

Subscribes for dropped tx events in the TxPool.

***

_**demoted**_

{% tabs %}
{% tab title="Syntax" %}
txpool subscribe \[--demoted LISTEN\_DEMOTED]
{% endtab %}

{% tab title="Example" %}
txpool subscribe --demoted
{% endtab %}
{% endtabs %}

Subscribes for demoted tx events in the TxPool.

***

_**added**_

{% tabs %}
{% tab title="Syntax" %}
txpool subscribe \[--added LISTEN\_ADDED]
{% endtab %}

{% tab title="Example" %}
txpool subscribe --added
{% endtab %}
{% endtabs %}

Subscribes for added tx events to the TxPool.

***

_**enqueued**_

{% tabs %}
{% tab title="Syntax" %}
txpool subscribe \[--enqueued LISTEN\_ENQUEUED]
{% endtab %}

{% tab title="Example" %}
txpool subscribe --enqueued
{% endtab %}
{% endtabs %}

Subscribes for enqueued tx events in the account queues.

***

#### Blockchain commands

| **Command** | **Description**                                                                   |
| ----------- | --------------------------------------------------------------------------------- |
| status      | Returns the status of the client. The detailed response can be found below        |
| monitor     | Subscribes to a blockchain event stream. The detailed response can be found below |
| version     | Returns the current version of the client                                         |

#### status flags

_**grpc-address**_

{% tabs %}
{% tab title="Syntax" %}
status \[--grpc-address GRPC\_ADDRESS]
{% endtab %}

{% tab title=" Example" %}
status --grpc-address 127.0.0.1:10003
{% endtab %}
{% endtabs %}

Address of the gRPC API. Default: `127.0.0.1:9632`.

#### monitor flags

_**grpc-address**_

{% tabs %}
{% tab title="Syntax" %}
monitor \[--grpc-address GRPC\_ADDRESS]
{% endtab %}

{% tab title="Example" %}
monitor --grpc-address 127.0.0.1:10003
{% endtab %}
{% endtabs %}

Address of the gRPC API. Default: `127.0.0.1:9632`.

***

### Secrets Commands

| **Command**      | **Description**                                                                       |
| ---------------- | ------------------------------------------------------------------------------------- |
| secrets init     | Initializes the private keys to the corresponding secrets manager                     |
| secrets generate | Generates a secrets manager configuration file which can be parsed by the EVMBuilder Edge |

#### secrets init flags

_**config**_

{% tabs %}
{% tab title="Syntax" %}
secrets init \[--config SECRETS\_CONFIG]
{% endtab %}

{% tab title="Example" %}
secrets init --config ./secretsManagerConfig.json
{% endtab %}
{% endtabs %}

Sets the path to the SecretsManager config file. Used for Hashicorp Vault. If omitted, the local FS secrets manager is used.

***

_**data-dir**_

{% tabs %}
{% tab title="Syntax" %}
secrets init \[--data-dir DATA\_DIRECTORY]
{% endtab %}

{% tab title="Example" %}
secrets init --data-dir ./example-dir
{% endtab %}
{% endtabs %}

Sets the directory for the EVMBuilder Edge data if the local FS is used.

#### secrets generate flags

_**dir**_

{% tabs %}
{% tab title="Syntax" %}
secrets generate \[--dir DATA\_DIRECTORY]
{% endtab %}

{% tab title="Example" %}
secrets generate --dir ./example-dir
{% endtab %}
{% endtabs %}

Sets the directory for the secrets manager configuration file Default: `./secretsManagerConfig.json`

***

_**type**_

{% tabs %}
{% tab title="Syntax" %}
secrets generate \[--type TYPE]
{% endtab %}

{% tab title="Example" %}
secrets generate --type hashicorp-vault
{% endtab %}
{% endtabs %}

Specifies the type of the secrets manager \[`hashicorp-vault`]. Default: `hashicorp-vault`

***

_**token**_

{% tabs %}
{% tab title="Syntax" %}
secrets generate \[--token TOKEN]
{% endtab %}

{% tab title="Example" %}
secrets generate --token s.zNrXa9zF9mgrdnClM7PZ19cu
{% endtab %}
{% endtabs %}

Specifies the access token for the service

***

_**server-url**_

{% tabs %}
{% tab title="Syntax" %}
secrets generate \[--server-url SERVER\_URL]
{% endtab %}

{% tab title="Example" %}
secrets generate --server-url http://127.0.0.1:8200
{% endtab %}
{% endtabs %}

Specifies the server URL for the service

***

_**name**_

{% tabs %}
{% tab title="Syntax" %}
secrets generate \[--name NODE\_NAME]
{% endtab %}

{% tab title="Example" %}
secrets generate --name node-1
{% endtab %}
{% endtabs %}

Specifies the name of the node for on-service record keeping. Default: `z-edge-node`

***

_**namespace**_

{% tabs %}
{% tab title="Syntax" %}
secrets generate \[--namespace NAMESPACE]
{% endtab %}

{% tab title="Example" %}
secrets generate --namespace my-namespace
{% endtab %}
{% endtabs %}

Specifies the namespace used for the Hashicorp Vault secrets manager. Default: `admin`

***

### Responses

#### Status Response

The response object is defined using Protocol Buffers.

minimal/proto/system.proto

```
message ServerStatus {
    int64 network = 1;

    string genesis = 2;

    Block current = 3;

    string p2pAddr = 4;

    message Block {
        int64 number = 1;
        string hash = 2;
    }
}
```

#### Monitor Response

minimal/proto/system.proto

```
message BlockchainEvent {
    // The "repeated" keyword indicates an array
    repeated Header added = 1;
    repeated Header removed = 2;

    message Header {
        int64 number = 1;
        string hash = 2;
    }
}
```

### Utilities

#### loadbot flags

_**tps**_

{% tabs %}
{% tab title="Syntax" %}
loadbot \[--tps NUMBER\_OF\_TXNS\_PER\_SECOND]
{% endtab %}

{% tab title=" Example" %}
loadbot --tps 2000
{% endtab %}
{% endtabs %}

The number of transactions per second to send. Default: `100`.

***

_**mode**_

{% tabs %}
{% tab title="Syntax" %}
loadbot \[--mode MODE]
{% endtab %}

{% tab title="Example" %}
loadbot --mode transfer
{% endtab %}
{% endtabs %}

Sets the loadbot run mode \[`transfer`, `deploy`]. Default: `transfer`.

***

_**chain-id**_

{% tabs %}
{% tab title="Syntax" %}
loadbot \[--chain-id CHAIN\_ID]
{% endtab %}

{% tab title="Example" %}
loadbot --chain-id 100
{% endtab %}
{% endtabs %}

Sets the network chain ID for transactions. Default: `100`.

***

_**gas-price**_

{% tabs %}
{% tab title="Syntax" %}
loadbot \[--gas-price GAS\_PRICE]
{% endtab %}

{% tab title="Example" %}
loadbot --gas-price 10000
{% endtab %}
{% endtabs %}

The gas price that should be used for the transactions. If omitted, the average gas price is fetched from the network.

***

_**gas-limit**_

{% tabs %}
{% tab title="Syntax" %}
loadbot \[--gas-limit GAS\_LIMIT]
{% endtab %}

{% tab title=" Example" %}
loadbot --gas-limit 10000
{% endtab %}
{% endtabs %}

The gas limit that should be used for the transactions. If omitted, the gas limit is estimated before starting the loadbot.

***

_**grpc-address**_

{% tabs %}
{% tab title="Syntax" %}
loadbot --grpc-address GRPC\_ADDRESS
{% endtab %}

{% tab title="Example" %}
loadbot --grpc-address 127.0.0.1:9645
{% endtab %}
{% endtabs %}

The GRPC endpoint used to send transactions

***

_**detailed**_

{% tabs %}
{% tab title="Syntax" %}
loadbot \[--detailed DETAILED]
{% endtab %}

{% tab title=" Example" %}
loadbot --detailed
{% endtab %}
{% endtabs %}

Flag indicating if the error logs should be shown. Default: `false`.

***

_**contract**_

{% tabs %}
{% tab title="Syntax" %}
loadbot \[--contract CONTRACT\_PATH]
{% endtab %}

{% tab title=" Example" %}
loadbot --contract ./myContract.json
{% endtab %}
{% endtabs %}

The path to the contract JSON artifact containing the bytecode. If omitted, a default contract is used.

***

_**sender**_

{% tabs %}
{% tab title="Syntax" %}
loadbot \[--sender ADDRESS]
{% endtab %}

{% tab title=" Example" %}
loadbot --sender 0x1010101010101010101010101010101010101020
{% endtab %}
{% endtabs %}

Address of the sender account.

***

_**receiver**_

{% tabs %}
{% tab title="Syntax" %}
loadbot \[--receiver ADDRESS]
{% endtab %}

{% tab title=" Example" %}
loadbot --receiver 0x1010101010101010101010101010101010101000
{% endtab %}
{% endtabs %}

Address of the receiver account.

***

_**jsonrpc**_

{% tabs %}
{% tab title="Syntax" %}
loadbot \[--jsonrpc ENDPOINT]
{% endtab %}

{% tab title="Example" %}
loadbot --jsonrpc http://127.0.0.1:8545
{% endtab %}
{% endtabs %}

A JSON RPC endpoint used to send transactions.

***

_**count**_

{% tabs %}
{% tab title="Syntax" %}
loadbot \[--count COUNT]
{% endtab %}

{% tab title="Example" %}
loadbot --count 100
{% endtab %}
{% endtabs %}

The total number of transactions to send. Default: `1000`.

***

_**value**_

{% tabs %}
{% tab title="Syntax" %}
loadbot \[--value VALUE]
{% endtab %}

{% tab title="Example" %}
loadbot --value 10000000000000000
{% endtab %}
{% endtabs %}

The value to send in each transaction.

***

_**max-conns**_

{% tabs %}
{% tab title="Syntax" %}
loadbot \[--max-conns MAX\_CONNECTIONS\_COUNT]
{% endtab %}

{% tab title="Example" %}
loadbot --max-conns 1000
{% endtab %}
{% endtabs %}

Sets the maximum no.of connections allowed per host. Default: `2*tps`.

***

#### backup flags
_**grpc-address**_

{% tabs %}
{% tab title="Syntax" %}
backup \[--grpc-address GRPC\_ADDRESS]
{% endtab %}

{% tab title="Example" %}
backup --grpc-address 127.0.0.1:9632
{% endtab %}
{% endtabs %}

Address of the gRPC API. Default: `127.0.0.1:9632`.

***

_**out**_

{% tabs %}
{% tab title="Syntax" %}
backup \[--out OUT]
{% endtab %}

{% tab title="Example" %}
backup --out backup.dat
{% endtab %}
{% endtabs %}

Path of archive file to save.

***

_**from**_

{% tabs %}
{% tab title="Syntax" %}
from \[--from FROM]
{% endtab %}

{% tab title="Example" %}
backup --from 0x0
{% endtab %}
{% endtabs %}

The beginning height of blocks in archive. Default: 0.

***

_**to**_

{% tabs %}
{% tab title="Syntax" %}
to \[--to TO]
{% endtab %}

{% tab title="Example" %}
backup --to 0x2710
{% endtab %}
{% endtabs %}

The end height of blocks in archive.

***

### Genesis Template

The genesis file should be used to set the initial state of the blockchain (ex. if some accounts should have a starting balance).

The following _./genesis.json_ file is generated:

```
{
    "name": "example",
    "genesis": {
        "nonce": "0x0000000000000000",
        "gasLimit": "0x0000000000001388",
        "difficulty": "0x0000000000000001",
        "mixHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
        "coinbase": "0x0000000000000000000000000000000000000000",
        "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000"
    },
    "params": {
        "forks": {},
        "chainID": 100,
        "engine": {
            "pow": {}
        }
    },
    "bootnodes": []
}
```

#### Data Directory

When executing the _data-dir_ flag, a **test-chain** folder is generated. The folder structure consists of the following sub-folders:

* **blockchain** - Stores the LevelDB for blockchain objects
* **trie** - Stores the LevelDB for the Merkle tries
* **keystore** - Stores private keys for the client. This includes the libp2p private key and the sealing/validator private key
* **consensus** - Stores any consensus information that the client might need while working

### Resources

* [**Protocol Buffers**](https://developers.google.com/protocol-buffers)
