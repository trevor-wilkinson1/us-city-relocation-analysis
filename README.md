# U.S. City Relocation Analysis for Entry-Level Data Analysts

An end-to-end data project identifying the highest-value U.S. cities for entry-level data analysts, built to answer a question most people in the field actually have when they are starting out: where should I go?

**[View the Live Tableau Dashboard](https://public.tableau.com/app/profile/trevor.wilkinson/viz/HighestValueCities-ELDataAnalysts/ELDataAnalystSalaryvs_Rent)**

<br>

## Overview

Most city comparison tools focus on one variable at a time, which makes them useful for a single lens but not much else. This project builds a composite scoring model that weighs salary, cost of living, crime, and demographics together, then visualizes the results in a way that lets you actually explore the tradeoffs rather than just look at a ranked list.

The final dashboard lets users navigate from a national view down to state, city, climate, and demographic detail, with tiered scoring at each level so the rankings are always in context.

<br>

## Data Sources

Raw data was pulled from three public sources and merged at the city level. The U.S. Census Bureau provided population, median age, and demographic breakdowns. OpenCrime supplied crime rate data by city. Salary.com covered entry-level data analyst compensation by market.

The starting dataset came in at over 32,000 rows. After cleaning, deduplication, and ensuring consistent city-level matching across all three sources, 200 cities made the final cut.

<br>

## Methodology

**Data cleaning and merging**

The three datasets did not share a common key out of the box. City names were inconsistently formatted across sources, some used county-level identifiers, and a handful of entries had obvious data quality issues. Python and pandas handled the bulk of the joining and normalization logic, with Excel used for manual verification passes and advanced functions including XLOOKUP, nested IFs, and pivot validation on the merged output.

**Feature engineering**

Once the data was clean and unified, features were engineered across four dimensions: salary percentiles relative to the national entry-level range, monthly rent as a percentage of median analyst take-home, violent and property crime rates normalized per 100,000 residents, and median age as a proxy for city demographic and lifestyle profile.

Each dimension was weighted and combined into a composite score, with cities bucketed into tiers rather than a single ranked list. The difference between rank 12 and rank 15 is rarely meaningful. The difference between tiers is.

**Tableau dashboard**

The dashboard uses calculated fields to display composite scores dynamically, with filter actions that let users drill from state to city to full demographic and climate detail. The tiered scoring system is built into the calculated fields rather than hardcoded, so the logic is transparent and adjustable.

<br>

## Key Findings

Salary alone is a poor predictor of analyst value by city. Several high-paying markets are effectively neutralized by rent and cost of living, while a number of mid-tier salary markets rank significantly higher once the full picture is accounted for. The dashboard makes this tradeoff visible at a glance.

<br>

## Tools

| Layer | Tools |
|---|---|
| Data collection | U.S. Census Bureau, OpenCrime, Salary.com |
| Cleaning and merging | Python (pandas), Excel |
| Feature engineering | Python (pandas), Excel |
| Visualization | Tableau Public |

<br>

## What I Would Build Next

The scoring model currently weights all four dimensions equally. A natural next step would be letting users adjust the weights themselves in the dashboard, so someone prioritizing low cost of living over salary growth gets a different ranked output than someone optimizing purely for earnings. Building that interactivity into Tableau with parameter actions is on the list.

The other big addition would be a career filter. Right now the salary data is scoped to entry-level data analysts specifically, but the underlying framework works for any role. Letting users swap between careers and watching the entire scoring model adjust accordingly would make the tool genuinely useful beyond one job title.

Adding more current salary data through a scraped or API-based source would also improve accuracy, since Salary.com figures can lag the actual market by a year or more in fast-moving cities.
