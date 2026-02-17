# AAS Submodel Template Grounding (for Prompt/Task Design)

Use this reference when building prompts that create, review, or transform AAS Submodel Templates.

## Core facts to enforce in prompts

- A submodel template is distinguished by modelling kind: `Submodel/kind = Template`.
- `ModellingKind` differentiates `Template` vs `Instance`; default kind is `Instance`.
- `Submodel/semanticId` is the key semantic anchor for validation and interoperability.
- `administration/templateId` identifies the template used to guide creation, but is not the primary validation anchor.

## Constraints to include when relevant

- If any `SubmodelElement/qualifier` has `Qualifier/kind = TemplateQualifier`, that element shall be part of a submodel template (AASd-129).
- Keep `idShort` handling explicit:
  - `idShort` is mandatory for referables except direct children of `SubmodelElementList` (AASd-117).
  - `idShort` must be unique in namespace for non-identifiable referables (AASd-022).
- For `SubmodelElementList`, preserve list constraints where used (AASd-107/108/109/114/115).

## Prompt pattern for template generation

Use this schema-oriented pattern:

```text
Role: You are an AAS metamodel specialist.
Task: Generate a Submodel Template skeleton for <domain>.
Context:
- Follow AAS v3.1 semantics for template/instance distinction.
- Use semantic IDs for submodel and template elements.
Constraints:
- Set Submodel/kind to Template.
- If TemplateQualifier is used, keep elements within template context (AASd-129).
- Keep idShort constraints valid (AASd-117, AASd-022).
- Do not invent external concept IDs; mark unknown IDs as TODO placeholders.
Output format:
- JSON object with fields: submodel, elements, qualifiers, validation_notes.
Quality bar:
- Constraint-aware
- Semantically explicit
- Ready for downstream validation/review
```

## Anti-patterns

- Treating `templateId` as equivalent to `semanticId`.
- Generating template-like structures with `Submodel/kind = Instance`.
- Using `TemplateQualifier` without ensuring template context.
- Producing free-form prose when downstream automation expects structured JSON.
