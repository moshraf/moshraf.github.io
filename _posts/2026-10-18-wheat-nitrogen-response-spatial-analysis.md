---
layout: posts
title:  "Wheat Yield and Nitrogen Response: A Spatial Analysis"
date:   2026-10-18
tags: [gis]
author_profile: true
author: Moshraf Hossain
categories: work
highlight_home: true
tagline: "Exploring wheat yield and nitrogen treatments with ArcGIS Pro and Jupyter Notebook"
excerpt: "Spatial analysis of wheat yield and nitrogen treatments in ArcGIS Pro, using Moving Window Kriging, Local Bivariate Relationships and pairwise Z-tests on a supplied teaching dataset."
header:
  overlay_color: "#2c4a5e"
  teaser: /assets/images/wheat-nitrogen/fig2_interpolated_yield_kriging.png
description: "Spatial analysis of wheat yield and nitrogen treatments using ArcGIS Pro for mapping and Moving Window Kriging, and Jupyter Notebook for pairwise Z-tests. Guided university exercise using a supplied teaching dataset with fabricated locations."
---

**GIS Portfolio Project — ArcGIS Pro, Geostatistics and Spatial Statistics**
> **About this project:** a guided laboratory exercise for SPAT5008 Applied GIS at Curtin University, using a supplied teaching dataset with fabricated locations. It demonstrates GIS and statistical methods. It is not original agronomic research, and its findings should not be applied to a real paddock.

## 🎯 The Question

Does applying more nitrogen produce more wheat, and is the pattern the same everywhere in a paddock? A single paddock-wide average can hide a lot, so this exercise combines mapping, interpolation, statistical tests and local relationship analysis to look at both the overall pattern and how it varies across space.

---

## 🗂️ Data and Setup

- **Dataset:** a yield-monitor point dataset supplied for the unit (5,728 points).
- **Variables:** wheat yield (kg/ha) and nitrogen treatment rate.
- **Treatments:** four nitrogen rates (0, 60, 120 and 180 kg/ha) applied in a checkerboard-style design.
- **Coordinate system:** WGS 1984 UTM Zone 50S.
- **Locations:** fabricated for the teaching exercise, so no basemap is used.

---

## 🛠️ Method

1. **Visualised the experiment:** mapped yield in five graduated classes alongside the four nitrogen treatments.
2. **Interpolated yield:** fitted an Ordinary Kriging model, then used it as the source for Moving Window Kriging (100-point neighbourhood, 5 m output cells), which fits a separate model in each local neighbourhood instead of assuming one spatial relationship across the whole paddock.
3. **Explored the relationship:** created a scatter plot with a linear trend line and a boxplot of yield by nitrogen rate.
4. **Tested for differences:** calculated mean yield for each treatment, then ran pairwise Z-tests (α = 0.05, critical Z = ±1.96) in a Jupyter Notebook.
5. **Mapped local associations:** used the Local Bivariate Relationships tool to classify local associations between nitrogen rate and wheat yield.

---

## 📊 Key Results

| Nitrogen rate (kg/ha) | Points (n) | Mean yield (kg/ha) |
| --------------------- | ---------- | ------------------ |
| 0                     | 2,875      | 4,679.29           |
| 60                    | 1,054      | 4,782.16           |
| 120                   | 944        | 4,716.36           |
| 180                   | 855        | 4,716.57           |

- **Overall pattern:** median yields were broadly similar across the four rates, with substantial overlap between groups and no consistent increase as nitrogen rate increased. The linear trend was essentially flat (R² = 0.00018).
- **Pairwise Z-tests:** only the 0 versus 60 kg/ha comparison met the unadjusted α = 0.05 threshold (Z = −2.372, p = 0.018). It would not remain significant under a Bonferroni adjustment for six comparisons. The other five comparisons had p-values from 0.223 to 0.997.
- **Spatial variation:** yield formed coherent patches, with higher yields concentrated in the west of the paddock. The local relationship map showed all six relationship types (Positive Linear, Negative Linear, Concave, Convex, Undefined Complex and Not Significant). Local associations varied in shape and direction across the paddock.

---

## 🗺️ Maps and Charts

![Wheat yield and nitrogen treatment maps](/assets/images/wheat-nitrogen/fig1_yield_and_nitrogen_treatment.png)

*Figure 1. Wheat yield (left) and the checkerboard nitrogen treatment design (right) across the experimental paddock.*

![Interpolated wheat yield using Moving Window Kriging](/assets/images/wheat-nitrogen/fig2_interpolated_yield_kriging.png)

*Figure 2. Predicted wheat yield using Moving Window Kriging, with a 100-point neighbourhood and 5 m output cells.*

![Boxplot of wheat yield by nitrogen rate](/assets/images/wheat-nitrogen/fig4_yield_by_nitrogen_rate.png)

*Figure 3. Wheat yield distributions across four nitrogen treatments (0, 60, 120 and 180 kg/ha; n = 2,875, 1,054, 944 and 855 points, respectively). Median yields were broadly similar, with substantial overlap between groups and no consistent increase as nitrogen rate increased.*

![Local bivariate relationships between wheat yield and nitrogen rate](/assets/images/wheat-nitrogen/fig7_local_bivariate_relationships.png)

*Figure 4. Local Bivariate Relationships between wheat yield and nitrogen rate, showing six local relationship types across the paddock.*

All figures were produced during a guided laboratory exercise using a supplied teaching dataset with fabricated locations.

---

## ⚠️ Limitations

- **Teaching exercise:** the data are a supplied teaching dataset with fabricated locations, so the results describe this dataset, not a real paddock.
- **Multiple comparisons:** six pairwise tests were run at α = 0.05 with no correction. Against a Bonferroni threshold of about 0.008 (0.05 ÷ 6), the 0 versus 60 kg/ha result (p = 0.018) would not be significant. Treat it as suggestive, not conclusive.
- **Spatial dependence:** spatial dependence between nearby observations may affect the independence assumption behind the Z-tests. Its extent and effect were not assessed.
- **Unequal group sizes:** treatment groups range from 855 to 2,875 observations. Unequal sample sizes can affect the precision of treatment estimates; precision also depends on within-group variability and spatial dependence.
- **Linear trend:** nitrogen was applied at four fixed rates, so a straight line is a limited summary of the pattern.
- **Local associations:** the mapped relationship types describe local statistical associations, not recommended nitrogen rates. Some of the example neighbourhoods examined in the original report had low adjusted R² (for example 0.085 and 0.10).

---

## 🧰 Tools and Skills

| Category | Detail |
| -------- | ------ |
| GIS | ArcGIS Pro (kriging, Summary Statistics, Local Bivariate Relationships, layouts and cartography) |
| Statistics | Pairwise Z-tests in a Jupyter Notebook |
| Skills | Spatial interpolation and geostatistics, experimental design interpretation, hypothesis testing, spatial pattern analysis, cartography, and clear reporting of limitations |

---

## 📂 Project Resources

- **GitHub Repository:** [View the README and figures](https://github.com/moshraf/on-farm-nitrogen-response-spatial-analysis)
- The supplied dataset and notebook are not included.

**Data and attribution:** supplied teaching dataset (SPAT5008 Applied GIS, Curtin University), not redistributed here. © 2026 Moshraf Hossain. All rights reserved in my original text and cartographic contributions. Supplied teaching materials and any third-party content are excluded from this notice and remain subject to their respective terms.

---

## 📧 Let's Connect

- Portfolio: <https://moshraf.github.io/>
- GitHub: <https://github.com/moshraf>
- LinkedIn: <https://linkedin.com/in/moshrafhossain>
