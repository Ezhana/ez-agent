# Technical Design

## Design Objectives

- Solve the underlying problem rather than only making the visible symptom disappear.
- Optimize for clear responsibilities, explicit dependencies, coherent boundaries, and long-term maintainability.
- Prefer the simplest design that adequately satisfies the real requirements.
- Avoid unnecessary abstraction, duplicated business logic, excessive indirection, and overengineering.

## Responsibility and Layer Boundaries

- Give each layer and module a clearly defined responsibility.
- Keep dependencies explicit and direct them toward appropriate abstractions or stable contracts.
- Avoid placing responsibilities in a layer merely because it is the easiest place to make a feature work.
- Do not compensate for missing lower-level capabilities by accumulating workarounds in higher layers.
- When an upper-layer requirement depends on a missing lower-level capability, evaluate and discuss implementing that capability at the appropriate layer.
- Keep integration, orchestration, presentation, and core business logic in their appropriate boundaries.

## Avoid Patch-based Design

- Do not stack special cases, fallback paths, duplicated transformations, or conditional branches to hide a structural problem.
- Before adding a workaround, identify why the existing design cannot support the requirement.
- Prefer correcting the responsible abstraction or capability over introducing another layer of exceptions.
- A workaround may be justified by a genuine external constraint, but make the constraint, trade-off, and expected lifetime explicit.

## Design Discussion

Before implementation, establish as applicable:

1. The problem being solved and the desired behavior.
2. The affected modules, layers, and system boundaries.
3. Ownership of data, business rules, and transformations.
4. Dependencies and direction of dependency flow.
5. Alternative approaches and material trade-offs.
6. Migration, compatibility, and operational implications.

Do not over-formalize low-risk changes. Focus discussion on decisions that could materially affect correctness, architecture, or future maintenance.

## Frontend-BFF Architecture

For systems using a Backend-for-Frontend layer, apply the contract-isolation principles in `frontend-bff-contract.md`. The frontend owns its consumption models; the BFF adapts backend representations into those models. Do not let backend DTOs become frontend page or component contracts.

## Decision Principles

- Prefer explicit ownership over implicit behavior.
- Prefer stable contracts over coupling to implementation details.
- Prefer semantic models over convenient but misleading shared structures.
- Prefer long-term architectural direction over preserving accidental historical structure.
- Explain material trade-offs rather than presenting a design choice as universally optimal.
