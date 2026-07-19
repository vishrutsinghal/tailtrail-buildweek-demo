<p align="center">
  <img src="assets/brand/tailtrail-mark.png" width="150" alt="TailTrail logo: a code trail moving forward" />
</p>

<h1 align="center">TailTrail</h1>

<p align="center">
  <strong>Keep AI-assisted code changes focused, reviewable, and provable.</strong>
  <br />
  OpenAI Build Week 2026 · Developer Tools submission
</p>

<p align="center">
  <code>Navigator-first</code> · <code>Local-first</code> · <code>Approval-first</code> · <code>No dependencies for the demo</code>
</p>

---

## The problem

Small coding tasks should stay small. But AI-assisted changes can drift into
unnecessary rewrites, lose the actual requirement, and make it hard to show why
a change is safe.

**TailTrail adds a lightweight workflow around Codex:** first make a plan, then
map the relevant code, get approval, make the smallest fix, run focused
validation, and leave clear evidence behind.

```mermaid
flowchart LR
    A[Failing test] --> B[Navigator plan]
    B --> C[Code Graph]
    C --> D[Human approval]
    D --> E[Codex makes the focused fix]
    E --> F[Focused tests]
    F --> G[Review + saved evidence]
```

### What the Navigator prints

```text
+--------------------------------------------+
| TailTrail                                  |
| Navigator online. Context stays lean.      |
|                                            |
| Navigator * Code Graph * Guardrails        |
| AIDLC * Review Lenses * Test Precision     |
| Token Budget * CI/Sonar * Security         |
| Learning * Handoff * Value Reports         |
| Meta-Harness * Shared Metadata             |
+--------------------------------------------+
```

## See it in two minutes

The included `buildweek-demo-project/` is a tiny Python claims service with one
intentional bug: it accepts a zero-dollar claim even though every amount must be
positive.

| You will see | Why it matters |
| --- | --- |
| A test fail for the right reason | The starting state is honest and reproducible. |
| Navigator plan before edits | Codex gets focused context instead of an open-ended rewrite request. |
| Code Graph impact map | The demo identifies the validation code and its focused test. |
| Small approved fix and test run | The result is validated, not merely described. |
| Evaluation Harness report | Saved artifacts make the submission replayable. |

> **Demo boundary:** the initial failing test is intentional. It is the bug fixed
> during the live recording—not a broken setup.

## Judge quickstart

**Requirements:** Python 3.9+ and a shell. The deterministic judge path needs
no API key, package install, network access, database, or external scanner.

From the repository root:

```bash
# 1. Show the approval-first plan — no edits are made.
python3 tailtrail/scripts/tailtrail.py start "fix the claim amount validation bug and add focused validation" --root buildweek-demo-project --changed src/claims_api/validation.py

# 2. Map the exact implementation and test scope.
python3 tailtrail/scripts/tailtrail.py graph ast --root buildweek-demo-project --changed src/claims_api/validation.py --depth v2

# 3. Replay the committed evaluation evidence.
python3 tailtrail/scripts/tailtrail.py eval scenario report --scenario buildweek-validation
```

On Windows, use `python` instead of `python3` if needed.

### Run the demo test

```bash
cd buildweek-demo-project
python3 -m unittest discover -s tests -v
```

Before the live fix, `test_rejects_zero_amount` fails by design. After updating
`src/claims_api/validation.py` to reject `amount <= 0`, all three tests pass.

## Use it with Codex

This repository includes a Codex plugin manifest plus bundled `@tailtrail` and
`@tailtrail-review` skills. Open this repository in Codex and start the demo
with the following prompt:

```text
Run TailTrail Navigator first for this task: fix the claim amount validation bug
and add focused validation. Use root buildweek-demo-project and changed file
src/claims_api/validation.py. Show the plan only. Do not implement until I approve.
```

### How Codex and GPT-5.6 are used

| Capability | Meaningful role in the demo |
| --- | --- |
| **Codex** | Inspects the code and tests, follows the Navigator plan, implements the approved minimal fix, and runs focused validation. |
| **GPT-5.6** | Powers the live reasoning conversation: translating the request into a scoped plan, explaining impact, and reviewing requirement fulfillment. |
| **TailTrail** | Supplies local workflow structure, guardrails, code mapping, evidence labels, and deterministic evaluation artifacts. |

TailTrail does not replace Codex, human judgment, tests, CI, security review, or
scanners. Token figures are estimates unless measured provider telemetry exists.

## Repository map

| Path | Purpose |
| --- | --- |
| [`buildweek-demo-project/`](buildweek-demo-project/) | The small, reproducible claims-service demo. |
| [`tailtrail/`](tailtrail/) | Bundled runtime, skills, scripts, templates, and evaluation harness. |
| [`.codex-plugin/plugin.json`](.codex-plugin/plugin.json) | Codex plugin manifest. |
| [`assets/brand/tailtrail-mark.png`](assets/brand/tailtrail-mark.png) | TailTrail brand mark used above. |

## Submission materials

- [Project description](buildweek-demo-project/SUBMISSION-NOTES.md)
- [Submission checklist](buildweek-demo-project/BUILDWEEK-SUBMISSION.md)
- [Recording runbook](buildweek-demo-project/DEMO-RUNBOOK.md)
- [Copy-paste demo prompts](buildweek-demo-project/DEMO-PROMPTS.md)
- [Video script](PITCH-SCRIPT.md)
- [One-page overview](PITCH-ONE-PAGER.md)

## License

[Apache-2.0](LICENSE)
