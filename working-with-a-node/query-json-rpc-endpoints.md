# Query JSON RPC endpoints

#### Overview[​](https://polygon-edge-v063.evmbuilder.com/docs/working-with-node/query-json-rpc#overview) <a href="#overview" id="overview"></a>

The JSON-RPC layer of the Z Smart Chain provides developers with the functionality of easily interacting with the blockchain, through HTTP requests.

This example covers using tools like **curl** to query information, as well as starting the chain with a premined account, and sending a transaction.

#### Step 1: Create a genesis file with a premined account[​](https://polygon-edge-v063.evmbuilder.com/docs/working-with-node/query-json-rpc#step-1-create-a-genesis-file-with-a-premined-account) <a href="#step-1-create-a-genesis-file-with-a-premined-account" id="step-1-create-a-genesis-file-with-a-premined-account"></a>

To generate a genesis file, run the following command:

```
z-edge genesis --premine 0x1010101010101010101010101010101010101010
```

The **premine** flag sets the address that should be included with a starting balance in the **genesis** file. In this case, the address `0x1010101010101010101010101010101010101010` will have a starting **default balance** of `0x3635C9ADC5DEA00000 wei`.

If we wanted to specify a balance, we can separate out the balance and address with a `:`, like so:

```
z-edge genesis --premine 0x1010101010101010101010101010101010101010:0x123123
```

The balance can be either a `hex` or `uint256` value.

{% hint style="danger" %}
**ONLY PREMINE ACCOUNTS FOR WHICH YOU HAVE A PRIVATE KEY!**

If you premine accounts and do not have a private key to access them, you premined balance will not be usable
{% endhint %}

#### Step 2: Start the Z Smart Chain in dev mode[​](https://polygon-edge-v063.evmbuilder.com/docs/working-with-node/query-json-rpc#step-2-start-the-polygon-edge-in-dev-mode) <a href="#step-2-start-the-polygon-edge-in-dev-mode" id="step-2-start-the-polygon-edge-in-dev-mode"></a>

To start the Z Smart Chain in development mode, which is explained in the [CLI Commands](../get-started/cli-commands.md) section, run the following:

```
z-edge server --chain genesis.json --dev --log-level debug
```

#### Step 3: Query the account balance[​](https://polygon-edge-v063.evmbuilder.com/docs/working-with-node/query-json-rpc#step-3-query-the-account-balance) <a href="#step-3-query-the-account-balance" id="step-3-query-the-account-balance"></a>

Now that the client is up and running in dev mode, using the genesis file generated in **step 1**, we can use a tool like **curl** to query the account balance:

```
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getBalance","params":["0x1010101010101010101010101010101010101010", "latest"],"id":1}' localhost:8545
```

The command should return the following output:

```
{
  "id":1,
  "result":"0x100000000000000000000000000"
}
```

#### Step 4: Send a transfer transaction[​](https://polygon-edge-v063.evmbuilder.com/docs/working-with-node/query-json-rpc#step-4-send-a-transfer-transaction) <a href="#step-4-send-a-transfer-transaction" id="step-4-send-a-transfer-transaction"></a>

Now that we've confirmed the account we set up as premined has the correct balance, we can transfer some ether:

```
var Web3 = require("web3");

const web3 = new Web3("<provider's websocket jsonrpc address>"); //example: ws://localhost:10002/ws
web3.eth.accounts
  .signTransaction(
    {
      to: "<recipient address>",
      value: web3.utils.toWei("<value in ETH>"),
      gas: 21000,
    },
    "<private key from premined account>"
  )
  .then((signedTxData) => {
    web3.eth
      .sendSignedTransaction(signedTxData.rawTransaction)
      .on("receipt", console.log);
  });
```
