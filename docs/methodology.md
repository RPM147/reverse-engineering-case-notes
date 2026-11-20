# Research Methodology

## Identifying samples

Record the build identification, size, and cryptographic digest of each file before drawing comparisons. Use full byte comparisons where references come from the same build. When build identities differ, limit the claim to the specific regions and fields compared. A supplied reference establishes what was compared. Its distribution provenance requires separate evidence.

## Interpreting runtime observations

A call-site hit establishes that an instruction was reached. A captured return records the immediate response. A returned handle identifies a result to follow, and that result can report a different outcome from the call itself. To correlate a call with a local write, the study used call nesting, thread identity, and the file handle. It checked the final captured bytes against the file after exit.

An incomplete trace remains bounded by its last retained event. Results from a later complete run can corroborate a finding under stated conditions. They do not supply events missing from an earlier run.

## Checking behavior in isolation

Controlled helper-process tests exercise call sequences that are difficult to isolate during a full application run. Recorded expectations can then support a replay against a standalone test component. Compare values and state transitions rather than memory addresses or incidental execution timing. Treat successful replay as evidence for the tested scenarios and check integration separately.

## Evidence terminology

| Term | What it means here |
| --- | --- |
| Static finding | Supported by inspecting a file or an analysis copy. |
| Runtime observation | Recorded during a specified run or at a specified checkpoint. |
| Corroborated interpretation | Supported by matching signals from more than one observation or method. |
| Controlled experiment | A deliberate sequence used to test behavior under stated conditions. |
| Replay | A test of recorded expectations against a separate component. |
