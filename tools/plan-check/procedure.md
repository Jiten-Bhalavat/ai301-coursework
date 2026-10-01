# Procedure: how this skill grades a plan package

## Read order

1. **Repro evidence first**: Read the "Repro evidence" section completely before reading the plan. Note:
   - What behavior the reproduction demonstrates (the bug symptom)
   - What control runs exist and what they isolate (e.g., "without flag X, it works")
   - What artifacts are shown (exit codes, output, errors)
   
   The repro evidence is the ground truth the plan must explain. Reading it first prevents the plan's diagnosis from coloring how you interpret the evidence.

2. **Issue context second**: Read the "Issue" section to understand what the reporter claims and what the thread highlights contain. Note any maintainer direction (culprit identified, testing requested, approach suggested).

3. **Repo facts third**: Read the "Repo facts" section. Note the contribution policy, especially any AI-disclosure requirements.

4. **Candidate plan fourth**: Read the plan's sections in order: Diagnosis, Scope, Files, Approach, Test plan, Risks/Unknowns. For each section, mentally check it against the repro evidence you already know.

5. **Candidate plan comment last**: Read the comment. Check it against the thread highlights and repo facts you noted.

## Evidence gathering

For each evidence family, gather as follows:

**Diagnosis grounding**: 
- From repro evidence: list each control run and what it rules in/out
- From plan: extract the stated cause
- Compare: does the diagnosis explain the repro artifacts without contradicting controls?

**Scope**:
- From plan: extract in-scope statement, not-in-scope statement, files list
- Count: how many distinct changes does the plan propose?
- Check: is there bundled work beyond the fix?

**Executability**:
- From plan: extract files, approach, order of work
- Test: could a stranger start working from this without asking questions?

**Test plan**:
- From plan: extract the test plan
- From repro evidence: recall the reproduction steps/artifacts
- Check: does the test plan name a specific observable tied to the fix?

**Honesty**:
- From plan: check for risks/unknowns section, deviation section
- Check: are uncertainties stated or hidden?

**Comms (thread + disclosure)**:
- From thread highlights: any maintainer direction?
- From repo facts: any AI-disclosure requirement?
- From plan comment: does it engage direction? does it disclose if required?

## Check execution

Execute checks in this order (dependencies flow down):

1. **diagnosis-grounded**: Must be checked first because scope and test plan assume a correct diagnosis. Compare the plan's stated cause against each control run in the repro evidence. If any control contradicts the diagnosis, fail immediately.

2. **scope-bounded**: Check after diagnosis is validated. A correct diagnosis with unbounded scope still fails.

3. **executable-by-stranger**: Check after scope is validated. Count whether files are named, approach is concrete, order is clear.

4. **test-plan-decisive**: Check against the repro evidence. Does the test plan name an observable outcome?

5. **unknowns-stated**: Quick scan for false confidence or missing uncertainty acknowledgment.

6. **ai-disclosed**: Check repo facts for disclosure requirement, then check plan comment for disclosure.

7. **engages-thread**: Check thread highlights for maintainer direction, then check plan comment for engagement.

8. **deviation-recorded** (preferred): Only if the plan has a deviation section.

**When evidence is absent**: If the evidence for a check is genuinely absent (e.g., no test plan section exists), grade `unclear`. Do not invent evidence.

**When evidence is ambiguous**: Grade based on what's written, not what might have been intended. A vague test plan is a fail, not an unclear.

## Verdict assembly

1. Collect all check grades: pass, fail, or unclear.

2. Apply the verdict rule from the rubric:
   - Accept if ALL required checks are `pass`
   - Reject if ANY required check is `fail` or `unclear`
   - Preferred checks do not affect the verdict

3. For the output:
   - List each check with its grade and one-line evidence quote
   - For the deciding check (the one that caused reject, or the last required check for accept), quote the specific evidence that decided it
   - Emit the verdict: `accept` or `reject`

4. The JSON block must contain:
   - `item`: the issue URL or bundle id
   - `checks`: array of {name, grade, evidence} for each check
   - `verdict`: "accept" or "reject"
