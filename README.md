# Universal AI Project Starter

A technology-neutral **governance and workflow template** for building software with AI coding assistants. It gives every project the same quality baseline: one set of shared AI instructions, role checklists, a staged prompt workflow with approval gates, and lightweight documentation templates.

> **This is not a runnable application scaffold.** It does not choose a language, framework, package manager, database, or cloud provider. Those decisions are made per project and recorded in `docs/`.

## What's inside
```text
.
├── AGENTS.md                  # Entry point: rules every AI assistant follows
├── .agents/                   # Role instructions (Markdown, not autonomous agents)
│   ├── software-architect.md
│   ├── tech-lead.md
│   ├── qa-engineer.md
│   └── security-engineer.md
├── commands/                  # Ordered copy-paste prompts, 00 → 07
├── docs/                      # Per-project source of truth (fill these in)
│   ├── project-context.md
│   ├── requirements.md
│   ├── architecture.md
│   ├── testing-strategy.md
│   ├── security.md
│   └── decisions/             # Architecture Decision Records (ADRs)
├── src/  tests/  scripts/     # Optional placeholders: replace or delete
└── .gitignore                 # Common ignores; extend for your stack
```

## Quick start: new project
1. Create a new repository from this template (copy it, or use GitHub's **Use this template** button).
2. Fill in `docs/project-context.md` and `docs/requirements.md`. Write `UNKNOWN` for anything undecided; never guess.
3. Connect your assistant to `AGENTS.md` (see [Tool compatibility](#tool-compatibility)).
4. Send `commands/00-discover.md` as your first prompt: paste it, or ask the assistant to "follow `commands/00-discover.md`".
5. Continue through the [workflow](#workflow), reviewing and approving each plan before any code changes.
6. Once you have chosen a stack, have the Tech Lead propose stack-appropriate folders, manifests, tests, and CI. Delete the placeholder `src/`, `tests/`, or `scripts/` folders if the project uses a different layout (`app/`, `packages/`, `cmd/`, …).

## Adopting into an existing repository
- Copy only `AGENTS.md`, `.agents/`, `commands/`, and `docs/`. Skip the placeholder folders.
- If the repo already has an `AGENTS.md` or `.gitignore`, **merge** this template's content in rather than overwriting.
- Run `00-discover` first. It reports the real stack and any conflicts between the docs and the code, and helps you fill in `docs/` from what already exists.

## Workflow
| Step | Prompt | Lead role | Writes files? | Output |
|------|--------|-----------|---------------|--------|
| 0 | `00-discover.md` | Tech Lead + Architect | No | Stack report, discrepancies, open questions |
| 1 | `01-requirements.md` | Tech Lead + Architect | After approval | Prioritized `REQ-`/`AC-` items |
| 2 | `02-architecture.md` | Architect | After approval | Options, recommendation, ADRs |
| 3 | `03-plan.md` | Tech Lead | No | Small, verifiable delivery steps |
| 4 | `04-implement.md` | Tech Lead | Yes (one approved step) | Diff and verification evidence |
| 5 | `05-qa.md` | QA Engineer | Tests only, if authorized | Test matrix and verdict |
| 6 | `06-security.md` | Security Engineer | No (unless approved) | Ranked findings and remediation |
| 7 | `07-release-check.md` | Tech Lead + QA + Security | No | `READY` / `NOT READY` / `NEEDS VERIFICATION` |

Repeat steps 1–7 for each feature. Small, low-risk changes can go 3 → 4 → 5. Approve the output of each step before moving on.

## Core principles
- **Evidence over claims:** nothing counts as "passing" unless it was actually run. Anything else is labeled `NOT RUN`.
- **Approval gates:** dependencies, schemas, deletions, deployments, and secrets always need explicit approval.
- **Smallest sufficient change:** no speculative architecture, no unrequested rewrites.
- **Secure and private by default:** synthetic test data only, no secrets in code or reports.
- **Living docs:** when docs and code disagree, report the conflict and update the docs.

The full rules, status vocabulary, and definition of done are in [`AGENTS.md`](AGENTS.md).

## Tool compatibility
| Assistant | Setup |
|-----------|-------|
| Tools that read `AGENTS.md` natively (for example OpenAI Codex, Cursor, GitHub Copilot) | Works as is. Check your tool's docs for its current behavior. |
| Claude Code | Create a `CLAUDE.md` in the repo root containing the line `@AGENTS.md` (an import), plus any Claude-specific notes. Role files can optionally be adapted into `.claude/agents/` subagents. |
| Other assistants | Point the tool's native instruction or rules file at `AGENTS.md`, or copy its content in. |

Plain Markdown files do not create autonomous delegation by themselves. Roles take effect only when the assistant is told to apply them, which the `commands/` prompts do.

## Reusing and updating the template
- **Template-owned** (safe to sync from your canonical copy): `AGENTS.md`, `.agents/`, `commands/`.
- **Project-owned** (never overwrite during updates): everything in `docs/`.
- Keep one canonical copy of this template under version control. Review diffs before syncing changes into a project.
- If your assistant cannot read folders outside the repository, keep the role files inside the repository.

## Customizing
- **Add a role:** create `.agents/<role>.md` with the same sections as the existing roles (Mission, Use when, First read, Responsibilities, Workflow, Guardrails, Deliverable), then add it to the role table in `AGENTS.md`.
- **Record a decision:** copy `docs/decisions/000-template.md` to `docs/decisions/NNN-short-title.md` (for example `001-choose-database.md`) and list it in `docs/architecture.md`.
- **Tighten quality gates:** override the default definition of done in `docs/project-context.md`.
