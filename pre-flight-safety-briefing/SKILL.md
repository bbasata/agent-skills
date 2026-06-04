---
name: pre-flight-safety-briefing
description: Run a brief safety check sequence before the first tool use in a session. Use this as a precursor skill to confirm the session is safe to proceed, then report a concise pass or failure message to the user.
---

Activation timing:

Load this skill before the first tool use in an agent session.

Purpose:

Before any tool is used, execute the safety checks below. Keep the check brief and deterministic. If all checks pass, tell the user concisely that the safety check is complete and append a pleasant emoji. If any check fails, tell the user concisely what safety problem was found, include the potentially unsafe environment-variable names that triggered the failure, and append a curious emoji.

Safety checks:

1. Confirm the agent does not have access to environment variables whose names contain any of these substrings, case-insensitive:
   - `password`
   - `token`
   - `key`
   Exceptions:
   - Ignore `AWS_BEARER_TOKEN_BEDROCK`, which may be required by the agent harness.
   - Ignore any environment variable whose name starts with `GIT_CONFIG_KEY_`.

Required behavior:

1. Perform the checks before the first tool use only.
2. Keep the user-facing message short.
3. On success, use a pleasant emoji such as `🙂`, `🌤️`, or `✨`.
4. On failure, state the problem directly, include the matching environment-variable names, and use a curious emoji such as `🤔` or `🧐`.
5. Do not claim the check passed unless it was actually verified.
6. If a check cannot be completed, explain why it cannot be completed.

Implementation notes:

1. To verify the environment-variable check, inspect the visible environment variable names and look only at the names, not the values.
2. A matching variable name means the safety check fails, even if the value is empty or redacted, unless it is the explicit allowlisted name `AWS_BEARER_TOKEN_BEDROCK` or it starts with the allowlisted prefix `GIT_CONFIG_KEY_`.
3. If the current platform or harness already exposed environment output earlier in the session, use that information.
