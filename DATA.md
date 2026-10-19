# Data note

This repository contains **no raw or processed imagery**. Everything under `data/` is
git-ignored and re-created by running the notebook. This note records exactly what the
notebook downloads, from where, and under which terms, so the work is reproducible and
licence-clean.

## 1. Sentinel-2 L2A surface-reflectance patches

- **Source:** Microsoft Planetary Computer STAC API
  (`https://planetarycomputer.microsoft.com/api/stac/v1`), collection `sentinel-2-l2a`.
- **Access:** free, anonymous (a signed URL is obtained via the `planetary-computer`
  package; no account or key is required).
- **What the notebook fetches:** scenes for three small, mutually disjoint geographic
  areas; per-scene cloud/shadow masking from the SCL band; a median composite; 64×64
  patches of 6 bands (B02, B03, B04, B08, B11, B12) at 10 m / 20 m native grid.
- **Where it lands:** `data/raw/` (scratch) and `data/interim/ssl_patches.npz`
  (uint16 cache). Deleting `data/interim` forces a fresh download.
- **Licence:** Copernicus Sentinel data — free, full and open access
  (Copernicus/Open Data Licence); redistribution of bulk raw products through this
  repository is not intended and not required for reproduction.

## 2. ESA WorldCover 2021 (downstream proxy labels only)

- **Source:** ESA WorldCover 10 m 2021 v200, accessed through the Planetary Computer
  collection `esa-worldcover`.
- **Role in the project:** provides the class raster for the downstream linear-probe
  task in one further, disjoint area. These are **proxy labels, not ground truth** —
  the notebook and README state this wherever results are discussed.
- **Licence:** CC-BY-4.0 (ESA WorldCover). Attribution: "Contains modified Copernicus
  data / ESA WorldCover 2021".

## 3. What is committed vs. not

| Item | Committed? | Why |
|---|---|---|
| Notebook, configs, README | Yes | Code only |
| `reports/` metrics + figures from a real run | Yes | Small PNG/CSV/JSON results |
| `data/raw`, `data/interim` | **No** (git-ignored) | Imagery/arrays, re-downloadable |
| `models/*.pth`, `*.joblib` | **No** (git-ignored) | Regenerable weights |

## 4. Reproduction

Run `sentinel2_self_supervised.ipynb` top-to-bottom (Colab T4 recommended).
Patch download volume for the demo configuration is modest (tens of MB), but exact
availability of specific Sentinel-2 scenes can change over time; the notebook raises a
clear error rather than silently substituting different scenes.
