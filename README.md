# Universal AI Project Starter

A technology-neutral **governance and workflow template**, not a runnable application scaffold. It deliberately does not prescribe `src/` subdirectories, a package manager, database, or framework: these depend on the project type. Empty `src/` and `tests/` are placeholders; remove or replace them for projects that use `app/`, `packages/`, `cmd/`, etc.

## Quick start
1. Copy this template to a new project repository.
2. Fill `docs/project-context.md` and `docs/requirements.md`; use `UNKNOWN` for undecided fields.
3. Open the repository with a coding assistant that can read local files.
4. Paste the contents of `commands/00-discover.md` as your first prompt; continue through `07-release-check.md` only as appropriate.
5. Review/approve proposed plans before code changes. Agents are **Markdown role instructions**, not independent workers or executable commands.
6. After choosing a stack, let the tech lead propose stack-appropriate folders, manifests, tests, and CI. Do not blindly force the placeholder structure.

## Folders
- `.agents/`: reusable role instructions (architect, tech lead, QA, security).
- `commands/`: ordered copy-paste prompts.
- `docs/`: per-project context, requirements, architecture, testing, security, ADRs.
- `src/`, `tests/`: optional placeholders only.
- `scripts/`: optional project automation.

## Reuse and synchronization
Keep a separate canonical copy of `.agents/` under version control. Copy or sync it into projects and review diffs before updating. Project-specific docs should not be overwritten during updates. If your assistant cannot access external folders, keep agent files inside the repository.

## Tool compatibility
`AGENTS.md` is commonly used by Codex-style agents; other assistants may require native adapters. For Claude Code, create a `CLAUDE.md` pointing to these instructions or copy role instructions into its native agent format. For Cursor, use its native project rules. Plain Markdown files alone do not provide autonomous delegation.

## Suggested sequence
Discover → Requirements → Architecture → Plan → Implement → QA → Security → Release check. At each stage, verify outputs and approve next actions. Steps can be repeated for each feature.
