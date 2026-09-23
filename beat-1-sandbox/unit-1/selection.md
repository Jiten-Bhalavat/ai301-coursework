# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/69

**Verdict output**

```
Grading issue #69: Output parser crashes on a top-level JSON array fallback

Check results:
- maintainer-commits: pass — Last commit 2026-09-16 by Aburke225 (human), within 90 days
- repo-alive: pass — Not archived, push within 90 days (2026-09-16)
- scope-bounded: pass — Single bounded bug fix with clear reproduction and named files
- unclaimed: pass — No assignees, no open linked PRs; classmate claim comments allowed per Path Review house rule
- ai-contributions-allowed: pass — No stated policy restriction
- reproducible-ask: pass — Body names expected vs actual behavior and specific files
- entry-labelled: pass — Has "good first issue" and "tier-1" labels
- files-named: pass — Body names rag/generator/output_parser.py and tests/unit/test_output_parser.py

Summary: RAG JSON parsing bug with clear scope, named files, and test coverage. Excellent fit for Python/RAG profile.

{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/69",
  "checks": [
    {"name": "maintainer-commits", "grade": "pass", "evidence": "Last commit 2026-09-16 by Aburke225, within 90 days"},
    {"name": "repo-alive", "grade": "pass", "evidence": "Not archived, pushed 2026-09-16"},
    {"name": "scope-bounded", "grade": "pass", "evidence": "Single bug fix: handle array responses in output_parser.py"},
    {"name": "unclaimed", "grade": "pass", "evidence": "No assignees, no open linked PRs"},
    {"name": "ai-contributions-allowed", "grade": "pass", "evidence": "No AI policy stated"},
    {"name": "reproducible-ask", "grade": "pass", "evidence": "Body names AttributeError on .items() call"},
    {"name": "entry-labelled", "grade": "pass", "evidence": "Labels: good first issue, tier-1"},
    {"name": "files-named", "grade": "pass", "evidence": "rag/generator/output_parser.py, tests/unit/test_output_parser.py"}
  ],
  "verdict": "accept"
}
```

---

## Eval iterations

**Run history**

1. 12/20 — Initial rubric with maintainer-answers (30-day threshold too strict)
2. 17/20 — Removed maintainer-answers, improved scope-bounded
3. 18/20 — Refined scope-bounded to distinguish umbrella issues from detailed single tasks

**Issue analysis**

issue-04 (gold: accept, rubric: reject). My rubric rejected this issue on scope-bounded because the issue body is terse: "Missing several basic rule previews. Including remove identity, fuse spiders, remove self loops, etc." The gold label accepts it because it's a maintainer-filed bounded bug (RazinShaikh is a COLLABORATOR) with clear behavior description. My rubric's word-count threshold for underspecified issues caught this false positive because it didn't account for maintainer-filed brief issues being inherently more trustworthy.

**Check rationale**

```
| scope-bounded | The issue body, comment count, and the full comment thread; linked PRs under Repo facts | The issue asks for one coherent change (bug fix, feature, or docs task), AND none of these is true: (1) it explicitly labels itself as an umbrella, tracking, or meta-issue with separate sub-tasks to be claimed independently; (2) the thread has more than 30 comments showing extended design debate with no maintainer settlement; (3) there are 2 or more closed unmerged linked PRs indicating repeated abandoned attempts; (4) the issue is a usage or support question rather than a change to the code; (5) the issue body is under 50 words AND lacks any of: acceptance criteria, expected behavior description, reproduction steps, or specific files to change (a terse feature wish with no specification fails; a terse bug report from a maintainer with clear behavior description passes) | required |
```

This check evolved through iterations to catch three failure modes: (1) umbrella issues that look like single tasks but list independent sub-items, (2) issues with years of design debate and abandoned PRs, and (3) underspecified feature wishes. The 30-comment and 2-closed-PR thresholds came from observing issue-15 (97 comments, 2 closed PRs) which should reject.

**Trade-offs**

The scope-bounded check still misses issue-04 (a terse maintainer-filed bug). The 50-word threshold with the "maintainer passes" exception in condition (5) was meant to handle this, but the model still rejected it. Accepting this trade-off: the check correctly rejects 3/4 scope issues and catches the underspecified feature wishes (issue-20) that would waste contributor time. A more complex rule risks overfitting to the eval set.

---

## Selection rationale

1. **Fit to interests and time:** Issue #69 is a RAG/JSON parsing bug in Python, directly matching my experience with retrieval pipelines and LLM systems. The estimated effort (2-4 hours) and tier-1 difficulty fit the course timeline. The test file is already present with an xfail marker, so reproduction is straightforward.

2. **Verdict accuracy:** The rubric correctly identified all passing signals: bounded scope, named files, good-first-issue label, no assignee. What the rubric couldn't weigh: this specific bug (list vs dict handling) is a common Python pattern I've debugged before, making it lower-risk than the rubric alone suggests.

3. **Claiming difficulty:** Two classmates have already commented claiming the issue, but per Path Review house rules, classmate claims don't block. Course credit attaches to the PR, not exclusivity. Low difficulty to claim.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
