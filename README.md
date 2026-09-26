# Kiro Steering Files

A compact set of reusable agent instructions for software development, architecture, documentation, and durable technical learnings. The guides are optimized for Kiro while keeping their substantive rules usable by other agent systems.

The set follows current guidance from [Kiro Steering](https://kiro.dev/docs/steering/), [Kiro Agent Skills](https://kiro.dev/docs/skills/), the open [Agent Skills specification](https://agentskills.io), and OpenAI guidance for lean prompts and progressive skill disclosure.

## What It Contains

| File | Inclusion | Purpose |
|---|---|---|
| [core.md](core.md) | Always | Instruction priority, action boundaries, execution, safety, validation, and communication |
| [architecture.md](architecture.md) | Auto | Architecture and code-quality decisions for structural work |
| [docs.md](docs.md) | Auto | Audience-led, source-verified project documentation |
| [learning.md](learning.md) | Auto | Portable, technology-scoped technical learning files and Agent Skills |

Only `core.md` is intended as universal context. The other guides have narrow activation descriptions so supported Kiro surfaces can load them only when relevant.

## Import Into a Kiro Workspace

From the root of a cloned copy, copy the guides into the target project:

```bash
mkdir -p /path/to/project/.kiro/steering
cp core.md architecture.md docs.md learning.md /path/to/project/.kiro/steering/
```

Replace `/path/to/project` with the project’s actual absolute path. Restart the Kiro session if the files are not detected immediately.

Workspace steering applies only to that project and is the recommended scope for team-shared rules. Commit the target project’s `.kiro/steering/` directory when the team should use the same guidance.

## Import as Global Kiro Steering

For personal guidance across local Kiro IDE and CLI workspaces:

```bash
mkdir -p ~/.kiro/steering
cp core.md architecture.md docs.md learning.md ~/.kiro/steering/
```

Review and adapt the files before installing them globally. Workspace steering takes precedence when it conflicts with global steering.

Kiro Web cannot read a local `~/.kiro/steering/` directory. Use Kiro Configuration Sync when the same personal guidance must apply to cloud sessions.

## Kiro CLI Context Note

Kiro IDE and Web support `always`, `auto`, `fileMatch`, and `manual` steering inclusion modes. Current Kiro CLI documentation notes that CLI loads all files in `.kiro/steering/` regardless of inclusion mode.

For the leanest CLI setup, install only `core.md` as steering and keep specialized workflows as Agent Skills. This prevents architecture, documentation, and learning-maintenance instructions from consuming context during unrelated work.

```bash
mkdir -p /path/to/project/.kiro/steering
cp core.md /path/to/project/.kiro/steering/
```

## Use Technology Learning Skills

The learning guide uses the open Agent Skills layout:

```text
skills/<technology>/
├── SKILL.md
└── references/
    └── <service-or-framework>/
        └── <concern>.md
```

Example:

```text
skills/aws/SKILL.md
skills/aws/references/bedrock/model-invocation.md
skills/python/SKILL.md
skills/python/references/uv/virtual-environments.md
```

Each `SKILL.md` contains a short `name`, an activation-focused `description`, and instructions to read only the relevant reference file. Reference files contain verified one-line facts, human overrides, gotchas, learnings, rules, patterns, and anti-patterns.

Do not put personal preferences, credentials, customer information, account identifiers, or private infrastructure details in a shared skill.

## Import a Technology Skill Into Kiro

Copy a complete technology skill folder into the target project’s workspace skills directory:

```bash
mkdir -p /path/to/project/.kiro/skills
cp -R skills/aws /path/to/project/.kiro/skills/aws
```

Alternatively, in Kiro open **Agent Steering & Skills**, choose **+**, select **Import a skill**, and import the technology folder from a local directory or its public GitHub folder.

Kiro discovers the skill from `SKILL.md`, initially loads only its name and description, and reads the detailed reference files when the task requires them.

Custom agents do not load skills automatically. Add the appropriate `skill://` resource to the custom agent configuration:

```json
{
  "resources": [
    "skill://.kiro/skills/*/SKILL.md"
  ]
}
```

## Recommended Workflow

1. Start with `core.md` as the universal behavioral baseline.
2. Add the three specialized guides only on Kiro surfaces where conditional steering is supported.
3. For Kiro CLI and cross-agent use, package specialized workflows as Agent Skills.
4. Keep each skill focused and each reference file scoped to one technology, service, and concern.
5. Test one prompt that should activate each skill and one similar prompt that should not.
6. Review guidance after major tool, framework, model, or platform changes.

## Safety

Review all steering and skill files before installation. They can affect planning, tool use, commands, and external actions. Imported content should be treated as privileged instructions, and scripts or dependencies should be inspected before use.

No license is included. Repository owners should select and add a license explicitly before redistributing under specific terms.
