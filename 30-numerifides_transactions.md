# Technical proposal
In order to secure a human readable authoritative “name” out of the possible
“namespaces”, a user constructs and signs a transaction from a previously unspent output
address funding a “numerifide” transaction with the below Script:

```
<blocks> OP_CHECKSEQUENCEVERIFY OP_DROP <C> OP_CHECKSIG
```

Where <blocks> is between 144 (1 day) and 52560 (1 year) and <C> is a hash of a contract constructed like so:

1.  Generate a secret private key p = random() and the public key P = p * G.
2.  Encode the Numerifides command (see below)
3.  Compute the pay-to-contract public key: C = P + h(P || command) * G.  This has corresponding private key c = p + h(P || command) that only the user knows.
4.  Generate a P2WSH to the script: <52560 blocks> OP_CHECKSEQUENCEVERIFY OP_DROP <C> OP_CHECKSIG
5.  Pay to that P2WSH on the Bitcoin network.
6.  Broadcast command, P, and the txid+outnum of the UTXO that pays to the P2WSH above, to the Numerifides network after some number of blocks

The "command" is a name->data mapping that also includes an additional area for a nonce.
