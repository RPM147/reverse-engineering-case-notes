# Observing Local Leaderboard Persistence

On November 15, 2026, we loaded an existing save in build 26315250 and monitored selected calls and local file operations. The experiment used the platform library already present in the examined package. It recorded arguments and return values without replacing them.

The game submitted a score of zero to each of two local tables. In both cases, the score call enclosed a serialization call on the same thread. Within that call, a file was opened, written synchronously, and closed successfully. Operation nesting, thread identity, and the file handle linked each write to its score submission.

| Submission | Bytes reported written | Change to the target table |
| --- | ---: | --- |
| First | 188 | Entry count increased from 3 to 4 and a zero score was appended. |
| Second | 202 | Entry count increased from 3 to 4 and a zero score was appended. |

The final write buffer matched the file read after process exit byte for byte. Both entry-count queries ran before the corresponding submission and returned three. Four statistics-save calls returned success. The observed leaderboard writes were nested under the score submissions.

The two capture channels agreed on all 370 retained events. The game exited with code zero. The operator restored the profile files and verified the hashes of the five tracked package files. The measurements cover the selected file and calls in this session. Successful synchronous writes and a post-exit read establish the resulting file contents without measuring resilience to power loss.
