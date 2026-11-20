# Listener Lifetime During Callback Delivery

On November 20, 2026, we tested how a callback can remain safe when another thread removes its listener during delivery. If dispatch holds a lock while running listener code, a callback that waits for another thread can block an operation that needs the same lock. Releasing the lock requires a separate guarantee that the listener stays alive until the call returns.

In a standalone Windows program, the dispatcher acquired a shared reference to the listener under the registration lock, then released the lock before calling it. A condition variable coordinated the two threads. After delivery began, a second thread removed the registration and attempted another delivery.

Removal completed while the first call was still active. The second delivery found no listener. The first callback observed the removal and returned. The listener was destroyed when the last reference was released. The program exited with code zero.

This experiment covers a dispatcher that participates in ownership of its listeners. An interface that receives a caller-owned raw pointer needs a lifetime agreement with the caller before dispatch can rely on the same guarantee.
