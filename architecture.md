---
inclusion: auto
name: architecture-guidance
description: Design or review software architecture, module boundaries, APIs, data models, integrations, security boundaries, or substantial refactors. Do not activate for typo-only, formatting-only, or content-only changes.
---
# Architecture and Code Quality

## Scope

Apply this guide when a task changes or evaluates system structure. Follow the repository’s established architecture unless the task requires changing it. Use these principles as decision criteria, not as mandatory patterns for every project.

## Decision Process

1. Identify the required behavior, constraints, affected users, and failure impact.
2. Inspect the existing code paths, tests, interfaces, and deployment model relevant to the decision.
3. Consider alternatives only when they create a material trade-off in simplicity, reliability, security, cost, or operability.
4. Choose the smallest design that meets the current requirement and fits the codebase.
5. Record a decision or trade-off only when a future maintainer would otherwise revisit it without the original context.

## Module Design

- Give each module a cohesive responsibility that can be described in one sentence.
- Group code by business capability when that matches the project; do not force a new folder taxonomy onto an established repository.
- Keep business rules independent of transport and persistence details when that separation improves testing or reuse.
- Prefer composition. Introduce interfaces, factories, repositories, or additional layers only when multiple implementations, isolation, or real complexity justifies them.
- Keep dependencies directed toward stable domain behavior and avoid circular imports.
- Localize a change to the owning module. Shared utilities must represent genuinely shared behavior, not convenient dumping grounds.
- Follow language-specific naming rules. For example, importable Python modules use underscores rather than hyphens.

## Complexity Signals

Function, class, and file sizes are review signals, not automatic failures. Investigate when a function becomes hard to test, a class owns unrelated behavior, nesting hides the main path, or a file changes for unrelated reasons. Split only when the result has clearer ownership and lower coupling.

## API and Interface Boundaries

- Use the project’s existing protocol and compatibility policy. Choose REST, events, commands, or another interface based on actual consumers.
- For HTTP APIs, use meaningful methods and status codes, validate input at the boundary, and return a consistent error shape.
- Version an interface when compatibility requirements demand it; do not add versioning ceremony without a consumer need.
- Keep handlers thin enough that business behavior can be tested without the transport.
- Paginate collections that can grow or are exposed to unbounded input. A demonstrably small bounded collection does not need pagination machinery.
- Define timeouts, request-size limits, and rate limits for public or externally reachable interfaces where abuse or resource exhaustion is possible.

## Data and State

- Use parameterized queries and validated key expressions; never concatenate untrusted input into a query.
- Use transactions when a multi-step write must succeed or fail as a unit.
- Make retryable jobs and event handlers idempotent.
- Stream or batch large data instead of loading it all into memory.
- Avoid per-item remote calls when a batch operation exists.
- Document ownership, lifecycle, consistency, retention, and recovery requirements for persistent data.
- Add caching only when repeated work is measurable and invalidation behavior is understood.

## Reliability and Errors

- Fail fast when required configuration is absent. Optional settings may have explicit, documented defaults.
- Distinguish expected domain errors from unexpected defects.
- Return safe external errors and log diagnostic context internally without secrets or personal data.
- Retry only transient failures, with bounded attempts, timeout, exponential backoff, and jitter.
- Use dead-letter handling when asynchronous work must not disappear after retries are exhausted.
- Include correlation identifiers across request, event, and background-job boundaries when the system spans multiple components.

## Security

- Enforce authentication and authorization at trusted boundaries; never rely on prompts or client-side checks as access control.
- Grant the minimum permissions required. Wildcards require a documented service constraint or explicit justification.
- Keep credentials in the project’s approved secret store or environment mechanism and reference them only by name.
- Use encrypted transport for external communication.
- Sanitize untrusted content before rendering and encode output for its destination.
- Treat changes to authentication, authorization, credential handling, or public exposure as security-sensitive and require focused review.

## Frontend

- Use components with clear ownership and keep state close to where it is consumed.
- Represent loading, empty, error, and success states for asynchronous behavior.
- Use semantic elements, keyboard access, visible focus, and appropriate accessible names.
- Prevent stale requests, subscriptions, timers, and event listeners from surviving component teardown.
- Optimize rendering, virtualization, code splitting, and media only where scale or measurement justifies them.

## Testing and Verification

- Test business behavior without unnecessary transport or database coupling.
- Use integration or contract tests at boundaries where mocks could hide incompatibility.
- Verify migrations, authorization changes, retries, and destructive operations against realistic failure cases.
- Run checks proportional to the change. A local refactor needs affected tests; an interface or data-model change needs boundary validation.
- Confirm the final implementation still follows the chosen dependency direction and has no newly duplicated policy.

## Architecture Output

When presenting an architecture decision, lead with the selected approach, affected components, data and control flow, material trade-offs, failure handling, security boundary, and verification plan. Do not produce diagrams or additional abstractions unless they make the decision easier to verify.
