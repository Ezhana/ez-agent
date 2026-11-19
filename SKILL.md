---
name: ez-agent
description: Apply my personal software engineering methodology to software development tasks, including requirements clarification, architecture and technical design, implementation, coding conventions, refactoring, code review, and frontend-BFF contract design. Use when creating, modifying, reviewing, or designing software.
---

# Personal Engineering Methodology

Apply this methodology consistently to relevant software engineering tasks. The references provide the detailed rules for each area. Read the relevant references before performing the corresponding work; read more than one when a task spans multiple areas.

## Core Working Agreements

- Communicate concisely, practically, and directly. Avoid unnecessary explanations, repetitive summaries, formalities, and emotional reassurance.
- Understand the actual requirement before proposing or implementing a solution. Ask targeted questions when material requirements, constraints, semantics, or expected behavior remain ambiguous.
- Aim for at least 90% confidence that the intended behavior and constraints are understood before implementation. Do not silently fill important gaps with assumptions.
- For substantive development work, discuss the architecture and design with me before implementation. Establish the problem, responsibilities, boundaries, dependencies, and implementation direction first.
- Do not start substantive implementation before the design direction has been discussed and agreed upon. For trivial, unambiguous changes, keep the discussion proportionate and avoid ceremony.
- Prefer root-cause solutions over local workarounds. Avoid patch-based implementation, especially when a missing lower-level capability is being compensated for with increasingly complex upper-layer logic.
- Keep responsibilities clear, dependencies explicit, and abstractions proportionate to actual needs.
- Optimize for long-term maintainability and the intended architectural direction rather than short-term convenience or preservation of accidental historical decisions.
- Be direct about flawed assumptions, design problems, trade-offs, risks, and breaking changes.

## Task Routing

Read the corresponding reference document before doing the relevant work:

| Work area | Reference |
|---|---|
| Collaboration, clarification, and design-first workflow | `references/collaboration.md` |
| Architecture, responsibility boundaries, and technical decisions | `references/technical-design.md` |
| Naming, comments, and language conventions | `references/engineering-style.md` |
| Frontend layout, styling, accessibility, component design, state management, and responsive development | `references/frontend-engineering.md` |
| Implementation and verification policy | `references/implementation.md` |
| Refactoring and compatibility policy | `references/refactoring.md` |
| Reviewing code and reporting findings | `references/code-review.md` |
| Frontend/BFF contract and data ownership | `references/frontend-bff-contract.md` |
| DTO-to-frontend-model mapping practices | `references/frontend-bff-mapping.md` |

For tasks spanning multiple areas, consult all applicable references. For example, a frontend feature involving a new backend field may require `technical-design.md`, `frontend-bff-contract.md`, `frontend-bff-mapping.md`, `engineering-style.md`, and `implementation.md`.

## Default Workflow

1. Understand the requirement, context, constraints, and expected behavior.
2. Identify material ambiguities. Ask focused questions rather than making consequential assumptions.
3. Discuss the architecture and design before substantive implementation.
4. Confirm the responsibilities, boundaries, dependencies, and intended direction.
5. Implement according to the agreed design and the applicable engineering conventions.
6. Review the changes for unnecessary complexity, incorrect naming, unclear responsibilities, and leaked dependencies.
7. Perform verification according to `references/implementation.md`.
8. Report what changed, significant decisions, compatibility implications, and exactly which checks were and were not performed.

## Cross-cutting Decision Priorities

1. Correct problem framing over premature implementation.
2. Root-cause solutions over surface-level workarounds.
3. Clear ownership and explicit dependencies over accidental coupling.
4. Long-term architecture over historical implementation constraints.
5. Accurate names and purpose-specific models over mechanical reuse.
6. Minimal necessary comments and explanations over verbosity.
7. Risk-proportionate verification over indiscriminate test execution.

## Important Boundaries

- A type-check or successful build is not proof of correct runtime behavior.
- Do not claim that functionality was manually exercised unless it actually was.
- Do not preserve backward compatibility by default during refactoring; explain the impact of breaking changes.
- Frontend pages and components must consume frontend-owned models, not backend response DTOs. The BFF owns the mapping boundary. See the two frontend-BFF references.
- Do not create a universal model merely to maximize reuse. Model boundaries should follow actual business semantics and consumer needs.
