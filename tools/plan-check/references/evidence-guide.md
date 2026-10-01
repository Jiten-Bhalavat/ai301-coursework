# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

**Where it lives:**
- In an eval bundle: The "Diagnosis" section of the Candidate plan, read against the "Repro evidence" section (which contains the reproduction steps, artifacts, and control runs).
- In live mode: The student's plan.md diagnosis section, read against their posted repro comment on the issue thread.

**What good looks like:**
- The diagnosis explains the specific behavior shown in the repro evidence
- If the repro has control runs (e.g., "same command without flag X works"), the diagnosis involves the factor the control isolated
- The diagnosis does NOT contradict control runs or artifacts in the repro evidence
- Example: if repro shows "width 2 works, width 1 crashes", diagnosis involves the width-dependent code path

**Red flags (wrong-cause):**
- Diagnosis blames component A, but repro control shows A works fine
- Diagnosis ignores contradicting evidence (e.g., control run that rules out the blamed component)
- Confident diagnosis that doesn't explain all the repro observations

## Scope

**Where it lives:**
- In an eval bundle: The "Scope" section of the Candidate plan, including "In scope" and "Not in scope" lines, plus the "Files" section.
- In live mode: The plan.md scope and files sections.

**What good looks like:**
- ONE bounded change that addresses the issue
- Explicit "Not in scope" line excluding tangential work
- Named files (not "somewhere in the codebase")
- No bundled refactors, migrations, or while-in-the-area improvements

**Red flags (scope-creep):**
- Fix bundled with a redesign, migration, or architecture rework
- Multiple unrelated changes in one plan
- "While I'm in there, I'll also..." additions
- The actual fix is buried inside a larger campaign

## Executability

**Where it lives:**
- In an eval bundle: The "Files" and "Approach" sections of the Candidate plan, plus any "Order of work" or numbered steps.
- In live mode: The plan.md files, approach, and steps sections.

**What good looks like:**
- Specific files named (e.g., `src/printer.rs`, not "the printer module")
- Concrete approach (e.g., "add saturating_sub at line 934", not "investigate the issue")
- A stranger could start working without asking the author
- Order of work is clear enough to begin

**Red flags (unbuildable):**
- No files named
- Approach is "investigate" or "poke around"
- Key decisions deferred to build time ("whichever is easier", "not sure yet")
- "Profile and optimize" with no chosen approach

## Test plan

**Where it lives:**
- In an eval bundle: The "Test plan" section of the Candidate plan, read against the Repro evidence section.
- In live mode: The plan.md test plan section, read against the posted repro comment.

**What good looks like:**
- Names a specific observable outcome (exit code, output content, behavior change)
- References the repro evidence's steps or artifacts
- "Re-run the repro command, expect exit 0" is decisive
- "Add a regression test with input X expecting output Y" is decisive

**Red flags (unbuildable/vague):**
- "Run the test suite" with no specific outcome
- "Nothing else should break" 
- "Should feel faster" with no measurement
- No observable tied to the fix

## Honesty

**Where it lives:**
- In an eval bundle: Any "Risks", "Unknowns", or "Deviation" sections in the Candidate plan, or their absence.
- In live mode: Same sections in plan.md.

**What good looks like:**
- Genuine uncertainties stated explicitly ("other underflow sites may exist")
- "I'll note anything suspicious in the PR" is honest
- Deviations from original plan are recorded with reasons
- Absence of unknowns section is fine if the plan is straightforward

**Red flags:**
- False confidence ("this will definitely fix it") on uncertain diagnosis
- Hidden uncertainties ("not sure" buried in confident prose)
- Deviations that exist in the diff but aren't recorded in the plan

## Comms

**Where it lives:**
- In an eval bundle: The "Candidate plan comment" section, read against "Thread highlights" and "Repo facts" (contribution policy).
- In live mode: The draft plan comment, read against the live issue thread and repo's CONTRIBUTING.md.

**What good looks like:**
- If thread has maintainer direction (culprit identified, testing requested), comment engages it
- If repo requires AI disclosure, comment includes disclosure
- Comment is specific to the issue, not boilerplate

**Red flags (thread-convention):**
- Thread has explicit maintainer direction that the comment ignores
- Repo requires AI disclosure but comment has none
- Generic boilerplate that could apply to any issue
