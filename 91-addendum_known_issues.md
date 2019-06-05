# Known issues

If a name is unseated, the original BTC are still locked up and essentially
useless. Perhaps "levels" of trust should be used rather than explicit TRUSTED
or UNTRUSTED. "namefights" like those outlined in the fifth example also mean
the loser still has his Bitcoin locked up for the full locktime, which is a poor
experience for the loser.

Storage of all mappings is rooted on the blockchain, but gossip about new
mappings could be partly blocked or censored.  This is also true of Bitcoin
itself, so once the network is of sufficient size and fault-tolerance, it should
be increasingly difficult to fully prevent a numerifide from being gossiped
about.

The data is like a blockchain itself, but without links between the numerifides
transactions.  If the network forgets about a mapping, it would have to be
gossiped about again. This is partially addressed by consensus hashes, as the
conensus hash should be the same for any given block height.

Storage of the mappings could get quite burdensome as users may want to register
large data mappings.
