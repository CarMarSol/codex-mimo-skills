# Block task template

Replace fields with verified project information. This template prepares a submission; it does not by itself authorize calls or access to data.

## First task

```text
Task ID:
Single observable outcome:
Exclusions:

Reference sources and version/hashes:
Authorized output files (indicate which are new):
Reviewed snippets:

Actual contract:
- Signatures and return values of dependencies.
- Units, missing data, and domain terms.
- Invariants to preserve.

Requested change:
Acceptance: expected inputs and outputs, rejections, and regressions.
Checks Codex will run:

Delivery: a unified patch only for the authorized outputs.
Do not run tools or request additional access.
Do not wrap the response in Markdown or claim tests were run.
```

Codex tracks limits, attempts, usage, and hashes separately. Do not include credentials or private logs in the prompt.

## Patch format

For a fictional existing one-line file:

```diff
--- a/src/example.py
+++ b/src/example.py
@@ -1 +1 @@
-LIMIT = 1
+LIMIT = 2
```

Headers are separate lines. Each line in a hunk starts with a space, `-`, or `+`. Counts must match context and changes. For a new file, the old header is `--- /dev/null`. Do not use absolute paths, renames, file deletions, or full replacements of existing files unless the task explicitly authorizes them.

## Correction after a failure

Update the first task with current sources and add the following for each verified failure:

| Field | Content |
| --- | --- |
| Type | Format, code, or provider. |
| Observed | The smallest reviewed input and result or error. |
| Expected | The result required by the contract. |
| Correction | Requested change and missing context. |
| Verification | The specific case Codex will run. |

Do not attribute a failure to MiMo when the test contract was incorrect. Preserve the cycle ID and its usage; a correction does not start a new budget.
