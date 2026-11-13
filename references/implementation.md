# Implementation and Verification

## Implementation

- Implement only after the requirement and design direction are sufficiently clear and, for substantive work, discussed and agreed upon.
- Follow the agreed design and preserve the responsibility boundaries established during design.
- Do not introduce a local workaround that contradicts the agreed architecture without raising the issue first.
- Avoid unrelated changes, speculative abstractions, and unnecessary code or documentation.
- Use the repository's existing conventions and toolchain unless a change is justified.

## Default Verification Policy

- Do not perform manual functional walkthroughs or end-to-end verification by default.
- Type checking is the default verification method when the project provides a type-checking tool.
- Decide whether to run compilation or a build based on the scope, structural impact, and risk of the changes.
- Larger changes, changes to foundational capabilities, cross-module changes, and changes that may affect application integration generally justify a compilation or build check.
- Do not run broad test suites, manual scenarios, or unrelated checks without a concrete reason or explicit request.
- If a focused automated check is necessary to validate a specific risk, explain why it is relevant and keep its scope proportionate.

## Interpretation of Results

- A successful type check verifies only the type constraints covered by that tool and configuration.
- A successful compilation or build does not prove that runtime behavior or business scenarios are correct.
- Do not equate type checking or compilation with manual runtime verification.
- Report the exact commands or categories of checks performed when relevant.
- State important checks that were not performed, especially where runtime behavior remains unverified.
- Never claim the application runs correctly unless that has actually been established through an appropriate execution or verification method.

## Completion Report

Keep the report concise and include:

1. What changed.
2. Important design or implementation decisions.
3. Breaking changes or compatibility implications, if any.
4. Verification performed and its result.
5. Material verification not performed, when relevant.
