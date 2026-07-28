# CLAUDE.md

Project instructions for Claude Code working in the Jahia QA Harness repository.
Read [AGENTS.md](AGENTS.md) in full before invoking any command — it is the
master instruction set (pipeline stages, constraints, extension points) and
applies to every coding agent, Claude Code included.

## Quick orientation

This repo is a **QA harness**: it validates a delivered feature from the product
perspective (acceptance criteria, test adequacy, persona UAT, documentation),
not the code-correctness perspective a developer harness already covers.

## Available commands

Six slash commands live in `.claude/commands/` (mirrored for GitHub Copilot as
`.github/copilot/*.prompt.md` — keep both in sync when editing either one):

| Command | Pillar / Stage | What it does |
|---|---|---|
| `/qa-run` | Orchestrator | Runs all six stages end-to-end, enforcing both human checkpoints |
| `/qa-ac-validate` | A — Acceptance Criteria | Drafts or validates ACs against test evidence |
| `/qa-cypress-analyze` | B — Test Adequacy | Analyses the Cypress suite for coverage gaps |
| `/qa-persona-uat` | C — Persona UAT | Generates and evaluates persona scenarios |
| `/qa-doc-review` | D — Documentation | Checks docs against user-visible changes |
| `/qa-report` | Stage 6 — QA Decision | Assembles the final report + release recommendation |

Run the computational sensors (`harness/sensors/*/*.js`, plain Node ≥ 18, zero
dependencies) with the `Bash` tool before the inferential (LLM) evaluation in
each pillar — they provide deterministic evidence that anchors the analysis.
Never skip this step; never fabricate a PASS in its place.

## Non-negotiable constraints

1. No fabrication — if evidence is absent, report MISSING, never infer PASS
2. Never skip the Stage 3 (scenario approval) or Stage 6 (final sign-off) human checkpoints
3. Never finalise ACs alone in REFINEMENT mode — wait for QA engineer sign-off
4. Accessibility scenarios are always MANUAL-REQUIRED, never synthetic PASS
5. Never issue a release READY verdict with `.only` left in a Cypress test file
6. Never issue READY with a missing migration guide for a declared breaking change

See `AGENTS.md` for the full pipeline, guides, sensors, templates, and
extension instructions (adding a persona, a scenario pattern, a doc standard).
