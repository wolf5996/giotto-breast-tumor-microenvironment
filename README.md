# Breast Cancer Analysis

Giotto/Seurat workflow for the public Xenium FFPE Human Breast Cancer Rep1 example, split into a standalone project with local `uv` environment metadata and numbered Quarto notebooks.

## Pipeline

1. `scripts/01-xenium-analysis.qmd`: Xenium ingest, image alignment, QC, clustering, marker visualisation
2. `scripts/02-single-cell-seurat.qmd`: matched scRNA-seq processing and manual annotation in Seurat
3. `scripts/03-single-cell-giotto.qmd`: Giotto scRNA-seq object build and label transfer from Seurat metadata
4. `scripts/04-integration.qmd`: Harmony integration between scRNA-seq and Xenium
5. `scripts/05-advanced-spatial.qmd`: network, CPE, ICG, niche, HMRF, and HER2/ERBB2 spatial analysis

## Project Layout

- `scripts/`: source notebooks
- `read/`: local raw inputs, not tracked
- `checkpoints/`: local intermediates, not tracked
- `write/`: local figures and tables, not tracked
- `pyproject.toml`, `uv.lock`, `.python-version`: reproducible Python environment metadata

## Environment

Create the local environment with:

```bash
uv sync
```

The notebooks expect Giotto to use `.venv/bin/python`.

## Data

This repository is source-only. Raw Xenium/scRNA-seq inputs, checkpoints, and generated outputs stay local and are excluded from git.

Expected local inputs include:

- `read/outs/`
- `read/tif_exports/`
- `read/GSM7782696_5p_count_filtered_feature_bc_matrix.h5`
- breast image/alignment files in `read/`

## Notes

- The advanced breast notebook prefers folder-based Giotto checkpoints, but also supports migrated legacy `.rds` checkpoints as a fallback for older local state.
- The `.Rproj` file is included for local RStudio use; `.Rproj.user/` is excluded.
