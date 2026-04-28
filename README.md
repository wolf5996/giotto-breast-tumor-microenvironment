# Giotto Breast Tumor Microenvironment Analysis

Source repository for a Giotto-centered spatial analysis of the public **Xenium FFPE Human Breast Cancer Rep1** dataset, paired with matched scRNA-seq annotation and integration. The workflow is organized around the biological question of how tumor, immune, endothelial, and stromal populations are arranged in space, how they interact locally, and how those interactions reshape transcriptional state across the breast tumor microenvironment.

## Biological Focus

This project is built around several linked breast-cancer questions:

- How do major tumor-microenvironment compartments resolve in Xenium space?
- Which cell types are spatially enriched together versus segregated?
- Which genes change in a cell type specifically when it is adjacent to another cell type?
- Do multicellular neighbourhoods and HMRF domains recover recognizable tumor, stromal, immune, and interface regions?
- How well does **ERBB2** transcript localization track **HER2** protein signal across spatial scales?

The notebooks therefore emphasize:

- malignant epithelial structure
- immune infiltration and exclusion
- stromal and vascular niches
- local interaction-dependent transcriptional change
- multimodal HER2/ERBB2 spatial concordance

## Why Giotto

Giotto is the analytical core of the repository, not just the IO layer. The workflow uses Giotto where it is strongest:

- **spatial object model** that keeps polygons, images, transcripts, and downstream metadata in one analysis frame
- **cell proximity enrichment** to quantify which cell types preferentially neighbour one another
- **interaction-changed genes (ICG)** to identify transcriptional shifts conditioned on spatial adjacency
- **niche analysis** to define multicellular neighbourhood composition
- **HMRF spatial domains** to recover spatially coherent transcriptional regions
- **joint handling of image and transcript modalities** for HER2 IF versus ERBB2 RNA comparison

Seurat is used only where it is pragmatically strongest in this project: reference-side scRNA-seq processing and manual cluster annotation before labels are carried into the Giotto workflow.

## Workflow

1. `scripts/01-xenium-analysis.qmd`
   Breast Xenium ingest, OME-TIFF handling, image alignment, Giotto QC, clustering, and marker visualization.
2. `scripts/02-single-cell-seurat.qmd`
   Matched scRNA-seq processing in Seurat and biologically guided manual annotation.
3. `scripts/03-single-cell-giotto.qmd`
   Rebuild of the single-cell object in Giotto with the Seurat-derived cell-type labels attached.
4. `scripts/04-integration.qmd`
   Harmony integration between scRNA-seq and Xenium on shared features, followed by label transfer onto Xenium cells.
5. `scripts/05-advanced-spatial.qmd`
   Giotto-native downstream analysis: spatial networks, cell proximity enrichment, ICG, niches, HMRF domains, and HER2/ERBB2 bivariate analysis.

## Data Model

This repository is **source-only**. The following stay local and are excluded from git:

- `read/`
- `checkpoints/`
- `write/`
- `.venv/`

Expected local inputs include:

- `read/outs/`
- `read/tif_exports/`
- `read/GSM7782696_5p_count_filtered_feature_bc_matrix.h5`
- breast image and alignment files in `read/`

The repository tracks only the analysis source, project metadata, and Python environment specification.

## Environment

Create the local environment with:

```bash
uv sync
```

The notebooks expect Giotto to use:

```bash
.venv/bin/python
```

## Project Structure

- `scripts/`: numbered Quarto notebooks
- `read/`: local raw inputs and image exports
- `checkpoints/`: local intermediate objects
- `write/`: local figures and tables
- `pyproject.toml`, `uv.lock`, `.python-version`: reproducible Python environment metadata

## Notes

- The advanced notebook prefers folder-based Giotto checkpoints, but also supports migrated legacy `.rds` checkpoints when older local state is the only available checkpoint form.
- The `.Rproj` file is included for local RStudio use; `.Rproj.user/` remains excluded.
