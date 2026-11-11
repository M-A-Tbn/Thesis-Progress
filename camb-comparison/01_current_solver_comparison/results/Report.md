# Linear matter power: solvers and the current CBL emulator

## Latest comparison — 7 November 2026

The earlier solver comparison has now been extended to CosmoBolognaLib's existing
emulator. CAMB2, CLASS and CBL emulator were compared at the
same cosmologies and redshifts using the supplied network weights.

All **three cosmologies at nine redshifts** have been evaluated: flat
LambdaCDM, curved LambdaCDM and evolving dark energy, at z=0, 0.25, 0.5,
0.75, 1, 1.25, 1.5, 1.75 and 2. Each case now has a CAMB 2.0.4 spectrum,
a CLASS 3.1.0 spectrum and an emulator spectrum.

### Main result

The curves lie almost on top of each other in the power-spectrum plots.
However, the percentage-difference plots reveal a clear distinction:
**CAMB2 and CLASS agree more closely with each other than either agrees
with the emulator**, as measured by maximum and RMS differences
in every tested case in the focus range, 0.02 < k < 0.3 Mpc^-1.

The table gives the largest sampled absolute percentage difference found
across the nine redshifts, separately for each pair and cosmology. The
three entries in a row do not necessarily occur at the same k or redshift.

| Cosmology | CAMB2 / CLASS | Emulator / CLASS | Emulator / CAMB2 |
|---|---:|---:|---:|
| Flat LambdaCDM | 0.06920% | 0.62622% | 0.68817% |
| Curved LambdaCDM | 0.06589% | 0.48513% | 0.42375% |
| Evolving dark energy | 0.06832% | 0.62089% | 0.68329% |

The 0.68817% value is the largest absolute emulator/CAMB2 difference at a
sampled point in the flat model. The root mean square (RMS) summarizes the
size of the differences over all sampled points at a given redshift. Across
the nine redshifts, the emulator/CAMB2 RMS is approximately 0.1795% for flat
LambdaCDM, 0.1576% for curved LambdaCDM and 0.1792% for evolving dark energy.

The [data appendix](Data%20appendix.md) gives the numbers for each pair and
redshift across all three sampling ranges.

![Three-way agreement across redshift](figures/11_three_way_agreement_by_redshift.png)

The emulator/CAMB2 differences change very little with redshift in these
tests. **Interpretation:** this is consistent with a persistent shape
difference being carried through the growth rescaling, rather than a
difference that becomes much larger with redshift. It does not identify
the physical or numerical cause of this behaviour. The curved case also uses
a different sampling grid, so its smaller maximum cannot by itself establish
that the emulator works better in curved cosmologies.

### What the emulator calculation includes

The network predicts a reference spectrum at z=0 from two density inputs.
The surrounding CBL code then changes its amplitude and shape using the
primordial parameters, the growth-factor ratio and the curvature correction.
This two-part construction is described in Emmanuel's thesis Section 4.2,
Equation (4.3), and illustrated in Figure 4.3. The comparison uses predictions
from **the complete implementation**.

The input densities are Omega_b=0.04936781 and Omega_CDM=0.26447041 at the
reference h=0.6736. These follow from the same physical densities used in
the solver comparison: omega_b=0.0224 and omega_CDM=0.120, with omega=Omega h².
They lie inside both the thesis and shipped density ranges. The wider ranges
listed in the shipped metadata were not treated as a newly validated domain.

### Inputs for the three-way comparison

The saved CAMB2 and CLASS spectra were reused. The target inputs shared
with the emulator were H0 = 67.36 km/s/Mpc, omega_b = 0.0224,
omega_CDM = 0.120, As = 2.1e-9 and ns = 0.9649, with a pivot of
0.05 Mpc^-1. The curvature and dark-energy parameters were as follows.

| Model | Omega_k | w0 | wa |
|---|---:|---:|---:|
| Flat LambdaCDM | 0 | -1 | 0 |
| Curved LambdaCDM | 0.01 | -1 | 0 |
| Evolving dark energy | 0 | -0.99 | -0.02 |


The emulator uses radiation in two places. First, radiation affects the shape
of the reference power spectrum that the network learned. Second, it affects
the expansion of the universe and therefore how matter fluctuations grow. Only
the second part—the growth calculation—can be given a new radiation density
without changing the trained network.

For the growth calculation, the same present-day radiation density as in CLASS
was used: $\Omega_r = 9.218085625177\times10^{-5}$. This includes photons and
massless neutrinos. The dark-energy density was then set by the expansion equation:
once matter, radiation and curvature were specified, the equation fixed how much
dark energy was needed to match the chosen expansion rate today. All three
predictions were compared in the same units: Mpc⁻¹ for $k$ and Mpc³ for $P(k)$.

The trained network’s documentation lists slightly different radiation settings:
$N_{\rm eff}=3.04$ and $\Omega_r=9.26535\times10^{-5}$. The solver runs used
$N_{\rm eff}=3.044$ and calculated the radiation density from that value and the
cosmic microwave background temperature. Since the network takes only baryon and
cold-dark-matter densities as inputs, matching the radiation density in the growth
calculation does not change the starting spectrum it predicts. The exact CAMB version
and precision settings used to generate the training data are also unknown. I am not
sure if the CAMB version included with the code is the one used for training.

The measured differences therefore show how closely the **complete emulator** agrees
with CAMB2 and CLASS in this setup. They do not show how much of the difference comes
from the original training spectra, the network’s approximation, interpolation, or
the growth calculation. Emmanuel’s thesis tested the emulator under its own settings,
and CLASS provides an independent comparison, not an exact answer to be treated as the ground truth.

### How the differences were measured

For each pair of predictions A and B, the percentage difference was calculated as $100(P_A/P_B - 1)$. The second prediction is the reference. For example, a positive emulator/CLASS difference means the emulator predicts more power than CLASS at that scale.

The original CLASS sampling points were used as the comparison grid. CAMB2 had already been evaluated at these points using its own interpolation routine. CBL used a cubic spline in linear $k$ and linear $P$ to evaluate the emulator at the same points.

The emulator’s native range starts at $k = 1.5 \times 10^{-4}\,\mathrm{Mpc}^{-1}$. The two lowest CLASS points fall below this limit and were omitted, leaving 99 common points per case. The highest sampled point is below $1\,\mathrm{Mpc}^{-1}$. The focus range, $0.02 < k < 0.3\,\mathrm{Mpc}^{-1}$, contains 63 points for flat ΛCDM and evolving dark energy, and 62 for curved ΛCDM.

Each sampled point was given equal weight. The **maximum** is the largest absolute difference among those points. The **RMS** summarizes the size of the differences by squaring them, averaging them and taking the square root. The **signed mean** shows the average offset, although positive and negative differences can cancel. The **95th percentile** gives the value below which about 95% of the absolute differences fall.

The appendix gives results for the full common grid, the focus range and the grid after applying the lower limits used in Emmanuel’s inference examples. Those limits are $8 \times 10^{-4}\,\mathrm{Mpc}^{-1}$ for curved ΛCDM and $3 \times 10^{-3}\,\mathrm{Mpc}^{-1}$ for evolving dark energy. The flat case keeps the full common grid. The red shading marks scales below these limits, which remain included in the full-grid statistics. The limits describe the scales selected in those inference examples.

### Power spectra and percentage differences

Each figure has one panel per redshift. Start with the power plot to see the
overall spectrum, then use its difference plot to see what the overlap hides.

| Cosmology | P(k) overlays | All three pairwise differences in the focus range |
|---|---|---|
| Flat LambdaCDM | [Power spectra](figures/05_three_way_power_flat.png) | [Percentage differences](figures/08_three_way_residuals_flat.png) |
| Curved LambdaCDM | [Power spectra](figures/06_three_way_power_curved.png) | [Percentage differences](figures/09_three_way_residuals_curved.png) |
| Evolving dark energy | [Power spectra](figures/07_three_way_power_evolving_de.png) | [Percentage differences](figures/10_three_way_residuals_evolving_de.png) |

### Checks, inference decision and next question

The network passed 10 test cases covering 9,960 checks. The growth calculation passed 14 cases covering 543 checks, and the rescaling and normalization passed 15 cases covering 220 checks.

An independent Python calculation agreed with the compiled network within $8.9 \times 10^{-16}$ in $\log_{10}P$ and with the interpolated spectrum within $1.2 \times 10^{-15}$ in relative power. All 243 statistical summaries were independently recalculated. Each of the 27 emulator predictions was run three times and gave identical values.

At the emulator’s original sampling points, the full CBL calculation agreed with an independent reconstruction of the rescaling and unit conversion. For flat ΛCDM at $z=0$, using the reference settings, that reconstruction recovered the spectrum predicted directly by the network. These checks establish consistency between the calculations. Assessing physical accuracy requires a separate comparison.

The percentage differences between the fixed spectra were calculated directly. A Markov chain Monte Carlo (MCMC) analysis would address whether those differences affect inferred cosmological parameters. It would require a separate setup with observations or mock data, their uncertainties and covariance, a likelihood, free parameters, priors and convergence checks.

The next question is **how much of the discrepancy is already present in the flat ΛCDM reference spectrum at $z=0$**. Recovering the original training settings would allow a solver comparison at that reference point and help distinguish the starting discrepancy from changes introduced by the growth rescaling.

## AI assistance and human review

AI tools helped draft and edit this report, organize the figures, and prepare
the data appendix from the saved numerical results. I reviewed and revised
the report before approving it for publication on GitHub.

The [weekly update](../../../meetings/2026-11-11.md) summarizes the findings.

For the original solver settings and results, see the [earlier solver report](https://github.com/M-A-Tbn/Thesis-Progress/blob/56e515fee4b34f244a41875708cf9e891690bfef/camb-comparison/01_current_solver_comparison/results/Report.md).
