# Search strategy: where your scout looks, and why

## Queries

```bash
# Python RAG and retrieval issues - traces to "retrieval pipelines, RAG"
gh search issues --label "good first issue" --language python --state open --limit 50 --json title,repository,labels,assignees,commentsCount,updatedAt,url "RAG OR retrieval OR embedding"

# Python parsing and validation issues - traces to "input validation and edge-case handling"
gh search issues --label "good first issue" --language python --state open --limit 50 --json title,repository,labels,assignees,commentsCount,updatedAt,url "parser OR parsing OR validation"

# Python test issues - traces to "writing tests that actually pin the behaviour"
gh search issues --label "good first issue" --language python --state open --limit 50 --json title,repository,labels,assignees,commentsCount,updatedAt,url "test OR pytest"

# FastAPI issues - traces to "FastAPI services around them"
gh search issues --label "good first issue" --language python --state open --limit 50 --json title,repository,labels,assignees,commentsCount,updatedAt,url repo:tiangolo/fastapi

# LLM/agent framework issues - traces to "LLM and agent systems"
gh search issues --label "good first issue" --language python --state open --limit 30 --json title,repository,labels,assignees,commentsCount,updatedAt,url repo:langchain-ai/langchain OR repo:run-llama/llama_index
```

## Ranking filters

Applied in order to the combined, deduplicated results:

1. **Drop any result with an assignee** - someone else is already working on it
2. **Drop any result not updated in the last 90 days** - stale issues are likely abandoned or outdated
3. **Drop any result with more than 10 comments** - high comment count often signals design debates or complex history
4. **Prefer issues that mention specific files** - traces to "rank an issue higher when it names the exact files to touch"
5. **Prefer issues from repos with recent activity** - updatedAt within 30 days indicates active maintenance
6. **Prefer fewer comments over more** - simpler, cleaner scope
7. **Tie-break: alphabetically by repository name** - deterministic ordering for reproducibility

## How many to grade

Grade the top **5** ranked results per scan.

Five candidates balance coverage against cost (~$1 per scan). If no good candidates emerge after multiple scans, I will revise the queries or ranking filters rather than increase the count.
