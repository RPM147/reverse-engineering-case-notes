# Testing Observable Behavior with Varied Inputs

A helper process compared five selected library queries with a standalone behavioral model. All 208 comparisons across eight configurations agreed after a discrepancy found during testing was corrected.

The default fixture already listed downloadable-content entries in the same order as the observed output. It therefore failed to expose the first model's assumption that configuration order determined response order. Changing the order and using identifiers of different lengths distinguished the two interpretations. A negative control that changed one configured entry also produced detectable differences.

The comparison demonstrates the value of varied inputs and a control that is expected to fail. It covers the queried behavior under the tested configurations. The model was exercised in a helper process and was never used to launch the game.
