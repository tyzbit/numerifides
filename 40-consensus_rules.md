# Rules of Consensus

## Calculating Trust

Numerifides mappings use the following formula to determine TRUST, with the winning
transaction being FULLY TRUSTED and any other transactions being UNTRUSTED (through
the user MAY be notified about the untrusted mappings outside of the protocol itself).

Each registration is evaluated only per each given data type.  A Bitcoin registration
of "Numerifides" is distinct from a GPG key registration of "Numerifides".

```
( ( T * P ) + ( T * B / S ) ) / N = TRUST
```

Where:
```
T = Timelock length (CheckSequenceVerify)
P = Proof of Work
B = Bitcoin locked up (in satoshis).
S = Number of Satoshis per Bitcoin (100,000,000)
N = The number of previous unlinked occurrences of this name registration + 1
```

The name being registered can be any latin character, but MUST BE case-insensitive.

## Checking for duplicates

The nonce and the authorized address are NOT evaluated as part of the mapping when checking for duplicates.

## Renewing and Updating Registrations

There will be many times that a record needs to be updated, for example if the
mapping becomes stale (DNS), or if the expiration of the original numerifide is
approaching and the user wishes to renew it early.

Records also have a grace period before expiring equal to 1/144 the total locktime of
the original numerifide.  So for a registration of one day (144 blocks), the total grace
period is 1 block.  A registration of one year has a 365 block grace period, which is
under 61 hours; just over two and a half days.  This means for short registrations,
it's crucial to be able to transmit a renewal numerifide to renew the registration
or else your mapping will become free for general use.  This applies to all data types.

#### Registering the update

A new Numerifides transaction is created **with one of the inputs being the "authorized update address."**
This transaction is only allowed to update the original record for the original record type.
Any other scenario and the mapping will be considered UNTRUSTED.

This transaction will also provide a new update address that is also authorized to
register new updates to the record.

#### "Strengthening" Registrations

After initially creating a numerifide, a user may "strengthen" it (and keep the PoW
the same) simply by paying more Bitcoin to the same contract hash.
