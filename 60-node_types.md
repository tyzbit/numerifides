# Implementations

Implementations of the Numerifides Trust Consensus Protocol will fall into two categories:
"Full" nodes and "Light" nodes.

## Full Nodes

A Full node will have all of the known mappings, and be able to perform lookups
locally.  Each full node will gossip about mappings to one another, and periodically
query one another to check consensus about mappings.  A full node should also
have a copy of the Bitcoin blockchain for maximum security, but it could be possible
to use a pruned backend node to use a pruned backend node AFTER the initial sync
if the user feels the level of risk is acceptable. If a mapping was originally
censored, once an honest node sees it, it will broadcast it to all nodes it knows
about.  Honest nodes will see it as either the first registration, or a more
trusted registration (since it was confirmed before the dishonest registration
that was gossiped about) and will reorganize the registrations for that name/data
type accordingly.

Nodes will gossip a "consensus hash"<sup>1</sup>
that is derived from every Numerifides registration. Each node will hash every Numerifides
registration it learns about per block sequentially in order of position in the
block.  This "Numerifides block hash" is then hashed together in sequence to
produce a Merkle branch.  These branches are then hashed together as assembled
until finally a consensus hash is produced for the highest known block.  With
the conensus hash derived from one's own calculation, a full node can know if
it agrees with consensus or not.

If the full node is not in consensus with spec, it can query a partner full node
and ask for its Numerifides Merkle tree.  With this tree, the local full node
can tell which block(s) it is missing registrations for, and request registrations
present in those blocks from the partner full node.  If consensus is broken becuase
the other node is missing data, the local node can pass the data along and "convert"
this node to our local node's view of consensus.

The full node spec is still largely unknown, but they may assign trust to their
peers much like Bitcoin nodes do (to guard against Sybil attacks), and punish
bad actors by refusing to propagate their updates.  There may also be a mechanism
so that full nodes can drop numerifides that don't meet certain criteria, such as
if the size is too great, or the trust level is too low.  This causes issues with
the consensus hash system, so this is still an area for improvement.

## Light Nodes

A Light node will query multiple Full nodes for the name they want to look up,
along with the anchoring transaction and the consensus hash and then confirm via
an SPV lookup on the Bitcoin network that the related transactions are valid according
to consensus rules. Light nodes should query more than one Full node for a lookup,
and likewise query more than one Bitcoin node to confirm the anchoring Numerifides
transaction.

# REFERENCES
- 1: [Blockstack's Whitepaper](https://blockstack.org/whitepaper.pdf)
