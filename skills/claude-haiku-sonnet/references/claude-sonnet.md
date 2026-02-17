# Claude Sonnet Profile

## Use profile when
- Higher reasoning quality or synthesis depth is required.
- The task has tradeoffs, edge cases, or policy constraints.

## Prompt design rules
- Keep structure explicit, but permit deeper analysis.
- Include evaluation criteria and failure modes.
- Ask for stepwise internal decomposition only when needed for reliability.
- Preserve strict output schema for downstream automation.
- Include brief edge-case guidance where ambiguity is expected.

## Recommended template

```text
Role: You are a domain expert delivering decision-grade output.
Task: <objective + decision/use-case>
Context:
- <fact 1>
- <fact 2>
Constraints:
- Prioritize correctness over verbosity.
- State uncertainty explicitly.
- Do not invent missing facts.
Output format:
<explicit schema>
Quality bar:
- Covers core case and key edge cases
- Explains tradeoffs briefly
- Actionable recommendations
```

## Anti-patterns
- Overly open-ended style prompts without success criteria.
- Hidden assumptions not present in context.
- Output formats that mix prose and structured data unpredictably.
