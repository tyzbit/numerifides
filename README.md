# A Proposal for Proof of Authority Rooted on Decentralized Blockchains

# Foreward

Since the earliest conventions of early humans gathering into tribes, people have
put their trust in centralized authority.  Whether that authority is a seasoned
witchdoctor who is trained to spot illnesses and deliver healing, a Certificate
Authority organization that attests to the authenticity of their record, or a
government that derives its power from the will of the people—the fact remains
people delegate and revoke authority based on nebulous, inconsistent, and often
unfair and sometimes unjust rules.  Actors in an unjust system must exercise their
inherent power as components of the system to exit such a system as quickly as
possible so as not to be complacent in the system’s inherent injustice.  The
injustice of authority exercising power unevenly, or using its granted authority
in a way that harms the users of the system is the result of the underlying rules
governing how people delegate trust. It is said that justice is blind.  
Considering the rules inherent in our systems of justice, she must be, but we
need not trust the concept of justice to match its execution.

Rather than deriving justice and authority from a system that’s not supposed to
look but too often does, I propose a DECENTRALIZED CONSENSUS PROTOCOL that
enables a system of decentralized authority, whereby an user or actor can assert
identity, existence and authority on a public piece of data, on an open blockchain
and any independent, skeptical user or actor operating the consensus protocol
can verify any other actor’s statement of authority in a decentralized, fair and
privacy-protective manner.

I propose this system be called the Numerifides (capitalized) Trust Consensus
Protocol, or Numerifides (Nu-mer-ih-fih-dees) for short.  Transactions using this
system are to be called “numerifide(noun) transactions” (nu-mer-ih-fi’d) or
“numerifides" (lowercase) (nu-mer-ih-fi-dz) and trusted mappings to be referred
to as numerified(verb) numerifides(plural noun) or Numerifides transactions).
This is derived from the latin word numeris for number, and the Roman goddess
Fidēs, the goddess of trust and good faith.

# Outline

I propose a new transaction type, dubbed a “numerifide” transaction, compatible
with Bitcoin today that allows a transaction to claim authority in a
decentralized way over a given “name” and associates user-supplied data to it.
In this way, a human-meaningful “name” can be registered in a way that associates
with a “value” that provides some utility, such as (but not limited to):

* Associating a specific username to a Bitcoin address to provide cryptographic
proof of ownership of the username, receiving Bitcoin funds, or optionally using
the Bitcoin key to sign messages.

* Advertising a human recognizable domain name→onion address mapping.

* Authenticating an “alias” for an Lightning Network node→node pubkey

* DNS -> IP mappings

* Public keys for signing software

In addition, the user can alter this data in a secure, uncensorable way via
already existing mining mechanisms present in Bitcoin as well as incentive and
disincentive structures I will outline below. The incentives are structured
such that “namesquatting” valuable names is thought to be unfulfilling.
This system creates a fair and just way of reserving, updating, and confiscating
names, as well as letting names expire after the owner no longer wishes to claim them.

Due to the incentive structures, names should be secure, decentralized and human
meaningful<sup>[1](#ref1)</sup>.

# Terminology used:

* NUMERIFIDES: The decentralized consensus protocol of TRUST described here.

* NUMERIFIDE: A transaction following the consensus rules of Numerifides.

* NUMERIFIED: A piece of data that exists on NUMERIFIDES that is TRUSTED according to consensus rules.

* TRUST: The method whereby a general mapping of names to data formalized in a “numerifide” transaction can be independently verified to be UNDISPUTED.

* TRUSTED: A “numerified” “numerifide” Numerifides transaction.  A valid, trusted, name mapping.

* MUST, MAY, SHOULD, SHOULD NOT, MUST NOT: Used as defined in RFC-21192<sup>[2](#ref2)</sup>

* CONSENSUS: The method by which the decentralized Numerifides consensus protocol agrees to the state of Numerifides

* CSV: CheckSequenceVerify – an encumbrance on spending funds until a certain number of Bitcoin (measured in blocks in a blockchain) have passed.

* UPDATE: The process whereby a name→data mapping can be changed or RENEWED by the owner of the private key locking the funds. As with usual cryptocurrency transactions, the funds are fully spent

* RELEASE(D)/EXPIRE(D): A name that is no longer TRUSTED due to expiry of the encumbering CSV.

* LOCK(ED): Funds that are unspendable until AFTER a specific period of time has passed measured in Bitcoin blocks.

* BEFORE, AFTER/SUBSEQUENT: Time as perceived by the succession of blocks on Bitcoin

* VALID: A numerifide that follows all consensus rules

* USER/ACTOR/NODE: A participant in the Numerifides consensus protocol that independently verifies protocol rules are being followed.

* PROOF OF WORK/PoW: A method of evaluating a resulting hash to be able to prove a specific amount of work was done to produce the hash.

* PROOF OF HODLING/PoH: A locktime encumberance on spending the Bitcoin locked in a Numerifides registration transaction.

* HODL: A drunken misspelling of HOLD.

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

---

There will also be another output on the transaction, typically of only 1 satoshi
in value, which can have whatever encumberance the user wishes (though typically
it will be a normal P2WKH or P2WSH address.)

```
OP_HASH <hash> OP_EQUAL
```

The purpose of this is to allow updates to the record after it is committed.
The original funds are still locked up for the entirety of the CSV, but if the
data needs to be changed, a new Numerifides transaction with an input from this
address is allowed to change the registration on the original record.  The datatype
and the name registration MUST stay the same.

## Example Registration Command:
```
05:google.com:127.0.0.1:tb1qyftceqpc48r33584gpsqp2wdy344rsth9jm803:11111111111111111
```

#### Breakdown:

Field                                      | Explanation
-------------------------------------------|--------------------------------------------------
05                                         | Data type, (05 currently proposed to be DNS type)
google.com                                 | Name registration.
127.0.0.1                                  | Data for the name to map to
tb1qyftceqpc48r33584gpsqp2wdy344rsth9jm803 | Authorized update address
11111111111111111                          | Nonce


The nonce is incremented and many transactions are produced and signed until the
resulting TXID meets a minimum proof of work acceptable to the user, which is broadcast.
Since Proof of Work and Proof of Hodling are BOTH used to determine the level of TRUST, a user
registering a popular or contentious name should probably lock up significant funds
and ALSO "mine" their name out of the reach of anyone else.

---

## Updating Mappings

There will be many times that a record needs to be updated, for example if the
mapping becomes stale (DNS), or if the expiration of the original numerifide is
approaching and the user wishes to renew it early.

#### Registering the update

A new Numerifides transaction is created **with one of the inputs being the "authorized update address."**
This transaction is only allowed to update the original record for the original record type.
Any other scenario and the mapping will be considered UNTRUSTED.

This transaction will also provide an update address that is also authorized to
register new updates to the record.

### "Strengthening" Registrations

After initially creating a numerifide, a user may "strengthen" it (and keep the PoW
the same) simply by paying more Bitcoin to the same contract hash.

## Checking for duplicates

The nonce and the authorized address are NOT evaluated as part of the mapping when checking for duplicates.
For example, although the nonces are the same, the data is different and thus the mapping is different.

"05:google.com:127.0.0.1:tb1qy....:1111"

"05:google.co:127.0.0.1:tb1qy....:1111"

Only the data type and name are compared to determine if the mapping is a duplicate.

A user will broadcast the transaction, wait for it to be mined for a few blocks,
and then announce it and the mapping they registered later so that miners cannot
censor registrations.

# NUMERIFIDES RULES OF CONSENSUS

Numerifides mappings use the following formula to determine TRUST, with the winning
transaction being FULLY TRUSTED and any other transactions being UNTRUSTED (through
the user MAY be notified about the untrusted mappings outside of the protocol itself).

Each registration is evaluated only per each given data type.  A Bitcoin registration
of "Numerifides" is distinct from a GPG key registration of "Numerifides".

```
( ( T * P ) + ( T * B ) ) / N = TRUST
```

Where:
```
T = Timelock length (CheckSequenceVerify)
P = Proof of Work
B = Bitcoin locked up.
N = The number of previous unlinked occurrences of this name registration + 1
```

The name being registered can be any latin character, but MUST BE case-insensitive.

# TRUST LEVELS

A user that locks up 1BTC for 144 blocks and provides a Proof of Work of 2 would then
have a TRUST level of 432.

`( ( 144 * 2 ) + ( 144 * 1 ) ) / 1 = 432`

A user that wishes to "take over" the name (keeping the locktime the same),
but doesn't have as much Bitcoin must mine until a PoW of 5 and "unseat the name" with
any amount more than the amount initially locked :

`( ( 144 * 5 ) + ( 144 * 1.1 ) / 2 = 439.2`

In this way, names are secured primarily by locktime and Proof of Work, but secondarily
by amount of Bitcoin locked up.  Also, "takeovers" require more PoW/Bitcoin/PoH
than the initial investment. (By the way, to "unseat" the registration a third time would
require a PoW of 8, and any amount more than the initially locked Bitcoin (1)).

If the previous user wanted to secure their name with the same Proof of Work and
amount locked up, she simply could increase the locktime to the max of 1 year:

`( ( 52,560 * 2 ) + ( 52,560 * 1 ) / 1 = 157,680`

The previous user, if wishing to unseat this name would need to also increase the locktime
of their funds to 1 year, beat the Proof of Work and then lock up more Bitcoin (1).

`( ( 52,560 * 5 ) + ( 52,560 * >1 ) / 2 = 157,680+`

# Proposed Data Encoding Table

Mappings should be [datatype][name][separator][data].

( Separator is proposed to be 0xFF but others could be used )

Constant length 2+-byte data field | Proposed Data Standard                 | Separator | Description
-----------------------------------|----------------------------------------|-----------|-------------
00                                 | Private Usage                          | 0xFF      | The data associated with the name has no explicitly stated purpose. The data SHOULD NOT be used to verify any other consensus-approved data standard.
01                                 | Bitcoin Address                        | 0xFF      | The data associated with the name SHOULD BE used to TRUST that the Bitcoin address is associated to the given name.
02                                 | Lightning Node Public Key              | 0xFF      | The data associated with the name SHOULD BE used to TRUST an advertised ALIAS of a Lightning node.
03                                 | GPG Public Key                         | 0xFF      | The data associated with the name SHOULD BE used to TRUST a GPG Public Key
04                                 | Domain-validated Certificate           | 0xFF      | The data SHOULD BE a domain certificate for the specified name (ex: example.com)
05                                 | DNS mapping                            | 0xFF      | The data SHOULD BE a valid IP address.
06                                 | Tor mapping                            | 0xFF      | The data SHOULD BE an Tor onion address.
07                                 | Software Signing Key                   | 0xFF      | The data SHOULD BE a public key to verify signed software packages.
08-FF                              | Future use decided upon via consensus. | 0xFF      | Future use

# Implementations

Implementations of the Numerifides Trust Consensus Protocol will fall into two categories:
"Full" nodes and "Light" nodes.

## Full Nodes

A Full node will have all of the known mappings, and be able to perform lookups
locally.  Each full node will gossip about mappings to one another, and periodically
query one another to check consensus about mappings.  A full node should also
have a copy of the Bitcoin blockchain for maximum security, but it could be possible
to use a pruned backend node AFTER the initial sync if the user feels the level
of risk is acceptable.

If a mapping was originally censored, once an honest node sees it, it will broadcast
it to all nodes it knows about.  Honest nodes will see it as either the first
registration, or a more trusted registration (since it was confirmed before a possible
dishonest registration that was gossiped about) and will reorganize the
registrations for that name/data type accordingly.

Nodes will gossip a "consensus hash"<sup>[1](https://blockstack.org/whitepaper.pdf)</sup>
that is derived from every Numerifides registration. Each node will hash every Numerifides
registration it learns about per block sequentially in order of position in the
block.  This "Numerifides block hash" is then hashed together in sequence to
produce a Merkle branch.  These branches are then hashed together as assembled
until finally a consensus hash is produced for the highest known block.  With
the conensus hash derived from one's own calculation, a full node can know if
it agrees with consensus or not.

If the full node is not in consensus with spec, it can query a partner full node
and ask for its Numerifides Merkle tree.  With this tree, the local full node
can tell which block(s) it is missing registrations for, and request registrations
present in those blocks from the partner full node.  If consensus is broken becuase
the other node is missing data, the local node can pass the data along and "convert"
this node to our local node's view of consensus.

The full node spec is still largely unknown, but they may assign trust to their
peers much like Bitcoin nodes do (to guard against Sybil attacks), and punish
bad actors by refusing to propagate their updates.

## Light Nodes

A Light node will query multiple Full nodes for the name they want to look up,
along with the anchoring transaction and the consensus hash and then confirm via
an SPV lookup on the Bitcoin network that the related transactions are valid according
to consensus rules. Light nodes should query more than one Full node for a lookup,
and likewise query more than one Bitcoin node to confirm the anchoring Numerifides
transaction.

## Plugins

Plugins can be written to interface the client into any legacy lookup standard such as
creating a virtual Certificate Authority for the system that vouches for certificates
looked up via Numerifides, or for DNS lookups.

# Example Numerifides registration

User wishes to register the name:data mapping of "03:Numerifides:FF:[GPG key]".
User creates the appropriate transaction that:

* Pays back to themselves .001 BTC
* Locks the Bitcoin for a duration of 52,160 blocks (1 year)
* Has an appropriate Proof of Work advertised via the TXID hash
* Can be updated with a key they control

User broadcasts this transaction and it is included in a block.  User waits
6 blocks, and then broadcasts the mapping she just registered to the Numerifides
network registered.

The user was the first to broadcast this name, so any full or light node that does
a lookup for a GPG record for Numerifides should get this new record.

Since no other user is interested in registering this name, the Proof of Work
and Proof of Hodling is enough to secure the name, and if the user does nothing else,
the name becomes available for registration again after 52,160 blocks.

# Second example ("driveby" registration that is unseated)

A user wishes to "namesquat" a name, so they register "05:Google.com:FF:127.0.0.1" with
1BTC locked up and a Proof of Work of 2 locked up for 52,560 blocks.  In this example,
lets say it took 1 day of "mining" the transaction to produce that level of Proof of Work.

* T=52,560
* P=2
* B=1
* N=1

`( 52,560 * 2 ) + ( 52,560 * 1 ) / 1= 157,680`

Google themselves come along and wish to register the name, but see it is already
registered. Google happens to have a lot of Bitcoin, and has a lot of processing power
to "mine" a new transaction.  Google spends some time "mining" and finally transmits a
transaction with a PoW level of 4(2 days of computing), and Google locks up 10BTC, also for 1 year.

* T=52,560
* P=4
* B=10
* N=2

`( 52,560 * 4 ) + ( 52,560 * 10 ) / 2 = 367,920`

This handily beats the previous registration, which is still locked for the rest
of the duration of the locktime, thereby strongly discouraging registering mappings
one does not wish to use.

# Third example ("namesquatted" by a user with a lot of BTC)

A user with a large amount of BTC, not a lot of PoW that wishes to "namesquat" registers
popular usernames on Numerifides.  Let's assume they registered 10,000 names and
were able to commit 0.5BTC to each of the names with a Proof of Work of 1. Let's
assume the user only wished to squat the names for a week.

* T=1,008
* P=1
* B=0.5
* N=1

`( 1,008 * 1 ) + ( 1,008 * 0.5 ) / 1 = 1,512`

The rightful owner of the username wishes to unseat this name, but he doesn't even
have 0.5BTC.  This user only has 0.1BTC they can lock up to register the name.

The rightful owner only needs to beat the Proof of Work by 1 for the same locktime,
but the rightful owner would prefer the name to be usable for the longest amount of time,
so the rightful owner handily beats the namesquatter simply by committing their funds
for 1 year.  The rightful owner also recognizes this was a name with some value (because
it was "namesquatted") so he "mines" the transaction until a PoW of 5.

* T=52,560
* P=1
* B=0.1
* N=2

`( 52,560 * 1 ) + ( 52,560 * 0.1 ) / 2 = 28,908`

# Fourth example (someone with a lot of PoW "DoS"es names)

Lets take the user in the previous namesquatted example with 0.1BTC, and say a
"name miner" comes along and unseats the name for fun (or profit).  The "name miner"
can also commit 0.1BTC for one month (4,320 blocks).  Lets say the "name miner"
has a lot of power, and reaches a Proof of Work of 10:

* T=4,320
* P=10
* B=0.1
* N=1

`( 4,320 * 10 ) + ( 4,320 * 0.1 ) / 3 = 14,544`

The miner still cannot reach the same level as the previous user before, even though
the miner did exponentially more work because the miner can't afford to lock up
that many BTC for that long, and because the miner is the 3rd user to try to register
the name.

# Fifth example (two similar users want the same name)

Imagine a user registers a name they want (lets say "John Smith") with PoW of 4
and 0.1BTC locked up:

* T=52,560
* P=4
* B=0.1
* N=1

`( 52,560 * 4 ) + ( 52,560 * 0.1 ) / 1 = 215,496`

Lets imagine another "John Smith" wants this name, so he registers the same name
with double the Proof of Work (as each additional level is exponentially more
work).  He also needs twice the Bitcoin to pass the threshold for the same locktime:

* T=52,560
* P=5
* B=0.1
* N=2

`( 52,560 * 8 ) + ( 52,560 * 0.2+ ) / 2 = 215,496+`

Imagine the previous user sees they have lost the name, and wishes to keep the registration.
The user can send additional funds to their initial contract hash in order to "reclaim"
the name.  Since their registration was first, they just need to add enough funds
to beat the previous name:

`( 52,560 * 4 ) + ( 52,560 * 0.11 ) / 1 = 216,021.6`

The second "John Smith" decides that's too much for the name, and decides to register "John Smith2" instead.

The second John Smith's still owns his Bitcoin, but they're unspendable for the duration
of his attempted registration.  This means if you want to unseat a name, you should
be prepared to do more than _the square_ of the initial PoW than the original registrant
did, if all other parameters are equal.

# Economic rationale:

Any user that wishes to register a name must commit scarce resources to do so:

* Locking a variable amount of Bitcoin to be unspendable for a variable amount of time
* Processing time in the form of Proof of Work

This disincentivzes "namesquatting" because any user that wishes to register a name
they do not intend to use will lose the use of their Bitcoin, and a user more interested
in the name could commit more Bitcoin or more Proof of Work and "steal" the name.

A user that registers a name no one cares to unseat can commit very little Bitcoin
and provide a low Proof of Work, and register the name for a short time if they wish.
The design of Numerifides was done with being egalitarian in mind.

A user with a very popular or contentious name mapping (example: DNS for google.com)
should:

1. Do as much Proof of Work as possible.
2. Provide the longest locktime possible.
3. Lock as much Bitcoin as possible

In this order.

Miners can only choose to attempt to censor the whole network, not individual mappings.
This is because a Numerifides mapping is only broadcast to the network once its
commitment transaction has had a certain number of confirmations. Users locking
up Bitcoin make the miner's(and everyone's) Bitcoin more valuable so unless there
is external pressure, miner's should be incentivized to encourage Numerifides transactions.

# Known issues

If a name is unseated, the original BTC are still locked up and essentially useless.
The original registrant can try to win back the name with the registration update
mechanism, but it is a little painful to make ones funds unspendable with nothing
to show for it. Perhaps "levels" of trust should be used rather than explicit TRUSTED
or UNTRUSTED.  "Namefights" like those outlined in the fifth example also mean
the loser still has his Bitcoin locked up for the full locktime, which is a poor
experience for the loser.

Storage of all mappings is rooted on the blockchain, but gossip about new mappings
could be partly blocked or censored.  This is also true of Bitcoin itself, so once
the network is of sufficient size and fault-tolerance, it should be increasingly
difficult to fully prevent a numerifide from being gossiped about.

The data is like a blockchain itself, but without links between the numerifides
transactions.  If the network forgets about a mapping, it would have to be
gossiped about again. This is partially addressed by consensus hashes, as the conensus
hash should be the same for any given block height.

Storage of the mappings could get quite burdensome as users may want to register
large data mappings.

# Prior art

Some similar work has already been done in this space, such as the first altcoin
ever, Namecoin.  Namecoin is a great system that does suffer from some technical
shortcomings such as the prevalence of "namesquatting".  Also, its mining algorithm
was a good choice at the time as the second crypto, but is a security liability
as one of hundreds of cryptos today.

Blockstack also has the Blockchain Name System<sup>[3](#ref3)</sup> where TLDs can be registered and
pricing schemes can be devised for any name being registered in the namespace.
This is distinct from Numerifides because TLDs can be "namesquat" or federated.
Names on Numerifides are registered in the namespace of each data type.

Other names in the space are Distributed ID, OneName, and others.

# REFERENCES
- < a id="ref1">[Zooko's Triangle on Wikipedia](https://en.wikipedia.org/wiki/Zooko%27s_triangle)</a>
- < a id="ref2">[RFC-2119](https://www.ietf.org/rfc/rfc2119.txt)</a>
- < a id="ref3">[Blockstack's Whitepaper](https://blockstack.org/whitepaper.pdf)</a>
