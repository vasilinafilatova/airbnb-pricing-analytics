# Airbnb Pricing Analytics — New York City

Exploratory data analysis and regression modelling of Airbnb rental prices in New York City using R.

## Project Overview

This project investigates the main factors influencing Airbnb nightly rental prices across New York City.

Using a dataset of 48,895 listings, the analysis combines exploratory data analysis, statistical modelling, visualization and regression diagnostics to determine how property type, location and host activity influence pricing.

The objective was not only to explain price variation, but also to translate statistical findings into practical pricing insights for Airbnb hosts and platform decision-makers.

## Business Problem

Airbnb hosts have significant flexibility when determining nightly rental prices.

Without a data-driven pricing strategy, listings may be:

- overpriced, reducing occupancy
- underpriced, reducing potential revenue
- incorrectly positioned relative to comparable listings

This project addresses the following business questions:

1. Which factors explain the greatest variation in Airbnb prices?
2. How strongly does room type influence nightly price?
3. How important is location compared with property characteristics?
4. Do reviews, availability and host activity provide additional pricing information?
5. How can these findings support more effective pricing decisions?

## Dataset

The analysis uses the New York City Airbnb 2019 dataset.

- **48,895 listings**
- **16 variables**
- Five NYC boroughs:
  - Manhattan
  - Brooklyn
  - Queens
  - Bronx
  - Staten Island

### Key Variables

- `price`
- `room_type`
- `neighbourhood_group`
- `neighbourhood`
- `number_of_reviews`
- `reviews_per_month`
- `calculated_host_listings_count`
- `availability_365`
- `minimum_nights`
- `latitude`
- `longitude`

## Tools & Technologies

- R
- R Markdown
- tidyverse
- ggplot2
- dplyr
- broom
- MASS
- car
- lmtest
- sandwich
- Multiple Linear Regression
- Exploratory Data Analysis
- Statistical Analysis
- Regression Diagnostics

## Analysis Workflow

### 1. Data Cleaning

The dataset was prepared by:

- removing non-positive prices
- filtering unrealistic minimum-night values
- handling missing `reviews_per_month`
- removing selected missing observations
- converting categorical variables into factors
- limiting extreme price outliers
- transforming price using `log(price)` to address right-skewness

## 2. Exploratory Data Analysis

The EDA investigated:

- price distribution
- price differences by borough
- price differences by room type
- geographic distribution of listings
- relationship between price and reviews
- listing availability
- host activity
- correlations between numerical variables

## Key EDA Findings

### Price Distribution

Airbnb prices are strongly right-skewed.

Most listings are priced below **$200 per night**, while a relatively small group of luxury listings creates a long upper tail.

This motivated the use of `log(price)` in the regression models.

### Room Type

Room type emerged as one of the strongest pricing signals.

- Entire homes/apartments have the highest prices
- Private rooms occupy the middle price range
- Shared rooms are the least expensive

### Location

Location also plays an important role.

Manhattan and Brooklyn show the highest price levels, while Queens, the Bronx and Staten Island are generally more affordable.

### Reviews & Host Activity

Numerical correlations with price were relatively weak.

This indicated that Airbnb pricing cannot be explained effectively by a single numerical variable and supported the use of multivariate regression.

## 3. Regression Modelling

Five regression specifications were developed incrementally.

| Model | Main Predictors | R² |
|---|---|---:|
| Model 1 | Room Type | 0.420 |
| Model 2 | + Borough | 0.491 |
| Model 3 | + Minimum Nights | 0.493 |
| Model 4 | + Availability | 0.508 |
| **Model 5** | **+ Reviews & Reviews per Month** | **0.510** |

Adding location and operational variables progressively improved the explanatory power of the models.

## Final Model

The final model achieved:

**R² = 0.5103**

meaning that approximately **51% of the variation in Airbnb log prices** was explained by the selected property, location and activity variables.

### Key Results

Compared with entire homes/apartments:

- Private rooms were approximately **54% cheaper**
- Shared rooms were approximately **69% cheaper**

Location premiums were also substantial.

Compared with the Bronx:

- Manhattan listings were approximately **75% more expensive**
- Brooklyn listings were approximately **28% more expensive**
- Queens listings were approximately **13% more expensive**

Operational variables had smaller but statistically significant effects.

## Model Diagnostics

The final model was evaluated using:

- residual analysis
- residual distribution
- Q-Q plots
- multicollinearity diagnostics
- Variance Inflation Factors (VIF)

The diagnostic analysis suggested low multicollinearity between the selected predictors.

## Key Business Insights

### 1. Room Type Is the Primary Pricing Driver

Property format has the largest practical influence on Airbnb prices.

Hosts should therefore benchmark pricing primarily against listings with the same room type rather than comparing against the entire local Airbnb market.

### 2. Location Creates a Strong Price Premium

Manhattan commands the strongest geographic premium.

Pricing strategies should therefore be calibrated at borough and neighbourhood level.

### 3. Operational Metrics Fine-Tune Price

Availability, minimum-night requirements and review activity affect price, but their influence is considerably smaller than property type and location.

These variables are better viewed as pricing adjustments rather than primary pricing determinants.

## Business Recommendations

### Pricing Benchmarking

Hosts should benchmark listings against:

1. the same room type
2. the same borough or neighbourhood
3. comparable availability and booking conditions

### Dynamic Pricing

Airbnb pricing systems could use room type and location as core pricing features and use host activity variables as secondary adjustments.

### Market Positioning

Hosts operating entire homes or apartments in high-demand areas such as Manhattan can justify significant price premiums compared with shared or private accommodation.

## Business Value

This project demonstrates how statistical analysis can support:

- pricing optimization
- revenue management
- market positioning
- competitive benchmarking
- host decision-making
- automated pricing systems

It also demonstrates how analytical results can be translated from statistical model outputs into practical business recommendations.

## Limitations

The project has several limitations:

- The dataset represents a 2019 snapshot.
- Detailed property amenities are not included.
- Pricing behaviour may have changed since the dataset was collected.
- External factors such as events, seasonality and macroeconomic conditions are not directly modelled.
- Regression explains association and should not automatically be interpreted as causal impact.

## Repository Structure

```text
airbnb-pricing-analytics/
│
├── README.md
│
├── analysis/
│   └── airbnb_pricing_analysis.Rmd
│
├── data/
│   └── AB_NYC_2019.csv
│
├── report/
│   └── Airbnb_Pricing_Analytics_Report.pdf
│
└── images/
    ├── price_distribution.png
    ├── price_by_room_type.png
    ├── price_by_borough.png
    └── geographic_distribution.png