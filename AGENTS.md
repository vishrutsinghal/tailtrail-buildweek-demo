# TailTrail Build Week Package

This is the standalone TailTrail Build Week submission.

## Layout

- `buildweek-demo-project/` is the intentionally small claims-service demo.
- `tailtrail/` is the bundled TailTrail runtime, skills, scripts, templates, and evaluation harness.
- `.codex-plugin/` lets Codex discover the bundled skills.

## Use the bundled runtime

Run TailTrail commands from this repository's root with:

```powershell
python3 tailtrail/scripts/tailtrail.py <command> --root buildweek-demo-project
```

On Windows, use `python` if `python3` is not registered.

Before changing the demo, read `buildweek-demo-project/tailtrail-policy.md`. Keep changes small, use Navigator before editing, and validate the focused test after a fix. The demo intentionally contains one claim-amount validation bug until the live demo fixes it.

No third-party dependencies are required for the judge path. Do not add dependencies or claim validation that was not actually run.
