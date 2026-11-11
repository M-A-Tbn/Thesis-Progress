# Thesis progress

This repository follows the thesis from the initial solver comparisons through
to emulator reproduction, training and validation. Reports, plots and weekly
updates are collected here for discussion with Professor Marulli.

**Latest update: 11 November 2026.** [Weekly note and plots](meetings/2026-11-11.md).

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
| 1. Solver study and comparison | Study CAMB2 and compare its predictions with CAMB, using CLASS as an independent reference. | Three models have been compared at nine redshifts. Numerical convergence remains to be checked. |
| 2. Reproduce Emmanuel's emulator | Obtain the implementation and trained weights, then reproduce the main results and plots. | The unchanged DIFA emulator has been checked and compared locally with CAMB2 and CLASS in all 27 cases. A persistent spectrum mismatch and incomplete training provenance remain; exact thesis reproduction is not claimed. |
| 3. Train and validate a CAMB2 emulator | Generate the training data, train the emulator and test it against CAMB2 on an independent test set. | Not started. |
| 4. Compare the emulators | Compare the CAMB2 and CBL emulators over their shared parameter range. | Planned after reproduction and training. |
| 5. Investigate massive neutrinos | Study an extension following Pezzotta et al. and agree on a suitable test and validation range. | Conditional on completing the baseline and having enough time. |

## Current step: compare the existing emulator with the solvers

The completed solver study has now been extended to CBL's shipped
emulator for the same three cosmologies and nine redshifts. The largest
sampled emulator/CAMB2 differences in 0.02 < k < 0.3 Mpc^-1 are **0.68817%**
for flat LambdaCDM, **0.42375%** for curved LambdaCDM and **0.68329%** for
evolving dark energy. CAMB2/CLASS differences stay below 0.070% there.

The comparison uses the existing CBL emulator. Its training assumptions
differ from the current solver setup, and the original training settings
are only partly known. The next step is to investigate the difference in
the flat reference spectrum at z=0.

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

The DIFA library, network and growth/rescaling checks now pass. Original
training/validation scripts and full dataset provenance remain to be obtained
before retraining. The source code and detailed setup records stay local.

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
│   └── 02_shared_inputs_and_z0_reference/
│       └── Source audit.md
└── meetings/
    ├── 2026-10-29.md
    └── 2026-11-11.md
```

The `meetings/` folder holds the weekly updates across the thesis. The
`camb-comparison/` folder contains the reports and plots for the solver-comparison
stage. Within it, `01_current_solver_comparison/` holds the current results,
while `02_shared_inputs_and_z0_reference/` records how the baseline inputs
were chosen. Those numbers identify folders within this stage; they are not
the stages of the whole thesis.

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
