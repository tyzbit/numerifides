# Examples of Trust Levels

A user that locks up 1BTC for 144 blocks and provides a Proof of Work of 2 would then
have a TRUST level of 432.

`( ( 144 * 2 ) + ( 144 * 100,000,000 / 100,000,000 ) ) / 2 = 432`

A user that wishes to "take over" the name (keeping the locktime the same),
but doesn't have as much Bitcoin must mine until a PoW of 5 and "unseat the name" with
any amount more than the amount initially locked :

`( ( 144 * 5 ) + ( 144 * 100,000,001 / 100,000,000 ) / 2 = 432.00000072`

In this way, names are secured primarily by locktime and Proof of Work, but secondarily
by amount of Bitcoin locked up.  Also, "takeovers" require more PoW/Bitcoin/PoH
than the initial investment. (By the way, to "unseat" the registration a third time would
require a PoW of 8, and any amount more than the initially locked Bitcoin (1)).

If the previous user wanted to usurp the registration using only funds, matching
the proof of work, she would have to commit 4X the amount of Bitcoin:

`( ( 144 * 2 ) + ( 144 * 500,000,000 / 100,000,000 ) / 2 )`

# Example Numerifides registration

User wishes to register the name:data mapping of `"03:Numerifides:FF:[GPG key]:[nonce]"`.
User creates the appropriate transaction that:

* Pays back to themselves .001 BTC
* Locks the Bitcoin for a duration of 52,160 blocks (1 year)
* Has an appropriate Proof of Work advertised via the TXID hash

User broadcasts this transaction and it is included in a block.  User waits
6 blocks, and then broadcasts to the Numerifides network the mapping she just
registered.

The user was the first to broadcast this name, so any full or light node that does
a lookup for a GPG record for Numerifides should get this new record.

Since no other user is interested in registering this name, the Proof of Work
and Proof of Hodling is enough to secure the name, and if the user does nothing else,
the name becomes available for registration again after 52,160 blocks.

# Second example ("driveby" registration that is unseated)

A user wishes to "namesquat" a name, so they register `"05:Google.com:FF:127.0.0.1:[nonce]"` with
1BTC locked up and a Proof of Work of 2 locked up for 52,560 blocks.  In this example,
lets say it took 1 day of "mining" the transaction to produce that level of Proof of Work.

* T=52,560
* P=2
* B=1
* N=1

`( 52,560 * 2 ) + ( 52,560 * 1,000,000 / 100,000,000 ) / 1= 157,680`

Google themselves come along and wish to register the name, but see it is already
registered. Google happens to have a lot of Bitcoin, and has a lot of processing power
to "mine" a new transaction.  Google spends some time "mining" and finally transmits a
transaction with a PoW level of 4, and Google locks up 10BTC, also for 1 year.

* T=52,560
* P=4
* B=10
* N=2

`( 52,560 * 4 ) + ( 52,560 * 1,000,000,000 / 100,000,000 ) / 2 = 367,920`

This handily beats the previous registration, which is still locked for the rest
of the duration of the locktime.

# Third example ("namesquatted" by a user with a lot of BTC)

A user with a large amount of BTC, not a lot of PoW that wishes to "namesquat" registers
popular usernames on the system.  Let's assume they registered 10,000 names and
were able to commit 0.5BTC to each of the names with a Proof of Work of 1. Let's
assume the user only wished to squat the names for a week.

* T=1,008
* P=1
* B=0.5
* N=1

`( 1,008 * 1 ) + ( 1,008 * 50,000,000 / 100,000,000 ) / 1 = 1,512`

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

`( 52,560 * 1 ) + ( 52,560 * 10,000,000 / 100,000,000 ) / 2 = 28,908`

# Fourth example (someone with a lot of PoW "DoS"es names)

Lets take the user in the previous namesquatted example with 0.1BTC, and say a
"name miner" comes along and unseats the name for fun (or profit).  The "name miner"
can also commit 0.1BTC for one month (4,320 blocks).  Lets say the "name miner"
has a lot of power, and reaches a Proof of Work of 10:

* T=4,320
* P=10
* B=0.1
* N=1

`( 4,320 * 10 ) + ( 4,320 * 10,000,000 / 100,000,000 ) / 3 = 14,544`

The miner still cannot reach the same level as the previous user before, even though
the miner did exponentially more work because the miner can't afford to lock up
that many BTC for that long, and because the miner is the 3rd user to try to register
the name.

# Fifth example (two similar users want the same name)

Imagine a user registers a name they want (lets say "johnsmith") with PoW of 4
and 0.1BTC locked up:

* T=52,560
* P=4
* B=0.1
* N=1

`( 52,560 * 4 ) + ( 52,560 * 10,000,000 / 100,000,000 ) / 1 = 215,496`

Lets imagine another "johnsmith" wants this name, so he registers the same name
with double the Proof of Work (as each additional level is exponentially more
work).  He also needs twice the Bitcoin to pass the threshold for the same locktime:

* T=52,560
* P=5
* B=0.1
* N=2

`( 52,560 * 8 ) + ( 52,560 * 20,000,002+ / 100,000,000 ) / 2 = 215,496.0005256`

Imagine the previous user sees they have lost the name, and wishes to reclaim the
registration. The user can send additional funds to their initial contract hash
in order to "reclaim" the name.  Since their registration was first, they just
need to add enough funds to beat the previous name:

`( 52,560 * 4 ) + ( 52,560 * 10,000,002 / 100,000,000 ) / 1 = 215,496.0010512`

The second "John Smith" decides that's too much for the name, and decides to register "johnsmith2" instead.

The second John Smith's still owns his Bitcoin, but they're unspendable for the duration
of his attempted registration.  This means if you want to unseat a name, you should
be prepared to do more than _the square_ of the initial PoW than the original registrant
did, if all other parameters are equal.
