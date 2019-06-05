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
commitment transaction has had a certain number of confirmations.  Users locking up
Bitcoin make the miner's Bitcoin more valuable so unless there is external pressure,
miner's should be incentivized to encourage Numerifides transactions.

Consequences of the formula:

* All else being equal, it takes ( the original PoW )^8, plus one satoshi to unseat a name

* All else being equal, it takes 3x the BTC, plus one satoshi to unseat a name

* All else being equal, it takes double the locktime, plus one satoshi to unseat a name
