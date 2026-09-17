# Causal Inference Methods: Three Research Designs, One Underlying Question

**"Is X correlated with Y" is easy. "Does X *cause* Y" is hard.** This repo walks through three
classic research designs economists use to answer causal questions with observational or
quasi-experimental data, each applied to a real, well-known dataset and reworked from coursework
originally done in Stata into Python (pandas, statsmodels).

The goal isn't just "I can run a regression." It's showing *which* design fits *which* kind of
data-generating process, and why getting that choice wrong quietly produces biased estimates.

## The three modules

### 1. [RCT vs. Selection Bias](01_rct_vs_selection_bias/notebook.ipynb)
**Data:** A GOTV (get-out-the-vote) phone call experiment in Iowa.
**Point:** The same dataset, analyzed two ways — once using true random assignment, once using
whether someone actually answered the phone (a choice, not a coin flip). The random-assignment
estimate barely moves as controls are added (~1.2pp, stable). The non-random estimate starts at
~11pp and gets cut roughly in half once you control for who tends to pick up the phone. This is
the cleanest possible illustration of why randomization matters — and what happens when you don't
have it.

### 2. [Regression Discontinuity](02_regression_discontinuity/notebook.ipynb)
**Data:** NHIS survey data on drinking behavior around the age-21 legal drinking cutoff.
**Point:** Nobody can manipulate their birthdate, so comparing people a few days below vs. above
age 21 isolates the effect of *legal access* to alcohol from the effect of simply aging. Finds a
sharp, robust 8-9 percentage point jump in reported drinking right at the cutoff, consistent
across linear/quadratic/cubic specifications, with no corresponding jump in unrelated
demographic characteristics (a key validity check).

### 3. [Difference-in-Differences](03_difference_in_differences/notebook.ipynb)
**Data:** The classic Card & Krueger (1994) minimum wage study — NJ raised its minimum wage in
1992, PA didn't.
**Point:** Comparing the *change* in outcomes in NJ to the *change* in PA over the same period.
Finds that the policy raised NJ wages by about $0.48/hour relative to PA, with no statistically
detectable drop in employment, hours, or evidence of offsetting benefit cuts — the famous result
that contradicted the standard textbook prediction at the time.

## Why these three together

Each design solves the same underlying problem, "how do I know X caused Y and not just that X
and Y happen to move together", using a different source of as-good-as-random variation:

| Design | Source of "randomness" | What breaks it |
|---|---|---|
| RCT | Explicit random assignment | Nothing, if implemented correctly (the gold standard) |
| Regression Discontinuity | A sharp, unmanipulable cutoff | Sorting around the cutoff |
| Difference-in-Differences | Policy timing + a comparison group | Non-parallel pre-trends |

Module 1 also directly demonstrates the failure mode: what a naive, non-random comparison looks
like next to the real thing, using the exact same data.

## Tools

Python, pandas, statsmodels, matplotlib, scipy. Original coursework was completed in Stata;
this repo is an independent rebuild using the tools more common in industry data roles.

## Data sources

- Voter mobilization: sample from a large-scale Iowa/Michigan GOTV field experiment
- Drinking age: National Health Interview Survey (NHIS) Sample Adult Files
- Minimum wage: Card & Krueger (1994) New Jersey/Pennsylvania fast-food restaurant survey
