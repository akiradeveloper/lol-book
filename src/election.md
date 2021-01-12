# Election

In Raft, every client requests are process by the leader.

The algorithm proves only one leader exists in one term and the leader is at least
"stronger" (I have no idea on better expression) than the majority of the cluster servers.
The principle is simple however, there are non-trivial corner cases and some useful extensions.