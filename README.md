# Genetic and Hydrodynamic Connectivity in Australian Coral Reef Species: A Meta-Analysis

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20031763.svg)](https://doi.org/10.5281/zenodo.20031763)
[![License: MIT](https://img.shields.io/badge/Code-MIT-blue.svg)](LICENSE-CODE)
[![License: CC BY 4.0](https://img.shields.io/badge/Data-CC%20BY%204.0-lightgrey.svg)](LICENSE-DATA)
[![R version](https://img.shields.io/badge/R-%3E%3D4.3.0-blue)](https://www.r-project.org/)

> **Note:** Replace `XXXXXXX` in the Zenodo badge URL with your actual DOI once the first release is published on Zenodo. Update the Dryad DOI in the Data Availability section similarly.

## Overview

This repository contains the complete analysis pipeline for a meta-analysis of pairwise FST-based genetic connectivity and Lagrangian hydrodynamic model connectivity across Australian coral reef species. The analysis spans 20 biogeographic regions of Australia and addresses the central question: how well does hydrodynamic larval dispersal modelling predict empirically measured genetic structure? The pipeline covers isolation-by-distance analysis, genetic and hydrodynamic network analysis, marker-type effects on FST, variance partitioning, and a concordance assessment between the two connectivity frameworks.

## Repository Contents

| Folder / File | Description |
|---|---|
| `FullPipeline.Rmd` | Complete analysis pipeline: raw data → cleaned data → figures → manuscript tables |
| `data/` | Input data files (also deposited on Dryad — see Data Availability) |
| `data/README_data.md` | Data dictionary: column definitions for every input file |
| `outputs/` | Generated files: cleaned data CSVs, analysis result CSVs, all manuscript figures |
| `map-assets/` | Static basemap images used as spatial reference |
| `references/` | Supporting reference data (supplementary table from Duffy et al. 2026) |
| `coral-reef-meta.Rproj` | RStudio project file — open this to set the working directory automatically |

## Data Availability

Input data are openly available on Dryad: **[doi:10.5061/dryad.XXXXXXX](https://doi.org/10.5061/dryad.XXXXXXX)**

The full repository — including analysis code, derived outputs, and all manuscript figures — is archived on Zenodo: **[doi:10.5281/zenodo.XXXXXXX](https://doi.org/10.5281/zenodo.XXXXXXX)**

## Reproducing the Analysis

### Requirements

- R ≥ 4.3.0
- RStudio (recommended; required for `.Rproj` working directory handling)
- Key packages: `tidyverse`, `metafor`, `lme4`, `lmerTest`, `MuMIn`, `boot`, `vegan`, `spdep`, `sf`, `rnaturalearth`, `rnaturalearthdata`, `igraph`, `ggspatial`, `ggrepel`, `cowplot`, `scatterpie`, `ggalluvial`, `treemapify`, `pheatmap`, `circlize`, `kableExtra`, `geosphere`, `here`

### Steps

1. Clone or download the repository:
   ```bash
   git clone https://github.com/kirabrereton/coral-reef-connectivity-metaanalysis.git
   ```

2. Open `coral-reef-meta.Rproj` in RStudio. This sets the working directory to the repository root automatically.

3. (Recommended) Restore the exact package environment used for the analysis:
   ```r
   install.packages("renv")
   renv::restore()
   ```

4. Open `FullPipeline.Rmd` and knit the document (Ctrl+Shift+K), or run all chunks sequentially.

5. All outputs — cleaned data CSVs, analysis result CSVs, and figures — will be written to the `outputs/` folder.

### Note on internet access

The pipeline uses `rnaturalearth::ne_countries()` to download the Australia/Indonesia coastline at runtime. A one-time internet connection is required for this step. All other data are read from the local `data/` folder.

## Citation

### Cite the thesis chapter

Brereton, K. (2026). *Multiscale coral connectivity across Western Australia: evidence from genetic structure and biophysical modelling*. PhD Thesis, University of Western Australia.

### Cite this code and data archive

See [CITATION.cff](CITATION.cff) or use GitHub's "Cite this repository" button (top right of the repo page).

```
Brereton, K. (2026). Genetic and hydrodynamic connectivity in Australian coral reef species:
a meta-analysis (v1.0.0). Zenodo. https://doi.org/10.5281/zenodo.XXXXXXX
```

## License

- **Code** (`FullPipeline.Rmd`): [MIT License](LICENSE-CODE)
- **Data and outputs** (`data/`, `outputs/`, `map-assets/`): [CC BY 4.0](LICENSE-DATA)

See [LICENSE](LICENSE) for the full dual-license statement.

## Contact

Kira Brereton — kirabrereton290@gmail.com
School of Biological Sciences, University of Western Australia
