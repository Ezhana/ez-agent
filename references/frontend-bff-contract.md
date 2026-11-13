# Frontend-BFF Contract Isolation

## Core Principle

The frontend owns the models consumed by its pages and components. The BFF owns the adaptation between backend representations and frontend-facing contracts.

Frontend pages and components must not directly depend on backend response DTOs or backend-specific field names and structures.

The frontend-facing model is an explicit contract between the BFF and frontend. It is not a pass-through representation of a backend response.

## Ownership Boundaries

### Backend

- Owns backend domain and service contracts.
- Exposes data and capabilities required by consumers.
- Does not need to shape internal DTOs around incidental frontend component implementation details.

### BFF

- Owns frontend-facing API contracts and backend-to-frontend adaptation.
- Integrates or aggregates backend data when required by the frontend use case.
- Maps backend field names, structures, enums, nullable values, and representations into frontend-facing semantics.
- Controls which backend data is exposed to the frontend.
- Does not become a place to hide missing core backend capabilities by accumulating business logic that belongs in backend services or domain layers.

### Frontend

- Owns page-facing models and view models according to actual UI and business requirements.
- Consumes frontend-facing contracts rather than backend DTOs.
- Keeps page and component logic independent of backend-specific response details.
- Does not perform scattered backend DTO transformations inside pages or presentation components.

## Contract Stability

- Backend response changes should normally be isolated within the BFF mapping layer.
- A backend field rename, structural change, or addition of internal fields should not automatically require changes to frontend pages or components.
- Frontend models should change when frontend requirements or business semantics change, not merely because a backend DTO changed.
- Do not expose backend-only fields to the frontend unless there is a justified frontend requirement.
- Do not add obsolete or compatibility fields to frontend contracts solely to preserve historical backend shapes.

## Model Granularity: No Universal Model

- Do not create one universal frontend model merely to maximize reuse.
- Define models around actual business semantics and the needs of their consumers.
- Different pages or use cases may have different view models even when they are derived from the same backend entity.
- Reuse a model when its meaning, lifecycle, and field semantics are genuinely the same—not merely because the fields currently look similar.
- Avoid both extremes: do not duplicate semantically identical models without reason, and do not force distinct use cases into a misleading shared model.
- Stability means stable ownership and semantics at the frontend boundary; it does not mean every page must share one data structure.

## Data Exposure and Transformation

- Use explicit mapping to determine which fields cross the BFF boundary.
- Do not blindly forward backend responses or pass backend objects through using object spreading.
- Normalize backend-specific enum values, date/time representations, nullability, nested structures, and naming where required by the frontend contract.
- Exclude internal, sensitive, irrelevant, or implementation-specific backend fields by default.
- Keep transformations in the BFF boundary rather than scattering them through frontend pages and components.

## Design Review Questions

- Is the frontend-facing model owned by the frontend use case rather than copied from a backend DTO?
- Is the BFF the explicit translation boundary?
- Can a backend response change be contained within the BFF?
- Are only necessary fields exposed?
- Does each model represent a coherent semantic concept?
- Are shared models genuinely semantically shared, rather than merely structurally similar?
- Is business logic kept in the correct layer?
