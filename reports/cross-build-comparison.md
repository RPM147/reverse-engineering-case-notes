# Comparing Executables Across Different Builds

Before a matched pair was available for build 26315250, we compared a launcher and shipping executable against files supplied as clean references. The 311,296-byte launcher matched its reference byte for byte. The two shipping executables represented different builds.

For the shipping files, we compared seven selected function bodies after excluding address fields affected by linking. The remaining 6,910 bytes matched. We separately checked selected call targets because matching instruction bodies outside address fields cannot establish where every reference leads.

The result corroborated selected code across builds. The later comparison of two copies from the same reported build supplied the direct whole-file evidence for that build. [Executable comparison](executable-comparison.md)
