# Evidence Guide: where to find what

This guide names the evidence families and where to find them for each check.

## Evidence families

### 1. plan-family

**Where**: The plan file (plan.md or equivalent), including any deviation notes

**Checks served**:
- diff-matches-plan: read the plan's in-scope and not-in-scope lists, and any deviation notes
- test-evidence-decisive: read the plan's test plan section
- deviation-honest: read the plan's deviation notes if present

**What to extract**:
- The list of files explicitly named as in-scope
- The list of files or patterns explicitly named as not-in-scope
- The test plan's stated steps and expected outcome
- Any deviation notes explaining changes from the plan

### 2. diff-family

**Where**: The diff block (git diff main...HEAD or equivalent)

**Checks served**:
- diff-matches-plan: the changed files list
- description-matches-diff: the actual changes
- diff-reviewable: every hunk, looking for debris

**What to extract**:
- The complete file list of changed files
- Whether changes are additions, deletions, or modifications
- Any debris: debug prints, commented code, unrelated edits, formatting-only changes
- Commit messages if visible in the package

### 3. description-family

**Where**: The PR title and description block

**Checks served**:
- description-matches-diff: the claims about what the PR does
- template-satisfied: the presence of required sections
- ai-disclosed: the disclosure statement if required

**What to extract**:
- The summary of what the PR claims to do
- Any claims about specific files or behaviors
- Completed or missing template sections
- Disclosure statements

### 4. evidence-family

**Where**: The test-evidence block

**Checks served**:
- test-evidence-decisive: the before/after demonstration
- repo-checks-run: mention of test suite execution

**What to extract**:
- The reproduction steps that were re-run
- The before state (showing the bug)
- The after state (showing the fix)
- Test suite output or CI status
- Whether the evidence exercises the fix or an unchanged path

### 5. repo-facts-family

**Where**: The repo-facts block or metadata

**Checks served**:
- template-satisfied: required PR template sections
- ai-disclosed: contribution policy on AI disclosure
- repo-checks-run: test suite expectations

**What to extract**:
- Any stated PR template requirements
- The contribution policy's stance on AI disclosure
- The repo's test suite (if named)

## Cross-referencing

Several checks require reading across families:

- **diff-matches-plan**: diff-family ↔ plan-family
- **description-matches-diff**: description-family ↔ diff-family
- **test-evidence-decisive**: evidence-family ↔ plan-family
- **template-satisfied**: description-family ↔ repo-facts-family
- **ai-disclosed**: description-family ↔ repo-facts-family
- **deviation-honest**: plan-family ↔ diff-family

Always extract from both families before grading these checks.
