---
type: llm
focus: trace
---

PASS if either import_seed was never called, or validate_seed was called before the first import_seed call.
FAIL if import_seed was called without an earlier validate_seed call.
