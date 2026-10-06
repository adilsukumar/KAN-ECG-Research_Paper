# Reproducing the staged workflow

This is a source release, not a complete executable evidence bundle. Extract `KAN_ECG_Source_Code.zip`; all paths below are relative to its root. Inspect notebooks and frozen protocols before execution. No new training run was performed for this documentation update.

## Environment and compute

Use an isolated Python environment with NumPy, pandas, SciPy, scikit-learn, PyTorch, joblib, SymPy, WFDB and matplotlib. Consult notebook installation/version settings; this list is not an exact lockfile. Arbitrary upgrades can break serialized-model compatibility. There is no validated one-command installer.

| Stage | Compute | Prerequisites |
| --- | --- | --- |
| Phase 1 | Kaggle CPU; internet on | PhysioNet signals and annotations |
| Phase 2 | Kaggle CPU; internet on | Attach Phase 1 output |
| Combined Phases 3–5 | Original configuration: GPU; internet on | Attach Phase 1 and Phase 2 outputs |
| Follow-ups | CPU | Original output hierarchy and compatible model-loading environment |

Check current Kaggle quotas before starting. Documentation work does not require training.

## Primary workflow

1. Run `02_Phase1_Preprocessing/notebook/phase1_clean_preprocessing.ipynb`. Retain `phase1_clean` at `02_Phase1_Preprocessing/outputs/kaggle_download/phase1_clean`.
2. Attach that output to `03_Phase2_Baselines/notebook/phase2_clean_baselines.ipynb`. Retain `phase2_clean` at `03_Phase2_Baselines/outputs/kaggle_download/phase2_clean`.
3. Attach both outputs to `04_Phase3_KAN_Symbolic/notebook/remaining_clean.ipynb`. Retain `remaining_clean` at `04_Phase3_KAN_Symbolic/outputs/kaggle_download/remaining_clean`.
4. Review and run `04_Phase3_KAN_Symbolic/outputs/audit_remaining.py` against the expected artifacts.

All public notebooks are output-cleared. Execution, downloaded artifacts and passing audits must be verified separately.

## Follow-up sequence

Work from `09_Stronger_Followup`. Read `PILOT_PROTOCOL.md`, `CONTROL_PROTOCOL.md` and `BROAD_EXTENSION_PROTOCOL.md`; inspect each script's paths and dependencies.

1. `run_distillation_pilot.py` — objective ablations.
2. `run_numerical_controls.py` — known-target recovery and dictionary normalization.
3. `run_broader_surrogates.py` — additive/edgewise fits and conditional stability.
4. `run_grouped_benchmark.py` — exploratory source-group-separated partitions.
5. `run_svdb_holdout.py` — additional database holdout with frozen models.

Checks include `audit_pilot.py`, `audit_numerical_controls.py`, `audit_broad_extension.py` and `audit_grouped_model_inference.py`. `secondary_svdb_comparison.py` provides a secondary descriptive comparison. Some checks expect historical artifacts. Regenerated outputs are not expected to reproduce every archived hash.

## Check source identity

`SOURCE_MANIFEST.json` inside the ZIP records original-source and released-file hashes. Compare extracted public files with **release_sha256**, not source_sha256: clearing notebook outputs changes bytes. The manifest covers scientific source/protocol files, not every repository document.

```python
import hashlib
import json
from pathlib import Path

root = Path(".")  # extracted archive root
manifest = json.loads((root / "SOURCE_MANIFEST.json").read_text(encoding="utf-8"))
for relative_path, expected in manifest.items():
    actual = hashlib.sha256((root / relative_path).read_bytes()).hexdigest()
    assert actual == expected["release_sha256"], relative_path
print("Released source files match the manifest")
```

Hashes verify identity, not absence of leakage or clinical validity. Raw signals, fitted models, participant-level predictions, private logs and the manuscript are not distributed. Obtain datasets directly from PhysioNet under its terms. Original evidence audits need fitted artifacts and predictions absent from this code-only download.

Do not retune using DS2, INCART or SVDB and then describe those same cohorts as untouched tests. New development needs a new protocol and appropriate independent confirmation.
