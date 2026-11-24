# Thesis progress

This repository follows the thesis from the initial solver comparisons through
to emulator reproduction, training and validation. Reports, plots and weekly
updates are collected here for discussion with Professor Marulli.

**Latest update: 24 November 2026.** [CAMB upgrade benchmark](camb-comparison/06_camb_upgrade_benchmark/Short%20report.md).

## Aim of the thesis

The aim is to reproduce Emmanuel's emulator (the current emulator living in CBL)
of the linear matter power spectrum and build a version based on CAMB2. An emulator
provides a fast approximation to a solver's predictions, so its accuracy needs to be
checked against the solver on cases that were not used for training.

The CAMB2 emulator will also be compared with current CBL's emulator over their
shared parameter range. Once that baseline works, and if time allows, a
massive-neutrino extension will be investigated following Pezzotta et al.

The CAMB comparison is the first practical step in this path. It helps check
the predictions that will later be used for the emulator work.

## Project path

| Stage | Work | Current status |
|---|---|---|
| 1. Solver study and comparison | Compare the CAMB versions used to calculate spectra for CBL and check their numerical behaviour. | CAMB 1.3.4, 1.6.6 and 2.0.5 were benchmarked on 49 density pairs and three main controls at four redshifts. The reports include the usual-settings comparison, runtime measurements and a recombination check. |
| 2. Evaluate the current CBL emulator | Check the existing implementation and compare its predictions with reference solvers. | The existing CBL emulator has been evaluated against CAMB2 and CLASS in 27 cases. The reference-spectrum mismatch remains open. |
| 3. Train and validate a CAMB2 emulator | Generate the training data, train the emulator and test it against CAMB2 on an independent test set. | Not started. |
| 4. Compare the emulators | Compare the CAMB2 and CBL emulators over their shared parameter range. | Planned after reproduction and training. |
| 5. Investigate massive neutrinos | Study an extension following Pezzotta et al. and agree on a suitable test and validation range. | Conditional on completing the baseline and having enough time. |

## Current step — assess the CAMB upgrade

The latest benchmark compares CBL’s bundled CAMB 1.3.4, CAMB 1.6.6 and
CAMB 2.0.5. It covers 49 pairs of baryon and cold-dark-matter densities,
plus a flat baseline, a curved model and evolving dark energy. Each run
returns spectra at redshifts 0, 0.5, 1 and 2.

At the usual settings, including **AccuracyBoost = 1**, the CAMB2 build was
about **3.8 times faster** on the median density-grid case. The largest
sampled differences in 0.02 < k < 0.3 Mpc⁻¹ were **1.54% against 1.3.4**
and **1.56% against 1.6.6**, at the lowest-CDM, highest-baryon grid corner.
Matching the older recombination calibration left the gap near 1.55%.

These measurements assess the solver upgrade for CBL and the generation
of new training spectra. The bundled solver provides an upgrade baseline.
The current emulator can be evaluated against CAMB2 to assess the result
of future retraining. The working setting remains AccuracyBoost = 1.

- [Short report with the main plots](camb-comparison/06_camb_upgrade_benchmark/Short%20report.md)
- [Detailed scientific report](camb-comparison/06_camb_upgrade_benchmark/Report.md)
- [Numerical data appendix](camb-comparison/06_camb_upgrade_benchmark/Data%20appendix.md)
- [Plot appendix covering all 52 presented cosmologies](camb-comparison/06_camb_upgrade_benchmark/Plot%20appendix.md)
- [Figure index and explanations](camb-comparison/06_camb_upgrade_benchmark/Figure%20index.md)

## Earlier work — the existing emulator comparison


The completed solver study has now been extended to CBL's shipped
emulator for the same three cosmologies and nine redshifts. The largest
sampled emulator/CAMB2 differences in 0.02 < k < 0.3 Mpc^-1 are **0.68817%**
for flat LambdaCDM, **0.42375%** for curved LambdaCDM and **0.68329%** for
evolving dark energy. CAMB2/CLASS differences stay below 0.070% there.

The comparison uses the existing CBL emulator. Its training assumptions
differ from the current solver setup, and the original training settings
are only partly known. The difference in the flat reference spectrum at z=0 remains an open
question for subsequent emulator validation.

- [Weekly update with two plots](meetings/2026-11-11.md)
- [Detailed comparison report](camb-comparison/01_current_solver_comparison/results/Report.md)
- [Data appendix](camb-comparison/01_current_solver_comparison/results/Data%20appendix.md)
- [Figure index](camb-comparison/01_current_solver_comparison/results/figures/Figure%20index.md)

### Earlier solver comparison

The earlier results compare CAMB 1.6.6, CAMB 2.0.4 and CLASS 3.1.0 for flat
LambdaCDM, curved LambdaCDM and evolving dark energy. Each model was tested at
nine redshifts from z=0 to z=2.

**CAMB2 had smaller maximum and RMS differences from CLASS in all 27 tested
model–redshift combinations**, within 0.02 < k < 0.3 Mpc^-1. RMS measures the
overall size of the sampled differences. This shows closer agreement with
CLASS under the tested settings, rather than establishing absolute accuracy.

- [Earlier weekly update — 29 October](meetings/2026-10-29.md): the solver-stage findings and remaining work at that date.
- [Earlier solver report](https://github.com/M-A-Tbn/Thesis-Progress/blob/56e515fee4b34f244a41875708cf9e891690bfef/camb-comparison/01_current_solver_comparison/results/Report.md) with the setup, results and limitations.
- [Input notes](camb-comparison/02_shared_inputs_and_z0_reference/Source%20audit.md): documented thesis settings and choices made for this comparison.

The DIFA library, network and growth/rescaling checks pass. The current CBL
implementation provides the reference emulator for subsequent training and
validation. The source code and detailed setup records stay local.

## Repository structure

The tree shows the files included in this progress update.

```text
thesis-progress/
├── .gitattributes
├── .gitignore
├── README.md
├── camb-comparison/
│   ├── 01_current_solver_comparison/
│   │   ├── Solver comparison guide.md
│   │   └── results/
│   │       ├── Data appendix.md
│   │       ├── Report.md
│   │       └── figures/
│   │           ├── 01_solver_agreement_by_redshift.png
│   │           ├── 02_matter_power_flat_lcdm.png
│   │           ├── 03_matter_power_curved_lcdm.png
│   │           ├── 04_matter_power_evolving_dark_energy.png
│   │           ├── 05_three_way_power_flat.png
│   │           ├── 06_three_way_power_curved.png
│   │           ├── 07_three_way_power_evolving_de.png
│   │           ├── 08_three_way_residuals_flat.png
│   │           ├── 09_three_way_residuals_curved.png
│   │           ├── 10_three_way_residuals_evolving_de.png
│   │           ├── 11_three_way_agreement_by_redshift.png
│   │           └── Figure index.md
│   ├── 02_shared_inputs_and_z0_reference/
│   │   └── Source audit.md
│   └── 06_camb_upgrade_benchmark/
│       ├── Data appendix.md
│       ├── Figure index.md
│       ├── Plot appendix.md
│       ├── Report.md
│       ├── Short report.md
│       └── figures/
│           ├── 01_density_difference_maps.png
│           ├── 02_native_runtime_maps.png
│           ├── 03_residuals_after_precision_checks.png
│           ├── 04_runtime_vs_numerical_deviation.png
│           ├── 05_gaps_above_1pct_vs_camb_1_3_4.png
│           ├── 06_gaps_above_1pct_vs_camb_1_6_6.png
│           └── plot-appendix/
│               ├── curved_lcdm.png
│               ├── evolving_dark_energy.png
│               ├── flat_baseline.png
│               ├── grid_b0c0.png
│               ├── grid_b0c1.png
│               ├── grid_b0c2.png
│               ├── grid_b0c3.png
│               ├── grid_b0c4.png
│               ├── grid_b0c5.png
│               ├── grid_b0c6.png
│               ├── grid_b1c0.png
│               ├── grid_b1c1.png
│               ├── grid_b1c2.png
│               ├── grid_b1c3.png
│               ├── grid_b1c4.png
│               ├── grid_b1c5.png
│               ├── grid_b1c6.png
│               ├── grid_b2c0.png
│               ├── grid_b2c1.png
│               ├── grid_b2c2.png
│               ├── grid_b2c3.png
│               ├── grid_b2c4.png
│               ├── grid_b2c5.png
│               ├── grid_b2c6.png
│               ├── grid_b3c0.png
│               ├── grid_b3c1.png
│               ├── grid_b3c2.png
│               ├── grid_b3c3.png
│               ├── grid_b3c4.png
│               ├── grid_b3c5.png
│               ├── grid_b3c6.png
│               ├── grid_b4c0.png
│               ├── grid_b4c1.png
│               ├── grid_b4c2.png
│               ├── grid_b4c3.png
│               ├── grid_b4c4.png
│               ├── grid_b4c5.png
│               ├── grid_b4c6.png
│               ├── grid_b5c0.png
│               ├── grid_b5c1.png
│               ├── grid_b5c2.png
│               ├── grid_b5c3.png
│               ├── grid_b5c4.png
│               ├── grid_b5c5.png
│               ├── grid_b5c6.png
│               ├── grid_b6c0.png
│               ├── grid_b6c1.png
│               ├── grid_b6c2.png
│               ├── grid_b6c3.png
│               ├── grid_b6c4.png
│               ├── grid_b6c5.png
│               └── grid_b6c6.png
└── meetings/
    ├── 2026-10-29.md
    └── 2026-11-11.md
```

The `meetings/` folder holds the weekly updates across the thesis. The
`camb-comparison/` folder contains the reports and plots for the solver and
emulator comparisons. The latest upgrade benchmark is in
`06_camb_upgrade_benchmark/`. The earlier three-way comparison is in
`01_current_solver_comparison/`, with its input notes in
`02_shared_inputs_and_z0_reference/`. These folder numbers identify studies
within the thesis.

The first unchanged-emulator comparison extends the current report. Later
training, validation and any neutrino-extension results will be added as the
work is carried out; those stages have not produced results yet.

## Discussion and feedback

Feedback and questions can be added in
[Issues](https://github.com/M-A-Tbn/Thesis-Progress/issues) or discussed alongside
the weekly updates.

This repository will continue to track the whole thesis through written
reports and PNG plots. Numerical data, calculation code, raw runs and SVG
originals remain in the local research workspace. A separate repository for
the complete code and calculation files is planned for later.
