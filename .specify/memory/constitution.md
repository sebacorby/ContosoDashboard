# ContosoDashboard Constitution

## Core Principles

### I. Training Scope Is Explicit
ContosoDashboard MUST remain an offline, local training application unless an approved amendment
changes that scope. Features MUST preserve the educational purpose and MUST document any deliberate
production limitation. Mock authentication and authorization MUST NOT be represented as production
security controls. This keeps training exercises reproducible and prevents unsafe reuse.

### II. Layered Boundaries and Dependency Injection
Business behavior MUST be implemented through the existing Models, Services, Data, and Pages
boundaries. Pages MUST delegate data access and authorization-sensitive operations to services;
services MUST depend on abstractions for replaceable infrastructure. New external or filesystem
dependencies MUST be registered through dependency injection. This preserves testability and enables
the documented migration path without rewriting business logic.

### III. Authorization Is Enforced in Depth
Every protected route MUST require authentication, and every operation that reads, changes, deletes,
downloads, or shares user- or project-scoped data MUST verify authorization in the service layer.
UI visibility alone MUST NOT grant access. Resource identifiers supplied by clients MUST be checked
against the authenticated user's permissions to prevent IDOR. This protects user isolation even when
routes or UI controls are bypassed.

### IV. Secure Local Storage with Cloud-Ready Abstractions
Files and other sensitive artifacts MUST be stored outside `wwwroot` and served only through
authorized application endpoints. User-provided names MUST NOT be used as storage paths; generated,
unique paths MUST be created before metadata is persisted. Storage implementations MUST conform to
an interface so local storage can be replaced by cloud storage without changing business logic, UI,
or persistence contracts. This makes offline training safe while retaining a clear migration path.

### V. Specification, Validation, and Simplicity
Each feature MUST begin with a written, testable specification that states user outcomes,
authorization rules, validation rules, and acceptance criteria. Changes MUST include validation
appropriate to their risk, including service-level authorization and data-integrity scenarios when
applicable. Implementations MUST use the smallest design that satisfies the approved specification;
new dependencies, abstractions, and complexity require documented justification. This keeps the
training code understandable and the exercises focused on fundamentals.

## Training and Security Constraints

- The supported stack is ASP.NET Core 8.0, Blazor Server, Entity Framework Core, and SQL Server
	LocalDB unless an approved specification explicitly changes it.
- The application MUST operate locally and offline; cloud services and external runtime dependencies
	are out of scope for training features.
- Authentication is intentionally mock-only. Production deployment requires a real identity provider,
	password protection, MFA where appropriate, OAuth 2.0/OpenID Connect, TLS, audit logging, and
	applicable accessibility and compliance controls.
- Input validation MUST enforce documented limits and allowlists before persistence or filesystem
	operations. Errors MUST be clear to users and MUST NOT expose sensitive implementation details.

## Development Workflow

1. Capture feature intent and acceptance criteria in a specification before implementation.
2. Review the specification for architecture boundaries, authorization, validation, and offline
	 constraints before planning tasks.
3. Implement only approved scope, keeping UI, services, data models, and infrastructure concerns
	 separated.
4. Review changes against this constitution and validate the affected behavior before approval.
5. Record known training limitations in the relevant documentation when they affect security,
	 reliability, or the production migration path.

## Governance

This constitution supersedes conflicting project practices for architecture, security, and delivery.
Amendments MUST identify the affected principles, explain the rationale and migration impact, and be
reviewed by the project owner before adoption. The version follows semantic versioning: MAJOR for
backward-incompatible governance changes or removed/redefined principles, MINOR for new principles
or materially expanded guidance, and PATCH for clarifications that do not change governance intent.

Every specification, plan, task review, and pull request MUST verify compliance with these principles.
Exceptions MUST be explicit, time-bounded, documented with their risk, and approved by the project
owner. The constitution MUST be reviewed whenever a feature introduces a new infrastructure boundary,
security model, persistence pattern, or deployment assumption.

**Version**: 1.0.0 | **Ratified**: TODO(RATIFICATION_DATE): original adoption date is unknown. | **Last Amended**: 2026-09-14
