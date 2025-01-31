# EIP-0003: Deterministic Wallet Standard

> 🔗 From [EIP-0003](https://github.com/ergoplatform/eips/blob/master/eip-0003.md)

Motivation
----------

[BIP-0044](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki) defines a logical hierarchy for deterministic wallets. This is a common standard that is used directly (or used as inspiration) by countless projects in the cryptocurrency sphere.

Such a standard allows end users to move between different wallet software trivially, and thus sets down a framework for a more cohesive ecosystem to grow.

The standard has 5 levels part of its path:

```
m / 44' / coin_type' / account' / change / address_index
```

This EIP attempts to define a specific `coin_type` for the Ergo ecosystem, as well as a policy for how wallets use the `change` level.


Coin Type
--------

Registered **coin_type**s can be found in [SLIP-0044](https://github.com/satoshilabs/slips/blob/master/slip-0044.md)

We will be using the word **ergo** summed based on the numerical values of the ASCII characters for the **coin_type**. As shown below, this means that our **coin_type** is `429`.

``
101 + 114 + 103 + 111 = 429
``

Thus our path will look as such:

```
m / 44' / 429' / account' / change / address_index
```

And the first default key pair for an Ergo wallet will be:

```
m / 44' / 429' / 0' / 0 / 0
```

Change
------
In BIP-44 the constant 0 is used for the external addresses and constant 1 for internal addresses (aka change addresses).

For EIP-3, we instead do not use constant 1 at all. Thus we do not support internal/change addresses, but only external addresses.

As such all wallets supporting EIP-3 should have any change within a transaction go back to the address using constant 0.

This decision was made to simplify the experience for end users and solidify a cohesive standard for wallets to target in the Ergo ecosystem. A full blown privacy-preserving mixer is already available within the ecosystem, ErgoMix, and thus the pseudo-anonymity provided by internal addresses is not particularly vital.

That said, in the future new wallets are more than welcome to create a new EIP for wallets which may wish to support internal addresses as well as an alternate standard (if valuable use cases arise).


Export and import of public keys
--------------------------------
For showing wallets in another wallet application as read-only wallets, it is possible to export the extended public key. This way, all addresses can be derived while signing is not possible. For this to work, the derived key on path m / 44' / 429' / 0' / 0 needs to be used for export and import.

The [BIP-0032](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki#Serialization_format) defines a serialization format for keys that we can use here to export and import the xpubkey.

Extended public keys are serialized as follows:

    4 byte: version bytes (mainnet: 0x0488B21E; testnet: 0x043587CF)
    1 byte: 4 (depth for our path m/44'/429'/0'/0)
    4 bytes: the fingerprint of the parent's key (or 0x00000000 can be used as we don't validate on import)
    4 bytes: 0x00000000 (child number)
    32 bytes: the chain code
    33 bytes: the public key key data
    
BIP-0032 leaves it open how this byte array should be encoded and suggests to use Base58 with a checksum. To not confuse Ergo xpubkeys with Bitcoin xpubkeys, we can use hex encoding instead.
