# Initial Survey of the Windows Binaries

The initial survey examined the executables and platform library in a redistributed Windows package. The import and export inventories showed that the library exposed the platform API names the executable expected. Its on-disk layout limited direct inspection of some function bodies, so the first inventory established names and file identity.

Later inspection and runtime observations showed that the game loaded a replacement platform library. Startup observations captured responses supplied by that module, while executable and symbol comparisons examined the game program separately. Tests with supplied references ultimately showed that the launcher and shipping executable in the later sample matched those references. [Executable comparison](executable-comparison.md)

The study therefore distinguishes the game executable from the platform implementation loaded at runtime. The identification applies to the examined samples. The records provide no basis to attribute the implementation to a specific upstream codebase or generalize it to other titles.
