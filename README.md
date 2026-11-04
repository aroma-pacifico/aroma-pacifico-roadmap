# Aroma Pacífico pilot

Design and infrastructure-as-code work for the 2026 update of the coffee traceability pilot (Cauca, Huila and Tolima).

Work is tracked on the [Aroma Pacífico Pilot board](https://github.com/orgs/aroma-pacifico/projects/1).

---

## Repository Map

```text
aroma-pacifico/
|-- AGENTS.md                  # Normative engineering constitution for agents and humans
|-- CLAUDE.md                  # Claude Code assistant context (@AGENTS.md)
|-- GEMINI.md                  # Gemini and Antigravity IDE guidance
|-- CONTRIBUTING.md            # Repository contribution and branch guidelines
|-- .gitmessage                # Conventional commit message template
|-- .agents/
|   `-- skills/                # Antigravity discoverable agent skills
|       |-- diagram-agent/     # Architecture diagram authoring and verification
|       |-- doc-agent/         # Technical documentation and troubleshooting log
|       `-- git-agent/         # Trunk-based git workflow and PR packaging
|-- .github/
|   |-- pull_request_template.md # PR submission template
|   `-- workflows/
|       `-- pr-conventions.yml # Conventional commits and zero-emoji PR gates
|-- docs/
|   `-- case/
|       `-- case-statement.pdf # Official challenge case statement (single source of truth)
`-- standards/
    |-- documentation.md       # Technical writing and living documentation standards
    |-- diagrams.md            # Draw.io and Mermaid architecture diagram standards
    |-- git-workflow.md        # Trunk-based development and conventional commits guide
    |-- terraform-iac-best-practices.md # Core Terraform standards and AI agent rules
    `-- iac-rules/             # 26 normative reference module rules (pc-iac-001..026)
        `-- README.md          # English index of reference module rules
```
