# Plan: Fix output parser crash on top-level JSON array fallback

Issue: https://github.com/codepath/pathreview-ai301-fa26-s3/issues/69

## Diagnosis

The crash occurs in `_parse_json_output` at `rag/generator/output_parser.py:68`. When the LLM returns a top-level JSON array instead of an object, `json.loads()` successfully parses it into a Python `list`. The function then calls `data.items()` assuming `data` is a `dict`, raising `AttributeError: 'list' object has no attribute 'items'`.

The repro evidence confirms this:
- Direct call with `json.dumps(['First feedback item', 'Second feedback item'])` raises `AttributeError` at line 68
- Control with a JSON object (`{'summary': 'Good work'}`) parses correctly and returns `FeedbackSection` objects
- The existing `test_json_array_fallback` test is marked `@pytest.mark.xfail` for this exact behavior (manifest H-02)

## Scope

**In scope:**
- Add type checking in `_parse_json_output` to handle `list` input alongside `dict` input
- Transform list elements into `FeedbackSection` objects (supporting both string and object elements)
- Remove the `@pytest.mark.xfail` marker from `test_json_array_fallback`

**Not in scope:**
- Changing the JSON extraction logic in `parse_review_output`
- Modifying the `FeedbackSection` dataclass
- Adding new test cases beyond removing the xfail marker

## Files

- `rag/generator/output_parser.py` (add `isinstance(data, list)` branch in `_parse_json_output`)
- `tests/unit/test_output_parser.py` (remove `@pytest.mark.xfail` decorator from `test_json_array_fallback`)

## Approach

1. In `_parse_json_output`, add an `isinstance(data, list)` check before the existing `for key, value in data.items()` loop
2. When `data` is a list, iterate through elements and convert each to a `FeedbackSection`:
   - String elements become `FeedbackSection(section_name='feedback', content=element, ...)`
   - Object elements are processed like the existing dict handling
3. Remove the `@pytest.mark.xfail` decorator from `test_json_array_fallback`

## Test plan

1. Run the direct reproduction command:
   ```bash
   .venv\Scripts\python -c "import json; from rag.generator.output_parser import parse_review_output; print(parse_review_output(json.dumps(['First feedback item', 'Second feedback item'])))"
   ```
   **Expected:** Returns a list of `FeedbackSection` objects, exit 0 (instead of `AttributeError`)

2. Run the existing test without xfail:
   ```bash
   .venv\Scripts\pytest tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback -v
   ```
   **Expected:** PASSED (not XFAIL)

3. Run the full output parser test suite:
   ```bash
   .venv\Scripts\pytest tests/unit/test_output_parser.py -v
   ```
   **Expected:** All tests pass, no regressions

## Risks and unknowns

- The exact structure of array elements varies (strings vs objects). The fix should handle both gracefully.
- Other code paths in `parse_review_output` (e.g., the JSON-in-fence branch at line 41) also call `_parse_json_output`, so the fix will apply there too.
