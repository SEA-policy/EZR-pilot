# Code and source data

**Wang et al. (2026). The integrated environmental zoning-based regulation further enhances sustainable development in China.** *Nature Communications*. https://doi.org/10.1038/s41467-026-78846-6

This package provides the analysis code, processed datasets, rendered reports, and figure source data accompanying the article.

## Files

### Analysis code and reports

| File | Description |
| --- | --- |
| `Code_ECI_causal_forest.Rmd` | ECI causal-forest analysis, heterogeneity analysis, and robustness checks. |
| `Code_PM_causal_forest.Rmd` | PM2.5 causal-forest analysis, heterogeneity analysis, and robustness checks. |
| `Code_ECI_causal_forest.html` | Rendered ECI analysis report. |
| `Code_PM_causal_forest.html` | Rendered PM2.5 analysis report. |

### Input data

| File | Description |
| --- | --- |
| `cityOES_merged_2015_2020.xlsx` | Ordinary ecological space panel data for the ECI analysis, 2015–2020. |
| `citypm_merged_2015_2020.xlsx` | City-level PM2.5 panel data and covariates, 2015–2020. Also supplies city identifiers and COVID-related information to the ECI analysis. |

### Figure source data

| File | Description |
| --- | --- |
| `Source_Data_Figure_2.xlsx` | Population density and average zoning-unit area, panel e. |
| `Source_Data_Figure_3.xlsx` | Spatial profiles and changes in NDVI and nighttime light intensity. |
| `Source_Data_Figure_4.xlsx` | ECI treatment effects, group comparisons, variable importance, and province-level estimates. |
| `Source_Data_Figure_5.xlsx` | PM2.5 treatment effects, group comparisons, variable importance, partial-dependence estimates, and province-level estimates. |
| `Source_Data_Supplementary_Figure_1.xlsx` | Province-level policy instruments. |
| `Source_Data_Supplementary_Figure_2.xlsx` | Seasonal changes in NDVI and ECI. |
| `Source_Data_Supplementary_Figure_3.xlsx` | ECI changes in ecological conservation redlines and ordinary ecological spaces. |
| `Source_Data_Supplementary_Figure_4.xlsx` | Event-study estimates and pre-trend tests. |
| `Source_Data_Supplementary_Figure_5.xlsx` | Placebo and falsification tests. |
| `Source_Data_Supplementary_Figure_6.xlsx` | Bootstrap estimates and diagnostics. |
| `Source_Data_Supplementary_Figure_7.xlsx` | COVID-related sensitivity analyses. |

Worksheet names identify the corresponding figure panels. Column names appear in the first row; processing notes and inclusion flags are provided where applicable. Variable definitions and methods are described in the article and Supplementary Information.

## Running the analyses

Keep the files in one directory. Open the HTML reports directly in a browser to view the results, or run the R Markdown files to repeat the analyses. Both input workbooks are required for the ECI analysis; the PM2.5 analysis uses `citypm_merged_2015_2020.xlsx`.

The code uses R and the following packages:

```r
install.packages(c(
  "readxl", "dplyr", "tidyr", "fixest", "grf", "openxlsx",
  "lmtest", "sandwich", "car", "scales", "knitr", "rmarkdown", "remotes"
))
remotes::install_version("ggplot2", version = "3.5.2", upgrade = "never")
remotes::install_version("patchwork", version = "1.3.2", upgrade = "never")
remotes::install_version("gghalves", version = "0.1.4", upgrade = "never")
```

Set the working directory to the package folder and render the reports. Pandoc is required for HTML rendering and is included with RStudio.

```r
setwd("/path/to/package")
rmarkdown::render("Code_ECI_causal_forest.Rmd")
rmarkdown::render("Code_PM_causal_forest.Rmd")
```

The main analyses use 2017–2020 data; extended-period analyses use 2015–2020. Default settings include seed 42, 8,000 trees for the main causal forests, and 1,000 placebo and bootstrap repetitions.

In addition to the HTML reports, the scripts generate diagnostic plots and two result workbooks:

- `ECI_calendar_year_main_robustness_results.xlsx`
- `PM_calendar_year_main_robustness_results.xlsx`
