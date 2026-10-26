---
name: mroowa-interrogate
description: Adversarially review code changes with one read-only reviewer and a parent judgment pass. Use for interrogate, challenge this code, stress test this diff, find blind spots, or a requested adversarial code review.
license: MIT
---

# Interrogate

Adapted from pstack's interrogate skill to use one review subagent. The deliverable is a judged review, not code changes. Do not auto-apply fixes or post findings externally.

## 1. Scope

Identify the requested diff or files. For branch review, determine the actual base branch and use `git diff <base>...HEAD`; include uncommitted changes when they are part of the request. Gather the surrounding context needed to assess the change, without exploring unrelated subsystems.

Prefer file paths, commit or diff commands, and relevant line ranges over copying large source files into the prompt. Make clear which changes are under review.

## 2. Intent

State the intended behavior in one short paragraph, using the user request, commit messages, PR description when relevant, and code. If the intent is materially ambiguous and cannot be inferred, ask for clarification before reviewing.

## 3. Launch one reviewer

Spawn exactly one read-only reviewer using the available subagent tool. Inherit the parent model and reasoning effort by default. Do not read Cursor model-panel configuration, create a reviewer roster, or run competing model reviews. Neither the reviewer nor the parent may spawn additional agents as part of this review, including verification or synthesis agents.

Read [references/reviewer-prompt.md](references/reviewer-prompt.md) and fill in its intent, code, rubric, and code-quality sections. Supply [references/rubric.md](references/rubric.md) and [references/code-quality-review.md](references/code-quality-review.md), along with the scoped file pointers or diff. Explicitly tell the reviewer to work read-only and return its findings without delegating.

Use only tool arguments supported by the current runtime. When there is no read-only tool flag, put the constraint in the task. If subagents are unavailable or prohibited, perform one review in the current agent and disclose the fallback. Do not compensate by running multiple sequential reviewer passes.

The reviewer covers every relevant lens in one pass. It must trace concrete failure paths, distinguish defects from preferences, and return no findings when that is the evidence. Do not force every lens onto a small change.

## 4. Parent judgment

The parent reads the review and applies [references/lead-judgment.md](references/lead-judgment.md). Deduplicate findings and check the code behind consequential claims. Use focused source reads or non-mutating local checks where useful; do not repeat the full review or launch another agent.

Judge each finding on its evidence and the actual task constraints. A single review provides no independent model consensus. Do not invent agreement, disagreement, or confidence from reviewer counts.

Classify findings:

- **Act on.** Confirmed issues that should block the change, with a concrete location, impact, and evidence.
- **Consider.** Legitimate concerns with a meaningful tradeoff or remaining uncertainty.
- **Noted.** Valid context with no action needed for this change.
- **Dismissed.** Incorrect claims, preferences, or issues outside scope, with a short reason.

## 5. Report

Lead with the verdict and any actionable findings. Include the intended behavior, reviewer mode (one subagent or local fallback), finding locations, evidence, and useful suggestions. Report the other categories only when they contain findings worth showing.

State important gaps, including behavior that was not executed or context that could not be checked. An empty review is a valid result. Omit the upstream reviewer roster and agreement map. Leave code, PR comments, and approval state unchanged unless the user separately asks for those actions.
