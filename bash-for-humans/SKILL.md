---
name: bash-for-humans
description: Make Bash command sequences easier for humans to read. Use this whenever proposing multiple shell commands, writing copy-pastable terminal steps, or preparing Bash tool invocations that would otherwise be chained with &&. Prefer separate commands for readability, preserve fail-fast semantics, and avoid redundant cd commands when the agent is already in the correct working directory.
---

When presenting multiple Bash commands:

1. Prefer one command per line instead of chaining commands with `&&`.
1. When there is more than one command, preserve circuit-breaking semantics as if the commands had been chained with `&&` or run under `set -e`.
1. If later commands depend on earlier ones, present them in order and make the fail-fast behavior clear.
1. Keep commands copy-pastable and avoid extra shell noise unless it is needed for correctness.

For Bash tool usage:

1. Prefer newline-separated commands in a single Bash invocation over `&&` chains when readability matters.
1. Use `set -e` only when needed to preserve fail-fast behavior across multiple commands. A single command does not need `set -e`.
1. Do not add `cd` to the current working directory of the agent session. Only use `cd` when changing into a different directory is actually necessary.

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
