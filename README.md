# Bottleneck recovery: simulations and figure code

SLiM simulations and R code reproducing the figures on heterozygosity,
nucleotide diversity, and site-frequency-spectrum recovery through a
population bottleneck, alongside real koala allele-frequency data from
Ahrens et al. (2026), for a manuscript on mutation rate and diversity
statistic recovery.

## Contents

- `paper_figures.Rmd` -- the analysis script. Runs the SLiM model, reads the
  koala allele-frequency data, and builds every figure.
- `bottleneck.slim` -- the SLiM (>= 5.0) neutral bottleneck-and-recovery
  model that `paper_figures.Rmd` drives.

## Requirements

- **SLiM >= 5.0**, on your `PATH` (or point the `SLIMR_PATH` environment
  variable at the binary). Earlier versions have a bug where `calcPi()`
  silently runs Watterson's theta's code instead -- `paper_figures.Rmd`
  checks the version and stops if it's too old.
- **R** with the packages: `dplyr`, `tidyr`, `readr`, `purrr`, `furrr`,
  `ggplot2`, `scales`, `rlang`, `patchwork`, `ggh4x`.
- A `data/` folder (see below) placed alongside `paper_figures.Rmd`.

## Data

Figure 4 reads twelve raw allele-frequency and VEP-consequence tables from a
`data/` folder next to `paper_figures.Rmd`. **These are not included in this
repository.** They were made available previously by:

> Ahrens, C. W., et al. (2026). Escaping bottlenecks: The demographic path to
> genetic recovery in koalas (*Phascolarctos cinereus*). *Science*.
> https://doi.org/10.1126/science.adz1430

The exact filenames expected in `data/` are listed in `paper_figures.Rmd`
(Figure 4 section).

## Running it

Knit `paper_figures.Rmd`. On a clean checkout this will:

1. Run the bottleneck simulations via SLiM (a few minutes, in parallel across
   5 workers) and cache the results.
2. Read and tidy the koala data from `data/`.
3. Rebuild every figure and save it as a PDF alongside the script:
   - `Figure2_combined_diversity_sfs.pdf`
   - `Figure3_simp_formula_recovery_and_loss.pdf`
   - `Figure4_combined_plot_rot.pdf`

Re-knitting after editing `bottleneck.slim` automatically reruns the
simulations -- the cache is keyed on the model file's checksum.
