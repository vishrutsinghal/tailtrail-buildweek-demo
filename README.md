# TailTrail for OpenAI Build Week

TailTrail is a local, approval-first workflow layer for Codex. It helps keep
AI-assisted code changes focused: plan before editing, map the relevant code,
approve the change, run focused validation, review the result, and preserve
clear evidence.

## Build Week demo

The included `buildweek-demo-project/` is a small Python claims service with an
intentional validation bug: it accepts zero-dollar claims even though amounts
must be positive. The demo shows TailTrail guiding Codex through a small,
reviewable fix.

```text
Failing test -> Navigator plan -> Code Graph -> approval -> Codex fix -> tests -> review -> repeatable proof
```

## Requirements

- Python 3.9 or later
- Codex with GPT-5.6 for the live Build Week recording

No model/API key, package installation, network access, database, or external
scanner is required for the judge test path.

## Judge test path

From this repository root:

```bash
python3 tailtrail/scripts/tailtrail.py start "fix the claim amount validation bug and add focused validation" --root buildweek-demo-project --changed src/claims_api/validation.py
python3 tailtrail/scripts/tailtrail.py graph ast --root buildweek-demo-project --changed src/claims_api/validation.py --depth v2
python3 tailtrail/scripts/tailtrail.py eval scenario report --scenario buildweek-validation
```

The `buildweek-validation` report is deterministic saved-artifact evidence. It
does not claim live model performance, production-defect reduction, or exact
token savings.

## Use with Codex

This repository includes a Codex plugin manifest and the TailTrail skills.
Open the repository in Codex, then use `@tailtrail` for implementation guidance
or `@tailtrail-review` for requirement-aware review.

For the live demo, first run the failing test and then ask Codex:

```text
Run TailTrail Navigator first for this task: fix the claim amount validation bug
and add focused validation. Use root buildweek-demo-project and changed file
src/claims_api/validation.py. Show the plan only. Do not implement until I approve.
```

The detailed recording flow is in
[DEMO-RUNBOOK.md](buildweek-demo-project/DEMO-RUNBOOK.md), and copy-paste prompts
are in [DEMO-PROMPTS.md](buildweek-demo-project/DEMO-PROMPTS.md).

## Submission materials

- [Project description](buildweek-demo-project/SUBMISSION-NOTES.md)
- [Submission checklist](buildweek-demo-project/BUILDWEEK-SUBMISSION.md)
- [Video script](PITCH-SCRIPT.md)
- [One-page overview](PITCH-ONE-PAGER.md)

## Boundaries

TailTrail does not replace Codex, tests, CI, scanners, security review, or human
review. Token savings are estimates unless measured provider telemetry is
supplied.
