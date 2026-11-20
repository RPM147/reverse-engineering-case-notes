# Following an Asynchronous Result Through a Queue

On November 11, 2026, a run of build 26315250 produced a continuous trace of 482 events through normal shutdown. We followed a statistics result using its operation identifier across queue insertion, the change that made it eligible for cleanup, copying the result to the caller, processing its completion notification, and removal from the queue.

The observed transitions tied the copied result and the removal to the same queued operation. Shutdown separately showed 22 callback unregistrations, a return from the platform shutdown routine, and process exit code zero.

An earlier checkpoint of 375 events came from a different run. Its exit status was unknown, so it was kept separate from the complete run. Selected queue records in the latter run corroborated the sequence. They leave other queue paths and concurrent behavior open.
