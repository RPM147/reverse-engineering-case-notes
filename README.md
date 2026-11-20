# Reverse Engineering Case Notes

This repository documents reverse engineering experiments for educational and research purposes. Mortal Shell II was picked as one example from among games available in cracked distributions. The game serves as a case study for examining Windows binaries, making runtime observations, and checking what those observations support. The project has no plans to modify the game itself.

| Report | Finding |
| --- | --- |
| [Executable comparison](reports/executable-comparison.md) | Both examined executables matched the supplied references for build 26315250 byte for byte. |
| [Build symbols and code identity](reports/build-symbols.md) | Build records corroborated seven selected functions in an earlier sample. |
| [Runtime code integrity](reports/runtime-code-integrity.md) | Seven complete reads of the sampled executable's code section matched the file on disk. |
| [API call coverage](reports/api-call-coverage.md) | A save-load trace added seven call sites and three method names to the observed set. |
| [Inventory and statistics results](reports/inventory-and-statistics.md) | Call success, output values, and result status conveyed different information. |
| [Queue lifecycle](reports/queue-lifecycle.md) | A live trace followed one asynchronous result through delivery and queue removal. |
| [Result retention and polling](reports/result-retention.md) | A controlled experiment found that polling could affect whether a result remained available. |
| [Result delivery and registration](reports/result-delivery.md) | A result and the registration of its listener had separate lifetimes. |
| [Statistics and persistence](reports/statistics-and-persistence.md) | A statistics success notification and local score persistence followed separate paths. |
| [Leaderboard persistence](reports/leaderboard-persistence.md) | Two score submissions led to local file writes. The final captured write matched the file read after exit. |
| [Asynchronous result replay](reports/async-result-replay.md) | A standalone component matched 322 comparisons across four recorded scenarios. |
| [Callback lifetime](reports/callback-lifetime.md) | A standalone Windows experiment verified that a callback could finish safely after another thread removed its registration. |

Each report identifies the samples or runs behind its conclusions. The English reports are adapted from the original lab notes for publication.

The original text in this repository is licensed under [Creative Commons Attribution 4.0 International](LICENSE.md). Product names identify the software under study.
