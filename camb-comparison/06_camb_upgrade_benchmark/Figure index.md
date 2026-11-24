# Figure index — CAMB2 upgrade benchmark

Start with the [short report](Short%20report.md) for the interpretation.
The figures below all come from saved numerical calculations. None shows
an emulator prediction or uncertainty from observations.

The [plot appendix](Plot%20appendix.md) has an individual figure for
each of the 52 cases discussed in the report. The figures below
summarize the comparison and retain the earlier diagnostics.

## Figures used in the reports

### [01 — Where the power spectrum changes](figures/01_density_difference_maps.png)

Each cell is one tested combination of baryon density and cold-dark-matter
density. The top panels show the largest absolute difference across the
four redshifts in the focus range. The bottom panels show the RMS, which
uses every point in that range. The columns compare CAMB2 with CAMB 1.3.4
and 1.6.6, using the same colour scale within each row. White outlines
identify the largest-gap grid points selected for follow-up checks.

### [02 — How much time the upgrade saves at native settings](figures/02_native_runtime_maps.png)

Each cell divides the older version’s median time by CAMB2’s median time
to deliver all four linear power spectra. A ratio of 4× means that the
older calculation took four times as long as CAMB2 on the benchmark
machine. These are not ratios at a common numerical precision target.

### [05 — Grid gaps above 1%: CAMB2 vs CAMB 1.3.4](figures/05_gaps_above_1pct_vs_camb_1_3_4.png)

The seven panels show the grid cosmologies whose largest absolute
difference exceeded 1% in either native-settings comparison over
$0.02 < k < 0.3\,\mathrm{Mpc}^{-1}$. Each panel shows the signed difference
at $z=0,\,0.5,\,1,\,2$, with dashed lines at $\pm1\%$. A dot marks
the largest absolute difference, and the panel title gives its sign,
magnitude, $k$ and $z$. The four curves can nearly overlap. The 1%
selection is separate from the white outlines in Figure 01.

### [06 — Grid gaps above 1%: CAMB2 vs CAMB 1.6.6](figures/06_gaps_above_1pct_vs_camb_1_6_6.png)

The same seven cosmologies and the same axes as Figure 05, now with
CAMB 1.6.6 as the reference. The dot and label are found independently
for this comparison, so the peak can be at a different $k$ or $z$.

## Earlier diagnostics, kept for reference

### [03 — What happens to the differences at tighter precision](figures/03_residuals_after_precision_checks.png)

The left column shows the flat reference cosmology; the right column
shows the grid point with the largest native gap for the comparison in
that row. The redshift is chosen separately for each panel from its
native maximum. Each line is a signed CAMB2/older-version difference
versus scale. The three lines show what happens after matching the
recombination calibration and then increasing numerical precision.
The vertical scales can differ between panels.

### [04 — Runtime and numerical stability at the same target](figures/04_runtime_vs_numerical_deviation.png)

Each panel shows one of the four cases from the earlier precision test,
including the additional `low_cdm` diagnostic. For each version
and setting, the horizontal position is the median runtime and the
vertical position is the largest difference from that version’s own
tightest run. Short horizontal bars show the three-run timing range.
The dashed line is the benchmark’s 0.1% focus-range target. A point below
the line is not enough on its own: the two tightest runs must also agree
within the separate 0.02% reference check. The appendix records
which cases met both conditions. The additional
baseline-only sampling check is reported in a table rather than
plotted here.

[Detailed report](Report.md) · [Data appendix](Data%20appendix.md)
