# A Proposal for Proof of Authority Rooted on Decentralized Blockchains

# Foreward

Since the earliest instances of early humans gathering into tribes, people have
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
meaningful<sup>1</sup>.

# Terminology used:

* NUMERIFIDES: The decentralized consensus protocol of TRUST described here.

* NUMERIFIDE: A transaction following the consensus rules of Numerifides.

* NUMERIFIED: A piece of data that exists on NUMERIFIDES that is TRUSTED according to consensus rules.

* TRUST: The method whereby a general mapping of names to data formalized in a “numerifide” transaction can be independently verified to be UNDISPUTED.

* TRUSTED: A “numerified” “numerifide” Numerifides transaction.  A valid, trusted, name mapping.

* MUST, MAY, SHOULD, SHOULD NOT, MUST NOT: Used as defined in RFC-21192<sup>2</sup>

* CONSENSUS: The method by which the decentralized Numerifides consensus protocol agrees to the state of Numerifides

* COMMAND: The registration portion of a Numerifides transaction.  This is propagated off-chain

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

# REFERENCES
- [Zooko's Triangle on Wikipedia](https://en.wikipedia.org/wiki/Zooko%27s_triangle)</a>
- [RFC-2119](https://www.ietf.org/rfc/rfc2119.txt)</a>
