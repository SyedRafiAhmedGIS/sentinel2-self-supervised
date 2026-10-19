# reports/ — real outputs from a full notebook run

Every file in this folder is produced by `sentinel2_self_supervised.ipynb` in a single
top-to-bottom run. Nothing is hand-edited; numbers in the README are copied from
`metrics.json` of the corresponding run. Files appear here as the run completes — a
missing file means the corresponding block did not run.

| File | Written by | What it is |
|---|---|---|
| `01_ssl_patches.png` | Block 2 | RGB previews of the unlabelled Sentinel-2 patches used for MAE pretraining |
| `02_masking.png` | Block 3 | Visualisation of the 60% random 8×8 sub-patch masking strategy |
| `03_reconstructions.png` | Block 4 | MAE reconstructions vs. inputs at the end of pretraining |
| `04_pretrain_curve.png` | Block 4 | MAE pretraining/validation loss curve (time-boxed run) |
| `05_labelled_area.png` | Block 5 | The downstream WorldCover-proxy labelled area and its spatial block grid |
| `06_learning_curves.png` | Blocks 6–7 | Probe performance vs. labelled-data fraction, both encoders, with bootstrap CIs |
| `07_confusion_100.png` | Block 7 | Held-out test-block confusion matrix at the 100% label setting |
| `data_quality.json` | Block 5 | Output of the independent data-quality gate (shapes, ranges, class counts, split integrity) |
| `pretrain_log.csv` | Block 4 | Per-epoch MAE training log |
| `probe_runs.csv` | Block 6 | One row per probe fit (encoder, label fraction, C, val/test metrics) |
| `metrics.json` | Block 7 | Final metrics: accuracies, paired delta, block-bootstrap 95% CIs |
| `run_info.json` | Block 8 | Run summary: config, timings, package versions, seeds |
| `README_note.md` | Block 8 | Short machine-written note about the run that produced this folder |
