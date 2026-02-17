# Claude Haiku Profile

## Use profile when
- Throughput and latency matter more than nuanced analysis.
- Tasks are repetitive, structured, or transformation-oriented.

## Prompt design rules
- Keep instructions linear and compact.
- Prefer one output schema and one primary objective.
- Keep context minimal; remove narrative detail.
- Use hard limits (word count, item count, strict fields).
- Provide a single short example only when format errors are likely.

## Recommended template

```text
Role: You are a precise task executor.
Task: <single objective>
Context: <essential inputs only>
Constraints:
- Follow all fields exactly.
- Do not add extra sections.
- Keep output under <limit>.
Output format:
<explicit schema>
Quality bar:
- Correct facts
- Complete required fields
- No extra commentary
```

## Anti-patterns
- Multi-goal prompts with competing priorities.
- Long background sections.
- Vague output requests like “be detailed but concise.”
