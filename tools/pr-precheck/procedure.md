# Procedure: how to grade a PR package

## Phase 1: Setup

1. Detect mode: if `packages/` folder exists, this is eval mode; otherwise live mode.
2. In live mode only:
   - Read `scope.md` first. If the `Repo:` line is unfilled, stop and tell the user.
   - Read `voice-guide.md` and note its rules for later.
3. In eval mode, ignore `scope.md` and `voice-guide.md` entirely.
4. Read `rubric.md` to load the checks and verdict rule.
5. Read `references/evidence-guide.md` to know where each evidence family lives.

## Phase 2: Gather evidence (per package)

For each package (one in live mode, one at a time in eval mode):

### 2a. Extract the plan-family

- Locate the plan content (plan.md or plan block in bundle)
- Extract: in-scope file list, not-in-scope patterns, test plan steps and expected outcome, deviation notes if any
- Record extracted facts

### 2b. Extract the diff-family

- Locate the diff content (git diff or diff block in bundle)
- Extract: changed file list, nature of changes, any debris (debug prints, commented code, formatting-only hunks, wip commits)
- Record extracted facts

### 2c. Extract the description-family

- Locate the PR title and description
- Extract: claims about what the PR does, template sections, disclosure statements
- Record extracted facts

### 2d. Extract the evidence-family

- Locate the test-evidence block
- Extract: reproduction steps re-run, before state, after state, test suite mentions
- Record extracted facts

### 2e. Extract the repo-facts-family

- Locate the repo-facts or metadata block
- Extract: PR template requirements, contribution policy on AI disclosure, test suite info
- Record extracted facts

## Phase 3: Grade each check

For each check in the rubric:

1. Identify which evidence families the check needs (see evidence-guide.md)
2. Retrieve the extracted facts from those families
3. Apply the check's pass condition to the facts
4. Assign: pass, fail, or unclear
5. Record the specific fact or quote that decided the grade

### Specific check logic

**diff-matches-plan**:
- List files in diff
- List files in plan's in-scope
- For each diff file: is it in-scope OR covered by deviation note?
- For each plan file: is it in diff OR covered by deviation note?
- Any silent addition or omission → fail

**description-matches-diff**:
- Read what description claims
- Read what diff actually does
- Do claims match reality? No overclaiming, no underclaiming
- Claims of "exactly as planned" with silent drift → fail

**test-evidence-decisive**:
- Read plan's test plan (steps + expected outcome)
- Read test-evidence block
- Does evidence show the same steps with before/after?
- Does it exercise the actual fix, not an unchanged path?
- "Tests pass" without specific demonstration → fail

**repo-checks-run**:
- Read repo-facts for test suite info
- Read test-evidence for test suite execution
- If repo has tests and evidence doesn't show them run → fail
- If no test suite mentioned → pass by default

**diff-reviewable**:
- Scan diff for debris: debug prints, commented code, dead functions, formatting-only hunks, unrelated edits
- Check commit messages for "wip" or meaningless text
- Minor debris (one commented line) → may pass
- Diff buried in churn → fail

**template-satisfied**:
- Read repo-facts for PR template requirements
- Read description for those sections
- Missing required sections or placeholder text → fail
- No template requirements → pass

**ai-disclosed**:
- Read repo-facts for contribution policy on AI
- If disclosure required, check description for disclosure
- Course packages are AI-assisted → disclose if required
- Policy silent or permissive → pass

**deviation-honest**:
- If no deviation notes → compare diff to plan directly
- If deviation notes exist → do they match actual diff?
- Deviation notes that misrepresent the diff → fail

## Phase 4: Render verdict

1. Apply the verdict rule from rubric.md
2. Treat unclear as fail for required checks
3. Verdict is accept (all required pass) or reject (any required fail)

## Phase 5: Output

1. Write a per-check summary: check name, grade, one-line evidence
2. In live mode: note any voice-guide violations
3. End with the fenced JSON block containing item, checks array, and verdict

## Edge cases

- **Empty diff**: A PR with no changes is not ready → reject
- **Missing blocks**: If a required block (plan, diff, description, test-evidence) is missing → checks depending on it are unclear → fail
- **Ambiguous scope**: If plan's scope is vague ("relevant files"), note the ambiguity in diff-matches-plan
- **No test plan**: If plan has no test plan section, test-evidence-decisive cannot be graded → unclear → fail
