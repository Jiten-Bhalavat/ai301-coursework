# Rubric: is this a good first issue?

Every check below names a source a grader can open, and a pass condition
with a number in it wherever a number is possible. Recency thresholds are
measured against the bundle's stated capture date in eval mode, and
against today in live mode.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| maintainer-commits | The "last 5 default-branch commits" list under Repo facts (eval) / the commit list on the repo front page (live) | At least one of the last 5 default-branch commits is authored by a human (username not ending in `[bot]`), or is a bot commit merging a human pull request, and is dated within 90 days of the capture date | required |
| maintainer-answers | The "maintainer first-response sample" under Repo facts (eval) / first reply carrying an Owner, Member, or Collaborator badge on recently updated issues (live) | The sampled first-response times show at least one maintainer reply within 30 days; a sample that is empty or shows no reply inside 30 days fails | required |
| repo-alive | The repo line under Repo facts: `archived:`, "latest release", "last push to any branch" (eval) / the archived banner, Releases sidebar, and newest commit date (live) | Not archived, AND either a release dated within 365 days of capture or a push to any branch within 90 days of capture | required |
| scope-bounded | The issue body and the full comment thread | The issue asks for one bounded change, and none of these is true: it is an umbrella or tracking issue listing sub-items; the thread shows an unsettled design debate no maintainer has closed; a maintainer states the fix touches core internals; the issue is a usage or support question rather than a change to the code | required |
| unclaimed | `assignees:` and `linked PRs:` under Repo facts, plus every claim comment in the thread (eval) / the Assignees box, the Development box, and the thread (live) | No assignee, AND no open linked PR, AND no claim comment from outside the classroom left within the last 30 days that a maintainer acknowledged. Per the Path Review house rule in scope.md, classmate claim comments in the course repo do not count as claims | required |
| ai-contributions-allowed | The "contribution policy" line under Repo facts (eval) / `CONTRIBUTING.md` in the repo root or `.github/`, plus any `AI_POLICY.md` or PR-template disclosure box (live) | No outright ban on AI-assisted or AI-generated contributions. Conditions such as disclosure, personal understanding, testing, or human review pass; stated silence passes | required |
| reproducible-ask | The issue body | The body names at least one of: a concrete reproduction, an expected-versus-actual pair, a failing test, or an acceptance-criteria checklist | preferred |
| entry-labelled | The issue's labels | Carries a maintainer-applied newcomer label such as `good first issue`, `good-first-issue`, or a starter difficulty tier | preferred |
| files-named | The issue body | The body names the specific file or files the change lands in, so the work can start without a repo-wide hunt | preferred |

## Verdict rule

Accept only if every `required` check grades `pass`. A single `fail` on any
required check rejects the issue. `unclear` counts as `fail` on required
checks: a first issue whose safety I cannot verify from the evidence in
front of me is not one I should take.

`preferred` checks never change a verdict. They rank the accepted issues
against each other: among accepted candidates, more preferred passes ranks
higher, and ties are broken by the fit profile in `scope.md`.
