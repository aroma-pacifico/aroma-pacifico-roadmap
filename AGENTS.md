# AGENTS.md — Aroma Pacífico Engineering Constitution

**Normative for every human and every AI agent that writes code, infrastructure, manifests or documentation in the Aroma Pacífico project.**

Adapted from SINTRATEL and FrioAndes reference standards.

---

## 0. Scope, Precedence, and Distribution

This file is the single normative constitution for how work is produced in this project. It is not advisory. Where it conflicts with habit, memory, a tutorial, or a model's prior training, **this file wins**.

**Precedence, highest first:**

1. An explicit instruction from the user in the current conversation
2. This file (`AGENTS.md`)
3. The `standards/` files (`standards/terraform-iac-best-practices.md`, `standards/iac-rules/`, `standards/documentation.md`, `standards/diagrams.md`, `standards/git-workflow.md`)
4. Repository-local `CONTRIBUTING.md`
5. Existing conventions visible in surrounding code
6. General best practice

**Distribution.** This repository is the canonical copy of `AGENTS.md`. Agents and developers operating in this repository or in linked project repositories must adhere to these rules. `CLAUDE.md` imports this file on its first line (`@AGENTS.md`), and `GEMINI.md` points Gemini and Antigravity to it.

**Maintenance.** Treat this file as a *failure log, not a wishlist*. When an agent makes the same mistake twice, this file is missing a line. Add the line.

---

## 1. Prime Directives

1. **English only.** Code, comments, documentation, commits, PR titles and bodies, branch names, file names, directory names. No exceptions.
2. **Zero emojis.** Strictly prohibited across all commits, branches, PRs, documentation, code, and agent responses.
3. **Academic delivery: plan-only.** Deliver design, modular Terraform, cost evidence, and a presentation. Never run `terraform apply`/`destroy`, never deploy, never register providers, and never create live cloud resources.
4. **Requirements source.** `docs/case/case-statement.pdf` is the sole source of requirements. Never invent a value, measurement, approval, or rehearsal result. Every assumption not in the case statement must be registered in the decision log (`docs/decision-log.md`) with a unique ID.
5. **Trunk-based development.** Direct commits to `main` are prohibited. Work on short-lived branches (`<type>/<issue-number>-<kebab-slug>`) under 48 hours and under 400 lines.
6. **Atomic Conventional Commits.** Every commit must follow `<type>(<scope>): <lowercase imperative subject>` with a mandatory `Refs #<issue>` footer. Commit incrementally as you go.
7. **Agent publishing boundary.** Agents commit locally and may push only their own assigned feature branch to open a PR to `main`. Agents never push to `main`, never merge, never force-push, and never create repositories. The lead reviews and merges.
8. **Repository model.** This repository holds architecture, ADRs, plans, costs, design system, and release notes. Terraform code belongs in a dedicated IaC repository created in task B01; no `.tf` files in this repository.
9. **Binding IaC rules.** The 26 reference module rules in `standards/iac-rules/` (`pc-iac-001.md` through `pc-iac-026.md`) and `standards/terraform-iac-best-practices.md` are binding for all Terraform work. Renaming a resource requires a `moved` block.
10. **Show your verification.** "Done" requires running formatting, validation, and verification checks and showing the actual terminal output. Never state something works without showing the verification evidence.

---

## 2. Language and Typography

**English, everywhere, without exception.**

| Surface | Rule |
|---|---|
| Source code, identifiers | English |
| Comments and docstrings | English |
| Documentation, README, ADRs | English |
| File and directory names | English, `kebab-case` for files, `kebab-case` for directories |
| Commit messages | English, imperative mood |
| Branch names | English |
| PR titles and bodies | English |
| Terraform variables, resources, outputs | English, `snake_case` |
| Issue and Kanban card titles | English |

No accents, no Spanish words, no mixed-language identifiers.

### Strict Zero-Emoji Mandate
Emojis are strictly prohibited across all surfaces. All communication and artifacts must use clean, professional plain text.
- Replace status icons with explicit plain text words: use `SUCCESS` instead of checkmarks, `WARNING` instead of caution triangles, and `ERROR` instead of crosses.

---

## 3. Requirements, Assumptions, and Truth

- **Single source of truth**: `docs/case/case-statement.pdf` is the only source of project requirements.
- **Decision and Assumption Log**: If a parameter, dimension, retention period, or design choice is not specified in `docs/case/case-statement.pdf`, it cannot be silently invented. It must be logged in the project decision log (`docs/decision-log.md`, created by task A01) with a unique ID: `ASM-NNN` for assumptions, `ADR-NNN` for architecture decision records (stored in `docs/adr/`) and `PD-NNN` for pending decisions.
- **Never invent evidence**: Do not invent performance measurements, latency metrics, failover timings, human approvals, or rehearsal results. Label latency, failover, rollout, and recovery metrics as targets or future tests.

---

## 4. Academic Delivery Model

This project is an academic DevOps challenge representing the 2026 update of a coffee traceability pilot across Cauca, Huila, and Tolima.
- **Scope**: High-level design, reusable modular Terraform, cost forecasts/evidence, and presentation materials.
- **Plan-only boundary**: No live cloud platform or running application is required.
- **Prohibited cloud mutations**:
  - Never run `terraform apply` or `terraform destroy`
  - Never run `kubectl apply`, `helm install`, or cloud resource creation commands
  - Never register cloud providers or create remote infrastructure
  - Never execute live deployment pipelines

---

## 5. Repository Model

This repository (`aroma-pacifico`) is the central architecture and process repository.

**What lives here:**
- Architecture specifications, design diagrams, data flow models
- Architectural Decision Records (`docs/adr/`)
- Requirements and case statement (`docs/case/`)
- Project decision and assumption log (`docs/decision-log.md`)
- Cost forecasts and Infracost plan evidence
- Presentation artifacts and release notes
- Engineering standards (`standards/`) and agent skills (`.agents/skills/`)

**What does NOT live here:**
- Live application source code
- Terraform `.tf` files (Terraform lives in a dedicated IaC repository created in task B01)
- State files (`.tfstate`), plans (`.tfplan`), credentials, or secrets

---

## 6. Source Control Architecture (Trunk-Based Development)

### 6.1 Trunk Stability
- `main` is protected and always in a releasable state.
- Direct commits to `main` are strictly forbidden.

### 6.2 Short-Lived Branches
- Every branch branches off `main` and merges back into `main`.
- Naming convention: `<type>/<issue-number>-<kebab-slug>` (e.g. `feat/12-telemetry-ingestion`, `chore/0-bootstrap-agent-rules`).
- Valid types: `feat`, `fix`, `docs`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`.
- Branch lifespan: Maximum 48 hours. Target PR size: under 400 lines.

### 6.3 Incremental Atomic Commits
- Commit changes incrementally as each logical unit of work is completed and verified.
- Do not batch all edits into a single end-of-session commit.

### 6.4 Conventional Commits
```text
<type>(<scope>): <lowercase imperative subject (max 72 chars, NO EMOJIS)>

[optional body explaining why, wrapped at 72 chars]

Refs #<issue-number>
```
- Imperative mood, lowercase start, no trailing period, no emojis.
- Body explains the rationale and trade-offs.
- `Refs #<issue-number>` footer is mandatory.
- No tool attribution: no `Co-Authored-By` trailer for an AI tool, no `Generated with` line, no session URL, and no notes about how the content was produced, in commits or PR bodies. `.claude/settings.json` suppresses Claude Code attribution; do not reintroduce it by hand.

### 6.5 Agent Publishing Model
- **Agents commit locally**: Local commits are expected as work progresses.
- **Feature branch push**: Agents may push only their own assigned feature branch (`<type>/<issue>-<slug>`) to the remote repository.
- **Pull Request creation**: Agents may open a Pull Request targeting `main`.
- **Prohibited agent actions**: Agents must never push directly to `main`, never merge PRs, never force-push (`git push --force`), never delete remote branches, and never create repositories.
- **Review and merge**: The lead reviews the PR, inspects verification output, and executes the squash merge.

---

## 7. Pull Requests

### Title
The PR title must be a valid Conventional Commit header (max 72 characters, no emojis), because repository squash-merges make the PR title the commit subject on `main`.

### Body
Use `.github/pull_request_template.md`:
1. What changed and why (2-3 concise sentences).
2. Issue traceability: `Closes #<issue>` or `Refs #<issue>`.
3. Acceptance criteria addressed (quoted from the issue with satisfaction notes).
4. Verification evidence (actual terminal commands run and output shown).
5. Terraform plan output (if applicable, with destroys/replacements called out).
6. Risk and rollback considerations.

---

## 8. Terraform and Infrastructure as Code

Detailed standards live in `standards/terraform-iac-best-practices.md` and `standards/iac-rules/`.
The 26 `pc-iac` rules (`standards/iac-rules/pc-iac-001.md` through `pc-iac-026.md`) are binding for every Terraform change.

### Key Enforceable Rules:
- **Reference modules**: Follow the mandatory layout defined in `pc-iac-001.md` (`main.tf`, `variables.tf`, `outputs.tf`, `versions.tf`, `README.md`).
- **No provider or backend blocks in child modules**: Child modules must remain pure and reusable (`pc-iac-005.md`).
- **Variables and outputs**: Every variable must declare `type` and `description` (`pc-iac-002.md`). Every output must declare `description` (`pc-iac-007.md`). No hardcoded environment-specific defaults.
- **Multiplicity**: Use `for_each` for multiple resource instances; use `count` only for boolean enabling (`count = var.enabled ? 1 : 0`) (`pc-iac-010.md`).
- **Version constraints**: Minimum Terraform core with `>=` (for example `>= 1.14.0`). Providers use a strict `~>` range in root stacks and a compatible `>=` minimum in reference modules (`pc-iac-006.md`). Scoped `.terraform.lock.hcl` committed in root stacks only.
- **Remote state**: Remote backend in S3 with encryption, versioning, and state locking (`pc-iac-008.md`). Strictly no local state.
- **Refactoring**: Renaming or moving a resource address requires a `moved` block. Never rename in place without `moved` (`standards/terraform-iac-best-practices.md` §12).
- **Secrets**: Mark secret variables with `sensitive = true` (`pc-iac-016.md`). Never commit plaintext secrets.
- **Domain separation**: Separate networking, compute, security, and data into distinct lifecycle domains (`pc-iac-022.md`).
- **Testing**: Plan-mode unit tests (`.tftest.hcl`) for reference modules (`pc-iac-018.md`).
- **Identity separation**: Agents operate with plan-only identity; apply is strictly prohibited (§4).

---

## 9. Documentation and Diagram Standards

- **Documentation**: Follow `standards/documentation.md`. Write explanatory prose and Markdown tables over long bulleted lists. Maintain dynamic README and directory tree accuracy. Record friction in `docs/troubleshooting-log.md`.
- **Diagrams**: Follow `standards/diagrams.md`.
  - Canonical format: Uncompressed UTF-8 Draw.io XML (`.drawio`) is preferred; Mermaid is accepted.
  - Required exports: Editable SVG (primary publication) and PNG (preview), committed atomically with the source.
  - Verification: Every diagram must undergo an individual semantic check, visible render, and inspection at actual publication size. Parser success is not visual approval.
  - Native official vendor libraries (AWS/cloud native); no generic shapes where official icons exist; no emojis.

---

## 10. Definition of Done

A task is not done until every applicable criterion is satisfied and verification evidence is shown:

**Every Change:**
- [ ] English throughout (code, comments, documentation, commit messages, PR).
- [ ] Zero emojis across all files, commits, PRs, and messages.
- [ ] Conventional Commit with `Refs #<issue>` footer.
- [ ] Branch created from latest `main` using `<type>/<issue>-<slug>`.
- [ ] Every acceptance criterion satisfied, or blockers explicitly documented.
- [ ] Verification commands executed and terminal output displayed in the report.

**Terraform Changes (when applicable in IaC repo):**
- [ ] `terraform fmt -check -recursive` clean.
- [ ] `terraform validate` clean on all stacks and modules.
- [ ] `tflint` clean.
- [ ] Security scanners (`trivy`/`checkov`) clean or findings justified.
- [ ] Plan-only evidence produced; destroys and replacements explicitly called out.
- [ ] `moved` blocks present for any relocated or renamed resource.

**Documentation and Diagram Changes:**
- [ ] Links resolve and directory maps match the filesystem.
- [ ] Diagrams re-exported to SVG and PNG, inspected at publication size.
- [ ] Architectural decisions recorded in numbered ADRs (`docs/adr/`).

---

## 11. Never / Always Quick Reference

### Never

| Prohibited Action | Rationale |
|---|---|
| Run `terraform apply` or `terraform destroy` | Academic delivery is strictly plan-only (§4). |
| Direct commit to `main` | Trunk-based development requires PRs (§6.1). |
| Force-push (`git push --force`) or merge own PR | Agents never force-push; lead reviews and merges (§6.5). |
| Use emojis anywhere | Strict Zero-Emoji mandate (§2). |
| Invent values, measurements, or approvals | All requirements originate from `docs/case/case-statement.pdf` (§3). |
| Rename Terraform resource without `moved` block | Renaming in-place causes a destroy and recreate (§8). |
| Put `.tf` files in this repository | Architecture repo only; IaC lives in separate repo (§5). |
| Hardcode credentials, account IDs, or secrets | Use variables, data sources, and secret managers (§8). |

### Always

| Required Action | Rationale |
|---|---|
| Write in English | Project-wide consistency (§2). |
| Reference issue in commits (`Refs #<issue>`) | Traceability across git history (§6.4). |
| Commit atomically as you go | Avoid end-of-session bulk commits (§6.3). |
| Keep feature branches under 48 hours | Prevent branch drift and merge debt (§6.2). |
| Log assumptions in `docs/decision-log.md` | Keep all assumptions traceable and numbered (§3). |
| Export diagrams to SVG and PNG | Provide publication-ready visual assets (§9). |
| Show verification output | "Done" requires concrete verification proof (§10). |

---

## 12. Grounding and Dealing with Errors

- When a tool, linter, or compiler contradicts you, the tool is right. Read the documentation and schemas.
- If an acceptance criterion cannot be satisfied, state the gap clearly and document the blocker. Never quietly reduce the scope.
- Maintain institutional transparency: if a check failed, display the failure and the resolution applied.
