# Frontend-BFF Mapping Practices

## Model Definition

- Define frontend-facing models according to the needs and semantics of their actual consumers.
- Keep backend DTO types and frontend model types distinct, even when their current fields are similar.
- Do not import backend DTO definitions into frontend page or component code.
- Prefer purpose-specific page models or view models when different pages have different needs.
- Reuse a model only when its semantics and lifecycle are genuinely the same.
- Avoid exposing fields merely because they exist in the backend response.

## Explicit Mapping

- Perform backend-to-frontend transformation at the BFF boundary.
- Use explicit mapping logic to define the fields and semantics exposed to the frontend.
- Avoid blind pass-through and object spreading of backend response objects.
- Keep mapping logic centralized enough to avoid duplication, but do not build a generic mapping framework without a concrete need.
- Keep core business rules in the appropriate backend/domain layer; BFF mapping should adapt representations and compose data for the frontend, not become a second domain layer.

## Mapping Responsibilities

Handle the following where relevant:

- Field renaming to frontend-facing semantic names.
- Nested object restructuring or flattening when justified by the frontend contract.
- Enum conversion from backend codes to frontend domain values.
- Nullable and optional field normalization with explicit semantics.
- Date/time conversion with an agreed timezone and representation.
- Numeric units, money representations, and other domain-specific formats where contracts differ.
- Filtering of internal or irrelevant backend fields.
- Aggregation of backend data when it belongs to the BFF's frontend composition responsibility.

Do not silently invent defaults for missing or invalid data. Choose and document behavior based on the business requirement.

## TypeScript Example

Backend DTO:

```typescript
interface BackendOrderDTO {
  order_id: string;
  buyer_info: {
    buyer_name: string;
  };
  order_status: number;
  created_timestamp: number;
  internal_risk_level: number;
  internal_source: string;
}
```

Frontend-facing model:

```typescript
type OrderStatus = 'pending' | 'paid' | 'cancelled';

interface OrderPageModel {
  id: string;
  customerName: string;
  status: OrderStatus;
  createdAt: string;
}
```

BFF mapping:

```typescript
function mapOrder(data: BackendOrderDTO): OrderPageModel {
  return {
    id: data.order_id,
    customerName: data.buyer_info.buyer_name,
    status: mapOrderStatus(data.order_status),
    createdAt: formatDate(data.created_timestamp),
  };
}
```

The frontend consumes only the frontend-facing contract:

```typescript
const order: OrderPageModel = await getOrder();
```

Avoid pass-through mapping:

```typescript
// Do not expose the backend DTO wholesale.
return {
  ...backendResponse,
  customerName: backendResponse.buyer_info.buyer_name,
};
```

The spread still leaks backend field names and internal fields into the frontend contract.

## API and Type Boundaries

- Keep backend DTO definitions on the backend/integration side of the BFF boundary.
- Keep frontend-facing response types in a clearly owned contract or shared boundary package where appropriate.
- Do not make frontend compile-time dependencies point directly at backend-internal DTO packages.
- Ensure the BFF response type matches the actual mapped response.
- Keep runtime validation at trust boundaries where required; static types alone do not validate external payloads at runtime.

## Change Handling

- When a backend DTO changes, update the BFF adapter and its relevant mapping checks first.
- Change the frontend-facing model only when the frontend contract or business semantics need to change.
- When a frontend requirement changes, update the relevant view model and BFF mapping rather than adding unrelated backend fields to the page.
- Treat breaking changes to the frontend-facing contract as explicit design changes, not incidental consequences of backend DTO evolution.

## Avoid Unnecessary Complexity

- Do not introduce a separate mapping abstraction for every trivial field unless it improves ownership, reuse, or clarity.
- Do not build a universal DTO-to-ViewModel conversion framework prematurely.
- Do not duplicate the same meaningful transformation across multiple endpoints when a shared mapping function is justified.
- Keep mapping code straightforward and typed; prefer explicit code over reflection or implicit field propagation.

## Implementation Review Checklist

- [ ] Frontend pages and components consume frontend-owned models.
- [ ] Backend DTOs do not leak into frontend contracts.
- [ ] BFF mapping explicitly selects and transforms exposed fields.
- [ ] No blind object spreading or raw response pass-through is used.
- [ ] Nullability, enums, dates, and units have intentional semantics.
- [ ] Internal or irrelevant backend fields are not exposed.
- [ ] Models are shared only when their semantics genuinely match.
- [ ] Business logic remains in the appropriate layer.
- [ ] Type checking is performed; compilation/build checks are considered according to change impact.
