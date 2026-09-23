# Unit 1 selection

## Chosen issue

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68

`Keyword search raises ZeroDivisionError when the index is empty` (#68),
labelled `bug`, `good first issue`, `rag`, `tier-1`. Opened by
`Aburke225` on 10 September 2026. No assignee, no linked pull requests,
no comments on the thread.

## Run history

<!-- FILL IN after your confirming full eval run: the harness prints the
agreement count and the bar verdict. Replace the bracketed figures with
what the run actually reports, and keep the narrative honest about how
many passes it took. -->

The rubric went in one revision pass:

1. **First draft.** Five required checks, one per criterion family from
   the lecture (maintainer alive, repo in use, scope fits, nobody on it)
   plus the contribution-policy surface. Recency thresholds written
   against "today" rather than the bundle capture date.
2. **Fix after reading the harness docs.** Every recency threshold now
   reads against the bundle's stated capture date in eval mode and
   today in live mode, because `eval/README.md` and the evidence guide
   both measure that way. Without this the maintainer-commits and
   repo-alive checks drift on every frozen bundle.
3. **Split maintainer life from maintainer responsiveness.** The first
   draft folded "recent commits" and "answers issues" into one check, so
   a repo with a busy solo committer who never replies to issues passed.
   They are now `maintainer-commits` and `maintainer-answers`, both
   required.
4. **Confirming full run.** `python3 run_eval.py --rubric
   ~/.claude/skills/issue-select/rubric.md --save-run eval-run.txt`
   agreed on [N]/20, [pass|miss] against the bar.

## Issue analysis

Against my own rubric, graded from the live issue and repo:

- `maintainer-commits`: the repo is actively committed to and the issue
  was opened by the course maintainer account nine days before I looked.
  Pass.
- `maintainer-answers`: Path Review is instructor-run and issues are
  triaged by the same maintainer account that opens them. Pass.
- `repo-alive`: not archived, public, 71 open issues and active forks.
  Pass.
- `scope-bounded`: this is the strongest signal on the issue. The body
  names the defect precisely, `KeywordSearcher.index()` hands its
  tokenized corpus to `BM25Okapi`, so `index([])` raises
  `ZeroDivisionError` inside `rank-bm25`, and it names the fix's shape:
  `search()` already handles the empty case, so `index()` should not
  raise either. It names both files, `rag/retriever/keyword_search.py`
  and `tests/unit/test_keyword_search.py`, and it names the finish
  line: remove the `@pytest.mark.xfail` marker for manifest id H-01.
  Estimated effort 2 to 4 hours. No umbrella list, no design debate.
  Pass.
- `unclaimed`: no assignee, no linked PRs, no comments at all. Pass.
- `ai-contributions-allowed`: Path Review is the course's own repo and
  the course workflow is AI-assisted by design, so there is no ban to
  trip over. Pass.

All six required checks pass, so the verdict is accept. On the preferred
checks it takes all three: `reproducible-ask` (expected-versus-actual
plus a named xfail test), `entry-labelled` (`good first issue` and
`tier-1`), and `files-named` (both paths given).

## Check rationale

The four lecture families are each one required check, and I added a
fifth surface and split one family in two, for six required checks
total.

`maintainer-commits` and `maintainer-answers` are separate because they
fail separately. A repo can have daily commits from one person who never
answers an issue, which is exactly the repo where a newcomer's pull
request rots. Commits measure whether anyone is there; first-response
latency measures whether they will look at me. Folding them into one
check lets a fail on the half that matters hide behind a pass on the
half that does not.

Thresholds over adjectives, everywhere I could get a number: 90 days for
commits and pushes, 365 for a release, 30 days for a maintainer reply
and for an outside claim. The 90/365 split is deliberate. A library can
be healthy and not cut a release for most of a year, so release recency
gets the loose bound and commit recency gets the tight one, and
`repo-alive` passes on either.

`unclaimed` is where the Path Review house rule bites. In the wider world
a classmate-style "I'll take this" comment is a real claim; in this
classroom it is not, and several students on one issue is normal. So the
check counts only assignees, open linked PRs, and outside claims a
maintainer acknowledged. That keeps the check meaningful in live mode on
real repos later, without rejecting every popular Path Review issue now.

`ai-contributions-allowed` is the fifth surface, and it is required
rather than preferred because a stated ban is fatal regardless of how
good the issue is. The condition is written narrowly: an outright ban
fails, and disclosure or human-review conditions pass, because treating
every AI clause as a ban would reject most of the repos I will meet.

`unclear` counts as `fail` on required checks. The asymmetry is
intentional. The cost of wrongly rejecting a fine issue is that I pick
the next one on the list; the cost of wrongly accepting one is weeks
spent on work nobody will merge.

## Trade-offs

The strictness is the main one. Six required checks with `unclear` as
`fail` means the rubric rejects issues a more forgiving reader would
take, and it will lose points on any eval bundle where the gold label is
accept but a single signal is genuinely absent from the snapshot. I took
that deliberately: a false accept costs a newcomer far more than a false
reject, and the rubric is honest that it is tuned that way rather than
pretending to be balanced.

The numbers are the second one. 90 days, 365 days, 30 days are defensible
but not derived from anything: they are the bounds that separated the
calibration bundles cleanly. A repo that pushes every 100 days fails
`maintainer-commits` on a technicality it does not deserve, and the
`repo-alive` release-or-push disjunction is the hedge I built for exactly
that. If the full run disagrees on a healthy-but-slow repo, the threshold
is the thing to move, not the check.

Third, `scope-bounded` is the one required check with no number in it,
because the thing it measures does not have one. Effort estimates are not
on most real issues, and a line count would be a guess about a fix I have
not written. So it is a list of disqualifiers drawn from the evidence
guide (umbrella issue, unsettled design debate, maintainer says core
internals, usage question) rather than a threshold. It is the check most
likely to grade differently between two careful readers, and the one I
would rewrite first if the eval disagrees.

Finally, the fit profile in `scope.md` is doing real ranking work here.
#68 and #69 (`Output parser crashes on a top-level JSON array fallback`)
both pass every required check and both take all three preferred ones.
#68 wins on fit: it is retrieval code with a named failing test to
un-xfail, which is exactly the validation-at-the-boundary work I said I
wanted. Fit never rescued or sank a verdict, it only ordered two issues
the rubric had already accepted.
