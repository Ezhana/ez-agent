# Refactoring

## Default Compatibility Assumption

- Refactoring does not carry a backward-compatibility obligation by default.
- Do not preserve historical interfaces, names, structures, or behaviors solely because they already exist.
- Optimize for the intended long-term architecture and coherent responsibilities.
- State this default assumption during design when compatibility could materially affect the solution.

## Refactoring Principles

- Identify the underlying design problem before changing structure.
- Improve responsibility boundaries, dependency direction, cohesion, and clarity.
- Remove obsolete abstractions, duplicated logic, dead paths, and workarounds when they are no longer needed.
- Rename files, types, functions, and variables when existing names no longer reflect their actual semantics.
- Avoid preserving accidental architecture through compatibility wrappers or aliases unless there is a concrete requirement.
- Avoid combining unrelated refactoring with feature changes unless the relationship is necessary and agreed upon.

## Breaking Changes

- Identify affected callers, integrations, stored data, public interfaces, and deployment boundaries as applicable.
- Explain the nature and likely impact of a breaking change before implementation when it is material.
- Do not add compatibility layers by default to conceal a deliberate design change.
- If compatibility is genuinely required, clarify who or what requires it, for how long, and what the removal strategy is.

## Verification

- Apply the default verification policy in `implementation.md`.
- Use type checking by default and consider compilation/build checks according to the scope and impact.
- Do not perform manual functional walkthroughs by default.
- Be explicit about migration and runtime behavior that has not been verified.
