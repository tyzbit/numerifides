# Simple Example

Consider a user, let's say Satoshi Nakamoto, who wants to be able to send PGP
signed emails that anyone in the world can independently and in a decentralized
way verify that the email is genuine.  Lets say Satoshi wanted to register the
PGP key with the name "Satoshi"

Satoshi creates a transaction that locks up some bitcoin; lets say 1BTC for one
year.  This Bitcoin is still Satoshi's, it just becomes impossible to spend for
a year.  Satoshi pays to an address he creates that is cryptographically linked
to a registration script that he keeps secret for now.  All the Bitcoin network
sees is that he locked up his Bitcoin*.  His transaction is mined, and reaches
a certain number of confirmations.  This takes less than an hour.  Now, Satoshi
broadcasts his registration to the Numerifides network, which verifies the name
was available, and that he followed Numerifides' rules about how to register
names.  Satoshi's registration now shows as TRUSTED on Numerifides! Satoshi sends
his signed email, and his email client indicates that the PGP key can be verified
with Numerifides.

Satoshi's friend Hal receives his email, and wants to verify it's really from
Satoshi.  Hal does an independent lookup for the PGP key assigned to "Satoshi"
on the Numerifides network from multiple nodes, and checks on the Blockchain
that the registration transaction follows Numerifides' rules.  Hal gets the PGP
public key from Numerifides and after checking multiple nodes, Hal confirms
that the signed email matches the PGP public key referenced by the network.

Most of these actions happen automatically, and transparently to the user.

\* _Numerifides transactions are likely to be unique enough that they can be
identified as Numerifides transactions by miners, but the name being registered
is not broadcast until the transaction already has enough confirmations to make
it infeasible to reverse._
