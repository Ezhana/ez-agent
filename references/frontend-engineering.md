# Frontend Engineering Guidelines

## 1. Layout & Spacing

### 1.1 Layout Ownership

- A parent component MUST own the layout relationship between its direct children.
- A component SHOULD own its internal layout and spacing.
- Components SHOULD NOT impose external margins on themselves to compensate for their position in a parent layout.
- Layout responsibilities SHOULD remain predictable when components are reordered, reused, or nested.

### 1.2 Spacing Strategy

- Prefer layout primitives such as Flexbox and Grid for arranging elements.
- Within Flexbox and Grid containers, prefer `gap-*` utilities for spacing between children.
- In traditional block-flow layouts, `space-y-*` and `space-x-*` MAY be used when their selector-based behavior is appropriate.
- Avoid mixing multiple spacing mechanisms for the same layout relationship.
- Prefer consistent spacing scales over arbitrary one-off values.

### 1.3 Padding, Margin, and Gap

Use each spacing mechanism according to its responsibility:

- **Padding** defines the internal spacing between a container's boundary and its content.
- **Margin** defines spacing outside an element when an external layout relationship cannot be expressed by the parent.
- **Gap** defines spacing between children in a Flexbox or Grid container.

Prefer parent-controlled spacing over child-specific margins when arranging sibling elements.

### 1.4 Responsive Spacing

- Spacing SHOULD adapt to available screen space and content density.
- Prefer a small, consistent set of responsive spacing steps.
- Avoid fixed spacing values that cause overflow or excessive whitespace on smaller screens.
- Use responsive overrides only when they improve readability or layout behavior.

## 2. Semantic HTML & Accessibility

### 2.1 Semantic Structure

- Use semantic HTML elements according to their intended meaning.
- Use headings to establish a logical document hierarchy.
- Use `<button>` for actions and `<a>` for navigation.
- Do not use generic elements such as `<div>` or `<span>` as substitutes for native interactive elements.
- Choose elements based on their semantics, not merely their default appearance.

### 2.2 Keyboard Accessibility

- All interactive functionality MUST be accessible through a keyboard.
- Interactive elements MUST expose a visible focus state.
- Do not remove focus indicators with `outline-none` or equivalent styles unless an equally visible and usable replacement is provided.
- Custom interactive components MUST implement appropriate keyboard interaction behavior.

### 2.3 Accessible Names and Descriptions

- Interactive controls MUST have accessible names.
- Images MUST have meaningful alternative text when they convey information.
- Decorative images SHOULD use empty alternative text.
- Use ARIA attributes only when native HTML semantics are insufficient.
- ARIA attributes MUST accurately reflect the component's current state and behavior.

### 2.4 Accessibility as a Design Constraint

Accessibility MUST be considered during component design rather than added as a final styling step.

Visual appearance MUST NOT take priority over essential interaction semantics, keyboard accessibility, or assistive-technology support.

## 3. State & Single Source of Truth

### 3.1 State Ownership

- Every piece of mutable UI state MUST have a clear owner.
- A state value SHOULD be maintained at the lowest component level that can reliably own it.
- State shared by multiple components SHOULD be lifted to their nearest appropriate common owner or managed through an established shared state mechanism.
- Avoid maintaining multiple independent copies of the same logical state.

### 3.2 Derived State

- Prefer deriving values from existing state and props instead of storing redundant state.
- Derived values SHOULD be calculated close to where they are consumed.
- Avoid synchronization effects whose only purpose is to keep duplicated state values aligned.
- A component MUST NOT maintain conflicting sources of truth for the same logical value.

### 3.3 Interaction and Visual State

- Visual states MUST be driven by actual component state or explicit props.
- Loading, disabled, selected, expanded, validation, and error states SHOULD have consistent representations.
- Do not use direct DOM manipulation as a substitute for the framework's state management model.
- State transitions MUST preserve the consistency of related UI elements.

### 3.4 State Boundaries

- Keep transient interaction state local when it does not need to be shared.
- Avoid introducing global state for component-local behavior.
- Shared state mechanisms SHOULD be introduced only when multiple consumers genuinely need coordinated access.

## 4. Design Tokens & Styling

### 4.1 Semantic Tokens

- Prefer semantic design tokens for colors, typography, spacing, borders, and other reusable design decisions.
- Use tokens such as `background`, `foreground`, `muted`, `border`, and `primary` according to their intended semantic roles.
- Avoid hardcoded color values when an appropriate project token exists.
- Avoid relying on raw palette values throughout application components when semantic tokens are available.

### 4.2 Consistent Styling

- Reuse established project styling conventions.
- Avoid introducing multiple competing approaches for the same visual concern.
- Custom utility classes and design tokens SHOULD be introduced when a repeated requirement cannot be expressed clearly through existing project conventions.
- One-off visual exceptions SHOULD remain local unless they represent a reusable design decision.

### 4.3 Visual Consistency

- Components serving the same purpose SHOULD have consistent visual behavior.
- Interactive states SHOULD be visually distinguishable.
- Styling SHOULD preserve sufficient contrast, readability, and clear interaction affordances.
- Prefer consistency over unnecessary visual variation.

## 5. Component Boundaries & Props Design

### 5.1 Component Responsibilities

- Each component SHOULD have a clear and cohesive responsibility.
- Separate business logic, data transformation, and presentation when doing so improves clarity or reuse.
- Avoid components that combine unrelated responsibilities.
- Avoid splitting components solely to reduce line count or create superficial abstractions.

### 5.2 Props and Native Attribute Forwarding

Component APIs MUST make their supported customization points explicit.

- Avoid indiscriminately forwarding arbitrary HTML attributes, DOM event handlers, or styling properties to deeply nested internal elements.
- Composite components SHOULD expose purpose-specific props rather than unrestricted access to their internal DOM structure.
- Components that are thin wrappers around native elements, such as buttons, links, and input controls, MAY forward relevant native attributes through a controlled and documented interface.
- A `className` or equivalent styling extension point MAY be exposed when external customization is an intentional part of the component API.
- Slots, children, and composition interfaces SHOULD be preferred when they provide a clearer extension mechanism than additional configuration props.
- Forwarded attributes MUST reach the intended element and MUST NOT silently alter unrelated internal behavior.

### 5.3 Component Composition

- Prefer composition over excessive configuration props when component structure is naturally composable.
- Avoid components with large numbers of boolean props that create ambiguous or conflicting combinations.
- Props SHOULD describe business or presentation intent rather than expose unnecessary implementation details.
- Public component APIs SHOULD remain stable and understandable.

### 5.4 Client-Side JavaScript and Hydration

- Prefer server-rendered or static output when client-side interactivity is not required.
- Add client-side JavaScript only when it provides necessary interactive behavior.
- In island-based architectures such as Astro, hydrate only the components that require client-side execution.
- Avoid hydrating entire pages or large component trees to support isolated interactions.
- Client-side dependencies SHOULD remain limited to what the interaction requires.

## 6. Edge Cases & Defensive Rendering

### 6.1 Boundary Scenarios

Frontend components SHOULD account for relevant boundary conditions, including:

| Scenario | Expected Consideration |
| --- | --- |
| Missing or optional fields | Provide safe fallbacks or omit unavailable content |
| Long text or large content | Prevent overflow and preserve readability |
| Unexpected data shape | Avoid unsafe assumptions and handle invalid values |
| Slow or interrupted requests | Preserve a usable loading or recovery experience |
| Repeated user interaction | Prevent inconsistent or duplicated operations |

Not every component needs custom handling for every scenario. Consider the data contract, interaction model, and user impact when deciding which cases require explicit treatment.

### 6.2 Empty States and Failure States

Different empty states represent different business conditions and MUST NOT be treated as interchangeable.

- **No data:** The resource exists, but currently contains no records.
- **No search or filter results:** Data may exist, but the current query or filter produces no matches.
- **Request failure:** The application could not retrieve or process the requested data.
- **Missing or unavailable resource:** The requested resource does not exist or is no longer accessible.

The UI SHOULD communicate the actual condition and provide an appropriate next step when possible.

Do not display an empty-state message for a request failure. Do not represent a valid empty result as an error.

### 6.3 Error Handling

- Errors MUST NOT be silently converted into successful-looking results.
- User-facing error messages SHOULD explain the impact and available recovery actions.
- Technical details SHOULD be logged or reported through the project's established error-handling mechanism rather than exposed directly to end users.
- Error handling SHOULD be consistent across components that share the same interaction pattern.

## 7. Copy & Internationalization

### 7.1 User-Facing Copy

- User-facing text SHOULD be separated from business logic and component implementation where the project supports centralized copy or localization.
- Avoid embedding long or frequently reused messages directly in component logic.
- Use consistent terminology across related pages and interactions.
- Error and empty-state messages SHOULD describe the actual condition rather than generic failure language.

### 7.2 Internationalization

- Use the project's established internationalization mechanism when localization is required.
- Translation keys SHOULD describe meaning or context rather than rely on positional identifiers.
- Avoid constructing translated sentences by concatenating fragments when complete translated messages are needed.
- Format dates, times, numbers, and currencies according to the active locale.

### 7.3 Content Expansion

- UI layouts SHOULD accommodate reasonable differences in text length across supported languages.
- Avoid fixed widths or heights that assume a specific language's text length.
- Test layouts with longer translations when localization is part of the product scope.

### 7.4 Text Direction

- Support right-to-left (RTL) layout behavior when the product includes RTL languages or bidirectional text requirements.
- Prefer logical CSS properties such as `margin-inline-start` and `padding-inline-end` over physical-direction properties when direction-independent behavior is required.
- RTL-specific testing is not required for projects that do not support RTL or bidirectional layouts.

## 8. Responsive Design

### 8.1 Content-Driven Layout

- Design layouts around content requirements rather than targeting specific device models.
- Prefer fluid sizing, flexible containers, and intrinsic layout behavior.
- Avoid fixed widths and heights when they can cause clipping or overflow.
- Use breakpoints to address actual layout constraints rather than to mirror a particular device catalog.

### 8.2 Mobile-First Development

- Prefer mobile-first styling when it fits the project's design system and implementation conventions.
- Ensure that primary content and interactions remain usable on narrow screens.
- Avoid relying on hover-only interactions for essential functionality.
- Consider touch target size and interaction spacing for touch-based devices.

### 8.3 Responsive Validation

- Validate layouts at representative viewport sizes.
- Check for horizontal overflow, clipped content, overlapping elements, and inaccessible controls.
- Responsive adjustments SHOULD preserve content hierarchy and interaction consistency.

## 9. Frontend Development Review

Use the following checklist as a review aid. Apply items according to the component's actual responsibilities and product requirements.

### Layout and Styling

- [ ] Layout ownership is clear between parent and child components.
- [ ] Spacing follows established project conventions.
- [ ] Existing design tokens are reused where appropriate.
- [ ] Responsive behavior has been considered.

### Semantics and Accessibility

- [ ] Semantic HTML elements are used appropriately.
- [ ] Interactive elements use native controls where possible.
- [ ] Keyboard access and visible focus states are preserved.
- [ ] Accessible names and relevant ARIA attributes are provided.

### State and Data

- [ ] State ownership and data flow are clear.
- [ ] Redundant or conflicting state is avoided.
- [ ] Loading, empty, and error states are handled according to their meaning.
- [ ] Missing and unexpected data cannot cause unsafe rendering.

### Component Design

- [ ] Component responsibilities are cohesive.
- [ ] Props expose intentional capabilities rather than unnecessary implementation details.
- [ ] Native attributes are forwarded only when appropriate.
- [ ] Client-side JavaScript and hydration are limited to necessary behavior.

### Maintainability

- [ ] User-facing copy follows project conventions.
- [ ] Internationalization requirements are considered where applicable.
- [ ] New abstractions solve a demonstrated problem.
- [ ] Exceptions to established conventions have a clear justification.

## 10. General Engineering Principles

1. **Clarity Over Cleverness** — Prefer straightforward implementations that are easy to understand and maintain.
2. **Consistency Over Personal Preference** — Follow established project conventions unless there is a concrete reason to change them.
3. **Semantic Correctness Over Visual Convenience** — Preserve HTML semantics and accessibility even when alternative implementations appear visually simpler.
4. **Single Source of Truth** — Avoid duplicated state and conflicting representations of the same data.
5. **Explicit Boundaries** — Keep component responsibilities, data ownership, and public APIs clear.
6. **Progressive Enhancement** — Provide usable output with the minimum client-side capabilities necessary.
7. **Defensive Rendering** — Handle relevant boundary conditions without obscuring genuine failures.
8. **User Experience Over Implementation Convenience** — Prioritize understandable content, predictable interactions, and recoverable errors.
9. **Consistency With Room for Context** — Apply shared conventions while accounting for genuine differences in component and product requirements.
10. **Avoid Unnecessary Abstraction** — Introduce abstractions when they reduce meaningful complexity, not merely to anticipate hypothetical reuse.

## 11. Exceptions & Decision Priorities

These guidelines establish default engineering expectations, not inflexible rules for every implementation.

When requirements conflict or a specific context justifies an exception, apply the following priorities:

1. **Correctness and data integrity** — The implementation MUST preserve correct behavior and avoid misleading or corrupted data.
2. **Accessibility and usability** — Essential interaction semantics and accessibility MUST NOT be sacrificed for implementation convenience.
3. **User experience** — Prefer predictable, understandable, and recoverable behavior.
4. **Consistency and maintainability** — Follow project conventions unless a justified exception produces a better long-term result.
5. **Implementation simplicity** — Avoid unnecessary complexity and abstraction.

An exception to a SHOULD-level recommendation MAY be appropriate when the alternative better serves the component's actual requirements.

Exceptions to MUST-level requirements require a compelling technical or product justification and MUST NOT compromise essential correctness, security, or accessibility.

When an implementation intentionally deviates from an established guideline, document the reason in the relevant pull request or code comment when the rationale would not otherwise be clear.

Code reviews SHOULD evaluate the underlying engineering outcome rather than mechanically enforce stylistic preferences.
