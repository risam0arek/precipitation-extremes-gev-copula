# Extreme Precipitation Analysis — Netherlands

**Master's thesis practical chapter** | Extreme Value Theory & Copula Dependence

This repository contains a fully reproducible analysis of daily precipitation extremes
at five long-record meteorological stations in the Netherlands, structured as a Quarto
document. It demonstrates methods directly applicable to **natural catastrophe (nat cat)
modelling** in the insurance and reinsurance industry.

## What's in the analysis

| Section | Methods |
|---------|---------|
| Data cleaning & EDA | NCEI GHCND data, block maxima extraction |
| Assumption testing | ACF plots, LOESS trend, stationarity assessment |
| Marginal GEV fitting | MLE, 95% CI, diagnostic plots, return level plots |
| Dependence analysis | Kendall's τ, Spearman's ρ (3 conditioning scenarios), tail dependence |
| Copula selection | Gumbel, Galambos, Hüsler–Reiss, t-EV, Tawn — AIC selection via MPL |
| Bivariate risk metrics | Joint exceedance probabilities, joint return periods |
| 5D copula | Gumbel, simultaneous 5-station exceedance |

## Project objective

This project demonstrates how extreme value theory and copula-based dependence modelling can be used to extend pointwise precipitation observations into a multivariate catastrophe risk framework.

The workflow bridges classical statistical modelling and insurance applications by transforming meteorological data into inputs for aggregate loss estimation in catastrophe models.

## Key finding

Although all station pairs exhibit relatively weak dependence (Spearman’s ρ ∈ [0.11, 0.24]), copula-based modelling indicates that the probability of simultaneous exceedance of 80 mm can be substantially higher than under an independence assumption (by factors ranging from 14× to 98× across pairs).

In the five-dimensional case, dependence modelling further amplifies joint exceedance probabilities, illustrating the strong sensitivity of aggregate risk estimates to the assumed dependence structure.

These results highlight that independence assumptions may materially understate aggregate risk in portfolio-level excess-of-loss pricing.

## Relevance to nat cat modelling

The analysis corresponds to the hazard component of a catastrophe model, which is responsible for generating stochastic event severity and spatial dependence structure.

In an insurance context, this translates into:

- GEV-based return levels used as event severity inputs

- Extreme value copulas capturing spatial dependence across exposure locations

- Joint exceedance probabilities informing portfolio-level risk metrics such as AAL, VaR, and TVaR

Natural extensions discussed in the document: vine copulas, hierarchical Archimedean
copulas, copula averaging, and spatial Bayesian hierarchical models for full
return-level mapping.

Key modelling assumptions and limitations

- Stationarity of annual maxima is assumed for GEV modelling, although some stations exhibit mild temporal trends

- Dependence is modelled using pairwise and simplified multivariate copulas, which may not fully capture high-dimensional structure

- The 5D Gumbel copula imposes a single dependence parameter and is therefore a simplification of the true spatial dependence structure

These assumptions are standard in practical catastrophe modelling but should be considered when interpreting tail risk estimates

## Reproducing the analysis

**Requirements:** R ≥ 4.3, Quarto ≥ 1.4

```r
install.packages(c(
  "dplyr", "ggplot2", "maps", "geosphere", "tidyr", "lubridate",
  "extRemes", "gridExtra", "copula", "ggrepel", "evd",
  "GGally", "reshape2", "stringr", "knitr", "kableExtra", "purrr"
))
```

Place `4257416.csv` (downloaded from [NCEI GHCND](https://www.ncei.noaa.gov/products/land-based-station/global-historical-climatology-network-daily))
in the same directory as the `.qmd` file, then:

```bash
quarto render extreme_precipitation_netherlands.qmd
```

## Data

Daily precipitation totals for five Dutch stations (Groningen, Roermond, Den Helder,
Hoofddorp, Putten) downloaded from NOAA NCEI GHCND. Years 2021 and 2024 excluded
due to excessive missing values. Analysis spans approximately 1900–2020 depending
on station.

## Stations

| Station |
|---------|
| Groningen | 
| Roermond | 
| Den Helder |
| Hoofddorp |
| Putten |

## Potential extensions
- Vine copula models for flexible high-dimensional dependence structures

- Spatial GEV models with covariates (elevation, distance to coast)

- Bayesian hierarchical models for joint estimation of marginal and dependence structure

- Stochastic event set generation for full catastrophe model integration
