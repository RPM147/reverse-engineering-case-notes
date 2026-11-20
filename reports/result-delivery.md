# Result Delivery and Listener Registration

A controlled November 12, 2026 experiment examined how a pending result and a listener registration interact. In the first sequence, a listener registered for an available result. The library copied a 24-byte payload and delivered it with the matching operation identifier. The queue entry was then removed. The listener registration remained until explicitly removed, and an extra callback cycle produced no duplicate delivery.

In the second sequence, the listener was removed before delivery. The pending result survived a callback cycle without a registered listener. Registering again allowed the next cycle to deliver it. These sequences distinguish the lifetime of the result from the lifetime of the registration.

The recorded evidence was independently checked on November 14. The experiments exercised selected helper-process sequences. The question of whether a listener stays alive during concurrent removal was tested separately in a standalone program. [Callback lifetime](callback-lifetime.md)
