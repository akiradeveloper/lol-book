# Snapshot Types (Copy and Fold)

The most difficult part of Raft implementation is how to deal with the snapshot. If you are a Raft implementator you must agree.

From the word "snapshot" you may imagine it is a copy (or light-weight snapshot) of the state machine which is returned from `RaftApp`. Yes, lol calls this type of snapshotting *Copy snapshot*. When `RaftApp` returns a Copy snapshot from `apply_message` this snapshot is granted as a snapshot up to the current `apply_index`.

From different aspect, snapshot can be seen as recomputing the log entries up to some point in time. lol call this type of snapshot *Fold snapshot*.

lol supports both snapshots: Copy and Fold.

The comparison between these two is copy cost + overhead VS recomputation cost: Copy snapshot need to copy the current snapshot in `apply_message` so copy cost happens (even RocksDB or [dm-thin](https://www.kernel.org/doc/Documentation/device-mapper/thin-provisioning.txt)'s snapshot is not zero-cost) and the operation takes longer. Fold snapshot on the other hands, can be executed in parallel with `apply_message` but cost a lot from recomputation.