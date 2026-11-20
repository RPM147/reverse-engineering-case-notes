# Reading State Transitions from a Queue Implementation

Static inspection of the platform library distinguished the availability of a result, delivery of its payload, and removal from the queue. A completion query could mark a record as eligible for cleanup. For a pending result that remained unread, the implementation had a path to retain it for a later processing cycle.

The initial interpretation came from an analysis copy and was checked against captured calls and their observed payloads. The static analysis described paths in the implementation. It did not establish when a process would take them, or whether an earlier observed result had already been copied by the time it was removed. A subsequent live trace and controlled experiments addressed those questions. [Queue lifecycle](queue-lifecycle.md) · [Result retention](result-retention.md)
