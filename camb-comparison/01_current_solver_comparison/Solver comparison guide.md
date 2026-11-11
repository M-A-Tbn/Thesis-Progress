# Solver and emulator comparison — report and plots

This folder holds one continuing experiment, with two completed comparisons.
The earlier stage compared CAMB 1.6.6, CAMB 2.0.4 and CLASS 3.1.0. The latest
stage adds Emmanuel's unchanged emulator alongside CAMB2 and CLASS. Both use
three cosmologies at nine redshifts from z=0 to z=2; no CAMB2 network was trained.

The [weekly update](../../meetings/2026-11-11.md) gives the main result
and two plots. The [detailed report](results/Report.md) explains the setup,
checks and limits. Per-redshift tables and the values for all three
sampling ranges are in the [data appendix](results/Data%20appendix.md).

The new calculation is complete for all 27 cases. In the focus range,
the largest emulator/CAMB2 sampled differences are about 0.69%, 0.42% and
0.68% for flat, curved and evolving dark energy. The report explains why
these are not isolated neural-network errors or parameter-bias measurements.

## Figures

The latest power spectra and residuals are linked in the
[figure index](results/figures/Figure%20index.md). Figures 05–11 show CAMB2,
CLASS and the emulator. Figures 01–04 preserve the earlier solver-only results.

The earlier power spectra are shown separately for
[flat LambdaCDM](results/figures/02_matter_power_flat_lcdm.png),
[curved LambdaCDM](results/figures/03_matter_power_curved_lcdm.png), and
[evolving dark energy](results/figures/04_matter_power_evolving_dark_energy.png).
Each figure has nine panels, one per redshift. The
[figure index](results/figures/Figure%20index.md) links each PNG plot.

## Inputs and results

The [input notes](../02_shared_inputs_and_z0_reference/Source%20audit.md) explain
which settings were taken from Emmanuel's thesis and where choices were needed.
The [report](results/Report.md) gives the input values and checks alongside the plots.

The numerical data, detailed calculation records and SVG originals are kept
locally. This repository contains the written results and PNG plots for discussion.
The emulator's fixed radiation assumptions and incomplete training provenance
are stated explicitly. MCMC has not been run: its inference setup has not
been agreed, and it is not required to compare fixed spectra. The next question
is the origin of the persistent reference-spectrum mismatch, before retraining.
