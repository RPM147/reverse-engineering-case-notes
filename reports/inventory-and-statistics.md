# Interpreting Inventory and Statistics Results

On November 4, 2026, a run of build 26315250 reached the main menu and later exited with code zero. An early checkpoint retained 171 events spanning roughly 10.5 seconds. It captured runtime result evidence for seven selected methods.

Some inventory methods reported success while leaving the caller's output handle unchanged. A statistics request returned a handle for an asynchronous result. The result became readable, and retrieving it succeeded. The delivered payload nevertheless reported a failure status for the underlying operation.

The experiment distinguishes call success, output values, and the status reported inside a result. The retained checkpoint contains the targeted observations. It cannot provide final callback totals or the complete shutdown sequence. A separate run captured that lifecycle. [Queue lifecycle](queue-lifecycle.md)
