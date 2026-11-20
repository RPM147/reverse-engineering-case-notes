# Result Retention and the Effects of Polling

On November 11, 2026, a helper process tested two sequences against the library in the examined package. Each used a statistics result that was already available in the queue.

In the first sequence, two callback cycles left the unread payload available. The trace showed that the record was deferred during each cycle and restored for later processing. Reading the result copied its payload and marked the record for cleanup. The next cycle removed it, and a later read failed without changing the output buffer.

In the second sequence, a completion query alone marked a fresh result for cleanup. A callback cycle then removed it before the caller attempted retrieval. This shows why observational probes that call a status method can change the state under study. The result applies to the tested call order in the helper process.
