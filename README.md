# Thesis progress

Weekly reports and plots are kept here for discussion.

**24 November 2026** · [This week’s short report on the CAMB upgrade](camb-comparison/06_camb_upgrade_benchmark/Short%20report.md)

## Aim of the thesis

The thesis aims to reproduce the behaviour of the emulator in CosmoBolognaLib
(CBL) and to train a new version using spectra calculated with CAMB2. CBL’s
emulator predicts the linear matter power spectrum, a measure of how strongly
matter clusters on different scales. Once trained, it can make that prediction
much faster than a numerical solver can calculate the spectrum directly.

The choice of solver matters because its spectra provide the examples from which
the new emulator will learn. The first part of the thesis therefore examines
how closely different solvers agree and how long they take to produce the
training spectra. Once trained, the new emulator will be tested against CAMB2
on cosmologies held back from training. A separate comparison with CBL’s emulator
will then show how their predictions differ over the parameter range both cover.

## Thesis progress

| Stage | Current progress |
|---|---|
| Compare the solvers | The October study compared CAMB with the independent solver CLASS. The November benchmark examined how changing the CAMB version affects both the spectra and the calculation time. |
| Reproduce CBL’s emulator | The existing implementation has been run and its predictions compared with CAMB2 and CLASS in 27 cases. The origin of a difference in the flat reference spectrum is still under investigation. |
| Train and validate a CAMB2 emulator | Training and independent validation are planned. The solver benchmark provides a timing estimate for generating the training data. |
| Compare the two emulators | Once validation is complete, the comparison will cover cosmologies within the range of both emulators. |
| Investigate massive neutrinos | If the baseline comparison is complete and time permits, the thesis will explore an extension following Pezzotta et al. |

## 24 November · The CAMB upgrade

Generating training data requires repeated calculations of the matter power
spectrum. This week’s benchmark addressed two questions. How much time would
CAMB2 save per calculation, and how much would the spectra used for training
change? The comparison included CAMB 1.3.4, the version bundled with CBL,
alongside CAMB 1.6.6 and CAMB 2.0.5. It covered 49 combinations of baryon and
cold dark matter densities. Three additional models served as controls, one
with a flat geometry, one with spatial curvature and one with evolving dark
energy. Each solver call returned spectra at four redshifts (0, 0.5, 1 and 2).

At each version’s usual settings (`AccuracyBoost = 1`), **the median speedup
across the 49 density pairs was about 3.8×** for CAMB 2.0.5 relative to either
older version. For the flat control, for example, the calculation took
0.141 seconds with CAMB 2.0.5, compared with 0.537 seconds for CAMB 1.3.4 and
0.543 seconds for CAMB 1.6.6. These timings cover the solver call itself.
Measuring the saving in a CBL calculation would require timing the same
request through the CBL interface.

Across most density pairs, the largest change in power stayed below 0.1% for
$0.02 < k < 0.3\,\mathrm{Mpc}^{-1}$, where $k$ is the wavenumber that identifies
the scale being compared. The largest differences occurred at the highest
baryon density and lowest cold dark matter density in the grid. There, the
difference reached **1.54% relative to CAMB 1.3.4 and 1.56% relative to CAMB
1.6.6**. Repeating the comparison with the older calibration of the
recombination model left the gap near 1.55%, so the change in calibration
alone does not explain it. The project continues to use `AccuracyBoost = 1`.

- [Short report with the main plots](camb-comparison/06_camb_upgrade_benchmark/Short%20report.md)
- [Detailed report](camb-comparison/06_camb_upgrade_benchmark/Report.md)
- [Data appendix](camb-comparison/06_camb_upgrade_benchmark/Data%20appendix.md)
- [Plots for all 52 cosmologies shown in the report](camb-comparison/06_camb_upgrade_benchmark/Plot%20appendix.md)
- [Figure index](camb-comparison/06_camb_upgrade_benchmark/Figure%20index.md)

## Earlier results

### 11 November · CBL’s emulator compared with CAMB2 and CLASS

This study used the solver spectra from October as a reference for CBL’s
emulator. Each of three cosmological models was tested at nine redshifts.
Over the same range of wavenumbers used in the November benchmark, the largest
differences between CBL’s emulator and CAMB2 were 0.68817% for flat ΛCDM,
0.42375% for curved ΛCDM and 0.68329% for evolving dark energy. CAMB2 and
CLASS agreed to within 0.070% across those cases.

CBL’s emulator first predicts a reference spectrum at $z=0$ and then rescales
it to other redshifts. The checks on the network, growth calculation and
rescaling all passed in the DIFA version of CBL. In the flat model, the
differences from CAMB2 followed a similar pattern at all nine redshifts.
Comparing the reference spectra at $z=0$ would help establish how much of
that difference was already present before rescaling. Only part of the
original training setup is known.

[Weekly update with two plots](meetings/2026-11-11.md) · [Detailed report](camb-comparison/01_current_solver_comparison/results/Report.md) · [Data appendix](camb-comparison/01_current_solver_comparison/results/Data%20appendix.md) · [Figure index](camb-comparison/01_current_solver_comparison/results/figures/Figure%20index.md)

### 29 October · Agreement between the solvers

The first study used CLASS 3.1.0 as an independent point of comparison for
CAMB 1.6.6 and CAMB 2.0.4. For each of the three models, the comparison
covered nine redshifts from $z=0$ to $z=2$. Within the range of wavenumbers
given above, **CAMB 2.0.4 agreed more closely with CLASS in all 27 cases**.
This held for both the largest difference at any sampled scale and the root
mean square (RMS) difference, which summarises the differences across all
sampled scales. The result measures agreement between these solvers under
the settings used in the study.

[Weekly update](meetings/2026-10-29.md) · [Solver report as published in October](https://github.com/M-A-Tbn/Thesis-Progress/blob/56e515fee4b34f244a41875708cf9e891690bfef/camb-comparison/01_current_solver_comparison/results/Report.md) · [Notes on the input settings](camb-comparison/02_shared_inputs_and_z0_reference/Source%20audit.md)

## Repository structure

The `meetings/` folder contains the October and 11 November meeting notes.
The `camb-comparison/` folder groups the scientific reports, appendices and
plots by study. The calculation code, raw solver outputs and original SVG
figures are kept in the local research workspace for a separate project
repository planned for later.

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
│               ├── grid_...
└── meetings/
    ├── 2026-10-29.md
    └── 2026-11-11.md
```

## Discussion and feedback

The reports provide the basis for discussion at thesis meetings. Questions
about a particular calculation or figure can also be recorded in
[GitHub Issues](https://github.com/M-A-Tbn/Thesis-Progress/issues).
