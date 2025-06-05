# Manage private keys

### Overview

The EVMBuilder Edge has two types of private keys that it directly manages:

* **Private key used for the consensus mechanism**
* **Private key used for networking by libp2p**

Currently, the EVMBuilder Edge doesn't offer support for direct account management.

Based on the directory structure outlined in the Backup & Restore guide, the EVMBuilder Edge stores these mentioned key files in two distinct directories - **consensus** and **keystore**.

### Key format

The private keys are stored in simple **Base64 format**, so they can be human-readable and portable.

```
# Example private key
0802122068a1bdb1c8af5333e58fe586bc0e9fc7aff882da82affb678aef5d9a2b9100c0
```

{% hint style="warning" %}
**KEY TYPE**

All private key files generated and used inside the EVMBuilder Edge are relying on ECDSA with the curve [secp256k1](https://en.bitcoin.it/wiki/Secp256k1).

As the curve is non-standard, it cannot be encoded and stored in any standardized PEM format. Importing keys that don't conform to this key type is not supported.
{% endhint %}

### Consensus Private Key

The private key file mentioned as the _consensus private key_ is also referred to as the **validator private key**. This private key is used when the node is acting as a validator in the network and needs to sign new data.

The private key file is located in `consensus/validator.key`, and adheres to the key format mentioned.

### Networking Private Key

The private key file mentioned for networking is used by libp2p to generate the corresponding PeerID, and allow the node to participate in the network.

It is located in `keystore/libp2p.key`, and adheres to the key format mentioned.

### Import / Export

As the key files are stored in simple Base64 on disk, they can be easily backed up or imported.

{% hint style="danger" %}
**CHANGING THE KEY FILES**

Any kind of change made to the key files on an already set up / running network can lead to serious network/consensus disruption, since the consensus and peer discovery mechanisms store the data derived from these keys in node-specific storage, and rely on this data to initiate connections and perform consensus logic
{% endhint %}
