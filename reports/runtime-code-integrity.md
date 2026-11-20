# Comparing Runtime Code with the File on Disk

On November 3 and 4, 2026, we compared the mapped executable code section of the earlier sample against its on-disk bytes. Each full read covered 142,988,284 bytes. The comparison excluded the file's alignment padding and required no normalization for relocations in that section.

Three full reads came from an attempt that stopped before the main menu. Four came from a separate run that reached the menu and then exited normally with code zero. One of those reads was taken after the instrumentation session detached. All seven matched the file byte for byte. Another attempt exited before a read could be taken.

A positive control changed one byte in a private copy used by the comparison program. The comparison detected the change and reported its location. The runtime result covers the executable's code section at the sampled times. Other modules, data regions, and intervals between measurements remain outside that result.
