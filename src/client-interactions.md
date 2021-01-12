# Client Interactions

In Raft, command is sent to the leader and the command is processed by the state machine. That is the textbook description.

However, this needs to send the request to the leader (lol implements forwarding so user request sent to any of the servers are forwarded to the leader), the command is replicated to the majority of servers, wait for application to state machine and finally acks. This takes much time.

Some command may need all these processes before ack but other may not. For example, some command may be allowed to ack before log application as it is guaranteed to be applied in some time later.

lol allows clients to interact with the cluster or particular node in a variety of ways. Here is the list:

- **RequestApply**: The command is sent to the leader, appended to log, replicated to majority, applied and then ack.
- **RequestCommit**: The command is sent to the leader, appended to log, replicated to majority and then ack.
- **RequestProcess**: The command is sent to the leader, processed and then ack.
- **RequestProcessLocally**: The command is sent to the designated server, processed and then ack.