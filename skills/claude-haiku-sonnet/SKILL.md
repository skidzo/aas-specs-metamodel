---
name: claude-haiku-sonnet
description: Generate and adapt prompts, instructions, and output schemas for Anthropic Claude models with profile-aware guidance for Claude Haiku and Claude Sonnet, with a built-in workflow for Asset Administration Shell (AAS) Submodel Template creation. Use when a user asks for Claude-compatible prompts, Haiku vs Sonnet prompt tuning, or prompt/tooling templates to design or review AAS Submodel Templates.
---

# Claude Haiku/Sonnet Prompt Engineering for AAS Submodel Templates

Use this skill to produce robust prompts for Claude Haiku, Claude Sonnet, or both, especially for AAS submodel-template tasks.

## 1) Select execution profile

Infer or ask for one of:
- `haiku` for throughput, low latency, or bulk transformation.
- `sonnet` for deeper synthesis, tradeoff analysis, and stricter review.
- `both` for one prompt that must run reliably on both models.

If unspecified, default to `both`.

## 2) Load only needed references

- Read `references/claude-haiku.md` for Haiku-specific controls.
- Read `references/claude-sonnet.md` for Sonnet-specific controls.
- For AAS Submodel Template work, read `references/aas-submodel-templates.md`.

For dual-model compatibility, apply the strict intersection: explicit structure, deterministic output schema, no ambiguous optional branches.

## 3) Build prompts with fixed sections

Always emit these sections in order:
1. **Role** — one sentence.
2. **Task** — objective and done criteria.
3. **Context** — only required facts and source constraints.
4. **Constraints** — forbidden actions and domain rules.
5. **Output format** — machine-checkable (JSON preferred for template generation).
6. **Quality bar** — concise checks.

## 4) Apply AAS-specific grounding (when applicable)

For submodel-template tasks:
- Require `Submodel/kind = Template`.
- Require explicit semantic references (`semanticId`) for submodel and relevant elements.
- Treat `administration/templateId` as informative provenance, not a validation substitute for `semanticId`.
- If `Qualifier/kind = TemplateQualifier` is used on a submodel element, ensure that element belongs to a submodel template.
- Ask for explicit handling of cardinalities and optional vs mandatory elements.

## 5) Add model-specific controls

- Haiku: minimize branching instructions, keep context compact, and force a single output path.
- Sonnet: allow deeper decomposition and review checks while preserving strict final schema.

## 6) Return deliverables

Return:
- `unified` prompt (works for both models), unless user asks for only one profile.
- Optional `haiku-optimized` and/or `sonnet-optimized` variant.
- A short “Why this works” note.

## 7) Validation checklist

Before finalizing, verify:
- No conflicting instructions.
- Output schema is explicit and testable.
- Prompt is self-contained and cites provided sources when requested.
- AAS rules for template semantics and qualifier usage are respected.
