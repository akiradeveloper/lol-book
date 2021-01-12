# The principle in membership change: single-server changes

There are two ways to change the cluster membership in Raft: one is by joint concensus algorithm and the another is single-server changes.

In the initial Raft dissertation in journal, joint consensus algorithm was used to change the membership but later the author found the fault in joint consensus algorithm, and the lastest dissertation uses single-server changes. lol uses this.

So what is single-server changes? In accordance with the name, this algorithm add or remove only one server at a time.

These operations are represented as special requests (`AddServer` and `RemoveServer`) and it turns into `ClusterConfiguration` command in the log which is then replicated to the cluster as well as normal commands.

The rational behind this is a single-server change always overlap at least one node between before and after. The following figure from Raft dissertation describes a case of adding one node.

![](images/single-server-changes.png)

So the next leader always know the lastest membership and the consensus on membership change never be lost.