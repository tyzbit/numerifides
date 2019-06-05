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

## Renewing and Updating Registrations

After initially creating a numerifide, a user may "strengthen" it (and keep the PoW
the same) simply by paying more Bitcoin to the same contract hash.

If a user wants to update their registration (such as to change the data mapping),
they must wait until their intial coins unlock (with new coins protecting the
registration or not), and pay _from the initial contract address_ to a new registration.
Re-registrations like this are "linked", so the `N` in the previous formula stays
the same, though the user must still do PoW and PoH (which could be more or less
than the initial registration transaction, up to the user) for the new registration.
