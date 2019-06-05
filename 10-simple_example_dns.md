# Simple Example

Consider a user, Satoshi Nakamoto, who wants to browse to the "bitcoin.site"
website, but does not want to trust his ISPs nameservers.  Satoshi installs a
"light" Numerifides client (a few megabytes in size), with a "DNS" plugin that
transparently catches local DNS requests and uses the Numerifides client to do
lookups.

Satoshi's computer connects with multiple Numerifides nodes and requests the IP
address associated with "bitcoin.site". Every server tells him the same result,
`127.0.0.1`, and includes a transaction ID that Satoshi can look up on the
Blockchain to verify they are telling the truth.  Satoshi's computer requests
the block that transaction was in from multiple Bitcoin nodes and verifies the
transaction was confirmed.  After verified, the computer continues on to connect
to that IP and browse to the website at that address.  This entire process
happens in less than a second, and Satoshi doesn't have to do anything.
