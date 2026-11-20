# Replaying Asynchronous Result Scenarios

On November 17, 2026, a standalone Windows component was tested against recorded expectations from the result-retention and listener-delivery experiments. Four scenarios produced 322 comparisons of values and state transitions. All matched. Expected values came from the earlier recordings.

The replay exercised retention of unread results, cleanup following a query, automatic delivery to a registered listener, and delivery after removing and restoring a registration. The test process supplied recorded payloads directly so the comparison covered result handling.

During review, we found that a temporary callback buffer could contain unwritten bytes when its capacity exceeded the payload size. The component was changed to initialize the entire buffer. Seventeen separate checks covered buffer handling and input cases in the test component. The replay and those checks passed after the change.

This component was exercised in a test process. The results establish agreement for the selected recorded scenarios. Integration and concurrent dispatch behavior require separate validation. [Callback lifetime](callback-lifetime.md)
