<div align="center">

# Iowa Climate Futures Explorer

## Model-preserving CMIP6 projections of heat and precipitation extremes across Iowa climatic regions

<p>
  <img src="https://img.shields.io/badge/Status-Analysis%20Complete-2E7D32?style=for-the-badge" alt="Analysis complete">
  <img src="https://img.shields.io/badge/Dashboard-In%20Development-E69F00?style=for-the-badge" alt="Dashboard in development">
  <a href="./LICENSE">
    <img src="https://img.shields.io/badge/License-MIT-1565C0?style=for-the-badge" alt="MIT License">
  </a>
</p>

<p>
  <img src="https://img.shields.io/badge/Observations-NOAA%20GHCN--Daily-0072B2?style=flat-square" alt="NOAA GHCN-Daily">
  <img src="https://img.shields.io/badge/Climate%20Models-6%20CMIP6%20GCMs-6A1B9A?style=flat-square" alt="Six CMIP6 models">
  <img src="https://img.shields.io/badge/Scenarios-SSP2--4.5%20%7C%20SSP5--8.5-C62828?style=flat-square" alt="SSP2-4.5 and SSP5-8.5">
  <img src="https://img.shields.io/badge/Indices-12%20Annual%20Extremes-00796B?style=flat-square" alt="Twelve annual extreme indices">
</p>

<p>
  <img src="https://img.shields.io/badge/Method-Quantile%20Delta%20Mapping-00796B?style=flat-square" alt="Quantile delta mapping">
  <img src="https://img.shields.io/badge/Method-Skill--Weighted%20Synthesis-00796B?style=flat-square" alt="Skill-weighted synthesis">
  <img src="https://img.shields.io/badge/Statistics-Mann--Kendall%20%2B%20FDR-00796B?style=flat-square" alt="Mann-Kendall and false-discovery-rate correction">
  <img src="https://img.shields.io/badge/Platform-Python%20%7C%20Google%20Colab-4285F4?style=flat-square" alt="Python and Google Colab">
</p>

**A reproducible climate-analysis pipeline and planned interactive decision-support dashboard for exploring regional changes in heat, precipitation, and hydroclimatic extremes.**

</div>

---

## Project Status

The corrected analytical pipeline has been completed and its final figures, validation outputs, projection tables, uncertainty diagnostics, and trend results have been generated.

The next development phase is the **Iowa Climate Futures Explorer dashboard**, which will allow users to interactively compare:

- climatic regions;
- CMIP6 models;
- emission scenarios;
- projection periods;
- extreme-climate indices;
- weighted projected changes;
- model agreement;
- residual historical bias; and
- model-family sensitivity.

The dashboard is planned as a **Streamlit application** using the final derived CSV and JSON products from this repository. It will not recompute the full climate pipeline during user interaction.

---

## Dashboard Preview

> Replace the placeholder below with the first dashboard screenshot after the application is developed.

<p align="center">
  <img src="./dashboard/assets/dashboard_overview.png" alt="Iowa Climate Futures Explorer dashboard preview" width="100%">
</p>

<p align="center">
  <sub>
    Planned interactive interface for comparing climatic regions, scenarios,
    future periods, climate indices, model spread, agreement, and uncertainty.
  </sub>
</p>

---

## Scientific Workflow

<p align="center">
  <img src="./figures/readme/01_methodology_workflow.png" alt="Model-preserving CMIP6 analysis workflow" width="95%">
</p>

<p align="center">
  <sub>
    Each GCM is preserved through extraction, bias correction, annual-index
    calculation, and model-specific change estimation before regional
    skill-weighted synthesis.
  </sub>
</p>

The workflow is intentionally **model preserving**. Daily outputs from different climate models are not averaged before bias correction or index calculation because the models do not simulate synchronized weather events. Premature daily averaging can create artificial sequences and distort threshold counts, rolling accumulations, and spell-duration indices.

The implemented sequence is:

1. screen NOAA GHCN-Daily stations for completeness and quality;
2. delineate five climatic regions using Ward hierarchical clustering;
3. audit CMIP6 models for a complete common-member chain;
4. extract daily precipitation and temperature at station locations;
5. evaluate historical regional skill in five contiguous temporal blocks;
6. apply quantile-delta mapping independently to each model, station, month, and variable;
7. calculate twelve annual extreme indices separately for every model;
8. estimate model-specific future changes relative to each model's own baseline;
9. apply regional skill weights to model-level changes;
10. classify robust directional agreement among the six models;
11. assess residual historical bias and related-model sensitivity;
12. evaluate Mann–Kendall trends with Benjamini–Hochberg false-discovery-rate control; and
13. produce station-network-weighted regional summaries and publication products.

---

## Quick Access

| Resource | Repository location |
|---|---|
| **Complete corrected notebook** | [`notebooks/Iowa_CMIP6_Corrected_Full_Pipeline.ipynb`](./notebooks/Iowa_CMIP6_Corrected_Full_Pipeline.ipynb) |
| **Dashboard application** | [`dashboard/app.py`](./dashboard/app.py) |
| **Dashboard documentation** | [`dashboard/README.md`](./dashboard/README.md) |
| **Publication figures** | [`figures/publication/`](./figures/publication/) |
| **Supplementary figures** | [`figures/supplementary/`](./figures/supplementary/) |
| **Publication tables** | [`outputs/publication_tables/`](./outputs/publication_tables/) |
| **Validation and trend outputs** | [`outputs/validation_and_trends/`](./outputs/validation_and_trends/) |
| **Figure-source data** | [`outputs/figure_source_data/`](./outputs/figure_source_data/) |
| **Environment specification** | [`environment/`](./environment/) |
| **License** | [`LICENSE`](./LICENSE) |

---

## Study Overview

This repository evaluates projected changes in heat and precipitation extremes across Iowa using quality-controlled station observations and six CMIP6 global climate models.

The study combines:

- **105 NOAA GHCN-Daily stations**;
- **five climatic regions**;
- **six CMIP6 models** with a common `r1i1p1f1` member;
- **historical, SSP2-4.5, and SSP5-8.5 experiments**;
- **station- and month-specific quantile-delta mapping**;
- **twelve annual extreme-climate indices**;
- **regional performance-based model weights**;
- **model-level agreement and uncertainty diagnostics**; and
- **Mann–Kendall trend analysis with false-discovery-rate control**.

The historical observation period is **1985–2014**. Future changes are evaluated for three equal 28-year windows:

- **2017–2044**
- **2045–2072**
- **2073–2100**

against the **1987–2014** model-specific baseline.

---

## Climatic Regionalization

<p align="center">
  <img src="./figures/readme/02_climatic_regionalization.png" alt="Iowa climatic regionalization and station network" width="95%">
</p>

The 105 retained stations were grouped into five climatic regions using standardized geographic and climatological features:

- latitude;
- longitude;
- elevation;
- mean annual precipitation;
- mean annual maximum temperature; and
- mean annual minimum temperature.

The resulting regions contain:

| Region | Stations | Fraction of network |
|---:|---:|---:|
| R1 | 12 | 0.114 |
| R2 | 27 | 0.257 |
| R3 | 27 | 0.257 |
| R4 | 11 | 0.105 |
| R5 | 28 | 0.267 |

These station fractions are used only for the reported station-network-weighted summaries. They are **not area weights**.

---

## CMIP6 Model Ensemble

The common-member audit retained six models with complete historical and future precipitation and temperature chains:

| Model | Member |
|---|---|
| CMCC-ESM2 | `r1i1p1f1` |
| GFDL-CM4 | `r1i1p1f1` |
| GFDL-ESM4 | `r1i1p1f1` |
| INM-CM4-8 | `r1i1p1f1` |
| MRI-ESM2-0 | `r1i1p1f1` |
| NESM3 | `r1i1p1f1` |

Variables:

- `pr` — precipitation;
- `tasmax` — daily maximum near-surface air temperature; and
- `tasmin` — daily minimum near-surface air temperature.

Experiments:

- historical;
- SSP2-4.5; and
- SSP5-8.5.

The complete extraction inventory contains **54 model–experiment–variable files**.

---

## Bias Correction and Independent Validation

Quantile-delta mapping is applied independently for every:

- climate model;
- station;
- calendar month; and
- climate variable.

The independent evaluation uses:

- **calibration:** 1985–1999;
- **validation:** 2000–2014.

Precipitation is corrected multiplicatively with explicit wet-day treatment and non-negativity constraints. Temperature is corrected additively.

<p align="center">
  <img src="./figures/readme/03_independent_qdm_validation.png" alt="Independent per-GCM QDM validation" width="95%">
</p>

Median Kolmogorov–Smirnov statistics across the six models changed as follows:

| Variable | Raw | Corrected | Median reduction |
|---|---:|---:|---:|
| Precipitation | 0.714 | 0.055 | 92.2% |
| Maximum temperature | 0.128 | 0.044 | 62.2% |
| Minimum temperature | 0.185 | 0.042 | 73.0% |

The projection configuration is then refitted on the full **1985–2014** interval before application to historical and future daily series.

---

## Extreme-Climate Indices

Twelve annual indices are calculated separately for each station and model.

| Index | Description | Unit |
|---|---|---|
| CDD | Maximum consecutive dry days | days |
| CWD | Maximum consecutive wet days | days |
| PRCPTOT | Annual precipitation on wet days | mm |
| R10mm | Days with precipitation ≥10 mm | days |
| R20mm | Days with precipitation ≥20 mm | days |
| R25mm | Days with precipitation ≥25 mm | days |
| R95p | Precipitation above the observed 95th wet-day percentile | mm |
| R99p | Precipitation above the observed 99th wet-day percentile | mm |
| RX1day | Annual maximum one-day precipitation | mm |
| RX5day | Annual maximum consecutive five-day precipitation | mm |
| SDII | Mean precipitation intensity on wet days | mm day⁻¹ |
| SU25 | Days with maximum temperature >25 °C | days |

A wet day is defined as precipitation ≥1 mm.

Precipitation-related future changes are reported as percentages. SU25 changes are reported as additional or fewer days.

---

## Key Results

### Increasing heat exposure

Summer days above 25 °C show the clearest regional signal. The station-network-weighted late-century SSP5-8.5 projection is:

- **+57.7 days annually**

with robust increases across all five climatic regions.

### Increasing precipitation intensity

Under late-century SSP5-8.5, the station-network-weighted projected changes are:

- **PRCPTOT:** +11.9%
- **R95p:** +38.6%
- **RX1day:** +26.0%
- **RX5day:** +18.8%

The stronger increases in upper-tail and short-duration precipitation than in annual totals indicate intensification of heavy precipitation rather than uniform scaling of all wet days.

### Growth in robust model agreement

The number of regional index projections classified as robust increases grows through the century:

| Scenario | 2017–2044 | 2045–2072 | 2073–2100 |
|---|---:|---:|---:|
| SSP2-4.5 | 22 of 60 | 50 of 60 | 51 of 60 |
| SSP5-8.5 | 37 of 60 | 50 of 60 | 51 of 60 |

A robust signal requires:

- at least five of six models agreeing on direction; and
- a weighted magnitude above 1% for percentage indices or 1 day for SU25.

### Rare-tail uncertainty

R99p shows a consistently positive projected direction but greater uncertainty in magnitude:

- median residual absolute bias: 22.62%;
- maximum residual absolute bias: 31.01%;
- median GFDL-family sensitivity: 5.10 percentage points; and
- maximum GFDL-family sensitivity: 15.77 percentage points.

R99p should therefore be interpreted as an uncertainty-qualified rare-tail indicator rather than a precise engineering design value.

### Trend significance after multiple-testing control

Across **420 Mann–Kendall tests**:

- 48 had nominal `p < 0.05`;
- 20 remained significant after Benjamini–Hochberg correction; and
- all retained trends were SU25 increases.

Period changes and within-period monotonic trends are different forms of evidence and are reported separately.

---

## Projection Visualizations

### Regional model-level projected changes

<p align="center">
  <img src="./figures/readme/04_regional_projected_changes.png" alt="Regional model-level projected changes" width="100%">
</p>

Boxes summarize the six independently corrected climate models. The models remain separate through bias correction, annual-index calculation, and change estimation.

### Robust model agreement

<p align="center">
  <img src="./figures/readme/05_model_agreement.png" alt="Robust model agreement across climatic regions" width="100%">
</p>

The agreement diagnostics identify where projected direction is supported by at least five of six models and where the signal remains mixed.

### Reliability and model-family sensitivity

<p align="center">
  <img src="./figures/readme/06_reliability_screen.png" alt="Index reliability and model-family sensitivity" width="90%">
</p>

Reliability categories combine residual historical bias and sensitivity to the related GFDL-CM4 and GFDL-ESM4 models. These classes are descriptive diagnostics rather than probabilities.

---

## Planned Interactive Dashboard

The planned dashboard will translate the final analysis outputs into an accessible comparison and decision-support environment.

### Dashboard modules

#### 1. Regional Climate Explorer

Users will be able to:

- select a climatic region;
- view the station network;
- compare regional baseline climates;
- examine station counts and data completeness; and
- display model weights by variable.

#### 2. Scenario and Period Comparison

Users will be able to compare:

- SSP2-4.5 and SSP5-8.5;
- near-, mid-, and late-century periods;
- regional and station-network-weighted summaries; and
- absolute versus percentage changes.

#### 3. Extreme-Index Explorer

Users will be able to select any of the twelve indices and view:

- weighted projected change;
- six-model distribution;
- regional minimum and maximum;
- model agreement;
- residual historical bias;
- reliability category; and
- related-model sensitivity.

#### 4. Model Comparison

Users will be able to:

- compare individual GCM changes;
- inspect regional skill weights;
- identify model spread;
- compare full and GFDL-family sensitivity results; and
- download filtered model-level tables.

#### 5. Agreement and Trend Diagnostics

The dashboard will display:

- robust increase, robust decrease, and mixed classifications;
- number of agreeing models;
- Mann–Kendall statistics;
- Sen slopes;
- nominal p-values;
- FDR-adjusted q-values; and
- clear separation between period changes and monotonic trends.

#### 6. Decision-Support View

A user-selected region, index, scenario, and period will return:

- projected magnitude;
- regional range;
- model agreement;
- reliability category;
- principal limitation;
- suggested interpretation; and
- downloadable evidence table.

The dashboard will support screening and comparison. It will not present rare-tail projections as site-specific engineering design values.

---

## Recommended Dashboard Controls

| Control | Options |
|---|---|
| Climatic region | R1–R5 or station-network-weighted summary |
| Index | CDD, CWD, PRCPTOT, R10mm, R20mm, R25mm, R95p, R99p, RX1day, RX5day, SDII, SU25 |
| Scenario | SSP2-4.5, SSP5-8.5 |
| Period | 2017–2044, 2045–2072, 2073–2100 |
| View | Weighted projection, individual models, agreement, trend, reliability |
| Comparison | Regions, scenarios, periods, indices, or models |
| Download | Filtered CSV and publication-ready PNG |

---

## Dashboard Data Products

The Streamlit application should read only compact derived outputs, including:

```text
dashboard/data/
├── station_regions.csv
├── regional_gcm_weights.csv
├── per_model_future_changes.csv
├── weighted_multimodel_projections.csv
├── model_agreement_summary.csv
├── weighted_historical_validation.csv
├── gfdl_family_sensitivity.csv
├── mann_kendall_trends_fdr.csv
├── statewide_station_weighted_projections.csv
├── index_reliability_screen.csv
└── dashboard_metadata.json
```

Large raw CMIP6 and daily corrected files should remain outside the deployed dashboard.

---

## Repository Structure

```text
Iowa-Climate-Futures-Explorer/
├── README.md
├── LICENSE
├── CITATION.cff
├── .gitignore
│
├── notebooks/
│   └── Iowa_CMIP6_Corrected_Full_Pipeline.ipynb
│
├── src/
│   ├── data_processing/
│   ├── bias_correction/
│   ├── climate_indices/
│   ├── weighting/
│   ├── trend_analysis/
│   └── visualization/
│
├── dashboard/
│   ├── app.py
│   ├── pages/
│   │   ├── 1_Regional_Explorer.py
│   │   ├── 2_Projection_Comparison.py
│   │   ├── 3_Model_Agreement.py
│   │   ├── 4_Reliability_and_Trends.py
│   │   └── 5_Data_Download.py
│   ├── components/
│   ├── data/
│   ├── assets/
│   │   └── dashboard_overview.png
│   └── README.md
│
├── data/
│   ├── README.md
│   ├── metadata/
│   └── derived/
│
├── outputs/
│   ├── publication_tables/
│   ├── model_level_results/
│   ├── validation_and_trends/
│   ├── figure_source_data/
│   └── run_summaries/
│
├── figures/
│   ├── publication/
│   ├── supplementary/
│   └── readme/
│
├── manuscript/
│   ├── main/
│   └── supplementary/
│
├── environment/
│   ├── requirements.txt
│   ├── environment.yml
│   └── software_versions.txt
│
└── docs/
    ├── methodology.md
    ├── data_dictionary.md
    ├── dashboard_design.md
    └── reproducibility.md
```

---

## Reproducing the Analysis

### Google Colab

1. Clone or download this repository.
2. Open:

   [`notebooks/Iowa_CMIP6_Corrected_Full_Pipeline.ipynb`](./notebooks/Iowa_CMIP6_Corrected_Full_Pipeline.ipynb)

3. Mount Google Drive when prompted.
4. update the project-root configuration cell;
5. run the notebook from top to bottom;
6. confirm that all validation checks pass; and
7. inspect the generated publication package.

### Local Python Environment

Create the environment using either:

```bash
pip install -r environment/requirements.txt
```

or:

```bash
conda env create -f environment/environment.yml
conda activate iowa-climate-futures
```

Package versions used for the final run should be recorded in:

```text
environment/software_versions.txt
```

---

## Running the Dashboard

After the dashboard code is added:

```bash
pip install -r environment/requirements.txt
streamlit run dashboard/app.py
```

The dashboard should be tested locally before deployment to Streamlit Community Cloud or another hosting platform.

---

## Data Sources

| Purpose | Source |
|---|---|
| Daily station precipitation and temperature | NOAA Global Historical Climatology Network-Daily |
| CMIP6 daily climate-model output | ESGF/Pangeo CMIP6 cloud catalogue |
| State boundary | U.S. Census Bureau cartographic or TIGER/Line boundary |
| Station coordinates and elevation | NOAA station metadata |

Source datasets retain their original licenses, attribution requirements, and terms of use.

---

## Data Availability and Repository Scope

This repository is intended to include:

- analysis code;
- the complete corrected notebook;
- station and model metadata;
- compact derived CSV and JSON products;
- figure-source tables;
- publication figures;
- dashboard code; and
- reproducibility documentation.

The repository should not include:

- the complete raw CMIP6 archive;
- all large daily extraction files;
- all daily QDM-corrected files;
- restricted or redundant source datasets;
- temporary caches; or
- obsolete outputs from earlier analytical designs.

Instructions for retrieving the original public datasets should be documented instead.

---

## Scientific Limitations

### Climate-model ensemble size

The study uses six models with one ensemble member per model. This supports a complete and comparable analysis chain but does not represent the full CMIP6 structural or initial-condition ensemble.

### Spatial representation

Nearest-grid extraction does not resolve all local terrain, land-cover, urban, soil, or convective-storm processes.

### Univariate bias correction

QDM adjusts marginal distributions but does not guarantee correction of spatial coherence, storm structure, temporal dependence, or cross-variable dependence.

### Rare-event uncertainty

The rarest precipitation tail, especially R99p, has larger residual bias and model-family sensitivity than more frequently sampled indices.

### Regional aggregation

The reported Iowa-wide summaries are weighted by the station distribution among the five climatic regions. They are not area-, population-, watershed-, or cropland-weighted means.

### Decision-support interpretation

The dashboard is intended for regional screening, comparison, research, and planning support. It does not replace site-specific hydrologic, engineering, agricultural, or regulatory analysis.

---

## Citation

A formal article citation and repository DOI should be added after publication and archival release.

Suggested repository citation:

> Mukarram, M. M. T. (2026). *Iowa Climate Futures Explorer: A model-preserving CMIP6 analysis and interactive decision-support platform for regional heat and precipitation extremes*. GitHub repository.

After creating a versioned release, archive the repository with Zenodo and update both this section and `CITATION.cff` with the DOI.

---

## Author

### Mirza Md Tasnim Mukarram

School of Earth, Environment, and Sustainability  
University of Iowa  
Iowa City, Iowa, USA

Email: [mtasnimmukarram@uiowa.edu](mailto:mtasnimmukarram@uiowa.edu)

---

## License

The original code in this repository is released under the **MIT License**, unless otherwise stated.

NOAA, CMIP6, ESGF/Pangeo, and U.S. Census Bureau datasets retain their respective licenses, acknowledgements, and citation requirements.

---

## Acknowledgements

This project uses:

- NOAA GHCN-Daily observations;
- CMIP6 climate-model simulations;
- ESGF and Pangeo data infrastructure;
- U.S. Census Bureau geographic data; and
- open-source Python scientific-computing libraries.

---

<div align="center">

## Iowa Climate Futures Explorer

**Regional climate projections • Model comparison • Extreme-index analytics • Decision support**

<br>

Dashboard development is in progress.

<br>

If this repository supports your research, consider giving it a ⭐

</div>
