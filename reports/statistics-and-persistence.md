# Statistics Notifications and Persistence

Static analysis on November 15, 2026 distinguished three paths in the examined platform library. The statistics-save method prepared a success notification. A record-count method read a count from memory. A separate leaderboard path updated a table and serialized its contents to a local file.

The distinction matters when interpreting a trace. A success notification establishes what the method reported. A count query establishes the value it read at that point. A file-write observation is needed to connect a particular operation to the contents stored locally.

The static analysis identified a candidate path for the file change seen during an earlier save-load run. A fresh runtime experiment captured both writes and compared their contents with the file after exit. [Leaderboard persistence](leaderboard-persistence.md)
