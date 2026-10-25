# Codex + MiMo Skills

Two skills for coordinating programming work between Codex and MiMo: Codex defines the task, reviews the patch, and runs the tests; MiMo proposes the implementation.

**Status: first public instruction release.** A complete manual workflow is included. Automation requires a compatible external integration, which this package does not install or include. This release has not been validated end to end with a real MiMo call.

## What it provides

- Tasks with verifiable outcomes, selected context, and specific output files.
- Delivery as a unified patch, reviewed before it is applied.
- Corrections based on verified errors, preserving attempts and usage for the same task.
- A clear distinction between what the worker proposes and what the coordinator verifies.

These are agent instructions: they are not a sandbox or a spending limit enforced by code. No savings percentage is promised, and delegation is not guaranteed to improve every task.

## The two skills

| Skill | Use |
| --- | --- |
| `mi` | One bounded change with a contract and independent review. |
| `orq` | Several related blocks, defined and accepted one at a time. Reuses the `mi` procedure. |

Example requests:

```text
$mi prepare a task to fix this bug. Use the manual workflow; review MiMo's response before applying the patch and running the tests.
```

```text
$orq split this feature into verifiable blocks and prepare the first one for MiMo. Do not start the next block until the current one is accepted.
```

The skills keep the chat's primary model unchanged. Choose MiMo model names from those available in the account; the package does not hard-code provider identifiers.

## Local installation

1. Download this repository with **Code → Download ZIP** and extract it.
2. Copy the complete `skills/mi` and `skills/orq` folders to Codex's user skill location:
   - Windows: `%USERPROFILE%\.agents\skills\`
   - macOS/Linux: `~/.agents/skills/`
3. If `mi` or `orq` already exists, compare it and keep a backup before replacing it. Do not install another copy with the same name in a different location.
4. Open Codex in your project and look for the skills. If they do not appear, restart Codex.

The resulting structure should be:

```text
.agents/skills/
├── mi/
│   ├── SKILL.md
│   ├── agents/openai.yaml
│   └── references/task-brief.md
└── orq/
    ├── SKILL.md
    └── agents/openai.yaml
```

Install both folders together: `orq` reads `../mi/SKILL.md`. No Python or Node packages are needed to read these instructions. Testing changes requires the relevant project environment.

See the [official skills documentation](https://learn.chatgpt.com/docs/build-skills) for locations and discovery.

## Complete manual workflow

1. Ask Codex to use `$mi` in your project and prepare a task using the [task brief template](skills/mi/references/task-brief.md).
2. Review the snippets that will leave your machine. Copy only the approved task to your MiMo tool, using an available model and your account's limits. Do not provide repository access or tools on your machine.
3. Return the proposed patch to Codex. Codex checks paths, content, and whether the source files have changed; then it reviews and applies the authorized change.
4. Codex runs the relevant tests. If they fail because of the change, it prepares a correction with verified errors and current context.
5. If the agreed attempts are exhausted or usage from an interrupted call is unknown, stop further submissions and retain the diagnosis. The manual workflow cannot prevent an individual call from exceeding an external budget.

See the [complete synthetic example](examples/normalize-label.md), with a task, patch, and local check. The example patch illustrates the format; it is not a real MiMo response.

## Optional automatic integration

Use only an adapter that you can inspect and that is already configured. Before calling, the coordinator must check:

- Which snippets it sends, to which provider/model, and under what authorization.
- That the worker receives no credentials or tools with general project access.
- How it records attempts, errors, and usage; which limits it enforces before the call and which it only checks afterward.
- How it preserves versions and detects concurrent changes before applying patches.

A provider CLI, a prompt listing paths, and a working directory do not prove isolation. If a required capability is missing, report the blocker and prepare the task for manual handoff; do not automatically send data through another channel. Configure keys outside the repository.

This package does not include an API client, MiMo installer, automatic patch applier, or unattended task scheduler.

## Validation and limits

During preparation, we checked metadata and local links and exercised the sample patch in a temporary repository, including against an incompatible source. No paid calls were made, and tokens, cost, or comparative quality were not measured.

Provenance: adapted for publication from the personal `mi` and `orq` skills. Machine paths, account details, and dependencies specific to private projects have been removed. Ponytail and other third-party plugins are not distributed. This is not an official OpenAI or Xiaomi project.

## License

[MIT](LICENSE). You may use, modify, and redistribute this content while retaining the license notice. External services remain subject to their own requirements and terms.
