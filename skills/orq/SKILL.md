---
name: orq
description: Coordinate multiple programming blocks for MiMo from Codex, with contracts and acceptance for each block. Use for the ORQ workflow; it does not start unattended tasks or install an executor.
license: MIT
---

# Coordinate multiple blocks with MiMo

Codex owns the design, dependencies, review, and acceptance. MiMo proposes patches. Read and apply the shared [mi procedure](../mi/SKILL.md) under this invocation; do not assume the other skill is loaded or active.

## From outcome to first block

1. Turn the request into a verifiable outcome and explain the necessary parts, their dependencies, and how they will be checked. Avoid adding infrastructure or an autonomous sequence the user did not request.
2. Design shared interfaces before delegating. Split work into outcomes that can be reviewed and tested separately; a dependency between modules does not mean they must all be sent together. Keep a change together when it cannot be integrated coherently in parts, and explain why.
3. Prepare one task per block using the `mi` procedure and template. Include only the necessary sources and signatures. Keep acceptance checks with Codex.
4. Use the agreed, available MiMo model. If the account offers Flash and Pro and no preference is set, propose Flash first for a bounded block; confirm the selection and limits before a paid call. A commercial name does not establish an API identifier.

## Implementation and corrections

Coordinate one block at a time: task, proposal, review, integration, and tests before the next block. Do not simultaneously change files assigned to the worker.

When something fails, first check whether the contract was ambiguous, context was missing, or the block was still too broad. Prepare a specific correction with current sources and verified failures. Do not repeat the same request hoping for a different result.

Propose a higher-tier model only for a specific technical failure or a justified new need, and only with current authorization for that model and its cost. Slowness, formatting, or a network error alone do not justify escalation. Do not switch silently.

Keep the task ID and budget across its blocks and corrections. Record attempts per block and aggregate usage without double-counting. If the next call would exceed applicable limits, keep the task pending. Do not renew the budget by creating another task or session.

## Acceptance and handoff

Keep ownership of the board if there is one. Mark a block complete only with a reviewed diff and required evidence. Status labels do not replace tests.

When integrating blocks, run checks that cover their interfaces and the combined outcome. Reuse a valid run on the same version when there are no changes or new risks that justify repeating it.

Report the outcome, accepted blocks, tests run and pending, verifiable models, and available usage. Do not claim autonomy, isolation, or savings that the tools and evidence do not establish.
