# Business Development Company Pricing and Returns

This repository supports our finance final paper on business development companies (BDCs), their pricing, and their returns.

Our literature review and written paper are in [BDC_Literature_Review.pdf](BDC_Literature_Review.pdf).

## Research Question

We study how BDC market returns relate to NAV while accounting for the fact that NAV is stale and updated only quarterly. Rather than treating NAV as contemporaneous, we use lagged NAV returns as the last observable fundamental signal available to investors at time `t`.

The main question is:

Does NAV's explanatory power decline when macro conditions shift investors toward discounting and risk premia instead of stale fundamentals?

We make this relationship state-dependent by interacting lagged NAV returns with:

- changes in the 10-year Treasury yield as a discount-rate channel
- changes in credit spreads as a risk-premia channel

## Model

We estimate the following monthly return specification:

```text
Market return(i,t)
= α
+ β1 * Lagged NAV return(i,t-1)
+ β2 * Change in 10-year Treasury yield(t)
+ β3 * Change in credit spread(t)
+ β4 * [Lagged NAV return(i,t-1) x Change in 10-year Treasury yield(t)]
+ β5 * [Lagged NAV return(i,t-1) x Change in credit spread(t)]
+ error(i,t)
```

### Variable Definitions

- `Market return (R^{MKT}_{i,t})`: monthly BDC market return
- `Lagged NAV return (R^{NAV}_{i,t-1})`: last available NAV-based return observed by investors at time `t`
- `Change in 10-year Treasury yield (ΔDGS10_t)`: proxy for discount-rate shocks
- `Change in credit spread (ΔSpread_t)`: Baa corporate yield minus 10-year Treasury yield, used as a proxy for credit-risk shocks
- `Error term (ε_{i,t})`: unexplained component of market returns

### Coefficient Interpretation

- `β1`: baseline relationship between lagged NAV returns and market returns
- `β2`: direct effect of changes in the 10-year Treasury yield on market returns
- `β3`: direct effect of changes in credit spreads on market returns
- `β4`: how the sensitivity of market returns to lagged NAV changes when Treasury yields move
- `β5`: how the sensitivity of market returns to lagged NAV changes when credit spreads move

The interaction terms are the key coefficients because they test whether lagged NAV matters less when valuation is driven more by discount-rate changes and credit risk premia than by stale fundamentals.

The implied effect of lagged NAV on market returns is:

```text
Effect of lagged NAV on market returns
= baseline NAV effect
+ (NAV x change in 10-year Treasury yield effect)
+ (NAV x change in credit spread effect)
```

```text
NAV effect_t = β1 + β4 * ΔDGS10_t + β5 * ΔSpread_t
```

If Treasury yields or credit spreads move sharply, investors may place less weight on the last reported NAV and more weight on current discounting conditions and required risk compensation.

## Repository Contents

- `BDC Sensitivity.ipynb`: main analysis notebook for NAV, returns, rates, and spread sensitivity
- `nav-edgar.ipynb`: NAV collection and processing work
- `data/`: intermediate datasets used in the analysis
- `BDC_Literature_Review.pdf`: paper and literature review draft
