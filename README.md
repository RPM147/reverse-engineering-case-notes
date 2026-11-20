# Mortal Shell II Reverse Engineering Notes

This repository documents a reverse engineering study of a Windows build of Mortal Shell II for educational and research purposes. It covers executable identity, a runtime observation of local leaderboard writes, and a standalone experiment on callback lifetimes.

| Report | Finding |
| --- | --- |
| [Executable comparison](reports/executable-comparison.md) | Both examined executables matched the supplied references for build 26315250 byte for byte. |
| [Leaderboard persistence](reports/leaderboard-persistence.md) | Two score submissions led to local file writes. The final captured write matched the file read after exit. |
| [Callback lifetime](reports/callback-lifetime.md) | A standalone Windows experiment verified that a callback could finish safely after another thread removed its registration. |

These reports describe the samples and runs identified in each report. The executable comparison is scoped to files on disk, the leaderboard result to one observed session, and the callback result to the standalone test program.

The original text in this repository is licensed under [Creative Commons Attribution 4.0 International](LICENSE.md). Product names identify the software under study.
