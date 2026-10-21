# Prompt Runbook

A step-by-step guide to running the prompts in `commands/`, with playbooks for common project types and tech stacks.

- `README.md` explains what the template is.
- `AGENTS.md` holds the rules every assistant follows.
- This guide explains **how to drive the workflow day to day**.

---

## 1. Before you start
- [ ] The repository is under git, and you're on a working branch (not `main`).
- [ ] Your assistant loads `AGENTS.md` (see `README.md` → *Tool compatibility*). To check, ask it: *"What approval rules do you follow in this repo?"*
- [ ] `docs/project-context.md` has at least the project name, problem, and project type. Use `UNKNOWN` for everything else.
- [ ] You know your project type. Find it in [section 5](#5-stack-playbooks) and keep that playbook open.

## 2. How to run a prompt
**Send the prompt.** Either paste the file's contents, or send a short instruction:
```text
Follow commands/02-architecture.md.
```

**Fill in the placeholders.** Replace every `<...>` value in the **Input** section, for example:
```text
Follow commands/04-implement.md.
Approved step:
STEP-02: Add login API endpoint | AC-003, AC-004 | Backend | src/auth/* | unit + integration tests | approvals: none | ...
Approvals granted for this step: none
```

**One prompt per message.** Let the step finish, then review the output before you send the next prompt.

**Approve explicitly.** Most steps stop and wait for you. Reply clearly, and the assistant applies exactly that. Example replies:

| You want to… | Say |
|--------------|-----|
| Accept everything | `Approved. Apply the proposed changes.` |
| Accept part of it | `Approve REQ-001 to REQ-004. Drop REQ-005. Change AC-002 to … then apply.` |
| Grant a gated action | `Approved: install <package> as a dev dependency.` |
| Ask for a revision | `Not approved. Revise: use option B for the datastore, and explain the migration cost.` |
| Accept a risk | `Accept SEC-003 (Medium) for this release. Record it in docs/security.md under accepted exceptions.` |

**Keep sessions short.**
- Start a **new session** for each major step (02, 03, each 04 step, 05, 06, 07).
- The docs in `docs/` carry the context between sessions, which is why each step writes its results there after approval.
- Paste only what the next step asks for, such as the `STEP-` row, the QA report, or the security report.

## 3. Step-by-step walkthrough

### Step 00: Discover (once per repo, then after big changes)
- **You provide:** nothing; just run it.
- **You get:** the real stack and commands, discrepancies with the docs, a draft `project-context.md`, and the top five questions.
- **You decide:** answer the questions, then approve the doc draft.
- **Watch for:** invented commands. Every command must cite where it was found (for example `package.json` scripts or a `Makefile`).

### Step 01: Requirements (once per feature)
- **You provide:** the feature or goal, in plain words or as an issue link.
- **You get:** `REQ-`, `AC-`, and `NFR-` items with priorities, out-of-scope items, and questions.
- **You decide:** cut scope aggressively (anything not `Must` can wait), then approve. The file is written with `Status: Approved`.
- **Watch for:** acceptance criteria that can't be tested ("works well"). Ask for them as Given / When / Then.

### Step 02: Architecture (when the work needs design decisions)
- **You provide:** nothing extra. It reads the approved requirements.
- **You get:** a decisions table with options, a diagram, ADR drafts, and updates to the security and testing docs.
- **You decide:** pick the options, then approve. ADRs are set to `Accepted` and the docs to `Approved`.
- **Skip it** when step 01 says no design decisions are needed.
- **Watch for:** extra infrastructure you didn't ask for (queues, microservices, Kubernetes). Ask: *"What is the smallest design that meets the Must requirements?"*

### Step 03: Plan (once per feature)
- **You get:** self-contained `STEP-` rows covering approvals, reviews, tests, and rollback, plus a check that every acceptance criterion is covered.
- **You decide:** approve `STEP-01`. Save the plan output somewhere you can copy from (an issue, a PR description, or your notes).
- **Watch for:** steps that are too big. A step should be reviewable in one sitting (roughly under 400 changed lines).

### Step 04: Implement (once per step, in a new session)
- **You provide:** the pasted `STEP-` row, and the approvals granted.
- **You get:** a diff, test results, doc updates, the definition-of-done status, and the next prompt to run.
- **You decide:** review the diff yourself, commit when satisfied, then move on to 05, or to the next step.
- **Watch for:** "done" without a command and result, or changes outside the step's files.

### Step 05: QA (after each step, or after a group of steps)
- **You provide:** the change under test, and whether it may write tests.
- **You get:** a test matrix (`AC-` → `TC-`), results, `BUG-` defects, and a verdict.
- **Next:** on `NOT READY`, run `bugfix.md` for each defect and then re-run 05. If the change is security-relevant, run 06. Otherwise run 07.

### Step 06: Security (only for security-relevant changes, and before major releases)
- **You provide:** the authorized scope.
- **You get:** a threat-model summary, `SEC-` findings, which checks were run, and proposed `security.md` updates.
- **Next:** fix `Critical` and `High` findings with `bugfix.md`, then re-run 06 on the fix.

### Step 07: Release check (before every release)
- **You provide:** the release candidate commit, and the QA and security reports.
- **You get:** a status table for that exact commit, a verdict, blockers, and checks to run after release.
- **You decide:** release yourself. The assistant never deploys. Any `NOT RUN` item blocks a `READY` verdict.

### Anytime prompts
- **`bugfix.md`:** reproduce → failing test → minimal fix → search for the same pattern elsewhere.
- **`code-review.md`:** read-only review of a diff, branch, or PR. Use it on your own changes before committing, too.

## 4. Common paths
| Situation | Run |
|-----------|-----|
| Brand-new project | 00 → 01 → 02 → 03 → (04 → 05)× → 06 → 07 |
| Existing repo, first time | 00 (and fill in `docs/` from its findings) → then as below |
| New feature | 01 → 02 (if needed) → 03 → (04 → 05)× → 06 (if relevant) → 07 |
| Small change (≤ 1 step, low risk) | 03 → 04 → 05 (or `code-review.md`) |
| Bug report | `bugfix.md` → 05 or `code-review.md` → 06 (if it's a security bug) |
| Review a PR | `code-review.md` |
| Release | 07 |
| Dependency upgrade | 03 (the plan lists the upgrade as a gated action) → 04 → 05 → 06 (supply-chain check) |

## 5. Stack playbooks
Pick the playbook that matches your project, and combine them if needed (a full-stack app = web frontend + backend API + its database).

Tools named below are **examples only**. Your project's actual tools and scripts always take precedence. Step 00 finds them, and `docs/project-context.md` records them.

### 5.1 Web frontend (SPA, SSR, or static site)
*Examples: React, Vue, Svelte, Angular, Next.js, Nuxt, Astro, plain HTML/CSS.*

- **Fill in first:** supported browsers, rendering mode (static, client-side, or server-side), the design system if any, and the accessibility target.
- **Step 02 decides:** framework and rendering mode, state management, styling approach, API client strategy, hosting (static/CDN or server), and test tooling (unit/component tests plus a browser end-to-end tool).
- **STEP-01 (setup):** project scaffold, linter and formatter, type-checking, a unit/component test runner, one passing smoke test, and CI running lint, type-check, test, and build.
- **Lead roles:** Frontend Engineer; DevOps Engineer (hosting and CI).
- **QA (05):** loading, empty, error, and offline states. Keyboard-only navigation, screen-reader labels, and contrast. Responsive breakpoints. Cross-browser checks on the supported list.
- **Security (06):** XSS (raw HTML injection), token storage, CSP and security headers, secrets accidentally bundled into client code, third-party scripts.
- **Release (07):** build size and performance budget, cache-busting, environment variables per environment, and the rollback (previous build or CDN version).

### 5.2 Backend API or service
*Examples: Node.js (Express, Fastify, NestJS), Python (FastAPI, Django), Go, Java/Kotlin (Spring), .NET, Ruby on Rails, PHP (Laravel).*

- **Fill in first:** API style (REST, GraphQL, or gRPC), consumers, data sensitivity, and hosting.
- **Step 02 decides:** framework, layering, auth approach, datastore (with the Database Engineer), API contract format (OpenAPI or schema), error model, configuration and secrets, and deployment.
- **STEP-01 (setup):** scaffold, linter and formatter, types or static analysis, a test runner with one unit and one integration test, a health-check endpoint, and CI.
- **Plan tip:** use vertical slices (one endpoint end to end, with tests) rather than one layer at a time.
- **Lead roles:** Backend Engineer; Database Engineer; Security Engineer (always involved in step 02 for auth).
- **QA (05):** contract tests against the API spec, validation errors, authorization per role, pagination, idempotency on retries, timeouts from dependencies.
- **Security (06):** authorization checks on every endpoint, injection (SQL/NoSQL/command), mass assignment, rate limiting, logs that leak sensitive data, dependency audit.
- **Release (07):** migration order versus deploy order, configuration and secrets present in the target environment (names only), health checks, dashboards and alerts, and the rollback.

### 5.3 Full-stack web app
*Combine 5.1, 5.2, and the database guidance. Examples: Next.js or Nuxt with an API, Django or Rails with templates, a SPA plus an API.*

- **Step 02 decides:** monorepo or separate apps, a shared types/contract strategy, and where authentication and sessions live.
- **Plan tip:** order each feature as **schema → API → UI**, with each slice deployable on its own. Assign roles per step (Database → Backend → Frontend).
- **QA (05):** end-to-end tests of the primary journeys from `docs/requirements.md`, plus the per-layer checks from 5.1 and 5.2.

### 5.4 Mobile app
*Examples: Swift/SwiftUI (iOS), Kotlin/Jetpack Compose (Android), Flutter, React Native, .NET MAUI.*

- **Fill in first:** target platforms and minimum OS versions, offline needs, push notifications, and app-store constraints.
- **Step 02 decides:** native or cross-platform, navigation, state and offline storage, API sync strategy, secure storage, and build and signing pipeline.
- **STEP-01 (setup):** project scaffold, linter, unit and widget/UI test setup, and CI that builds for each platform. Signing keys are delivered by CI secrets, never committed; this needs approval.
- **Lead roles:** Frontend Engineer (for the UI); Backend Engineer (for the API); DevOps Engineer (builds and signing).
- **QA (05):** different screen sizes and OS versions, poor or no network, app backgrounding and resuming, permission prompts and denials, accessibility (screen readers and dynamic type), upgrades from the previous version.
- **Security (06):** secure storage of tokens (Keychain/Keystore), certificate handling, deep-link validation, data in logs and backups. Use OWASP Mobile Top 10 as the checklist.
- **Release (07):** version and build numbers, store metadata, staged rollout, a forced-update strategy, crash reporting. Rollback is usually a hotfix release, so plan for that.

### 5.5 Desktop app
*Examples: Electron, Tauri, .NET (WPF, WinUI), Qt, native macOS.*

- **Step 02 decides:** framework, auto-update mechanism, local data storage, process/IPC model, and code signing.
- **QA (05):** each supported OS, installing, upgrading, and uninstalling, offline use, file permissions, high-DPI and accessibility.
- **Security (06):** IPC boundaries and remote-content isolation (especially for Electron), update-channel integrity, local file and secret storage.
- **Release (07):** signed and notarized installers, an update rollout and rollback path.

### 5.6 CLI tool, library, or SDK
*Examples: Node.js packages, Python packages, Go modules, Rust crates, .NET or Java libraries.*

- **Fill in first:** supported runtime versions and operating systems, the public API surface, and the versioning policy (semantic versioning).
- **Step 02 decides:** API design and naming, error handling, configuration, packaging and distribution, and the compatibility policy.
- **STEP-01 (setup):** package manifest, linter, type-check, a test runner, and a CI matrix covering the supported versions and operating systems.
- **Lead roles:** Tech Lead, Backend Engineer (for logic), and DevOps Engineer (publishing).
- **QA (05):** public-API tests, backward-compatibility checks against the previous version, the CLI's exit codes, stdout/stderr, help text, and invalid arguments, and cross-platform paths.
- **Security (06):** command injection, path traversal, unsafe deserialization, the dependency footprint, and publishing credentials.
- **Release (07):** changelog, version bump, a test of the built package, publishing (needs approval), and deprecation notices.

### 5.7 Data pipeline or analytics
*Examples: Python with SQL, dbt, Spark, Airflow or another orchestrator, notebooks promoted into jobs.*

- **Step 02 decides:** batch or streaming, orchestration, storage layers, schema evolution, data-quality checks, and backfill strategy.
- **Lead roles:** Database Engineer, Backend Engineer, and DevOps Engineer (scheduling and infrastructure).
- **QA (05):** data-quality assertions (row counts, nulls, uniqueness, ranges), idempotent re-runs, late or duplicate data, and tests on small synthetic datasets.
- **Security (06):** personal-data classification and masking, access per dataset, credentials in notebooks or job configurations.
- **Release (07):** backfill plan, downstream consumers notified, and the rollback (re-run or restore).

### 5.8 AI / LLM application
*Examples: chatbots, retrieval-augmented generation (RAG), agents with tool use, AI features inside an existing app.*

- **Fill in first:** model provider(s), what data is sent to the model, cost and latency budgets, and acceptable failure behavior.
- **Step 02 decides:** model choice, prompt and version management, retrieval design, tool and agent permissions, an evaluation approach, fallbacks, and cost controls.
- **Lead roles:** Architect, Backend Engineer, and Security Engineer (always).
- **QA (05):** an evaluation set of representative inputs with expected properties, regression evaluations when prompts or models change, handling of empty, long, multilingual, or adversarial input, timeouts, and rate limits. Model output varies between runs, so assert properties of the output rather than exact text.
- **Security (06):** prompt injection (direct, and indirect through retrieved content), over-permissive tools, data leakage into prompts or logs, output used without validation. Use the OWASP Top 10 for LLM Applications as the checklist.
- **Release (07):** evaluation results on this exact revision, cost and usage monitoring, a kill switch or feature flag, and the pinned model version.

## 6. Command reference by ecosystem
Step 00 should find the **project's own** commands (scripts in a manifest, a `Makefile`, or task runners) and record them in `docs/project-context.md`. The table below shows common defaults, for orientation only.

| Ecosystem | Install | Lint / format | Types / static | Test | Build | Dependency audit* |
|-----------|---------|---------------|----------------|------|-------|-------------------|
| Node.js (npm) | `npm ci` | `npm run lint` | `npx tsc --noEmit` | `npm test` | `npm run build` | `npm audit` |
| Python | `pip install -r requirements.txt` or `uv sync` | `ruff check .` | `mypy .` | `pytest` | `python -m build` | `pip-audit` |
| Go | `go mod download` | `go vet ./...` | (compiler) | `go test ./...` | `go build ./...` | `govulncheck ./...` |
| Java / Kotlin (Maven) | `./mvnw dependency:resolve` | (plugin) | (compiler) | `./mvnw test` | `./mvnw package` | (plugin) |
| Java / Kotlin (Gradle) | `./gradlew dependencies` | (plugin) | (compiler) | `./gradlew test` | `./gradlew build` | (plugin) |
| .NET | `dotnet restore` | `dotnet format --verify-no-changes` | (compiler) | `dotnet test` | `dotnet build` | `dotnet list package --vulnerable` |
| Rust | `cargo fetch` | `cargo fmt --check`, `cargo clippy` | (compiler) | `cargo test` | `cargo build --release` | `cargo audit` |
| PHP | `composer install` | (project tool) | `vendor/bin/phpstan analyse` | `vendor/bin/phpunit` | — | `composer audit` |
| Ruby | `bundle install` | `bundle exec rubocop` | — | `bundle exec rspec` | — | `bundle exec bundle-audit` |
| Flutter / Dart | `flutter pub get` | `dart format --set-exit-if-changed .` | `flutter analyze` | `flutter test` | `flutter build <target>` | — |

\* Some audit tools are not installed by default. Installing one is an approval-gated action (`AGENTS.md` section 4). Until then, the check is reported as `NOT RUN`.

## 7. Troubleshooting
| Symptom | Fix |
|---------|-----|
| The assistant edits files without waiting for approval | Say: *"Stop. Re-read `AGENTS.md` sections 3–4, revert your unapproved changes, and show me the plan."* Check that your tool actually loads `AGENTS.md`. |
| The report says `PASS` with no command shown | Say: *"Show the exact command and output for each result. Anything you didn't run is `NOT RUN`."* |
| A later step ignores earlier decisions | The doc wasn't written or approved. Check its `Status` and `Last updated` fields, and re-run the approval for the earlier step. |
| The assistant invents the stack or commands | Mark the fields `UNKNOWN` in `docs/project-context.md`, then re-run 00. |
| A step is too big, or the diff is hard to review | Stop. Ask step 03 to split the step, then re-run 04 on the smaller pieces. |
| The session lost context mid-feature | Start a new session and reference the docs plus the pasted `STEP-` row. Don't re-paste the whole conversation. |
| Tests fail before you changed anything | Report it as a pre-existing failure, with evidence. Fix it in a separate step (or with `bugfix.md`) first. Never weaken the tests. |
