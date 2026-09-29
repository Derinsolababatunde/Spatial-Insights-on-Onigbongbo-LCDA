# Spatial Market Intelligence Analysis

## Project Overview

This project uses spatial and market data to examine indicative land price levels across five wards in Lagos State: **G R A, Opebi, Onigbongbo, Oregun, and Wasimi**.

The analysis combines ward boundary data with current land price information collected from property listings. The aim is to identify differences in observed market levels and visualize how these prices vary spatially.

This analysis provides an **indicative market signal**, not a formal property valuation.

---

## Problem

Property prices can vary significantly between locations, even within the same general area. The objective of this analysis was to use available property-market data and spatial information to investigate differences in land prices across selected wards.

The main questions were:

* What are the observed land prices across the selected wards?
* How can these observations be summarized into an indicative market level?
* Are there unusual values that may influence the results?
* What spatial or local factors could potentially explain the differences?
* What limitations should be considered when interpreting the results?

---

## Data

Two main datasets were used.

### 1. Ward Spatial Data

A GeoJSON file containing the boundaries of five wards:

* G R A
* Opebi
* Onigbongbo
* Oregun
* Wasimi

The spatial data uses **EPSG:4326 (WGS 84)** and contains five ward features. The ward name was obtained from the `wardname` field.

### 2. Property Market Data

A CSV dataset containing one market observation for each ward.

Important fields include:

* `Town`
* `Current Land Price/sqm`
* `Supporting Source`
* `Date Searched`

Additional fields were created during the analysis, including:

* `Price_sqm`
* `n`
* `Indicative`
* `Mean`
* `Indicative Market Level`

---

## Analysis Method

The analysis was carried out using Python in Google Colab.

The main workflow was:

1. Load the ward GeoJSON using GeoPandas.
2. Standardize ward names to ensure they could be matched with the market data.
3. Load the market CSV using Pandas.
4. Clean the land-price values and convert them into numeric values.
5. Check for missing ward names and prices.
6. Compare the ward names in both datasets.
7. Match the market observations to the five spatial wards.
8. Calculate ward-level market indicators.
9. Produce charts and spatial maps showing the observed market levels.

All five wards were successfully matched between the spatial and market datasets.

---

## How the Indicative Market Level Was Produced

The **Indicative Market Level** was calculated from the available usable land-price observations for each ward.

The median price was used as the main indicative measure because the median can be less affected by extreme values than the mean when multiple observations are available.

However, an important limitation exists in this dataset:

**There is only one observation for each ward (`n = 1`).**

Therefore, the median, mean, and observed price are identical for each ward. The Indicative Market Level should consequently be interpreted as the **observed price from the available listing**, rather than a statistically robust estimate of the entire ward's market.

### Indicative Market Levels

| Ward       | Observations | Indicative Market Level |
| ---------- | -----------: | ----------------------: |
| G R A      |            1 |          ₦3,500,000/sqm |
| Opebi      |            1 |          ₦2,000,000/sqm |
| Onigbongbo |            1 |          ₦1,550,000/sqm |
| Oregun     |            1 |          ₦1,200,000/sqm |
| Wasimi     |            1 |            ₦260,000/sqm |

The observed prices range from **₦260,000/sqm to ₦3,500,000/sqm**.

The overall mean of the five observations is approximately **₦1,702,000/sqm**, while the median is **₦1,550,000/sqm**.

Because there is only one observation per ward, a reliable current market range was not produced.

---

## Results and Observations

The analysis shows substantial differences between the observed land prices.

G R A has the highest observed price at **₦3,500,000/sqm**, followed by Opebi at **₦2,000,000/sqm**, Onigbongbo at **₦1,550,000/sqm**, Oregun at **₦1,200,000/sqm**, and Wasimi at **₦260,000/sqm**.

The difference between the highest and lowest observations is **₦3,240,000/sqm**.

However, these differences should not be interpreted as definitive differences in the actual market value of all land within each ward because each ward is represented by only one listing.

---

## Are There Unusual Values That Affect the Result?

**Wasimi is the clear outlier in the dataset.**

Its observed price of **₦260,000/sqm** is substantially lower than the other four observations.

There are also important differences in the supporting sources:

* Wasimi is supported by a **single listing for a mixed-use plot in Peace Estate**, rather than a broader market page.
* Onigbongbo is supported by a general **"Property in Onigbongbo"** page rather than a land-specific listing.
* G R A and Oregun cite listing pages containing many plots, with **72+ and 11+ plots respectively**, but only one price was recorded from each source.

Because **n = 1 for every ward**, one unusually cheap or expensive listing effectively determines the entire indicative level for that ward.

This is particularly important when interpreting Wasimi's very low value.

---

## What Spatial or Local Factors Might Explain the Differences?

The following are **hypotheses that would need further data to test**, rather than conclusions from the current dataset.

### Location and Prestige

G R A is a long-established residential area, while Opebi is located along an important commercial corridor. These characteristics could potentially contribute to higher land prices.

### Neighbouring Locations

Wasimi shares boundaries with Onigbongbo and Opebi, yet its observed price is considerably lower than both.

This shows that proximity alone does not explain the observed price differences.

### Plot Type and Estate Context

Different types of land may have different prices. For example, estate plots, mixed-use plots, and undeveloped/raw land may not be directly comparable.

The Wasimi observation is particularly important because it relates to a mixed-use plot in Peace Estate.

### Accessibility and Infrastructure

Factors such as:

* distance to major roads
* accessibility
* drainage
* flood exposure
* infrastructure
* land title and documentation

could influence land prices.

However, these variables were not included in the current dataset, so their effects cannot be measured here.

### Ward Size and Land Use

The wards differ in their size, shape, and land-use characteristics. Therefore, a single property listing may represent only a small part of a ward and may not reflect the conditions across the entire ward.

---

## Any Surprises?

The main surprise is how low the Wasimi observation is compared with its neighbouring areas.

Wasimi is located next to Onigbongbo and Opebi, yet the recorded price is far below both.

This contrast is an important spatial question to investigate further. A logical next step would be to collect more Wasimi listings and examine whether the low price is associated with particular plot types, estates, accessibility, documentation, or other local characteristics.

The numbers differ, but with one observation per town they cannot yet tell us **why**.

The honest conclusion is that the gaps are real in this sample and need more data to explain.

---

## Limitations

The main limitation of this analysis is the **very small sample size**.

There is only one market observation for each of the five wards. This means:

* The results cannot represent the full land market within each ward.
* One unusually high or low listing can determine the entire ward's indicative level.
* The calculated median is not statistically meaningful as a market distribution because `n = 1`.
* The observations may represent different types of properties and therefore may not be perfectly comparable.
* Asking prices from online listings may differ from actual transaction prices.
* Some supporting sources are general property pages rather than directly comparable land listings.
* Important property characteristics such as plot size, land use, title, accessibility, infrastructure, and flood exposure were not available for all observations.
* The spatial analysis identifies location differences but does not establish causation.

For these reasons, the Indicative Market Level should be treated as a **descriptive spatial market signal**, rather than a formal valuation.

---

## Outputs

The analysis produces the following outputs:

* `sprint3_outputs/market_intelligence.csv`
* `sprint3_outputs/market_intelligence.json`
* `sprint3_outputs/market_levels_bar.png`
* `sprint3_outputs/towns_orientation_map.png`
* `sprint3_outputs/towns_orientation_map.html`
* `sprint3_outputs/towns_market_map.png`

These outputs provide both tabular and visual representations of the observed market information.

---

## Tools and Technologies

* Python
* Google Colab
* Pandas
* GeoPandas
* Matplotlib
* Folium
* MapClassify
* Branca

---

## Conclusion

This analysis demonstrates how spatial data and property-market observations can be combined to investigate differences in indicative land prices across selected Lagos wards.

The results show substantial differences in the observed prices, particularly the contrast between Wasimi and the other wards. However, the analysis also demonstrates why **data quantity and comparability are important in spatial market analysis**.

The next stage should involve collecting more comparable listings for each ward, with particular attention to Wasimi, and incorporating additional spatial and property variables.

This would make it possible to move from a simple observed-price comparison toward a more reliable understanding of the factors influencing land prices across the study area.
