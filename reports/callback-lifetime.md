# Listener Lifetime During Callback Delivery

On November 20, 2026, we tested how a callback can remain safe when another thread removes its listener during delivery. If dispatch holds a lock while running listener code, a callback that waits for another thread can block an operation that needs the same lock. Releasing the lock requires a separate guarantee that the listener stays alive until the call returns.

In a standalone Windows program, the dispatcher acquired a shared reference to the listener under the registration lock, then released the lock before calling it. A condition variable coordinated the two threads. After delivery began, a second thread removed the registration and attempted another delivery.

Removal completed while the first call was still active. The second delivery found no listener. The first callback observed the removal and returned. The listener was destroyed when the last reference was released. The program exited with code zero.

This experiment covers a dispatcher that participates in ownership of its listeners. An interface that receives a caller-owned raw pointer needs a lifetime agreement with the caller before dispatch can rely on the same guarantee.

### When can the caller destroy its listener?

A later test of our asynchronous component found that a listener waiting for removal on another thread could stall during either the size query or result delivery. In a revised component, both operations ran outside the registration lock. The other thread then finished removal during either operation. An invocation selected before removal still completed. Those tests kept listener storage alive throughout.

On November 27, 2026, we tested caller-owned storage in a standalone C++ program. The caller held the only owning reference. A gate counted admitted calls before they could use the listener. Requesting closure stopped new admissions immediately. The owner waited for admitted calls to finish before destroying the listener. A callback could request closure and return while the owner handled the wait.

Three scenarios passed on Windows. An idle gate tolerated repeated closure. In the two concurrent scenarios, either the owner or a callback requested closure while two calls were active. A third delivery was rejected. With one call still active, the gate reported that work remained and the listener was alive. After both callbacks completed, the owner destroyed the listener once and another delivery was rejected.

The lifetime guarantee depends on every delivery passing through the gate and on the gate outliving its callers. The test exercised a standalone owner and dispatcher. Whether the game caller provides that coordination remains open.
