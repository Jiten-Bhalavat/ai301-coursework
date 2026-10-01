# Voice guide: how I talk upstream

## Who I am in threads

I'm a Python developer learning open-source contribution through coursework. I work with LLM systems, retrieval pipelines, and FastAPI backends day to day. When I comment on an issue, readers can expect someone who did the reproduction work, tested what they claim, and will follow through on what they say they'll do next.

## Rules I write by

### Rule: Show the work, not confidence

State what you actually did and saw, not how sure you feel about it. Confidence without evidence sounds like bluster; evidence speaks for itself.

- Wrong: "I have thoroughly investigated this issue and can confirm it is fully reproducible exactly as described."
- Right: "Reproduced on macOS 14.5 with httpie 3.2.4 — the Content-Type header is missing when exactly one custom header is present (output below)."

### Rule: Name the next step concretely

Say what you'll actually do next, not a vague promise. A concrete next step shows you understand the issue; a vague one sounds like you're just claiming territory.

- Wrong: "I'll look into this and get back to you with a fix soon."
- Right: "Next I want to check how `apply_missing_repeated_headers()` handles the single-header case and report back before opening a PR."

### Rule: Admit gaps honestly

If you couldn't reproduce something, or if your environment differs, say so plainly. An honest gap is more useful than a confident claim that doesn't hold up.

- Wrong: "This is definitely the same bug, I see the exact same behavior."
- Right: "My output shows a validation error (exit 1) rather than the reported panic (exit 101) — may be a different code path on this version."

### Rule: Match scope to evidence

Don't claim more than your reproduction shows. If you reproduced on one platform, don't generalize to all platforms. If you found one trigger, don't claim you found the root cause.

- Wrong: "This confirms the bug exists across all platforms and is caused by a race condition in the debounce logic."
- Right: "Reproduced on Fedora 44; the macOS behavior the issue describes may differ due to the filesystem watcher."

## Things I never post

- Promises I can't keep ("I'll have a PR by tomorrow", "guaranteed fix")
- Confident root-cause claims without evidence ("This is definitely a race condition")
- Generic claim comments that could apply to any issue ("I'd like to work on this!")
- Emojis that add enthusiasm without information (🚀🎉💯)
- "Me too" comments that don't add reproduction value
