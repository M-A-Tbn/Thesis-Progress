# Comparison figures

These figures belong to the same [report](../Report.md). The latest set adds
Emmanuel's unchanged emulator to CAMB2 and CLASS. Each new plot contains all
nine redshifts. Start with the summary, then open one cosmology at a time.

## Latest three-way comparison — 7 November

| Plot | What it shows |
|---|---|
| [Summary across redshift](11_three_way_agreement_by_redshift.png) | Maximum and RMS percentage differences for all three pairs in the focus interval |
| [Flat LambdaCDM power](05_three_way_power_flat.png) | CLASS, CAMB2 and the original emulator spectra |
| [Flat LambdaCDM differences](08_three_way_residuals_flat.png) | CAMB2/CLASS, emulator/CLASS and emulator/CAMB2 residuals |
| [Curved LambdaCDM power](06_three_way_power_curved.png) | The same three predictions, including the labelled low-k caution region |
| [Curved LambdaCDM differences](09_three_way_residuals_curved.png) | All three pairs in the focus interval |
| [Evolving-dark-energy power](07_three_way_power_evolving_de.png) | The same three predictions, including the labelled low-k caution region |
| [Evolving-dark-energy differences](10_three_way_residuals_evolving_de.png) | All three pairs in the focus interval |

Residuals mean 100 × (first/second − 1), with the denominator named in each
legend. The focus interval is 0.02 < k < 0.3 Mpc^-1. Power overlays use the
full shared supported grid; red shading marks scales below the conservative
low-k cuts in the thesis inference examples, not a universal accuracy boundary.

## Earlier solver-only figures — unchanged

These compare CAMB 1.6.6, CAMB 2.0.4 and CLASS 3.1.0, not the emulator.
Their original SVG versions remain local. The new set was generated as PNGs.

| Plot | What it shows |
|---|---|
| [Agreement across redshifts](01_solver_agreement_by_redshift.png) | Maximum and RMS disagreement with CLASS for the three models across nine redshifts |
| [Flat LambdaCDM spectra](02_matter_power_flat_lcdm.png) | Flat LambdaCDM P(k): nine redshift panels, three solvers per panel |
| [Curved LambdaCDM spectra](03_matter_power_curved_lcdm.png) | Curved LambdaCDM P(k): nine redshift panels, three solvers per panel |
| [Evolving-dark-energy spectra](04_matter_power_evolving_dark_energy.png) | Evolving-dark-energy P(k): nine redshift panels, three solvers per panel |

The first figure shows the differences between the solvers. The other three
show the power spectra themselves, with one panel for each redshift.
