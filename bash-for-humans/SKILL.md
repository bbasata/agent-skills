---
name: bash-for-humans
description: Make Bash command sequences easier for humans to read. Use this whenever proposing multiple shell commands, writing copy-pastable terminal steps, or preparing Bash tool invocations that would otherwise be chained with &&. Prefer separate commands for readability while preserving fail-fast semantics.
---

When presenting multiple Bash commands:

1. Prefer one command per line instead of chaining commands with `&&`.
1. Preserve circuit-breaking semantics as if the commands had been chained with `&&` or run under `set -e`.
1. If later commands depend on earlier ones, present them in order and make the fail-fast behavior clear.
1. Keep commands copy-pastable and avoid extra shell noise unless it is needed for correctness.

For Bash tool usage:

1. Prefer newline-separated commands in a single Bash invocation over `&&` chains when readability matters.
1. Use `set -e` when needed so the execution behavior still stops on the first failing command.

Example:

Instead of:

```bash
terraform fmt && terraform validate && terraform plan
```

Prefer:

```bash
set -e
terraform fmt
terraform validate
terraform plan
```
