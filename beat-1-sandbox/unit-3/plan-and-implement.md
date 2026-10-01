# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

Jiten-Bhalavat

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/69#issuecomment-5923196037

Following up on my reproduction, here's my plan for the fix:

**Diagnosis:** The crash is at `_parse_json_output` line 68 where `data.items()` is called. When `json.loads` returns a list (from a top-level JSON array), calling `.items()` raises `AttributeError`. My repro confirmed: object input works, array input crashes at the same line.

**Fix:** Add an `isinstance(data, list)` check in `_parse_json_output` before the dict-handling loop. List elements get converted to `FeedbackSection` objects (strings become content, objects are processed like the existing dict handling).

**Files:** `rag/generator/output_parser.py`, `tests/unit/test_output_parser.py` (remove xfail marker)

**Test:** Re-run my repro command expecting a list of `FeedbackSection` objects and exit 0, then run `test_json_array_fallback` expecting PASSED instead of XFAIL.

I'll build this on branch `fix/69-json-array-fallback` and report back.

I used Claude to help draft this comment.

---

## Your branch

**Branch**

fix/69-json-array-fallback

**Evidence**

Before (from my Unit 2 reproduction):
```
$ .venv\Scripts\python -c "import json; from rag.generator.output_parser import parse_review_output; parse_review_output(json.dumps(['First feedback item', 'Second feedback item']))"
Traceback (most recent call last):
  File "<string>", line 1, in <module>
  File "rag/generator/output_parser.py", line 48, in parse_review_output
    return _parse_json_output(data)
  File "rag/generator/output_parser.py", line 68, in _parse_json_output
    for key, value in data.items():
AttributeError: 'list' object has no attribute 'items'
```

After (on fix/69-json-array-fallback branch):
```
$ .venv\Scripts\python -c "import json; from rag.generator.output_parser import parse_review_output; print(parse_review_output(json.dumps(['First feedback item', 'Second feedback item'])))"
[FeedbackSection(section_name='feedback', content='First feedback item', confidence=0.85, suggestions=[]), FeedbackSection(section_name='feedback', content='Second feedback item', confidence=0.85, suggestions=[])]
```

Test run:
```
$ .venv\Scripts\pytest tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback -v
tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback PASSED
```

---

## Eval iterations

**Run history**

1. 19/20 — First full run with the rubric covering diagnosis grounding, scope bounding, executability, decisive test plan, unknowns, AI disclosure, and thread engagement.

**Package analysis**

pkg-14 (gold: accept, rubric: reject). My rubric rejected this package on `executable-by-stranger` because the plan describes a "reattach handshake fix" but the approach section lacks specific line numbers or code changes a stranger could start implementing. The gold label accepts it because the plan names specific files, describes the fix approach (reattach handshake), and defers the Windows variant honestly. My `executable-by-stranger` check may be too strict about requiring line-level specificity when the approach is conceptually clear.

**Check rationale**

```
| diagnosis-grounded | The plan's stated cause read against the repro evidence's artifacts and control runs | The diagnosis explains the behavior the repro evidence shows, and does NOT contradict any control run in the repro evidence. If the repro shows a control where removing X makes the bug disappear, the diagnosis must involve X. If the diagnosis blames component A but the repro evidence rules A out (e.g., control run shows A works fine), the check fails. | required |
```

This check is the most important for catching wrong-cause packages. I designed it to directly compare the plan's diagnosis against the repro evidence's control runs. Packages like pkg-01 and pkg-07 confidently blame one component, but their own repro evidence contains control runs that rule that component out. The check forces the grader to verify that the diagnosis explains all observations, not just the failing case.

**Trade-offs**

The `executable-by-stranger` check rejects pkg-14 (gold: accept) because it expects more specificity than the gold standard requires. A plan that names files and describes the conceptual fix should arguably pass even without line numbers. Making the check more lenient risks accepting truly unbuildable plans like pkg-10 ("profile and optimize" with no chosen approach). I accept this trade-off: 19/20 passes the bar, and pkg-14's borderline executability is a defensible edge case.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
