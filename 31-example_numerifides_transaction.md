# Command Registrations

#### Example Command: "05:google.com:127.0.0.1:11111111111111111"

Breakdown:

Field             | Explanation
------------------|--------------
05                | Data type, (05 currently proposed to be DNS type)
google.com        | Name registration.
127.0.0.1         | Data for the name to map to
11111111111111111 | Nonce


The nonce is incremented and many transactions are produced and signed until the
resulting TXID meets a minimum proof of work acceptable to the user, which is broadcast.
Since Proof of Work and Proof of Hodling are BOTH used to determine the level of TRUST, a user
registering a popular or contentious name should probably lock up significant funds
and ALSO "mine" their name out of the reach of anyone else.

The nonce is NOT evaluated as part of the mapping when checking for duplicates.
For example, although the nonces are the same, the data is different and thus the mapping is different.

```
"05:google.com:127.0.0.1:1111"
```

```
"05:google.co:127.0.0.1:1111"
```

Only the data type and name are compared to determine if the mapping is a duplicate.

A user will broadcast the transaction, wait for it to be mined for a few blocks,
and then announce it and the mapping they registered later so that miners cannot
censor registrations.
