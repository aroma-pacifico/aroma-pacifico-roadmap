# Delivery audit: board against repositories

| Field | Value |
|---|---|
| Date | 2026-11-11 |
| Scope | Every roadmap issue A01-A25, B01-B13 and G01-G06 (44 issues) |
| Method | Each acceptance criterion was checked against `main` of the target repository, read-only. Open pull requests and unmerged branches were listed but never counted as delivered. |
| Trigger | B06, B08 and B10 were found marked Done while their stack wiring was missing. This audit looks for any other case of the same kind. |

## 1. Result

| Verdict | Count | Issues |
|---|---|---|
| OK | 37 | A01-A24, B02, B03, B04, B05, B06, B08, B10, B11, G01, G02, G03, G04, G05 |
| Partial | 5 | A25, B01, B07, B09, B12 |
| Missing | 2 | B13, G06 |

No other issue shares the B06, B08 and B10 defect: every other IaC issue marked Done (B02, B03, B04, B05, B11) has both halves on `main`. B06, B08 and B10 are now complete too, because the wiring pull requests merged after the issues were reopened.

Verdict meaning. OK: every acceptance criterion is satisfied by merged content. Partial: the main deliverable is merged but at least one criterion is not satisfied. Missing: the deliverable is not on `main`.

## 2. IaC wiring check

An IaC task is complete only when the tagged module exists in `aroma-pacifico-terraform-modules` (half a) and a root stack in `aroma-pacifico-infrastructure` calls it at that tag (half b).

| Box | Task | Module and tag | Stack wiring | Both halves |
|---|---|---|---|---|
| D02 | B02 | `modules/state-backend`, v0.3.0 | `stacks/state-backend/main.tf`, ref v0.3.0 | Yes |
| D04 | B04 | `modules/network`, v0.1.0 and later | `stacks/network/main.tf`, ref v0.3.0 | Yes |
| D05 | B05 | `modules/collection-center-association`, v0.4.0 | `stacks/network/main.tf`, ref v0.4.0 | Yes |
| D06 | B06 | `modules/security`, v0.5.0 | `stacks/security/main.tf`, ref v0.5.0 | Yes |
| D07 | B07 | `modules/firewall-rules`, v0.3.0 | none | No: wiring missing |
| D08 | B08 | `modules/farm`, v0.2.0 and later | `stacks/workload/farm.tf`, ref v0.4.0 | Yes |
| D09 | B09 | `modules/telemetry-ingestion`, v0.4.0 | none; `stacks/workload/locals.tf` still reads `var.telemetry_references` | No: wiring missing |
| D10 | B10 | `modules/inference-functions`, v0.4.0 | `stacks/workload/inference_functions.tf`, ref v0.4.0 | Yes |

## 3. Audit table

Repository short names: roadmap, architecture, diagrams, design-system, presentation, ai-agents, modules (`aroma-pacifico-terraform-modules`), infra (`aroma-pacifico-infrastructure`), web. PR numbers belong to the repository named in the same cell.

| Issue | Board status | Evidence (repo, path, PR) | Verdict | Action needed |
|---|---|---|---|---|
| A01 | Done | architecture `docs/decision-log.md`, PR 3; linked from `README.md` | OK | None |
| A02 | Done | architecture `docs/adr/adr-001-primary-and-second-cloud.md`, PR 8 | OK | None |
| A03 | Done | architecture `docs/adr/adr-002-drone-flight-mode-and-governance.md`, PR 14 | OK | None |
| A04 | Done | architecture `docs/adr/adr-003-iac-tool-remote-state-and-pattern-module.md`, PR 10 | OK | None |
| A05 | Done | architecture `docs/legacy-2020.md`, PR 15; diagram in diagrams `legacy/legacy-2020.drawio`, PR 15 | OK | None |
| A06 | Done | architecture `docs/clarification-questions.md`, PR 18 | OK | None |
| A07 | Done | architecture `docs/addressing-plan.md`, PR 16; diagrams `network/addressing-plan.drawio`, PR 4 | OK | None |
| A08 | Done | architecture `docs/landing-zone.md`, PR 22; diagrams `accounts/landing-zone.drawio`, PR 5 | OK | None |
| A09 | Done | architecture `docs/security-and-identity.md`, PR 26; diagrams `security/identity-and-access.drawio`, PR 17 | OK | None |
| A10 | Done | architecture `docs/connectivity.md`, PR 21; diagrams `network/connectivity.drawio`, `network/no-signal-sequence.drawio`, PR 6 | OK | None |
| A11 | Done | architecture `docs/collection-center-network.md`, PR 23; diagrams `network/collection-center.drawio`, PR 10 | OK | None |
| A12 | Done | architecture `docs/firewall-policy.md`, PR 27; diagrams `security/firewall-policy.drawio`, PR 18 | OK | None |
| A13 | Done | diagrams `data-paths/telemetry.drawio`, `transporter-position.drawio`, `drone-objects.drawio`, PR 2 | OK | None |
| A14 | Done | architecture `docs/farm-monitoring.md`, PR 31; diagrams `flows/farm-monitoring-sequence.drawio`, PR 8 | OK | None |
| A15 | Done | architecture `docs/drone-service.md`, PR 28; diagrams `flows/drone-fumigation-sequence.drawio`, `flows/drone-state-machines.drawio`, PR 12 | OK | None |
| A16 | Done | architecture `docs/sack-and-trip.md`, PR 32; diagrams `flows/sack-states.drawio`, `flows/sack-and-trip-sequence.drawio`, PR 13 | OK | None |
| A17 | Done | architecture `docs/inference-functions.md`, PR 33; diagrams `flows/inference-functions.drawio`, PR 14 | OK | None |
| A18 | Done | architecture `docs/automation-and-pipelines.md`, PR 34; diagrams `pipelines/*.drawio`, PR 16 | OK | None |
| A19 | Done | architecture `docs/architecture.md` (sections 3 to 9 cover the 7 points, section 14 maps D01-D13), PR 37; diagrams `complete/architecture.drawio`, `.svg`, `.png`, PR 19 | OK | Low priority: `complete/architecture-iac.svg` and `.png` have no `.drawio` source in diagrams (diagram owner) |
| A20 | Done | architecture `docs/iac-plan-100h.md`, PR 38 | OK | None |
| A21 | Done | architecture `docs/observability.md`, `docs/dashboards/operational.json`, `docs/dashboards/cost.json`, PR 39 | OK | None |
| A22 | Done | architecture `docs/release-notes/` (two templates, two examples), PR 35 | OK | None |
| A23 | Done | architecture `docs/pilot-costs.md`, PRs 44 and 46 | OK | None |
| A24 | Done | design-system `brand/`, `tokens/`, `components/`, `icons/`, `docs/design-system.md`, PRs 4 and 5 | OK | None |
| A25 | Done | presentation `deck/aroma-pacifico-sustentacion.pptx` and `.pdf`, `docs/speaker-script.md`, `docs/defense-qa.md`, PRs 3, 4, 8 and 9. `docs/speaker-script.md` and `docs/defense-qa.md` state "Agent draft, not rehearsed" | Partial | Criterion "the team rehearses a full 20-minute run" is not met. SR1 and the team run the rehearsal, record it in the speaker script and update answer 17 of `docs/defense-qa.md` (presentation owner). Open presentation pull request 10 (deck refresh) does not change this |
| B01 | Done | infra layout (`stacks/`, `environments/`, `.github/workflows/`), `README.md` with prerequisites, `docs/diagram-boxes.md` D01-D13, PR 5. Branch protection is not enabled: the infra README (section "Branch protection") says a private repository needs a paid plan. The public modules repository has no protection rule either | Partial | SR1 enables branch protection on `main` of modules (public, possible today). For infra and the other private repositories SR1 decides between a plan upgrade and accepting the limitation in the decision log. Not reopened: the code deliverable is complete and the gap is an administrative step outside the repositories |
| B02 | Done | modules `modules/state-backend`, tag v0.3.0, PR 4; infra `stacks/state-backend/`, PR 3 | OK | None |
| B03 | Done | infra `environments/{dev,qa,pdn}/*.tfvars.example`, `environments/README.md`, `scripts/check-env-secrets.sh`, PRs 6 and 5 | OK | None |
| B04 | Done | modules `modules/network`, tags v0.1.0 to v0.3.0, PRs 6 to 11; infra `stacks/network/main.tf` ref v0.3.0 and `stacks/network/tests/network.tftest.hcl`, PRs 13 and 16 | OK | None |
| B05 | Done | modules `modules/collection-center-association`, tag v0.4.0, PR 21; infra `stacks/network/main.tf` ref v0.4.0 and `tests/association.tftest.hcl`, PR 4 | OK | None |
| B06 | Was In review, now Done | modules `modules/security`, tag v0.5.0, PRs 12 and 25; infra `stacks/security/main.tf` ref v0.5.0 and `tests/security.tftest.hcl`, PR 22; architecture PRs 43 and 53 | OK | Close the issue (done in this audit) |
| B07 | In progress (open) | modules `modules/firewall-rules`, tag v0.3.0, PR 20. No `module` call in any infra stack | Partial | B07b: wire firewall rules into `stacks/network` and `stacks/security` (SR2). Not touched by this audit |
| B08 | Was In review, now Done | modules `modules/farm`, tag v0.2.0 and later, PR 3; infra `stacks/workload/farm.tf` ref v0.4.0 and `tests/farm.tftest.hcl`, PR 21 | OK | Close the issue (done in this audit) |
| B09 | In progress (open) | modules `modules/telemetry-ingestion`, tag v0.4.0, PRs 22 to 24. No `telemetry_ingestion.tf` in `stacks/workload` | Partial | B09b: add `telemetry_ingestion.tf` and replace `var.telemetry_references` (SR2). Not touched by this audit |
| B10 | Was In review, now Done | modules `modules/inference-functions`, tag v0.4.0, PR 14; infra `stacks/workload/inference_functions.tf` ref v0.4.0 and `tests/inference_functions.tftest.hcl`, PR 20 | OK | Close the issue (done in this audit) |
| B11 | Done | infra `.github/workflows/infrastructure-ci.yml`, `floci-plan.yml`, `infracost.yml`, `pr-conventions.yml`, PRs 9 to 12 | OK | None |
| B12 | In review (open) | infra `.github/workflows/cd-promotion.yml`, `cd-plan.yml`, `scripts/cd-verify-approval.sh`, `scripts/cd-cost-summary.py`, `docs/cd-pipeline.md` (sections 5 to 7: approval record, notice, rollback), PRs 14, 19, 23 and 24. Branches `docs/32-cd-runbook` and `docs/32-cd-pipeline-runbook` still carry unmerged commits | Partial | SR2 merges or abandons the two runbook branches; then the issue can close. Not closed by this audit because not all its work is merged |
| B13 | In review (open) | Nothing on `main`. infra pull request 25 (`ci/33-end-to-end-plan`) is open with the end-to-end plan script, secret and state validation, and D01-D13 evidence | Missing | Merge pull request 25 after B07b, B09b and B12 land, then close (B13 assignees) |
| G01 | Done | ai-agents `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, `standards/`, `.agents/skills/`, `scripts/sync-rules.sh` (with `check`), PRs 1 and 2; copies verified in the six delivery repositories | OK | None |
| G02 | Done | modules `.github/workflows/module-ci.yml`, `infracost.yml`, `README.md`, PR 15 | OK | None |
| G03 | Done | ai-agents `standards/iac-rules/pc-iac-027.md`, `standards/terraform-iac-best-practices.md`, `AGENTS.md`, PR 3; sync PRs in the six delivery repositories | OK | None |
| G04 | Was In review, now Done | ai-agents `standards/iac-rules/pc-iac-028.md`, PR 4; modules `.github/workflows/module-ci.yml` job with the Floci service container, PR 19; pointers on B02, B11 and B13 in roadmap comments; sync PRs in the six delivery repositories | OK | Tick the criteria and close the issue (done in this audit) |
| G05 | Done | architecture `docs/adr/adr-004-drone-capability-orchestration.md`, PR 50; diagrams `complete/architecture.drawio` and `flows/inference-functions.drawio`, PR 23; presentation slide 11, PR 7 | OK | None |
| G06 | In review (open) | web has only `README.md` on `main`. Pull request 1 (`feat/46-technical-showcase-site`) is open | Missing | SR1 finishes and merges web pull request 1 |

## 4. Board corrections made by this audit

| Issue | Correction |
|---|---|
| B06, B08, B10 | Both halves are on `main`. The issues were closed automatically when the wiring pull requests merged during the audit; evidence comment posted and board status set to Done. |
| G04 | All criteria met on `main`. Criteria ticked, evidence comment posted, issue closed, board status Done. |
| B01, B04, B11, G03 | Closed with unticked boxes although the work is merged. Boxes verified and ticked (B01 keeps the branch protection box open). |
| A25, B01 | Comment posted naming the unmet criterion. Left closed, see the table. |
| B07, B09, B12, B13, G06 | In-flight work. Not closed and not edited. |

## 5. Items that still need work

| Item | Owner role | Work |
|---|---|---|
| B07 | SR2 | B07b firewall wiring in `stacks/network` and `stacks/security` |
| B09 | SR2 | B09b `telemetry_ingestion.tf` in `stacks/workload` |
| B12 | SR2 | Merge or drop the two runbook branches, then close |
| B13 | SR1 | Merge infra pull request 25 after B07b, B09b and B12 |
| G06 | SR1 | Merge web pull request 1 |
| A25 | SR1 and team | Full 20-minute rehearsal and record |
| B01 | SR1 | Branch protection on modules; decision for the private repositories |
| A19 (minor) | Diagram owner | `.drawio` source for `complete/architecture-iac` |

## 6. How to repeat the checks

Read-only commands, run from a clone of each repository on `main`:

```
gh project item-list 1 --owner aroma-pacifico --limit 100 --format json
git -C aroma-pacifico-infrastructure grep -n 'source *= *"git::' -- stacks
git -C aroma-pacifico-terraform-modules tag -l
git -C aroma-pacifico-terraform-modules ls-tree --name-only <tag> modules/
gh pr list -R aroma-pacifico/<repo> --state open
```

No decision-log entry was needed (IDs 440 to 449 unused).
