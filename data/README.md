# Data directory

This directory holds the input data shipped with the repository and the
public working sample exported by `notebooks/data_pipeline.ipynb`.

## Input files (read by the notebook)

### `supplementary_stars.csv`

The 50 non-Ye et al. (2024) stars used to complete the working sample
(Section 3.1 of the manuscript): 9 stars in common with the AMBRE-HARPS
catalogue of Gomes da Silva et al. (2021) (with rotation periods from
Baliunas et al. 1996), the Sun, and 40 further Mount Wilson stars from
Hall et al. (2007), of which 23 can be matched by name to published
rotation periods (Wright et al. 2011) and 17 have no machine-readable
public source for their period (Hall et al. 2007 manual compilation;
`star_name` is blank for these rows, provenance `Hall2007+Supp`).

Columns `star_name, source, logRHK, e_logRHK, Prot, Teff, BV, tau_conv,
tau_Noyes1984` are the raw compiled measurements. Everything else used in
the analysis (`F_Ca`, `F_bas`, `Ro`, `epsilon`, ...) is *derived* by the
notebook from these columns with the same formulas used for the Ye et al.
(2024) stars — nothing beyond these 9 columns is taken as given for the
supplementary sample.

### `ye_isaacson_crossmatch.csv`

Raw Gaia DR3 cross-match table between the Ye et al. (2024) sample and the
independent California–Kepler Survey activity catalogue (Isaacson et al.
2024, J/ApJ/961/85), used only for the independent validation of
`logR'HK` and `Prot` (Section 3.1 of the manuscript). Not used to compute
any frozen result. Column names are duplicated between the two source
catalogues (`logRHK`/`logRHK.1`, `Prot`/`Prot.1`); the notebook disambiguates
them by column position relative to the `KOI` column, not by suffix.

### `ye_bv_legacy.csv`

`(Teff_key, Prot_key, logRHK_key, BV)` for the 1095 Ye et al. (2024) stars
of the working sample, keyed by rounded physical parameters
(`Teff` as an integer, `Prot` to 2 decimals, `logR'HK` to 4 decimals —
unique for all 1095 stars) rather than by Gaia identifier. The Gaia
column recorded in the legacy `p6_data_combined_v3.csv` was found to be
corrupted for roughly half of the Ye stars (a `float()` round-trip during
a past export step loses precision for 19-digit Gaia DR3 identifiers);
the physical-parameter key gives an exact, collision-free 1095/1095
match against a freshly acquired Ye et al. (2024) catalogue, so it is
used here instead.

**Provenance note:** the Ye et al. (2024) VizieR table
(`J/ApJS/271/19/table3`) does not publish a `B-V` colour — it provides
`Teff`, `logg`, `[Fe/H]`, `Mass`, `Age`, `Prot`, `logR'HK` and Gaia/KIC
identifiers only. The `B-V` values in this file were computed at an
earlier stage of the project by a method that is no longer recoverable
from the notebook's visible history. They are **not** used anywhere in
the primary scientific pipeline: the adopted convective-turnover-time
calibration is the mass-based relation of Wright et al. (2011) (Eq. 11),
which uses `Mass` from Ye et al. (2024) directly and needs no colour term.
`BV` is used only for two secondary, explicitly-labelled checks:

- the `(B-V)`-based convective-turnover-time calibration of Noyes et al.
  (1984), reported as a robustness/sensitivity comparison against the
  adopted Wright et al. (2011) calibration (manuscript Table 2), never as
  an alternative primary result; and
- the cosmetic gyrochronology isochrones drawn in Figure 2, which are a
  visualization of the fitted relation, not an independent fit.

No new colour-temperature relation was introduced during this
repository cleanup to "fill in" this column; the frozen values are
carried forward unchanged, consistent with the reproducibility policy of
this repository (see `NOTEBOOK_REFACTOR_GUIDE.md`, not included in the
public repository).

## Output file (written by the notebook, after the reproducibility gate)

### `fgk_activity_sample.csv`

The full N = 1145-star combined working sample with all derived
quantities (`Ro`, `epsilon`, `F_Ca`, `F_bas`, `log_Ro`, `log_epsilon`,
`dTeff`, ...), reconstructed in memory from `supplementary_stars.csv` and
the Ye et al. (2024) catalogue acquisition. This file is a pipeline
*output*, not an input — it is written only after all reproducibility
gates in the notebook have passed.
