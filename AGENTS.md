# TailTrail Build Week Package

This is the standalone TailTrail Build Week submission.

## Layout

- `buildweek-demo-project/` is the intentionally small claims-service demo.
- `tailtrail/` is the bundled TailTrail runtime, skills, scripts, templates, and evaluation harness.
- `.codex-plugin/` lets Codex discover the bundled skills.

## Use the bundled runtime

Run TailTrail commands from this repository's root with:

```powershell
py -3 tailtrail/scripts/tailtrail.py <command> --root buildweek-demo-project
```

On Windows, prefer `py -3`. If the Python Launcher is unavailable, use
`python3`; do not fall back to the Microsoft Store `python` app-execution alias.

When a user says `tailtrail hello`, `hello tailtrail`, or the `taitrail` typo,
run `py -3 tailtrail/scripts/tailtrail.py hello` from this repository root.
Return the command's ASCII TailTrail banner and installation result verbatim;
do not reduce it to an "installation passed" summary.

For any explicit `tailtrail <command>` request, run the equivalent command with
`py -3 tailtrail/scripts/tailtrail.py <command>` and return the actual command
result, including errors and validation status. Do not claim a command succeeded
unless it ran successfully.

Before changing the demo, read `buildweek-demo-project/tailtrail-policy.md`. Keep changes small, use Navigator before editing, and validate the focused test after a fix. The demo intentionally contains one claim-amount validation bug until the live demo fixes it.

No third-party dependencies are required for the judge path. Do not add dependencies or claim validation that was not actually run.

## Semantic V3 Demo Presentation

For the Build Week Semantic V3 prompt, run the Semantic V3 graph command and return its command output verbatim; do not write a custom summary. The command is `py -3 tailtrail/scripts/tailtrail.py graph ast --root buildweek-demo-project --changed src/claims_api/validation.py --depth v3 --provider-output tailtrail-meta/providers/sample-semantic.json --approved` when run from this package root. Use only this format: title; approved-local-file statement; no-external-provider statement; one `Evidence type | Count | Meaning` table; a `Provider-backed additions include:` list; then `The report labels this input as: provider-backed.` Do not add symbol tables, impact tables, evidence-total sections, prose totals, or other sections.
