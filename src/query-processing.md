# Optimized Query Processing

In bare Raft, any application commands are appended to log and brought to the state machine to apply. However, if the command is query which doesn't have any side-effects, optimization is possible.

In `RequestApply`, if the request's `mutation` is false then the request is recognized as query. As described in $6.4 of Raft dissertation, the query waits for the `read_index` (the `commit_index` at the moment the query hit the server) to be applied and processed soon after that.

In implementation, queries are firstly put into `QueryQueue` and processed laster in parallel if there are more than one queries waiting for the same `read_index` to complete.