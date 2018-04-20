# A Proposal for a Novel Proof of Authority Rooted on Decentralized Blockchains

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
enables a system of  decentralized authority, whereby an user or actor can assert
identity, existence and authority on a public piece of data, on an open blockchain
and any independent, skeptical user or actor operating the consensus protocol
can verify any other actor’s statement of authority in a decentralized, fair and
privacy-protective manner.

I propose this system be called the Numerifides (capitalized) Trust Consensus
Protocol, or Numerifides (Nu-mer-ih-fie-dees) for short.  Transactions using this
system are to be called “numerifide(noun) transactions” (nu-mer-ih-fi’d) or
“numerifides (lowercase)” (nu-mer-ih-fi-dz) and trusted mappings to be referred
to as numerified(verb) numerifides(plural noun) or Numerifides transactions).
This is derived from the latin word numeris for number, and the Roman goddess
Fidēs, the goddess of trust and good faith.

# Outline

I propose a novel new transaction type, dubbed a “numerifide” transaction,
compatible with Bitcoin that allows a transaction to be created that associates
an authority over a given “name” and associates user-supplied data to it.  In this way,
a human-meaningful “name” can be registered in a decentralized way that associates with a
“value” that provides some utility, such as (but not limited to):

* Associating a specific username to a Bitcoin address to provide cryptographic
proof of ownership of the username, receiving Bitcoin funds, or optionally using
the Bitcoin key to sign messages.

* Advertising a human recognizable domain name→onion address mapping.

* Authenticating an “alias” for an Lightning Network node→node pubkey

In addition, the user can alter this data in a secure, uncensorable way via
already existing mining mechanisms present in Bitcoin as well as incentive and
disincentive structures I will outline below. Further, “abandoned names” can be
claimed via a Proof of Work mechanism, and incentives are structured such that
“namesquatting” valuable names is disincentivized. This system creates a fair
and just way of reserving, updating, revoking via consensus and abandoning names
in a way that solves Zooko’s triangle of useful names being memorable,
secure and decentralized.

# Terminology used:

* NUMERIFIDES: The decentralized consensus protocol of TRUST described here.

* NUMERIFIDE: A transaction following the consensus rules of Numerifides.

* NUMERIFIED: A piece of data that exists on NUMERIFIDES that is TRUSTED according to consensus rules.

* TRUST: The method whereby a general mapping of names to data formalized in a “numerifide” transaction can be independently verified to be UNDISPUTED.

* TRUSTED: A “numerified” “numerifide” Numerifides transaction.

* MUST, MAY, SHOULD, SHOULD NOT, MUST NOT: Used as defined in RFC-21192

* CONSENSUS: The method by which the decentralized Numerifides consensus protocol agrees to the state of Numerifides

* CLTV: CheckLockTimeVerify – an encumbrance on spending funds until a certain number of Bitcoin (measured in blocks in a blockchain) have passed.

* UPDATE: The process whereby a name→data mapping can be changed or RENEWED by the owner of the private key locking the funds. As with usual cryptocurrency transactions, the funds are fully spent

* RENEW: A numerifide transaction that keeps the node→data mapping the same, but moves the funds from an EXPIRED numerifide to a numerified numerifide

* RELEASE(D): A name that is no longer TRUSTED due to expiry of the encumbering CLTV.

* REVOKE(D): A name that is CONTESTED due to a spend from the “Transaction Puzzle” portion of the transaction.

* CONTESTED: A name (and by extension a numerifide) that is SWEPT via proof of work of the TRANSACTION PUZZLE.

* CONTEST: A incentive mechanism whereby names can be wrestled from their owners with a combination of Proof of Work and making owned funds unspendable via CLTV encumberances.

* TRANSACTION PUZZLE: A series of Script OPCODEs that provide for Proof of Work on a specific numerifide.

* LOCK(ED): Funds that are unspendable until AFTER a specific period of time has passed measured in Bitcoin blocks.

* BEFORE, AFTER/SUBSEQUENT: Time as perceived by the succession of blocks on Bitcoin

* VALID: A numerifide that follows all consensus rules

* USER/ACTOR/NODE: A participant in the Numerifides consensus protocol that independently verifies protocol rules are being followed.

* PROOF OF WORK: A method of evaluating a resulting hash to be able to prove a specific amount of work was done to produce the hash.

* PROOF OF PROOF OF WORK (TRANSACTION PUZZLE): A specific set of Script OPCODES that prove a minimum amount of work was done to arrive at a particular hash.  Essentially synonymous with a Transaction Puzzle.

HODL: A drunken misspelling of HOLD.

# Technical proposal
In order to secure a human readable authoritative “name” out of the possible “namespaces”, a user constructs and signs a transaction from an unspent output address funding a “numerifide” transaction with the below Script:

```
OP_IF
	[bindata1] [bindata2] OP_2DUP # duplicate the first two inputs
	OP_EQUAL # push an equals onto the stack
	OP_NOT OP_VERIFY #ensure the two pieces of data are not equal
	[hashdata1] OP_SHA1 # hash the first data (SHA-256? Other available hashing function, if SHA1 collisions still are out of the reach of normal users?)
	OP_SWAP # swap top 2 items on stack
	[hashdata2] OP_SHA1 # hash the second data
OP_EQUAL #Ensure the two hashes match (Proof of Work)
OP_ELSE # allow the funds to be re-spent after CSV expires
	<signature> CheckSigVerify
[user data] OP_PUSHDATA[1, 2 or 4]
[any number between 144 and 52,560] CHECKSEQUENCEVERIFY
```

(Numerifides transactions such as this MUST also enable Replace-by-fee (RBF) on the funding transaction for reasons outlined below.)

Numerifides transactions can also substitute the specific CheckSigVerify for a CheckMultiSigVerify OPCODE with no additional considerations.)

Where [user data] refers to data in any of these formats:

Format | Script OPCODE | Notes
-------|---------------|------
[name]:[data-type][data] | OP_PUSHDATA1 | (Must be less than 255 total bytes to be a valid transaction according to my understanding of the rules today)
[name]:[data-type][data] | OP_PUSHDATA2 | (Must be less than 511 total bytes to be a valid transaction according to my understanding of the rules today)
[name]:[data-type][data] | OP_PUSHDATA4 | (Must be less than 1023 total bytes to be a valid transaction according to my understanding of the rules today)

Further, the hash in the proof of work included in the transaction must also
match at least 1 digit of the resulting TXID, which prevents “premine” attacks
against names that malicious actors first see in the numerifides transaction and
decide are valuable enough to attack.  Every additional digit that matches is
proof of more work done, and thus would be TRUSTed over a transaction that didn’t match.

Consensus mechanism:  Since the transaction outlined above is constructable by
anyone who can find a SHA1 collision of some two pieces of secret data and
publish a transaction spending the inputs LOCKED at this address, a simple
consensus mechanism is necessary to allow users a set of rules for CREATING
UPDATING and REVOKING via consensus mechanisms.

Assigning TRUST to “Numerifide” name→data mappings
TRUSTING UPDATES to “Numerifide” name→data mappings
and RELEASING “abandoned” "Numerifide" name→data mappings.  The rules of the
consensus algorithm are defined below:

# NUMERIFIDES RULES OF CONSENSUS

These rules MUST BE evaluated in this order, with rules that have a lower number being superceded by rules with a higher number.

For example, a Numerifides transaction with more matching digits between the TXID hash and the included Proof of Work takes precedence over any amount of Proof of Work.

1. The FIRST transaction as seen on the Bitcoin blockchain to create a “numerified” name→data mapping (a “numerifide”) from the “namespace” is TRUSTED BEFORE any SUBSEQUENT ones, IF NO OTHER RULE IS VIOLATED

2. All other criteria equal, the LONGEST LOCKED transaction is valid OVER any lower time-locked transactions, IF NO OTHER RULE IS VIOLATED

3. All other criteria equal, the HIGHEST value transaction is valid BEFORE any lower values ones, IF NO OTHER RULE IS VIOLATED

4. All other criteria equal, the MOST MATCHING DIGITS of the transaction ID of a specific numerifide is TRUSTED, IF NO OTHER RULE IS VIOLATED.

5. All other criteria equal, the MOST PROOF OF WORK in the “numerifide” CONTEST section of the script is TRUSTED over any lower proof of work transactions, IF NO OTHER RULE IS VIOLATED

6. The timelock on the transaction MUST NOT BE longer than 52,560 blocks (roughly equivalent to one year as perceived by the Bitcoin blockchain), and MUST BE longer than 144 blocks in length (one day).

7. The name reserved MUST NOT BE any combination of case for the name “NUMERIFIED” OR “NUMERIFIDE”.

8. If the CLTV encumbrance on a numerifide expires, the numerifide MUST NOT BE TRUSTED.

9. If a numerifide is confirmed with 6 blocks of confirmation, it MUST BE TRUSTED IF NO OTHER RULE IS VIOLATED.

10. In the event of a chain split longer than 6 blocks, numerifides present in the contested blocks MUST NOT BE TRUSTED EVEN IF NO OTHER RULE IS VIOLATED until the LONGEST chain with the winning numerifide transaction has settled with twice the length of the previous block parameter, proposed to be 6.

11. If the inputs locked in a “numerifide” are spent via a CONTEST transaction, the numerifide is said to be CONTESTED and MUST NOT BE TRUSTED.  The next numerifide added to the chain longer than 6 blocks MUST BE TRUSTED IF NO OTHER RULE IS VIOLATED.

12. Numerifide transactions MUST TRUST a numerifide with no data, EVEN IF NO OTHER RULE IS VIOLATED.

13. Numerifide transactions MUST include a name but MAY include no data.  This is done by omitting the OP_PUSHDATA Script OPCODE

14. Names in numerifides SHOULD BE case-insensitive, and using English characters. Names MAY BE any valid combination of valid data that fits in an overall transaction.

15. The target data MUST BE identified with an encoding, as defined in a simple proposed spec below.

16. If every other rule is not violated, a USER MUST accept the name→data mapping as TRUSTED.

17.  A Numerifide transaction MUST use the table below to add a relevant data encoding to their attached data, IF it is included.

18. A Numerifide transaction MAY choose the incorrect data encoding for their attached data.

19. Numerifide transactions MUST USE ASCII characters only.

20. Numerifide transactions MUST allow data of any length to be attached to a name for ANY encoding, IF NO OTHER RULE IS VIOLATED

# PROPOSED DATA ENCODING TABLE:

Constant length 2+-byte data field
Proposed Data Standard
Constant length separator (2 byte) (proposed 0XFF in Hex, but not certain the best arrangement here)
Description

00
Private Usage
The data associated with the name has no explicitly stated purpose. The data SHOULD NOT be used to verify any other consensus-approved data standard.

01
Bitcoin Address
The data associated with the name SHOULD BE used to TRUST that the Bitcoin address is controlled by the name it is associated to.

02
Lightning Node Public Key
The data associated with the name SHOULD BE used to TRUST an advertised ALIAS of a Lightning node.

03
GPG Public Key
The data associated with the name SHOULD BE used to TRUST a GPG Public Key

04-FF
Future use decided upon via consensus.

# Implementations
Implementations of the Numerifides Trust Consensus Protocol will fall into two categories:
“namemining” nodes, and “simple” nodes.

“Name miners”: If the user wishes to further secure their already TRUSTED name
against being CONTESTED can choose to preemptively mine their next update (that
is a transaction that proves sufficient proof of work and also doesn't violate
any rules) after their first update becomes TRUSTED.  A node can be a “namemining”
node or not, as the user sees fit according to the risk of attack of their name
(a name such as “XESPQCGGBHHX7BCN1VNR” is less likely to have the risk of being
CONTESTED than a name like “SATOSHI”) .  

"Simple" or "light" nodes: The storage of the entire block chain, while necessary
to retain a full index of numerifides if one wishes, is not necessary to perform
a decentralized lookup for any given name as already existing SPV technologies
(such as BIP-157 or BIP-158) can be used to look names up in a decentralized and
censorship-resistant way.  Using already existing filtering technologies, a user
can trustlessly issue (via Bloom filters or other means) a query in the form of
a normal filter request against multiple fully validating nodes, receive the
full block that matches the query, and verify it.  To look this data up again,
a SPV node can issue a new query to many nodes and simply ensure it matches the
previous block the node downloaded.

# Economic rationale:

Any user wishing to “register” a name simply needs to “mine” a valid numerifide
transaction that locks up a specific amount of value for an amount of time.  
If the name registered is not disputed or contentious, the data associated with
the name can be trusted in a decentralized way.  Names that are unique and not so
memorable, and data that is not contentious will get confirmed and trusted easily
on Numerifides. A user with some small amount of Bitcoin wishing to register a
name→data mapping special to them but mostly meaningless to others can easily do
so with very little investment.  The user simply performs some small amount of
work of a Proof of Work function, constructs the creation transaction along with
a sufficiently long CheckLockTimeVerify, and the Bitcoin network adds it to its
open and public blockchain.

Users who wish to register a popular name such as “SATOSHI” or “BITCOIN” to
"namesquat" will necessarily have to secure their name with appropriate means.  
This can be done via a as high Proof of Proof of Work mechanism for users not
willing to lock up many Bitcoin funds but with a large amount of Bitcoin, it can
be done via a “Proof of Hodling” mechanism (a longer CLTV on the numerifide)
for users not willing to submit the anticipated necessary Proof of Work to secure a name.

When a user attempts to register a name that any malicious actor wishes to censor,
the user must include the anticipated appropriate fee, and a minimum Proof of Work
to prevent the name being “snatched” before it can confirm.  Because of this, users
will be incentivized to “mine” their own names so as to ensure they can broadcast
a higher Proof of Work should a malicious actor wish to attempt to “steal” their name.
If a user fails to contest their name via the combination of Proof of Hodling and
Proof of Work, the user will be unable to retain their desired name.

Miners will be incentivized to attempt to “snatch” high value names, but are
disincentivized by the Proof of Hodling, Proof of Work, and the possibility of
honest miners that wish to continue to mine and collect the Bitcoin block reward
plus fees rather than attack and censor numerifides transactions.  Further,
since every transaction broadcast to the network is RBF, a user can “attempt” to
register a transaction and if it isn’t confirming due to a censorship or to being
contested, the user can replace their transaction's fee with a higher one to
essentially enter into a bidding war for the name they want.

Further, since a numerifide with a Proof of Proof of Work hash with more than
one matching character to it’s transaction ID (something that can be precomputed
noninteractively), essentially any given reservation of a name comes with it the
creating of a “virtual blockchain” with the genesis block being the first reservation
of a given name and the difficulty is the Proof of Proof of Work represented by
matching the first characters of the minimum Transaction Puzzle hash to the TXID.

Miners are also incentivized to try to split the chain, and stealth mine popular
names they anticipate, but are required to lock Bitcoin to be unspendable for the
duration of time they have the address, so they must choose very carefully which
names they wish to attack.

(TODO: further economic analysis/discussion)

# Example Numerifides registration

User wishes to register the name:data mapping of "Numerifides:[GPG key]".
User creates the appropriate transaction for a duration of 52,160 blocks (1 year) that:

* Pays back to themselves .001 BTC

* Has an appropriate Proof of Work attached in the form of the transaction puzzle

User broadcasts this transaction and it is not included in the next 4 blocks.

User increases the fee according to the current block space and it is finally included in a block.

User was the first to broadcast this name, so after 6 blocks, user then performs a light client
lookup against Bitcoin network for mappings that match "Numerifides" and only receives
a single transaction, the user's.  The user's software evaluates it against consensus
rules, finds it violates none and provides the user with the mapping on demand and caches it as
trusted for one year.

Since no other user is interested in registering this name, the transaction puzzle
is never solved, even by passive crackers who try to crack every name's puzzle.

# Known issues

Numerifides transactions are prone to being censored, even if they're not contentious
because for one because as ZmnSCPxj on the lightning-dev mailing list points out,
they do not pass the IsStandard() check many miners impose on transactions they mine.

Numerifides transactions also bloat the blockchain, perhaps unnecessarily as one
could commit just a script hash, and reveal the script when it is confirmed on the
blockchain.  This, also proposed by ZmnSCPxj, would mean all transactions could be one
size, but the incentive for the secondary network to gossip about mappings is questionable.

# REFERENCES
https://en.wikipedia.org/wiki/Zooko%27s_triangle

https://www.ietf.org/rfc/rfc2119.txt

https://en.bitcoin.it/wiki/Script#Transaction_puzzle
