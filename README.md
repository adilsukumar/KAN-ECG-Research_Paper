# ECG KAN generalization and symbolic distillation

Code accompanying a study of a custom degree-one spline KAN on twelve engineered ECG features. This is a research implementation, not a clinical device or a claim that all KAN architectures are ineffective.

## Study scope

Development uses MIT-BIH Arrhythmia data, with frozen external assessments on INCART and SVDB. The conventional MIT-BIH record split has a known shared-source limitation for records 201 and 202; the study retains its sensitivity analysis. SVDB source-patient independence is unverified. Compact polynomial, additive and edgewise candidates did not meet the joint acceptance gates. Successful simple numerical controls do not imply success on physiological data.

## Contents and execution

The directory structure preserves source scripts' relative paths. Run the Phase 1 notebook first on Kaggle with CPU and internet enabled. Download its `phase1_clean` output into `02_Phase1_Preprocessing/outputs/kaggle_download/phase1_clean`. Attach the Phase 1 output to the Phase 2 notebook and run on CPU; place its `phase2_clean` output in `03_Phase2_Baselines/outputs/kaggle_download/phase2_clean`. Run the combined Phases 3–5 notebook with both preceding outputs attached, following its accelerator settings and internet/download requirements; place `remaining_clean` in `04_Phase3_KAN_Symbolic/outputs/kaggle_download/remaining_clean`. Inspect notebook configuration before execution. Outputs are intentionally absent from these public source notebooks.

Follow-up scripts run from `09_Stronger_Followup` and depend on those archived outputs. Read each frozen protocol before execution. Run `run_distillation_pilot.py`, then `run_numerical_controls.py`, `run_broader_surrogates.py`, `run_grouped_benchmark.py` and `run_svdb_holdout.py` in that order; run the corresponding audit scripts. Review dependencies and paths first. This release has syntax checks, not a new end-to-end training run. Some audits expect the original archived checksums and artifacts; a regenerated execution is not the same immutable evidence archive.

Use an isolated Python environment with NumPy, pandas, SciPy, scikit-learn, PyTorch, joblib, SymPy, WFDB and matplotlib. Original notebooks contain installation/version settings. Follow-up serialized-model compatibility was checked using the archived environment; arbitrary library upgrades may prevent loading old models. No GPU run should be launched merely to reproduce the CPU follow-up.

## Data and access

Obtain signals and annotations directly from PhysioNet: MIT-BIH Arrhythmia Database (`mitdb`), St Petersburg INCART 12-lead Arrhythmia Database (`incartdb`) and MIT-BIH Supraventricular Arrhythmia Database (`svdb`). Comply with each dataset's terms. Raw signals, participant-level outputs, fitted models, private execution logs, credentials and the manuscript are not included in this code-only release. A public code repository alone is not a complete public evidence archive.

Authors: Adil Sukumar and Somya Sisodia, VIT Bhopal University. Public repository: https://github.com/adilsukumar/KAN-ECG-Research_Paper . Download and extract `KAN_ECG_Source_Code.zip` to obtain the preserved directory structure and source manifest. No reuse license has been selected; licensing requires an explicit author decision. No submitted/published article DOI is claimed.
