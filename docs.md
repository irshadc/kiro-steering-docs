---
inclusion: auto
name: documentation-guidance
description: Create, update, or review project documentation when the task explicitly concerns docs or changes behavior, interfaces, configuration, deployment, or architecture that existing docs describe. Do not activate for code-only work with no documentation impact.
---
# Documentation Standards

## Objective

Documentation must help a defined audience complete a real task and must match the current source, configuration, and deployed design. Prefer a small accurate document over comprehensive boilerplate.

## Decide What to Update

- Update documentation when the user requests it or when an authorized change makes existing instructions, interfaces, examples, paths, configuration, deployment steps, or architecture materially inaccurate.
- Update the existing authoritative document before creating another one.
- Create a new document only when it serves a distinct audience or workflow that the current documents cannot cover clearly.
- Do not force every module to have the same documents. A README, architecture guide, and deployment guide are useful defaults only when the module needs all three.
- Do not generate unrelated documentation during a code change.

## Document Roles

| Document | Primary question | Typical audience |
|---|---|---|
| `README.md` | What does this do and how do I use it? | Users and new contributors |
| `ARCHITECTURE.md` | How is it structured and why? | Maintainers and reviewers |
| `DEPLOYMENT.md` | How is it configured, run, deployed, verified, and recovered? | Operators and developers |
| Other focused guide | What distinct workflow is not covered above? | The people performing that workflow |

Keep information in the document that owns it. Link to the source of truth rather than copying the same configuration or procedure into several files.

## Documentation Workflow

1. Read the relevant implementation, configuration, scripts, and existing documentation.
2. Identify the audience, task, and exact behavior that must be documented.
3. Change only the affected sections and preserve established terminology.
4. Verify every referenced file, command, option, endpoint, port, resource, and example against the project.
5. Check links and cross-references after renames or moves.
6. Review the final diff for invented details, duplicated sources of truth, stale guidance, and sensitive data.

Do not infer undocumented infrastructure, permissions, models, integrations, or operational procedures. Mark a genuine unknown explicitly or obtain evidence.

## README Guidance

A README normally contains only the sections that help its audience:

- Title and concise purpose.
- Capabilities or supported use cases.
- A short explanation of the user-visible flow.
- Realistic usage examples with expected outcomes.
- A minimal quick start when the project supports one.
- Relevant verification or test commands.
- Links to deeper architecture, deployment, API, or contribution guidance.

Keep detailed environment-variable inventories, IAM policies, infrastructure setup, and operational recovery outside the README. A quick start may include minimal installation commands; detailed setup belongs in the deployment guide.

Reference the repository’s existing license. Never add, replace, or select a license without explicit owner approval. Include maintainer or author information only when the project already uses that convention.

## Architecture Documentation

Include only what maintainers need to understand or change the system:

- System boundary and major components.
- Component ownership and verified source paths.
- Synchronous and asynchronous control flow.
- Data ownership, storage, lifecycle, and consistency.
- External integrations and trust boundaries.
- Important decisions, constraints, and trade-offs.
- Retry, timeout, failure, recovery, concurrency, and security behavior.

Use a table for comparable component facts. Use a diagram when relationships are difficult to understand in prose. Do not add a diagram merely to satisfy a template.

## Deployment and Operations Documentation

Document applicable items only:

- Supported tool and runtime versions.
- Required access and permissions described by role or policy source.
- Required resources and dependencies.
- Account- or environment-specific variables with placeholder values.
- Local installation, run, and verification commands.
- Data preparation or migration steps.
- The authoritative deployment script or infrastructure definition.
- Health checks, logs, alerts, rollback, and expected first-run behavior.

Commands must be runnable from the stated directory and use actual project tooling. If deployment automation does not exist, identify the manual process as a current limitation rather than inventing a script.

## Configuration and Secrets

- Keep committed examples free of real credentials and account-specific values.
- Document required configuration explicitly and distinguish it from optional settings with documented defaults.
- Keep configuration templates and documentation synchronized.
- Reference secret names and storage locations, never secret values.
- Avoid copying generated configuration, schemas, policies, or resource inventories when an authoritative file can be linked.

## Cloud and Serverless Content

When applicable, document only services and regions proven by code, configuration, or infrastructure state. Use project-configured values or placeholders such as `<region>` in reusable examples. Include resource, event-source, timeout, concurrency, retry, dead-letter, network, and cold-start details only when they affect setup or operation.

## Diagrams

Choose the simplest format supported by the repository:

| Need | Preferred representation |
|---|---|
| Small component overview | Concise text, table, or ASCII when plain text is required |
| Multi-step interaction | Mermaid sequence diagram |
| Event or data flow | Mermaid flowchart |
| Dependencies | Mermaid graph |
| State transitions | Mermaid state diagram |
| Relational overview | Mermaid ER diagram |

Verify that labels match the implementation. Keep diagrams readable without color alone and accompany complex diagrams with a short textual explanation.

## Style

- Lead with the reader’s task or decision.
- Use direct language, active voice, and established project terminology.
- Use headings for navigation, tables for real comparisons, and code blocks for commands or payloads.
- Prefer concrete examples over marketing language or generic claims.
- Avoid arbitrary length targets; remove repetition and details owned elsewhere.
- Use relative links inside the repository and never link to a path that does not exist.

## Validation Checklist

Before completing a documentation change, confirm:

- The described behavior matches the current implementation.
- Commands, working directories, arguments, ports, and examples are valid.
- File paths, links, component names, and resource names resolve.
- Configuration names match their authoritative templates.
- No secret, credential, private customer data, or personal information is present.
- No unsupported claim, invented prerequisite, or accidental license change was introduced.
- Only documents affected by the task were changed.
