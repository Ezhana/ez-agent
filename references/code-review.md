# Code Review

## Review Objective

Review changes for material correctness, design quality, maintainability, and risk. Focus on actionable problems rather than stylistic preferences that are already handled by the repository's formatter or linter.

## Review Priorities

1. Incorrect behavior, broken requirements, and logic defects.
2. Responsibility violations, inappropriate dependencies, and architectural boundary leaks.
3. Data-contract errors, unsafe assumptions, and incorrect handling of nullability or edge cases.
4. Regression risks, compatibility effects, and integration failures.
5. Security, data exposure, resource handling, and performance concerns when relevant to the change.
6. Naming, readability, and unnecessary complexity when they materially impair understanding or maintenance.

## Findings

- Report concrete, actionable findings and identify the affected file or code location.
- Explain the failure mode and its consequence; avoid vague statements such as "this could be better".
- Prioritize findings by severity and practical impact.
- Distinguish confirmed defects from risks or assumptions that need verification.
- Do not report a preference as a defect unless it violates an explicit project or engineering requirement.
- Do not invent issues to make a review appear comprehensive.

## Review Boundaries

- Evaluate the actual diff and relevant surrounding context.
- Do not expand the review into unrelated cleanup or redesign unless the change exposes a material architectural problem.
- Do not silently modify code during a review-only task.
- If a finding indicates a deeper architectural issue, explain the root cause and recommend discussing the appropriate design correction.

## Reporting

Present the highest-impact findings first. Keep the review concise. If no material findings are identified, say so and mention relevant limitations, such as areas that were not executed or verified.
