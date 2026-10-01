# Evidence guide: where proof lives in a reproduction package

## Environment

**Where it lives:**
- In an eval bundle: The repro report's first paragraph or a clearly labeled "Environment:" line. Look for OS name, tool version, runtime version.
- In live mode: The student's draft repro comment, same locations.

**What good looks like:**
- Names the OS with enough specificity to matter (macOS 14.5, Fedora 44, Windows 11)
- Names the exact tool version being tested (bat 0.26.1, httpie 3.2.4, pandas 2.2.0)
- For libraries/frameworks, includes the runtime version (Python 3.12.4, Node 20.11.0)
- For issues where build configuration matters, includes that too (release vs debug, cargo vs package manager)

**Red flags:**
- No environment section at all
- "Latest version" without a number
- OS missing entirely on a platform-specific issue

## Steps

**Where it lives:**
- In an eval bundle: The repro report's numbered steps or command sequence, usually after the environment line.
- In live mode: The student's draft repro comment.

**What good looks like:**
- Starts from a reachable state: "With a clean install" or "In an empty directory" or "After running the setup from the README"
- Every command is shown, not summarized ("Run the test" → "`pytest tests/test_parser.py::test_array_fallback`")
- File contents are shown inline or as minimal reproducible snippets, not "use your config file"
- Does not require access to private repos, monorepos, or unshared configs

**Red flags:**
- "Set up the project" with no commands
- References to private repositories or configs a stranger cannot access
- Missing the actual trigger command (setup shown, but not the failing invocation)
- "Same as the issue" without showing the steps

## Behavior shown

**Where it lives:**
- In an eval bundle: The repro report's output blocks, error excerpts, or screenshot descriptions. Look for fenced code blocks after the steps.
- In live mode: The student's draft repro comment, same locations.

**What good looks like:**
- The artifact (output, error, log excerpt) shows the SAME symptom the issue describes
- If the issue says "panic with capacity overflow (exit 101)", the artifact shows that panic and exit code
- If the issue says "Content-Type header missing", the artifact shows the headers without Content-Type
- The artifact is the proof, not the narrator's claim about it

**Red flags (wrong-target):**
- Issue describes exit 101 panic, artifact shows exit 1 validation error
- Issue describes crash, artifact shows the program still running
- Issue describes missing header, artifact shows a different error
- Syntax error in reproduction command (wrong operator, wrong argument) producing a different failure mode
- Testing on a completely different version without acknowledging the gap

**How to check:**
1. Read the issue's described behavior carefully
2. Read the artifact in the repro report
3. Ask: does this artifact show THAT behavior, or something adjacent?

## Honesty

**Where it lives:**
- In an eval bundle: The repro report's conclusion sentences ("confirmed", "could not reproduce", "reproduced on X but not Y") read against its own artifacts.
- In live mode: Same.

**What good looks like:**
- The stated outcome matches what the artifacts show
- "Confirmed the crash" when the artifact shows a crash
- "Could not reproduce" with a real attempt shown, naming what differed
- "Partially reproduced" with specifics about what worked and what didn't
- Humble accuracy: "The output shows X, which matches the report"

**Red flags:**
- "Guaranteed reproducible" with no artifacts
- "Confirmed exactly as described" but the artifact shows different behavior
- Confident root-cause diagnosis with no shown evidence
- "Fully verified" backed by nothing

## Comms

**Where it lives:**
- In an eval bundle: The claim comment and repro report; the Repo facts section for contribution policy.
- In live mode: The student's draft comments; the repo's CONTRIBUTING.md or AI_POLICY.md.

**What good looks like for claim comments:**
- Specific intent: names what was done (reproduced, investigated), what will be done next
- Shows understanding of the issue (mentions the actual behavior, affected code path, or relevant files)
- Modest and honest about scope ("as a first contribution", "I want to check X")

**Red flags for claim comments:**
- Pure "+1" or "me too" with no intent to contribute
- Generic "I'll take this" or "assigning myself" without specifics
- Over-promising ("I'll fix this in 2 days", "guaranteed")
- Boilerplate that could apply to any issue

**AI disclosure:**
- Check the Repo facts for contribution policy
- If policy says "must disclose AI usage", "state the tool used", or similar mandatory language, the comments must include disclosure
- If policy is silent or says "AI welcome" without disclosure requirement, this passes
- Course packages are treated as AI-assisted work, so disclosure requirements apply

**What disclosure looks like:**
- "I used Claude to help draft this reproduction" 
- "AI-assisted investigation, all steps verified manually"
- A note in the comment acknowledging AI assistance
