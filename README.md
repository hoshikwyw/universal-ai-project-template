# Universal AI Project Starter

A technology-neutral **governance and workflow template** for building software with AI coding assistants. It gives every project the same quality baseline: one set of shared AI instructions, role checklists, a staged prompt workflow with approval gates, and lightweight documentation templates.

> **This is not a runnable application scaffold.** It does not choose a language, framework, package manager, database, or cloud provider. Those decisions are made per project and recorded in `docs/`.

## What's inside
```text
.
├── AGENTS.md                  # Entry point: rules every AI assistant follows
├── .agents/                   # Role instructions (Markdown, not autonomous agents)
│   ├── project-manager.md
│   ├── software-architect.md
│   ├── tech-lead.md
│   ├── frontend-engineer.md
│   ├── backend-engineer.md
│   ├── database-engineer.md
│   ├── qa-engineer.md
│   ├── security-engineer.md
│   └── devops-engineer.md
├── commands/                  # Ordered prompts 00 → 07, plus bugfix.md and code-review.md
├── docs/                      # Per-project source of truth (fill these in)
│   ├── project-context.md
│   ├── requirements.md
│   ├── architecture.md
│   ├── testing-strategy.md
│   ├── security.md
│   └── decisions/             # Architecture Decision Records (ADRs)
├── .github/                   # PR template and issue forms (bug, feature)
├── src/  tests/  scripts/     # Optional placeholders: replace or delete
├── .editorconfig              # Consistent charset, line endings, indentation
├── .gitattributes             # Normalizes line endings to LF across OSes
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
- Copy `AGENTS.md`, `.agents/`, `commands/`, and `docs/`. Skip the placeholder folders. Optionally copy `.github/`, `.editorconfig`, and `.gitattributes`.
- If the repo already has an `AGENTS.md`, `.gitignore`, `.editorconfig`, `.gitattributes`, or `.github/` templates, **merge** this template's content in rather than overwriting.
- After adding `.gitattributes` to a repo with existing files, run `git add --renormalize .` once, and commit the result separately so the line-ending changes don't clutter feature diffs.
- Run `00-discover` first. It reports the real stack and any conflicts between the docs and the code, and helps you fill in `docs/` from what already exists.

## Workflow
| Step | Prompt | Lead role | Writes files? | Output |
|------|--------|-----------|---------------|--------|
| 0 | `00-discover.md` | Tech Lead + Architect | Docs only, after approval | Stack report, discrepancies, draft `project-context.md` |
| 1 | `01-requirements.md` | Project Manager + Tech Lead | `requirements.md`, after approval | Prioritized `REQ-` / `AC-` / `NFR-` items |
| 2 | `02-architecture.md` | Architect (+ Database, DevOps, Security, QA as relevant) | Docs and ADRs, after approval | Options, recommendation, ADRs, security and testing doc updates |
| 3 | `03-plan.md` | Tech Lead + Project Manager | No | Self-contained `STEP-` rows with approvals and reviews |
| 4 | `04-implement.md` | Tech Lead + Frontend / Backend / Database / DevOps | Yes (one approved step) | Diff, verification evidence, definition-of-done status |
| 5 | `05-qa.md` | QA Engineer | Tests only, if authorized | Test matrix and verdict |
| 6 | `06-security.md` | Security Engineer | `security.md` only, after approval | Ranked findings and remediation |
| 7 | `07-release-check.md` | Tech Lead + PM + QA + Security + DevOps | No | `READY` / `NOT READY` / `NEEDS VERIFICATION` for an exact commit |

Repeat steps 1–7 for each feature. Approve the output of each step before moving on. Shortcuts:
- Skip step 2 when step 1 finds that no design decisions are needed.
- Run step 6 only when a change touches authentication, authorization, user input, sensitive data, dependencies, or CI/CD. Step 5 tells you when.
- Approved docs are marked `Status: Approved` in their header. Later steps check this before relying on them.

**Ad-hoc prompts** (use at any time, outside the sequence):
| Prompt | Use for | Output |
|--------|---------|--------|
| `bugfix.md` | Reproduce a bug, add a failing regression test, apply a minimal fix | Root cause, fix, and test evidence |
| `code-review.md` | Review an uncommitted diff, branch, or PR (read-only) | Findings table and `Approve` / `Request changes` / `Comment` |

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
| Claude Code | Current versions load `AGENTS.md` as project instructions. If yours does not, or you want Claude-specific notes, add a `CLAUDE.md` containing the line `@AGENTS.md` (an import). Role files can optionally be adapted into `.claude/agents/` subagents. |
| Other assistants | Point the tool's native instruction or rules file at `AGENTS.md`, or copy its content in. |

Plain Markdown files do not create autonomous delegation by themselves. Roles take effect only when the assistant is told to apply them, which the `commands/` prompts do.

## Reusing and updating the template
- **Template-owned** (safe to sync from your canonical copy): `AGENTS.md`, `.agents/`, `commands/`, `.github/` templates.
- **Project-owned** (never overwrite during updates): everything in `docs/`.
- Keep one canonical copy of this template under version control. Review diffs before syncing changes into a project.
- If your assistant cannot read folders outside the repository, keep the role files inside the repository.

## Customizing
- **Add a role:** create `.agents/<role>.md` with the same sections as the existing roles (Mission, Use when, First read, Responsibilities, Workflow, Guardrails, Deliverable), then add it to the role table in `AGENTS.md`.
- **Record a decision:** copy `docs/decisions/000-template.md` to `docs/decisions/NNN-short-title.md` (for example `001-choose-database.md`) and list it in `docs/architecture.md`.
- **Tighten quality gates:** override the default definition of done in `docs/project-context.md`.
