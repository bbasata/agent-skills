--
name: secrets
description: My personal system for managing secrets. Use this when a secret needs to be generated, when a secret value is needed to call a remote API, or when a secret value needs to be stored securely for later retrieval.
--

When a secret named "ThisIsASecret" needs to be generated:

1. Run this 1Password CLI command:
   ```
   op item create --generate-password --title "ThisIsASecret"
   ```

When a remote API needs a secret value:

1. Prompt for the name of a 1Password item. Do not list 1Password items, out of
   concern for exposing the names of unrelated secrets in my Vault.
1. Run this 1Password CLI command. Do not echo the output to the terminal. Do
   not display the output anywhere. It is okay to keep this value in the system
   clipboard or in a new temporary file with mode 0600.
   ```
   op item get "{ name }"
   ```
1. If the secret value if found, then offer to use the secret value in the remote API call.
1. If the secret value is not found, then offer to try again or to skip.

