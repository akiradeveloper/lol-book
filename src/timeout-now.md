# Leadership Transfer

In Raft, leader is chosen by election.
Election happens when follower considers leader is dead.

If leader is removed from the cluster, every client requests
fails before a new leader is elected.

To avoid this, lol implements `TimeoutNow` RPC which asks some node to
immediately start election (by becoming candidate in new term) regardless of election timeout.

In lol, when leader is removed from the cluster, this `TimeoutNow` RPC is sent to 
one of the living nodes so a new leader is immediately chosen.

This RPC is also used to pin leader node by sending it from outside the cluster.
In some senario, some node is more suitable for being a leader than other nodes.
Leader pinning is used in such case.