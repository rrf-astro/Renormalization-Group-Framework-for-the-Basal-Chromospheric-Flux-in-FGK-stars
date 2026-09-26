# An Effective Renormalization-Group Framework for the Basal Chromospheric Flux in FGK Dwarfs

Reproducibility repository accompanying the manuscript:

**“An Effective Renormalization-Group Framework for the Basal Chromospheric Flux in FGK Dwarfs”**

by R. R. Ferreira et al.

## Overview

This repository contains the data-analysis pipeline, processed analysis data, machine-readable results, tables, and figures used in the manuscript.

The analysis describes the chromospheric excess above the basal Ca II H&K flux through the dimensionless quantity

\[
\epsilon = \frac{F_{\rm Ca}-F_{\rm bas}}{F_{\rm bas}},
\]

and uses the Rossby number

\[
Ro = \frac{P_{\rm rot}}{\tau_{\rm conv}}
\]

as the scale variable.

For the selected FGK main-sequence sample in the unsaturated regime, the effective scaling relation is

\[
\epsilon \propto Ro^{-\omega}.
\]

The primary multivariate analysis of the full sample (\(N=1145\)) gives

\[
\omega = 0.900 \pm 0.047.
\]

The repository also contains the spectral-type fits and the robustness tests discussed in the manuscript.

## Repository structure

```text
.
├── README.md
├── requirements.txt
├── LICENSE
├── Ye2024.tsv
├── Gomes2021.tsv
├── Wright2011.tsv
├── Baliunas1996.tsv
├── J_AJ_132_161_table2.tsv
├── notebooks/
│   └── data_pipeline.ipynb
├── data/
│   ├── fgk_activity_sample.csv
│   ├── supplementary_stars.csv
│   ├── ye_isaacson_crossmatch.csv
│   ├── ye_bv_legacy.csv
│   └── README.md
├── tables/
│   ├── table1_powerlaw_fits.csv
│   ├── table2_tauconv_sensitivity.csv
│   └── table3_FG_boundary_sensitivity.csv
├── figures/
│   ├── fig1_activity_rossby.pdf
│   ├── fig2_rg_flow.pdf
│   └── fig_validation_isaacson.pdf
└── results/
    ├── main_results.json
    ├── robustness_results.json
    ├── reproducibility_manifest.json
    └── reproducibility_summary.txt
```

## Data

The working sample contains 1145 FGK main-sequence stars.

The primary component consists of 1095 stars from the Ye et al. (2024) sample. An additional 50 stars from supplementary sources are included as described in the manuscript.

The repository provides the processed dataset used in the statistical analysis and the supplementary measurements needed to reproduce the combined sample.

Five raw source-catalogue TSV files are included at the repository root for transparency and offline reproducibility. Of these, only `Ye2024.tsv` is actually read by the notebook, as the local fallback tier of the Ye et al. (2024) acquisition (used only if the live VizieR TAP/HTTP services are unreachable). `Gomes2021.tsv`, `Wright2011.tsv`, `Baliunas1996.tsv`, and `J_AJ_132_161_table2.tsv` are not read by any notebook cell; they are included as a historical/provenance record of the catalogues consulted during development, not as pipeline inputs.

See `data/README.md` for data provenance and column definitions.

## Analysis notebook

The complete analysis is contained in:

```text
notebooks/data_pipeline.ipynb
```

The notebook reproduces the main processing and analysis steps used in the manuscript, including:

- construction and validation of the working FGK sample;
- calculation of Rossby numbers;
- calculation of the basal Ca II H&K flux;
- calculation of the dimensionless chromospheric excess;
- F-, G-, and K-star power-law fits;
- the full-sample multivariate regression;
- metallicity and convective-turnover-time robustness tests;
- signal-to-noise sensitivity tests near the basal floor;
- F/G temperature-boundary sensitivity tests;
- source-to-source consistency tests;
- independent activity/rotation cross-checks;
- generation of manuscript tables;
- generation of manuscript figures;
- export of machine-readable results.

The notebook is intended to be executed from top to bottom.

## Installation

A Python virtual environment is recommended.

For example:

```bash
python -m venv .venv
source .venv/bin/activate
```

On Windows:

```bash
.venv\Scripts\activate
```

Install the required packages with:

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

Start Jupyter with:

```bash
jupyter lab
```

or:

```bash
jupyter notebook
```

Then open `notebooks/data_pipeline.ipynb` and run all cells in order.

## Reproducibility

The processed analysis dataset is included so that the statistical results can be reproduced without depending on the availability of every external catalogue service.

Where the notebook accesses public catalogues, those data retain their original provenance and should be cited using the references given in the manuscript.

The principal numerical outputs are also provided in machine-readable form under `results/`, while the values corresponding to the manuscript tables are exported under `tables/`.

## Main outputs

The principal results reproduced by the notebook include:

- full-sample multivariate exponent: \(\omega = 0.900 \pm 0.047\);
- F dwarfs: \(\omega_F = 0.721 \pm 0.080\);
- G dwarfs: \(\omega_G = 1.031 \pm 0.062\);
- K dwarfs: \(\omega_K = 0.823 \pm 0.202\).

Additional robustness and sensitivity results are reported in the manuscript and exported by the notebook.

## Figures and tables

The `figures/` directory contains the publication figures generated by the analysis pipeline.

The `tables/` directory contains machine-readable versions of the numerical tables reported in the manuscript.

Generated files should be reproducible by running the notebook from a clean environment with the dependencies listed in `requirements.txt`.

## Citation

If you use this repository, please cite the accompanying manuscript.

A complete journal citation and DOI will be added after publication.

A permanent archival DOI for this repository will also be added here when available.

## Authors

R. R. Ferreira et al.

Federal Institute of Triângulo Mineiro (IFTM), Uberaba, Minas Gerais, Brazil.

## License

See the `LICENSE` file for the license applying to the repository code.

Data originating from external catalogues remain subject to the citation requirements and usage conditions of their original sources.
