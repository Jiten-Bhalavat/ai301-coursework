# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s3/pull/246

**Branch**

fix/69-json-array-fallback

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. First run: 19/20 - pkg-16 failed on `description-matches-diff` and `deviation-honest`
2. Final run: 20/20 - all packages correct

The final score matches `eval-run.txt`: "agreement: 20/20 scored items  (bar: 18/20: PASS)"

**Package analysis**

Package: pkg-16 (kubernetes/minikube#23471)

My rubric initially rejected this as failing `description-matches-diff` and `deviation-honest`. The gold label says "accept" with note: "honestly disclosed shortfall: image-load path fails loudly with before/after transcripts; the start-path behavior deliberately deferred with the maintainer discussion cited in plan and description."

The issue was that my rubric treated "deliberately deferred" items as deviations, when they're actually part of the original plan's scope boundaries. The plan explicitly states the start-time loading path is "deliberately deferred" - it's not a deviation, it's an honest scope boundary.

**Check rationale**

Check from `tools/pr-precheck/rubric.md`:

> | deviation-honest | The plan's scope and deviation notes read against the diff and description | Items the plan marks "not in scope" or "deliberately deferred" are NOT deviations - they're planned scope boundaries. Deviation notes (changes from the plan) must match the actual diff. When a description restates the plan's scope boundaries (deferred items, out-of-scope items), that's honest disclosure, not a deviation. This check fails only when the diff or description misrepresents what was actually done. | preferred |

I revised this check after pkg-16 failed. The original version read "If the plan has deviation notes, they accurately describe the actual deviations in the diff." This was too narrow - it didn't account for the distinction between:
1. Deviation notes (changes FROM the plan)
2. Scope boundaries (things never in scope per the plan)

The revised check explicitly recognizes that "deliberately deferred" and "not in scope" items are honest scope boundaries, not deviations requiring notes.

**Trade-offs**

The revised `deviation-honest` check is more permissive for PRs that honestly restate the plan's scope boundaries in the description. I verified this doesn't break other packages by re-running the full eval - all 20 scored packages agreed after the change. The clear-accept packages (pkg-02, 05, 08, 11, 13, 16, 19) all correctly accept, and no reject packages flipped to accept. The distinction between "scope boundary" (never in scope) and "deviation" (changed from plan) aligns with how real PRs document their scope.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
