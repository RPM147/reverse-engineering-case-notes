# Comparing Executable Code with Build Records

On November 3, 2026, we compared an earlier shipping executable with its packaged Program Database (PDB). The executable's CodeView GUID and age matched the PDB. A candidate Steam build had a plausible release date, but the available provenance did not establish that it was the same build.

In this PDB, a recorded 32-bit value for code contributions matched a value derived from each contribution's SHA-256 digest. The relationship held across 36,529 code records before accounting for address fields. It is an observed property of this PDB.

Seven selected functions agreed with their build records after accounting for address fields affected by linking. In one function, the initial comparison differed. Symbol lookup showed that a reference pointed inside a symbol rather than at its start. Preserving that displacement resolved the discrepancy.

The PDB corroborated the selected functions. A full-file claim required a separate same-build reference. That comparison was later made for a newer build. [Executable comparison](executable-comparison.md)
