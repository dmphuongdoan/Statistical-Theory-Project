# Statistical Theory Project For Final Exam 
# Project 2.1 — Gaussian CI: Comparison of Level and Observed Coverage

**By:** Doan Duy My Phuong

**Instructor:** Prof. Samantha Leorato

> Simulation study of the confidence interval for the mean μ of a
> Gaussian population, comparing σ² known vs. σ² unknown.

## Table of contents

- [Assignment](#assignment)
- [Repository structure](#repository-structure)
- [What the report covers](#what-the-report-covers)
- [Key results](#key-results)
- [Requirements](#requirements)
- [How to run](#how-to-run)
- [References](#references)

## Assignment

From the course project list, section **2.1 "Comparison of level and
observed coverage"**:

> After choosing one of the distributions below, compute the observed
> coverage probability and compare with the chosen α by the following
> steps:
>
> 1. Generate `M = 10000` random samples of size `n` from the same
>    distribution `f(x | θ)`
> 2. Compute the corresponding `M` confidence intervals and the
>    proportion of intervals that include the parameter
> 3. Possibly allow for: different sample size, different parameter(s)
>    values
>
> **Gaussian CI for μ.** Make the steps above with `θ = μ` and
> `f(x | μ, σ) ~ N(μ, σ²)`. Consider both the cases `σ²` known and not
> known.

## Repository structure

```
.
├── README.md                      # this file
├── gaussian_CI_full_project.Rmd   # main deliverable: report + code
└── presentation_script_2.1.md     # ~10-min spoken presentation script
```

## What the report covers

| # | Section | Content |
|---|---|---|
| 1 | Goal | Why observed coverage is worth checking by simulation |
| 2 | Theoretical CIs | Z-based and t-based formulas, incl. S² |
| 3 | Theory: "exact CI" | Why coverage is exact at *every* n, not just asymptotically |
| 4 | Simulation function | `simulate_coverage()`, M = 10,000 by default |
| 5 | Varying n | Fixed μ = 5, σ = 2; n ∈ {3, 5, 10, 20, 30, 50, 100} |
| 5b | Varying μ, σ | Fixed n = 20; several (μ, σ) combinations |
| 6 | Discussion | Coverage vs. width trade-off |

### Theory in brief

Both intervals are shown to be **exact** — coverage equals the nominal
level 1-α at every sample size, not only in the large-n limit:

```math
Z = \frac{\bar X - \mu}{\sigma/\sqrt{n}} \sim N(0,1) \quad \text{exactly, for every } n
```

```math
T = \frac{\bar X - \mu}{S/\sqrt{n}} \sim t_{n-1} \quad \text{exactly, for every } n \ge 2
```

This follows from Theorem 5.3.1 in Casella & Berger, built on Cochran's
theorem (1934) and Gosset's original derivation of the t-distribution
(1908) — see [References](#references).

## Key results

- Observed coverage stays close to **0.95** for every sample size tested,
  including `n = 3` — confirming both CIs are exact, not asymptotic.
- Observed coverage also stays close to 0.95 across different true `μ`
  and `σ` — confirming `Z` and `T` are pivotal quantities.
- The unknown-`σ` (t-based) interval is noticeably **wider** than the
  known-`σ` (Z-based) interval at small `n` (e.g. nearly 2x wider at
  `n = 3`); the gap shrinks as `n` grows.

## Requirements

- R (>= 4.0 recommended)
- R packages: `knitr` (bundled with RStudio), `shiny`

```r
install.packages("shiny")
```

## How to run

The file uses `runtime: shiny` in its YAML header, so open it in
**RStudio** and click **Run Document** (not *Knit*) to render the full
report — theory, code, tables, and plots — as a single scrollable page.

`set.seed(2024)` is used throughout for reproducibility.

## References

- Casella, G. and Berger, R. L. (2002). *Statistical Inference* (2nd
  ed.), Duxbury. Theorem 5.3.1.
- Cochran, W. G. (1934). "The distribution of quadratic forms in a
  normal system, with applications to the analysis of covariance."
  *Mathematical Proceedings of the Cambridge Philosophical Society*,
  30(2), 178-191.
- Student [Gosset, W. S.] (1908). "The probable error of a mean."
  *Biometrika*, 6(1), 1-25.
