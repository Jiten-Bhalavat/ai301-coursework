# Toolkit Portfolio

Path: `beat-3-portfolio/toolkit-portfolio.md`

This file is Assignment 6, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. It has been waiting here since you created the repo in unit 1;
unit 9 is when you write it.

**Only this page is read.** Your `tools/` folders and your installed skill folders are never
opened, so every piece of evidence you want seen has to live inline here: an output excerpt,
a before/after pair, a dated commit reference.

**Write every sentence yourself.** AI may gather diffs, dates and excerpts for you; it does
not draft entries.

**Keep every section header below under its exact name** — Featured Tools, Inventory, The
Arc, and Limitations and What's Next. Feature three or four tools, each in the entry shape
shown below; give every other tool one inventory line.

**Some lines below are labelled, and the label is how they are read.** Three places on this
page use a `Label: your words` shape — the arc's beats, the tool-limits list, and nothing
else. Keep those labels exactly as written, one per line, and never delete a labelled line:
where you have nothing to put after a label, write `none` and move on. A deleted label reads
as a deleted answer.

**Student:** Jiten Bhalavat

## Featured Tools

Three or four tools, presented in depth. Open with a few sentences
on why you chose these.

I chose these four tools because each one evolved through real friction during the course. issue-scout grew from issue-select through adding search capabilities. pr-precheck reached a perfect 20/20 after I learned to distinguish scope boundaries from deviations. repro-check and plan-check both required iteration to handle edge cases in the eval sets. Together they cover the full contribution workflow: find an issue, reproduce it, plan the fix, and verify the PR.

**issue-scout**

**What it is, and the judgment hole I wrote:** issue-scout searches GitHub for first-contribution candidates using `gh search issues`, ranks them against my fit profile, and grades the top candidates against my rubric. The judgment I wrote: a search-strategy.md with 5 queries targeting Python RAG/retrieval, parsing/validation, test/pytest, FastAPI, and LLM framework issues, plus ranking filters (drop assigned, >90 days stale, >10 comments; prefer issues naming files) and an 8-check rubric (maintainer-commits, repo-alive, scope-bounded, unclaimed, ai-contributions-allowed, reproducible-ask, entry-labelled, files-named).

**How it evolved, dated:**
- September 23, 2026: Started as issue-select with a simple rubric. First eval run scored 12/20 because maintainer-answers check had a 30-day threshold that was too strict.
- September 23, 2026: Removed maintainer-answers, improved scope-bounded to catch umbrella issues. Score improved to 17/20.
- September 23, 2026: Refined scope-bounded to distinguish terse maintainer-filed bugs from underspecified feature wishes. Added exception for COLLABORATOR/MEMBER badges. Final score 18/20.
- October 16, 2026: Renamed to issue-scout, added search-strategy.md with 5 queries and ranking filters. Regression test on Unit 1 eval passed 19/20.

**Evidence:** Unit 1 eval output from selection.md:
```
Check results:
- maintainer-commits: pass — Last commit 2026-09-16 by Aburke225 (human), within 90 days
- scope-bounded: pass — Single bounded bug fix with clear reproduction and named files
- unclaimed: pass — No assignees, no open linked PRs; classmate claim comments allowed per Path Review house rule
```
Issue #69 was correctly accepted and became my real contribution.

**repro-check**

**What it is, and the judgment hole I wrote:** repro-check grades reproduction reports to verify they contain enough evidence for a maintainer to trust the reproduction. The judgment I wrote: a 6-check rubric (env-recorded, steps-followable, artifact-shows-issue, honest-outcome, ai-disclosed, claim-specific) plus a voice-guide.md for formatting standards and an evidence-guide.md mapping where to find each piece of evidence.

**How it evolved, dated:**
- September 30, 2026: Initial rubric with basic checks. First eval scored 16/20 due to edge cases in artifact-shows-issue.
- September 30, 2026: Refined artifact-shows-issue to require specific observable output, not just "tests fail". Score improved to 18/20.
- September 30, 2026: Added voice-guide template for consistent formatting. Final score 19/20 with one edge case (pkg-16 version deviation).

**Evidence:** My reproduction comment on issue #69 followed the voice-guide format:
```
Environment: Windows 10, Python 3.12.4, pytest 9.1.1
Steps: .venv\Scripts\pytest tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback --runxfail -v
Observed: AttributeError: 'list' object has no attribute 'items' at line 68
```
This structured format matched the eval's high-scoring packages.

**plan-check**

**What it is, and the judgment hole I wrote:** plan-check grades implementation plans to verify they have clear diagnosis, bounded scope, named files, and a test strategy. The judgment I wrote: a 7-check rubric (diagnosis-grounded, scope-bounded, executable-by-stranger, test-plan-decisive, unknowns-stated, ai-disclosed, engages-thread) plus procedure.md defining the grading workflow.

**How it evolved, dated:**
- September 30, 2026: Initial rubric focused on diagnosis quality. First eval scored 15/20 because executable-by-stranger was too strict.
- September 30, 2026: Refined executable-by-stranger to allow reasonable assumptions about developer environment. Score improved to 17/20.
- September 30, 2026: Added test-plan-decisive check requiring specific observable outcomes. Final score 19/20 with one edge case (pkg-14 executability).

**Evidence:** My plan comment on issue #69 hit all the checks:
```
Diagnosis: line 68 calling .items() on a list
Fix: add isinstance check for lists  
Files: rag/generator/output_parser.py, tests/unit/test_output_parser.py
Test plan: re-run reproduction, remove xfail marker
```

**pr-precheck**

**What it is, and the judgment hole I wrote:** pr-precheck grades pull requests to verify the diff matches the plan, tests are decisive, and the PR is reviewable. The judgment I wrote: an 8-check rubric (diff-matches-plan, description-matches-diff, test-evidence-decisive, repo-checks-run, diff-reviewable, template-satisfied, ai-disclosed, deviation-honest) plus procedure.md and evidence-guide.md.

**How it evolved, dated:**
- October 16, 2026: Initial rubric with strict deviation-honest check. First eval scored 19/20 - pkg-16 failed because I treated "deliberately deferred" items as deviations.
- October 16, 2026: Revised deviation-honest to recognize scope boundaries (items the plan marks "not in scope" or "deliberately deferred") are NOT deviations. Final score 20/20 - perfect agreement with gold labels.

**Evidence:** Before/after from pull-request.md:
```
Before: deviation-honest read "If the plan has deviation notes, they accurately describe the actual deviations"
After: "Items the plan marks 'not in scope' or 'deliberately deferred' are NOT deviations - they're planned scope boundaries"
```
This fix correctly accepted pkg-16 (kubernetes/minikube#23471) which had an honestly disclosed shortfall.

## Inventory

One line each for the rest of the toolkit: what it is and where it
stands (one bullet per tool; a compact sentence or two is fine).

- issue-select: The original Unit 1 issue grading tool, now superseded by issue-scout. The rubric and evidence-guide are shared; issue-scout adds the search layer.
- voice-guide: Template files for consistent formatting of comments (reproduction reports, plans). Used in repro-check and plan-check to ensure structured output.
- scope.md files: Per-tool scope definitions naming where candidates come from and house rules. issue-scout's scope expanded from Path Review only to all public repos.

## The Arc

The story of the toolkit in order: friction, change, result, dated.
Your weekly Toolkit entries are the source; read your own record and
tell it oldest first.

**Beat 1**
Date: September 23, 2026
Friction: issue-select rubric scored 12/20 on first eval run. The maintainer-answers check had a 30-day threshold requiring maintainer response within 30 days, but many good issues in active repos don't get maintainer comments because the issue description is already clear.
Change: Removed maintainer-answers check entirely, shifted focus to maintainer-commits (human commits in last 90 days) as the liveness signal.
Result: Score improved to 17/20. The rubric now correctly accepts issues in active repos regardless of whether maintainers commented.

**Beat 2**
Date: September 23, 2026
Friction: After reaching 17/20, issue-04 (zxcalc/zxlive#555) was still being rejected. Gold label said accept because it's a "maintainer-filed bounded bug." My scope-bounded check rejected it for being under 50 words.
Change: Added exception to scope-bounded: "a terse bug report from a maintainer with clear behavior description passes." The check now looks for COLLABORATOR/MEMBER/OWNER badges.
Result: Score reached 18/20 (passing bar). issue-04 correctly accepted as a maintainer-filed bug.

**Beat 3**
Date: September 30, 2026
Friction: repro-check initial rubric scored 16/20. artifact-shows-issue was passing packages that just said "tests fail" without showing the actual error output.
Change: Tightened artifact-shows-issue to require specific observable output (error message, stack trace, or before/after behavior) rather than generic "it doesn't work" claims.
Result: Score improved to 19/20. Reproduction reports now required concrete evidence.

**Beat 4**
Date: October 16, 2026
Friction: pr-precheck scored 19/20 on first run. pkg-16 (kubernetes/minikube#23471) failed deviation-honest even though the gold label said accept. The package had "deliberately deferred" items restated in the PR description.
Change: Rewrote deviation-honest to distinguish scope boundaries (things the plan says are out of scope) from actual deviations (changes from the plan). "Deliberately deferred" items in both plan and description are honest disclosure, not deviations.
Result: Score reached 20/20 - perfect agreement. The distinction between "never in scope" and "changed from plan" matches how real PRs document their work.

**Beat 5**
Date: October 16, 2026
Friction: issue-select needed search capabilities for real-world use beyond the classroom repo. The rubric worked but had no way to find issues.
Change: Renamed to issue-scout, added search-strategy.md with 5 GitHub search queries targeting my fit profile (Python RAG/parsing/test), and ranking filters to narrow results before grading.
Result: Regression test passed 19/20 on Unit 1 eval. Used the scout to select issue #69 for my real contribution.

## Limitations and What's Next

What the toolkit as a whole still does not do, and what you would
build or change next. Write this section last; it will be better
after the rest.

The toolkit handles the full contribution workflow from issue finding through PR submission, but it's built for first contributions to unfamiliar repos. It doesn't help with ongoing maintenance, multi-PR features, or navigating complex codebases over time. The checks are calibrated for "good first issue" difficulty - larger scope work would need different thresholds.

What I would build next: a PR-response tool that drafts replies to maintainer feedback. My PR #246 is still awaiting review, and when feedback comes, having structured guidance for iteration would help. The current toolkit ends at submission.

**Tool limits.** One line per featured tool, in the same order as the entries above, naming
where that tool still stops or what it still gets wrong. A small honest limit is full credit;
"none really" is not a limit. If a tool genuinely has none you can name, write `none` after
its label rather than deleting the line.

issue-scout: Still misses issue-20 (bot-filed thin-spec feature requests) on the eval set. The scope-bounded check accepts them because they have filled template sections, but the actual specification is too vague for a first contribution.
repro-check: One edge case at pkg-16 where version deviation between report and eval package caused a miss. The check doesn't account for package updates between reproduction and grading.
plan-check: One edge case at pkg-14 where executability judgment was borderline. The executable-by-stranger check can't perfectly distinguish "needs context" from "underspecified."
pr-precheck: No current misses (20/20), but the deviation-honest revision was reactive. A proactive approach would have distinguished scope boundaries from deviations in the initial design.
