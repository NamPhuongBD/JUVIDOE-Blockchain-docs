# Local Setup



{% hint style="danger" %}
**THIS GUIDE IS FOR TESTING PURPOSES ONLY**

The below guide will instruct you on how to set up a Z Edge network on your local machine for testing and development purposes.

The procedure differs greatly from the way you would want to set up Z Edge network for a real use scenario on a cloud provider:[ Cloud Setup](cloud-setup.md)
{% endhint %}

### Requirements[​](https://polygon-edge-v063.evmbuilder.com/docs/get-started/set-up-ibft-locally#requirements) <a href="#requirements" id="requirements"></a>

Refer to [Installation](https://polygon-edge-v063.evmbuilder.com/docs/get-started/installation) to install JUVIDOE Edge.

### Overview[​](https://polygon-edge-v063.evmbuilder.com/docs/get-started/set-up-ibft-locally#overview) <a href="#overview" id="overview"></a>

![Local Setup](https://polygon-edge-v063.evmbuilder.com/assets/images/local-ee63da94702b8a5a77350848f8b64221.svg)

In this guide, our goal is to establish a working `JUVIDOE-edge` blockchain network working with [IBFT consensus protocol](https://github.com/ethereum/EIPs/issues/650). The blockchain network will consist of 4 nodes of whom all 4 are validator nodes, and as such are eligible for both proposing block, and validating blocks that came from other proposers. All 4 nodes will run on the same machine, as the idea of this guide is to give you a fully functional IBFT cluster in the least amount of time.

To achieve that, we will guide you through 4 easy steps:

1. Initializing data directories will generate both the validator keys for each of the 4 nodes, and initialize empty blockchain data directories. The validator keys are important as we need to bootstrap the genesis block with the initial set of validators using these keys.
2. Preparing the connection string for the bootnode will be the vital information for every node we will run as to which node to connect to when starting for the first time.
3. Generating the `genesis.json` file will require as input both the validator keys generated in **step 1** used for setting the initial validators of the network in the genesis block and the bootnode connection string from **step 2**.
4. Running all the nodes is the end goal of this guide and will be the last step we do, we will instruct the nodes which data directory to use and where to find the `genesis.json` which bootstraps the initial network state.

As all four nodes will be running on localhost, during the setup process it is expected that all the data directories for each of the nodes are in the same parent directory.

{% hint style="warning" %}
**NUMBER OF VALIDATORS**

There is no minimum to the number of nodes in a cluster, which means clusters with only 1 validator node are possible. Keep in mind that with a _single_ node cluster, there is **no crash tolerance** and **no BFT guarantee**.

The minimum recommended number of nodes for achieving a BFT guarantee is 4 - since in a 4 node cluster, the failure of 1 node can be tolerated, with the remaining 3 functioning normally.
{% endhint %}

### Step 1: Initialize data folders for IBFT and generate validator keys[​](https://polygon-edge-v063.evmbuilder.com/docs/get-started/set-up-ibft-locally#step-1-initialize-data-folders-for-ibft-and-generate-validator-keys) <a href="#step-1-initialize-data-folders-for-ibft-and-generate-validator-keys" id="step-1-initialize-data-folders-for-ibft-and-generate-validator-keys"></a>

In order to get up and running with IBFT, you need to initialize the data folders, one for each node:

```
JUVIDOE-edge secrets init --data-dir test-chain-1
```

```
JUVIDOE-edge secrets init --data-dir test-chain-2
```

```
JUVIDOE-edge secrets init --data-dir test-chain-3
```

```
JUVIDOE-edge secrets init --data-dir test-chain-4
```

Each of these commands will print the validator key and the [node ID](https://docs.libp2p.io/concepts/peer-id/). You will need the Node ID of the first node for the next step.

### Step 2: Prepare the multiaddr connection string for the bootnode[​](https://polygon-edge-v063.evmbuilder.com/docs/get-started/set-up-ibft-locally#step-2-prepare-the-multiaddr-connection-string-for-the-bootnode) <a href="#step-2-prepare-the-multiaddr-connection-string-for-the-bootnode" id="step-2-prepare-the-multiaddr-connection-string-for-the-bootnode"></a>

For a node to successfully establish connectivity, it must know which `bootnode` server to connect to in order to gain information about all the remaining nodes on the network. The `bootnode` is sometimes also known as the `rendezvous` server in p2p jargon.

`bootnode` is not a special instance of the JUVIDOE-edge node. Every JUVIDOE-edge node can serve as a `bootnode`, but every JUVIDOE-edge node needs to have a set of bootnodes specified which will be contacted to provide information on how to connect with all remaining nodes in the network.

To create the connection string for specifying the bootnode, we will need to conform to the [multiaddr format](https://docs.libp2p.io/concepts/addressing/):

```
/ip4/<ip_address>/tcp/<port>/p2p/<node_id>
```

In this guide, we will treat the first and second nodes as the bootnodes for all other nodes. What will happen in this scenario is that nodes that connect to the `node 1` or `node 2` will get information on how to connect to one another through the mutually contacted bootnode.

{% hint style="warning" %}
**YOU NEED TO SPECIFY AT LEAST ONE BOOTNODE TO START A NODE**

At least **one** bootnode is required, so other nodes in the network can discover each other. More bootnodes are recommended, as they provide resilience to the network in case of outages. In this guide we will list two nodes, but this can be changed on the fly, with no impact on the validity of the `genesis.json` file.
{% endhint %}

Since we are running on localhost, it is safe to assume that the `<ip_address>` is `127.0.0.1`.

For the `<port>` we will use `10001` since we will configure the libp2p server for `node 1` to listen on this port later.

And lastly, we need the `<node_id>` which we can get from the output of the previously ran command `JUVIDOE-edge secrets init --data-dir test-chain-1` command (which was used to generate keys and data directories for the `node1`)

After the assembly, the multiaddr connection string to the `node 1` which we will use as the bootnode will look something like this (only the `<node_id>` which is at the end should be different):

```
/ip4/127.0.0.1/tcp/10001/p2p/16Uiu2HAmJxxH1tScDX2rLGSU9exnuvZKNM9SoK3v315azp68DLPW
```

Similarly, we construct the multiaddr for second bootnode as shown below

```
/ip4/127.0.0.1/tcp/20001/p2p/16Uiu2HAmS9Nq4QAaEiogE4ieJFUYsoH28magT7wSvJPpfUGBj3Hq 
```

### Step 3: Generate the genesis file with the 4 nodes as validators[​](https://polygon-edge-v063.evmbuilder.com/docs/get-started/set-up-ibft-locally#step-3-generate-the-genesis-file-with-the-4-nodes-as-validators) <a href="#step-3-generate-the-genesis-file-with-the-4-nodes-as-validators" id="step-3-generate-the-genesis-file-with-the-4-nodes-as-validators"></a>

```
JUVIDOE-edge genesis --consensus ibft --ibft-validators-prefix-path test-chain- --bootnode /ip4/127.0.0.1/tcp/10001/p2p/16Uiu2HAmJxxH1tScDX2rLGSU9exnuvZKNM9SoK3v315azp68DLPW --bootnode /ip4/127.0.0.1/tcp/20001/p2p/16Uiu2HAmS9Nq4QAaEiogE4ieJFUYsoH28magT7wSvJPpfUGBj3Hq 
```

What this command does:

* The `--ibft-validators-prefix-path` sets the prefix folder path to the one specified which IBFT in Z Edge can use. This directory is used to house the `consensus/` folder, where the validator's private key is kept. The validator's public key is needed in order to build the genesis file - the initial list of bootstrap nodes. This flag only makes sense when setting up the network on localhost, as in a real-world scenario we cannot expect all the nodes' data directories to be on the same filesystem from where we can easily read their public keys.
* The `--bootnode` sets the address of the bootnode that will enable the nodes to find each other. We will use the multiaddr string of the `node 1`, as mentioned in **step 2**.

The result of this command is the `genesis.json` file which contains the genesis block of our new blockchain, with the predefined validator set and the configuration for which node to contact first in order to establish connectivity.

{% hint style="warning" %}
**PREMINING ACCOUNT BALANCES**

You will probably want to set up your blockchain network with some addresses having "premined" balances.

To achieve this, pass as many `--premine` flags as you want per address that you want to be initialized with a certain balance on the blockchain.

For example, if we would like to premine 1000 ETH to address `0x3956E90e632AEbBF34DEB49b71c28A83Bc029862` in our genesis block, then we would need to supply the following argument:

```
--premine=0x3956E90e632AEbBF34DEB49b71c28A83Bc029862:1000000000000000000000
```

**Note that the premined amount is in WEI, not ETH.**
{% endhint %}

{% hint style="warning" %}
**SET THE BLOCK GAS LIMIT**

The default gas limit for each block is `5242880`. This value is written in the genesis file, but you may want to increase / decrease it.

command/helper/helper.go

```
const (
    GenesisFileName       = "./genesis.json"
    DefaultChainName      = "example"
    DefaultChainID        = 100
    DefaultPremineBalance = "0x3635C9ADC5DEA00000"
    DefaultConsensus      = "pow"
    GenesisGasUsed        = 458752
    GenesisGasLimit       = 5242880 // The default block gas limit
)
```

To do so, you can use the flag `--block-gas-limit` followed by the desired value as shown below :

```
--block-gas-limit 1000000000
```
{% endhint %}

{% hint style="warning" %}


**SET SYSTEM FILE DESCRIPTOR LIMIT**

The default file descriptor limit ( maximum number of open files ) on some operating systems is pretty small. If the nodes are expected to have high throughput, you might consider increasing this limit on the OS level.

For Ubuntu distro the procedure is as follows ( if you're not using Ubuntu/Debian distro, check the official docs for your OS ) :

* Check current os limits ( open files )

ulimit -a

```
ubuntu@ubuntu:~$ ulimit -a
core file size          (blocks, -c) 0
data seg size           (kbytes, -d) unlimited
scheduling priority             (-e) 0
file size               (blocks, -f) unlimited
pending signals                 (-i) 15391
max locked memory       (kbytes, -l) 65536
max memory size         (kbytes, -m) unlimited
open files                      (-n) 1024
pipe size            (512 bytes, -p) 8
POSIX message queues     (bytes, -q) 819200
real-time priority              (-r) 0
stack size              (kbytes, -s) 8192
cpu time               (seconds, -t) unlimited
max user processes              (-u) 15391
virtual memory          (kbytes, -v) unlimited
file locks                      (-x) unlimited
```

*   Increase open files limit

    * Localy - affects only current session:

    ```
    ulimit -u 65535
    ```

    * Globaly or per user ( add limits at the end of /etc/security/limits.conf file ) :

    ```
    sudo vi /etc/security/limits.conf  # we use vi, but you can use your favorite text editor
    ```

    /etc/security/limits.conf

    ```
    # /etc/security/limits.conf
    #
    #Each line describes a limit for a user in the form:
    #
    #<domain>        <type>  <item>  <value>
    #
    #Where:
    #<domain> can be:
    #        - a user name
    #        - a group name, with @group syntax
    #        - the wildcard *, for default entry
    #        - the wildcard %, can be also used with %group syntax,
    #                 for maxlogin limit
    #        - NOTE: group and wildcard limits are not applied to root.
    #          To apply a limit to the root user, <domain> must be
    #          the literal username root.
    #
    #<type> can have the two values:
    #        - "soft" for enforcing the soft limits
    #        - "hard" for enforcing hard limits
    #
    #<item> can be one of the following:
    #        - core - limits the core file size (KB)
    #        - data - max data size (KB)
    #        - fsize - maximum filesize (KB)
    #        - memlock - max locked-in-memory address space (KB)
    #        - nofile - max number of open file descriptors
    #        - rss - max resident set size (KB)
    #        - stack - max stack size (KB)
    #        - cpu - max CPU time (MIN)
    #        - nproc - max number of processes
    #        - as - address space limit (KB)
    #        - maxlogins - max number of logins for this user

    #        - maxsyslogins - max number of logins on the system
    #        - priority - the priority to run user process with
    #        - locks - max number of file locks the user can hold
    #        - sigpending - max number of pending signals
    #        - msgqueue - max memory used by POSIX message queues (bytes)
    #        - nice - max nice priority allowed to raise to values: [-20, 19]
    #        - rtprio - max realtime priority
    #        - chroot - change root to directory (Debian-specific)
    #
    #<domain>      <type>  <item>         <value>
    #

    #*               soft    core            0
    #root            hard    core            100000
    #*               hard    rss             10000
    #@student        hard    nproc           20
    #@faculty        soft    nproc           20
    #@faculty        hard    nproc           50
    #ftp             hard    nproc           0
    #ftp             -       chroot          /ftp
    #@student        -       maxlogins       4

    *               soft    nofile          65535
    *               hard    nofile          65535

    # End of file
    ```

    Optionaly, modify additional parameters, save the file and restart the system. After restart check file descriptor limit again. It should be set to the value you defined in limits.conf file.
{% endhint %}

### Step 4: Run all the clients[​](https://polygon-edge-v063.evmbuilder.com/docs/get-started/set-up-ibft-locally#step-4-run-all-the-clients) <a href="#step-4-run-all-the-clients" id="step-4-run-all-the-clients"></a>

Because we are attempting to run a JUVIDOE Edge network consisting of 4 nodes all on the same machine, we need to take care to avoid port conflicts. This is why we will use the following reasoning for determining the listening ports of each server of a node:

* `10000` for the gRPC server of `node 1`, `20000` for the GRPC server of `node 2`, etc.
* `10001` for the libp2p server of `node 1`, `20001` for the libp2p server of `node 2`, etc.
* `10002` for the JSON-RPC server of `node 1`, `20002` for the JSON-RPC server of `node 2`, etc.

To run the **first** client (note the port `10001` since it was used as a part of the libp2p multiaddr in **step 2** alongside node 1's Node ID):

```
JUVIDOE-edge server --data-dir ./test-chain-1 --chain genesis.json --grpc-address :10000 --libp2p :10001 --jsonrpc :10002 --seal
```

To run the **second** client:

```
JUVIDOE-edge server --data-dir ./test-chain-2 --chain genesis.json --grpc-address :20000 --libp2p :20001 --jsonrpc :20002 --seal
```

To run the **third** client:

```
JUVIDOE-edge server --data-dir ./test-chain-3 --chain genesis.json --grpc-address :30000 --libp2p :30001 --jsonrpc :30002 --seal
```

To run the **fourth** client:

```
JUVIDOE-edge server --data-dir ./test-chain-4 --chain genesis.json --grpc-address :40000 --libp2p :40001 --jsonrpc :40002 --seal
```

To briefly go over what has been done so far:

* The directory for the client data has been specified to be **./test-chain-\***
* The GRPC servers have been started on ports **10000**, **20000**, **30000** and **40000**, for each node respectively
* The libp2p servers have been started on ports **10001**, **20001**, **30001** and **40001**, for each node respectively
* The JSON-RPC servers have been started on ports **10002**, **20002**, **30002** and **40002**, for each node respectively
* The _seal_ flag means that the node which is being started is going to participate in block sealing
* The _chain_ flag specifies which genesis file should be used for chain configuration

The structure of the genesis file is covered in the [CLI Commands](https://polygon-edge-v063.evmbuilder.com/docs/get-started/cli-commands) section.

After running the previous commands, you have set up a 4 node JUVIDOE Edge network, capable of sealing blocks and recovering from node failure.

{% hint style="warning" %}
**START THE CLIENT USING CONFIG FILE**

Instead of specifying all configuration parameters as CLI arguments, the Client can also be started using a config file by executing the following command:

```
JUVIDOE-edge server --config <config_file_path>
```

Example:

```
JUVIDOE-edge server --config ./test/config-node1.json
```

Currently, we only support `json` based configuration file, sample config file can be found [here](https://polygon-edge-v063.evmbuilder.com/docs/configuration/sample-config)
{% endhint %}

{% hint style="warning" %}
**STEPS TO RUN A NON-VALIDATOR NODE**

A Non-validator will always sync the latest blocks received from the validator node, you can start a non-validator node by running the following command.

```
JUVIDOE-edge server --data-dir <directory_path> --chain <genesis_filename> --grpc-address <portNo> --libp2p <portNo> --jsonrpc <portNo>
```

For example, you can add **fifth** Non-validator client by executing the following command :

```
JUVIDOE-edge server --data-dir ./test-chain --chain genesis.json --grpc-address :50000 --libp2p :50001 --jsonrpc :50002 

```
{% endhint %}

{% hint style="warning" %}
**SPECIFY THE PRICE LIMIT**

A JUVIDOE Edge node can be started with a set **price limit** for incoming transactions.

The unit for the price limit is `wei`.

Setting a price limit means that any transaction processed by the current node will need to have a gas price **higher** then the set price limit, otherwise it will not be included in a block.

Having the majority of nodes respect a certain price limit enforces the rule that transactions in the network cannot be below a certain price threshold.

The default value for the price limit is `0`, meaning it is not enforced at all by default.

Example of using the `--price-limit` flag:

```
JUVIDOE-edge server --price-limit 100000 ...
```

It is worth noting that price limits **are enforced only on non-local transactions**, meaning that the price limit does not apply to transactions added locally on the node.
{% endhint %}

### Step 5: Interact with the JUVIDOE-edge network[​](https://polygon-edge-v063.evmbuilder.com/docs/get-started/set-up-ibft-locally#step-5-interact-with-the-polygon-edge-network) <a href="#step-5-interact-with-the-polygon-edge-network" id="step-5-interact-with-the-polygon-edge-network"></a>

Now that you've set up at least 1 running client, you can go ahead and interact with the blockchain using the account you premined above and by specifying the JSON-RPC URL to any of the 4 nodes:

* Node 1: `http://localhost:10002`
* Node 2: `http://localhost:20002`
* Node 3: `http://localhost:30002`
* Node 4: `http://localhost:40002`

Follow this guide to issue operator commands to the newly built cluster: [How to query operator information](https://polygon-edge-v063.evmbuilder.com/docs/working-with-node/query-operator-info) (the GRPC ports for the cluster we have built are `10000`/`20000`/`30000`/`40000` for each node respectively)
