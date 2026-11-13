# Engineering Style

## Naming

- Names of files, directories, modules, classes, types, functions, methods, and variables must reflect their actual purpose, behavior, and business meaning.
- Follow the conventions and idioms of the relevant programming language, framework, and repository.
- Prefer precise semantic names over vague names, abbreviations, or names tied only to implementation mechanics.
- Do not mechanically preserve existing names when they are misleading or no longer describe the responsibility.
- During modification or refactoring, rename identifiers when doing so improves semantic accuracy and does not create an unaddressed external contract change.

## Code Structure

- Prefer readable, straightforward control flow.
- Keep functions and modules focused on coherent responsibilities.
- Avoid deeply nested logic when early returns or clearer decomposition improve readability.
- Avoid unnecessary abstraction, indirection, generic frameworks, and speculative extensibility.
- Follow established repository conventions unless there is a concrete reason to change them.

## Comments

- Write no comments by default; use comments sparingly.
- Prefer clear names, structure, types, and straightforward logic to explanatory comments.
- Add a comment only when the code cannot accurately express the relevant information or when a non-obvious constraint, assumption, rationale, or business rule could otherwise be misunderstood.
- Comments should explain why something is necessary, what constraint applies, or what non-obvious behavior must be preserved—not simply restate what the code does.
- Keep comments synchronized with the implementation. Remove comments that have become redundant or inaccurate.

## Language and Repository Conventions

- Follow the applicable language and ecosystem conventions rather than imposing one naming or formatting style across all languages.
- Inspect existing formatter, linter, compiler, and type-checker configuration before proposing style changes.
- Avoid unrelated formatting churn or repository-wide style changes during a focused task.
- When existing conventions are inconsistent or harmful, identify the issue and discuss a coherent direction rather than introducing another local convention.
