# sentinel2-self-supervised

Self-supervised pretraining (masked autoencoder) on unlabelled Sentinel-2 patches, compared against an identical architecture trained from scratch, using a paired frozen-encoder probe under spatially blocked evaluation.

> **Status:** notebook complete; a full GPU run is pending. Every number below is a **placeholder** until the notebook has been run end-to-end and `reports/` has been regenerated. Nothing here is claimed as a result.

## Purpose

The notebook pretrains a compact Vision-Transformer masked autoencoder (MAE) on cloud-masked Sentinel-2 patch composites that come from **no labels at all**, then asks one controlled question: does MAE pretraining help a small linear probe compared with the *same* encoder randomly initialised? Both encoders are frozen, features are extracted once, and logistic probes are fit on identical subsets so the comparison is paired. Evaluation uses whole 2.56 km spatial blocks so that neighbouring, highly similar patches cannot leak between train and test.

## Data sources & licences

| Data | Source | Licence / access |
|---|---|---|
| Sentinel-2 L2A | Microsoft Planetary Computer (STAC API) | Free API access; Copernicus data |
| ESA WorldCover 2021 (proxy labels only) | Planetary Computer / ESA | CC-BY-4.0 |

Proxy-label caveat: WorldCover classes are used only to build the downstream probe task; they are **not** ground truth, and the README/results say so wherever they appear. Full details in [DATA.md](DATA.md). No raw imagery is committed to this repository.

## How to run

**Google Colab (recommended, free GPU):** open `sentinel2_self_supervised.ipynb` → `Runtime` → `Change runtime type` → `T4 GPU` → `Runtime` → `Run all`. Missing packages are installed by the first cell.

**Locally:**
```bash
pip install -r requirements.txt
jupyter lab sentinel2_self_supervised.ipynb   # or jupyter notebook
```

## Expected runtime

Roughly **10–20 minutes** on a free Colab T4 for the demo configuration shipped in the notebook (patch download is the most variable part). MAE pretraining is time-boxed by a config value and stops early on a validation split, so runtime stays bounded. Run times are printed per block by the notebook.

## Results

<!-- FILL AFTER REAL RUN: paste the numbers exactly as printed in reports/metrics.json. Do not estimate. -->

| Quantity | MAE-pretrained encoder | Scratch encoder |
|---|---|---|
| Test accuracy (100% labels) | *placeholder — from reports/metrics.json* | *placeholder — from reports/metrics.json* |
| 95% CI (paired block bootstrap) | *placeholder* | *placeholder* |

Learning curves across labelled-data fractions and the paired delta with bootstrap CI are in `reports/06_learning_curves.png` and `reports/metrics.json` after a run. **No claim is made that pretraining beats training from scratch until the paired interval for this run says so.**

Result figures will appear here after the real run:
`reports/06_learning_curves.png`

## Limitations

- WorldCover labels are proxies, not field data; probe accuracy is bounded by their quality.
- Three small geographic areas only; conclusions do not generalise to other biomes or dates.
- A linear probe measures linear separability of features, not full fine-tuning performance.
- MAE is time-boxed for the free-tier GPU, so it is likely under-trained relative to published MAE recipes.
- Single run per configuration (no seed replicates) in the current notebook.

## Repository structure

```
sentinel2-self-supervised/
├── README.md                        ← this file
├── LICENSE                          ← MIT
├── DATA.md                          ← data sources, licences, download notes
├── requirements.txt
├── sentinel2_self_supervised.ipynb  ← the full pipeline (8 blocks)
└── reports/                         ← real outputs from a full run (see reports/README.md)
```

The notebook writes `data/` (cached patches) and `models/` (encoder + probe weights); both are git-ignored and never committed.

## Licence

MIT — see [LICENSE](LICENSE).

## Author

**[full name]** · GitHub: [@username] · [email]

*Remote-sensing / data-science portfolio project. Feedback welcome via issues.*
