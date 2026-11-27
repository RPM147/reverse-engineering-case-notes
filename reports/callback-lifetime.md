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

### What the game recorded at shutdown

We revisited the 482-event game capture from phase 17. Its SHA-256 digest matched the archived capture summary, its sequence numbers were contiguous, and the recorder reported no message truncation. We matched listener addresses across registration, delivery and removal within this run.

The game registered 22 distinct listeners. All 25 recorded delivery entries referred to members of that set. The last recorded delivery entry was event 436. After the exit request at event 456, events 458 through 479 recorded removal of each of the 22 listeners exactly once. Shutdown began at event 480 and returned at event 482.

This establishes the order of registration removal and shutdown in one game run. The trace records entry into the observed listener methods but provides no matching return event for each call. None of the 40 pointer arguments seen at the monitored deallocation helper matched a registered listener address. A listener could be embedded in a larger allocation, and a destructor could run without a corresponding call to that helper. The time of the last listener return and the time of listener destruction therefore remain unknown.

The controlled phase 19 host recorded returns from its own test listeners. The phase 20 game capture retained only part of the session, and the phase 22 game trace followed score persistence. These records add no observation linking a game listener's final return to its destruction.
