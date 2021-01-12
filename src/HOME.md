# Welcome! lol

This is a set of documents to understand how lol is designed and how to make your own application with this library.

Table of Contents:

- **Architecture**
  - [Overview](overview-architecture): RaftApp, RaftCore and companion threads
  - [Log and Snapshot](log-snapshot): How the design's evolved
  - [How snapshots are managed](snapshot-tag): Snapshot tag and resource
  - [Storage Abstraction](storage-abstraction): About RaftStorage
  - [Two ways of making snapshot](snapshot-types): Copy snapshot and Fold snapshot
- **Client Interaction**
  - [Interaction Types](interaction-types)
  - [Optimized Query Processing](query-processing)
  - [Gateway](gateway): Track the cluster membership from outside the cluster
- **Cluster Management**
  - [Single-server changes](membership-change): No joint consensus
  - [Cluster Management APIs](cluster-management): How to manage a cluster by AddServer and RemoveServer APIs
  - [Leader Liveness](leader-liveness): How to detect leader failure
  - [Leader Transfer](timeout-now): TimeoutNow RPC
- **Tools**
  - [lol-admin](https://github.com/akiradeveloper/lol/tree/master/lol-admin): Command line tool for admin
  - [lol-monitor](https://github.com/akiradeveloper/lol/tree/master/lol-monitor): TUI application to monitor the cluster
- **Reference**
  - [Raft Dissertation](https://github.com/ongardie/dissertation): Diego Ongaro's Dissertation in Stanford Univ.