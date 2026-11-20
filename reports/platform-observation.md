# Attributing Platform Calls During Startup

We used executable call sites, build symbols, and interface declarations to identify selected platform calls. For an indirect call, an interface name alone is insufficient. We also checked the dispatch target in the loaded module and used the declared interface to interpret the observed call.

A November 4, 2026 run of build 26315250 reached the main menu and exited normally. Twelve interface requests returned non-null objects in the selected trace. The main-menu observation identified fourteen virtual call sites for twelve distinct methods. The trace records the calls visible to instrumentation, which does not imply that every exported function ran or that every interface method was exercised.

The methodology distinguishes an imported name, a request for an interface, and a call that reaches an implementation. Later observations extended the run to a save load. [API call coverage](api-call-coverage.md)
