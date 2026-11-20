# Measuring API Call Coverage Across Game States

An initial main-menu observation identified 14 selected virtual call sites corresponding to 12 distinct methods in build 26315250. Method names were assigned by checking the observed interface version and dispatch target against interface declarations and the loaded implementation. The observation covered a selected set of sites.

On November 14, 2026, loading an existing save added seven sites and three previously unobserved methods. The retained set reached 21 sites and 15 distinct methods. Some sites were additional callers of methods already observed at the menu.

The save-load result comes from a retained checkpoint of 284 events. The final gameplay and shutdown counters were unavailable. Counts at these sites record arrivals at the selected instructions. Return values and output buffers require separate observation. A later focused experiment captured returns and writes for selected leaderboard operations. [Leaderboard persistence](leaderboard-persistence.md)
