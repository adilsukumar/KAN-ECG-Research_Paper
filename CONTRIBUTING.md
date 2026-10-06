# Contributing

Useful contributions include reproduction fixes, dependency/path documentation, independent checks and carefully specified follow-up experiments. Keep the archived experiment distinct from a new experiment.

## Report a reproduction problem

Open an issue with the affected notebook/script, repository commit or archive identifier, Python/OS/library versions, CPU/GPU configuration, input-directory layout, expected behavior and a minimal sanitized traceback. State whether you used historical or regenerated artifacts.

Never post API tokens, private logs, raw recordings, participant-level predictions or other sensitive information.

## Propose a change

Describe the problem before a large refactor. Preserve training-only preprocessing and distinguish validation selection from held-out assessment. Do not change gates or thresholds after inspecting test outcomes and call it the original protocol.

Documentation changes should not trigger training. Report which checks ran and which did not; syntax checks alone are not reproduction. New experiments need their own protocol, seed settings, environment record, artifacts and uncertainty analysis.

## Licensing

No reuse license has yet been selected. Ask the authors before reusing or redistributing beyond applicable rights; public visibility is not an open-source license. Dataset terms are independent.
