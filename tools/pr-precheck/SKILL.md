---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

This tool answers exactly one question about exactly one PR package: **is this ready to submit?**

A PR package consists of:
- A candidate pull request (title, description, commits, diff)
- Test evidence showing the fix works
- Read against the plan it claims to implement
- Read against the issue that plan belongs to

The tool never answers a different question, never grades more than one package per run, and never answers from gut feel.

## Inputs and modes

**Live mode**: Grade your own submission before it goes out. Inputs are:
- Your `plan.md` including any deviation notes
- Your branch's diff: the output of `git diff main...HEAD` (three dots) from your working copy
- Your draft PR title and description
- Your test evidence (captured before/after output)
- Your issue (fetched live from the repo)

For a house-chain student, read the house plan and house repro pack instead of your own.

**Eval mode**: A package bundle is the whole world. Every fact comes from the bundle text; nothing is fetched, nothing else is read. Grade every check with the full verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` before anything else. It names where the PR must live and the house rules of that environment. Refuse to grade work outside the scoped repo. If the scope's `Repo:` line still carries an unfilled placeholder, stop without grading and tell the student to fill the `Repo:` line with their section's Path Review repo. Never guess a scope.

In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, read `voice-guide.md` and hold the outgoing PR text (title and description) against those rules. Report any rule the draft breaks in the summary. The voice guide never changes the verdict on its own unless the rubric has a check that reads it.

In eval mode, ignore `voice-guide.md` entirely.

## Component reads

Read the components in this order:
1. `rubric.md` defines the checks and the verdict rule
2. `references/evidence-guide.md` maps where each evidence family lives
3. `procedure.md` is executed as written

When the procedure is silent on a step, report the gap in the summary rather than silently inventing steps.

When `rubric.md` or `procedure.md` has no content (still a template), refuse to grade and say so. An empty tool that invents checks at runtime is worse than no tool.

## Verdict and output

The verdict space is binary:
- **accept**: ready to submit
- **reject**: hold

End the reply with the fenced JSON block below, valid and last, with nothing after it:

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

A readable per-check summary may come before the block.

## Grading discipline

- **Evidence first**: No check is graded without naming the fact or quote that decided it. "Looks fine" is not evidence.
- **Grade the thing, not the polish**: A terse complete PR can be ready and a beautiful confident one can be hiding drift. Every check reads the artifact itself against the plan, the issue, and the stated standards.
- **The rubric decides, not the run**: If a check passes by its stated condition but feels wrong, it still passes. The fix belongs in the rubric, not in the run.
- **The procedure decides how, not the run**: Follow `procedure.md` as written and report its gaps instead of silently inventing steps.
- **Unclear defaults to fail**: Where the rubric's verdict rule is silent on unclear, treat an unverifiable claim as a failing one. A PR you cannot verify from the package is not ready to submit.
