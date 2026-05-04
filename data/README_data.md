# Data Dictionary

All files in this directory are the original input data for the meta-analysis.
These files are also deposited on Dryad: [doi:10.5061/dryad.XXXXXXX](https://doi.org/10.5061/dryad.XXXXXXX)

These files should not be modified. All cleaning is performed programmatically
in `FullPipeline.Rmd`, and cleaned versions are written to `outputs/`.

---

## fst.csv

**Size:** ~31 KB | **Unit of observation:** pairwise site comparison

Pairwise FST estimates between sampling sites, compiled from published studies
of coral reef species around Australia.

| Column | Type | Description |
|---|---|---|
| `Site_A` | character | First site identifier (matches `siteID` in `geneticMeta.csv`) |
| `Site_B` | character | Second site identifier (matches `siteID` in `geneticMeta.csv`) |
| `Fst` | numeric | Pairwise FST estimate (0–1). Negative values (a small-sample artefact) are clamped to 0 in the pipeline. |
| `significant` | character | Whether the FST estimate is statistically significant: `"y"` / `"n"` |
| `f'st` | numeric | Alternative standardised differentiation estimate (Hedrick's G'ST or Jost's D where reported) |
| `significantLevels` | character | P-value level if reported by the original study (e.g., `*`, `<0.05`) |

**Notes:**
- Site IDs follow the convention `[first-author initials][2-digit year][location code]`, e.g. `ev19K` = Evans et al. (2019), Kimberley.
- Some rows contain trailing empty columns; these are skipped during import.

---

## geneticMeta.csv

**Size:** ~26 KB | **Unit of observation:** sampling site

Site-level metadata for all genetic sampling localities, one row per site.

| Column | Type | Description |
|---|---|---|
| `region` | character | Biogeographic region name. Must match one of the 17 canonical names in `regionData.csv`. |
| `reef` | character | Reef or locality name within the region |
| `siteID` | character | Unique site identifier. Matches `Site_A` / `Site_B` in `fst.csv`. |
| `author` | character | First author of the source study |
| `year` | numeric | Publication year of the source study |
| `taxon` | character | Broad taxonomic group (e.g., `"fish"`, `"coral"`, `"invertebrate"`) |
| `species` | character | Species binomial |
| `studyID` | character | Unique study identifier. Matches `studyID` in `allStudies.csv`. |
| `lat` | character | Latitude as reported in the original study (may be a range or note) |
| `lon` | character | Longitude as reported in the original study (may be a range or note) |
| `lat_spec` | numeric | Specific site latitude, decimal degrees (negative = south) |
| `lon_spec` | numeric | Specific site longitude, decimal degrees |
| `spawnMode` | character | Reproductive mode: `"broadcast"`, `"brood"`, or `NA` |
| `studyType` | character | `"genetic"` for all records in this file |
| `geneMarkers` | character | Molecular marker type: `"microsatellite"`, `"SNP"`, `"allozyme"`, `"mtDNA"`, or a combination |

---

## allStudies.csv

**Size:** ~5 KB | **Unit of observation:** individual published study

Study-level metadata for both genetic studies (`studyType == "genetic"`) and
hydrodynamic dispersal modelling studies (`studyType == "dispersal"`).

| Column | Type | Description |
|---|---|---|
| `studyType` | character | `"genetic"` or `"dispersal"` |
| `location` | character | Semicolon-separated list of biogeographic regions covered by the study |
| `studyID` | character | Unique study identifier. Matches `studyID` in `geneticMeta.csv` and `hydrodynamic.csv`. |
| `publishedYear` | numeric | Year of publication |
| `yearModelled` | character | Year(s) the oceanographic model was run (dispersal studies only) |
| `species` | character | Species modelled (dispersal studies); `"na"` for genetic studies |
| `taxa` | character | Broad taxonomic group modelled (dispersal studies only) |
| `spawnType` | character | Reproductive mode used in the dispersal model |
| `seasonModel` | character | Season(s) modelled (dispersal studies) |
| `numSites` | numeric | Number of sites or nodes included in the study |
| `sampleSize` | character | Genetic sample sizes per site (genetic studies) |
| `trackingApproach` | character | Particle-tracking method description (dispersal studies) |
| `modelRes` | character | Spatial resolution of the hydrodynamic model (dispersal studies) |
| `modelType` | character | Name of the hydrodynamic model used (dispersal studies) |
| `markerType` | character | Molecular marker type (genetic studies) |
| `valuesAvail` | character | `"y"` if quantitative connectivity values are available and usable; `"n"` otherwise |
| `excluReas` | character | Reason for exclusion when `valuesAvail == "n"` |

---

## hydrodynamic.csv

**Size:** ~1.7 KB | **Unit of observation:** directional region pair

Region-pair hydrodynamic connectivity derived from published Lagrangian particle
tracking studies. Values represent consensus summaries across multiple studies.

| Column | Type | Description |
|---|---|---|
| `studyID` | character | Source study providing this connectivity estimate. Matches `studyID` in `allStudies.csv` where `studyType == "dispersal"`. |
| `region_A` | character | Source region name (larval origin) |
| `region_B` | character | Destination region name (larval settlement) |
| `direction` | character | Net cardinal direction of larval transport (e.g., `"SW"`, `"NE"`) |
| `conn` | character | Whether connectivity was detected between the pair: `"y"` / `"n"` |
| `connect_str` | character | Qualitative connectivity strength: `"high"`, `"mod"` (moderate), `"low"`, or blank |

---

## regionData.csv

**Size:** ~506 B | **Unit of observation:** biogeographic region

Authoritative centroid coordinates for each of the 17 biogeographic regions
used as the spatial framework throughout the analysis.

| Column | Type | Description |
|---|---|---|
| `region` | character | Canonical region name. This is the authoritative spelling — all other files must match exactly. |
| `lat` | numeric | Region centroid latitude, decimal degrees (negative = south) |
| `lon` | numeric | Region centroid longitude, decimal degrees |

**Notes:**
- Region names in all other files are matched against this list during data cleaning.
- Leading/trailing whitespace is stripped by the pipeline, but capitalisation must match.
