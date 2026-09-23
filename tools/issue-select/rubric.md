# Rubric: is this a good first issue?

Every check below names a source a grader can open, and a pass condition
with a number in it wherever a number is possible. Recency thresholds are
measured against the bundle's stated capture date in eval mode, and
against today in live mode.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| maintainer-commits | The "last 5 default-branch commits" list under Repo facts (eval) / the commit list on the repo front page (live) | At least one of the last 5 default-branch commits is authored by a human (username not ending in `[bot]`), and is dated within 90 days of the capture date | required |
| repo-alive | The repo line under Repo facts: `archived:`, "latest release", "last push to any branch" (eval) / the archived banner, Releases sidebar, and newest commit date (live) | Not archived, AND either a release dated within 365 days of capture or a push to any branch within 90 days of capture | required |
| scope-bounded | The issue body, comment count, and the full comment thread; linked PRs under Repo facts | The issue asks for one coherent change (bug fix, feature, or docs task), AND none of these is true: (1) it explicitly labels itself as an umbrella, tracking, or meta-issue with separate sub-tasks to be claimed independently; (2) the thread has more than 30 comments showing extended design debate with no maintainer settlement; (3) there are 2 or more closed unmerged linked PRs indicating repeated abandoned attempts; (4) the issue is a usage or support question rather than a change to the code; (5) the issue body is under 50 words AND lacks any of: acceptance criteria, expected behavior description, reproduction steps, or specific files to change (a terse feature wish with no specification fails; a terse bug report from a maintainer with clear behavior description passes) | required |
| unclaimed | `assignees:` and `linked PRs:` under Repo facts, plus every claim comment in the thread (eval) / the Assignees box, the Development box, and the thread (live) | No assignee, AND no open linked PR, AND no claim comment from outside the classroom left within the last 30 days that a maintainer acknowledged. Per the Path Review house rule in scope.md, classmate claim comments in the course repo do not count as claims | required |
| ai-contributions-allowed | The "contribution policy" line under Repo facts (eval) / `CONTRIBUTING.md` in the repo root or `.github/`, plus any `AI_POLICY.md` or PR-template disclosure box (live) | No outright ban on AI-assisted or AI-generated contributions. Conditions such as disclosure, personal understanding, testing, or human review pass; stated silence passes | required |
| reproducible-ask | The issue body | The body names at least one of: a concrete reproduction, an expected-versus-actual pair, a failing test, or an acceptance-criteria checklist; OR the issue opener has a COLLABORATOR, MEMBER, or OWNER badge | preferred |
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
