::: {align="center"}
# Principal Component Analysis & K-Means Clustering in R

**Exploring dimensionality reduction through linear algebra, statistical analysis, and unsupervised learning.**


## Overview

This project explores **Principal Component Analysis (PCA)** as a method for identifying patterns and reducing the dimensionality of a multivariate dataset. PCA is implemented in two ways: **from first principles using matrix operations and eigendecomposition**, and using R's built-in `prcomp()` function. The results are compared, and **K-means clustering** is applied to the PCA-transformed data to visualize groupings.

The analysis emphasizes both the mathematics behind PCA and its practical application in exploratory data analysis.

## Highlights

- **93.38%** of total variance is explained by the first **three** principal components.
- Manual PCA closely matches the cumulative explained variance returned by `prcomp()`.
- K-means with **k = 3** is applied to the retained principal components.
- Visualizations include a PCA biplot, cumulative explained-variance plots, a method comparison, and a cluster scatter plot.

## Dataset

The supplied CSV contains a categorical `brand` field, an `id` field, and numeric measurements including `mois`, `prot`, `fat`, `ash`, `sodium`, `carb`, and `cal`.

For consistency with the original analysis, the manual and `prcomp()` approaches both use the numeric columns, **including `id`**, after excluding `brand`. Since `id` behaves like an identifier, a future improvement would be to exclude it from the PCA features and compare the results.

## Methodology

### 1. Data preparation

- Load the dataset into R.
- Select the numeric columns.
- Standardize each selected variable using `scale()` so variables with different scales are comparable.

### 2. PCA from first principles

1.  Compute the covariance matrix of the standardized data.
2.  Obtain eigenvalues and eigenvectors with `eigen()`.
3.  Sort the components in descending order of eigenvalue.
4.  Project the standardized observations onto the eigenvector basis.
5.  Calculate the variance explained by each component and its cumulative proportion.

### 3. Built-in PCA and comparison

- Run `prcomp(numeric_data, scale. = TRUE)`.
- Examine component importance and the PCA biplot.
- Compare cumulative explained variance from the manual implementation and `prcomp()`.

### 4. K-means clustering

- Retain the minimum number of components that together explain at least **90%** of variance.
- Run `kmeans()` with **three clusters** and a fixed random seed (`123`).
- Plot cluster assignments against the first two principal components.

> **Note:** The choice of three clusters is an analysis setting, not an independently validated optimal cluster count.

## Key results

| Principal components retained | Cumulative explained variance |
|:------------------------------|------------------------------:|
| PC1                           |                        52.16% |
| PC1–PC2                       |                        80.79% |
| PC1–PC3                       |                    **93.38%** |
| PC1–PC4                       |                        98.47% |

Three components therefore meet the 90% explained-variance target in this analysis. The manual and built-in PCA approaches produce matching cumulative explained-variance patterns, supporting the manual calculation. The cluster scatter plot shows distinct groupings in the PCA projection.

## Visualizations

The complete rendered plots are available in [**`pca_analysis_report.pdf`**](pca_analysis_report.pdf), including:

- **Cumulative explained variance:** how quickly the leading components capture overall variation.
- **PCA biplot:** the arrangement of observations and variable directions in the first two components.
- **Manual vs. built-in PCA:** an overlay of cumulative variance curves.
- **K-means cluster plot:** cluster assignments displayed on PC1 and PC2.

## Repository structure

``` text
principal-component-analysis-r/
├── README.md
├── pca_analysis.Rmd          # Analysis source and R code
├── pca_analysis_report.pdf   # Rendered report and plots
└── sample_dataset.csv        # Input dataset
```

## Run the analysis

**Requirements:** R, RStudio (recommended), and the R packages `readr`, `ggplot2`, `ggbiplot`, `devtools`, and `rmarkdown`. A LaTeX distribution may be needed to render the PDF.

1.  Clone the repository:

    ``` bash
    git clone https://github.com/YOUR-USERNAME/principal-component-analysis-r.git
    cd principal-component-analysis-r
    ```

2.  Install the required packages in R:

    ``` r
    install.packages(c("readr", "ggplot2", "devtools", "rmarkdown"))
    devtools::install_github("vqv/ggbiplot")
    ```

3.  Open `pca_analysis.Rmd` in RStudio and run its code chunks, or render it with:

    ``` r
    rmarkdown::render("pca_analysis.Rmd")
    ```

    The script expects the CSV file in the same directory. Its data-loading line should read:

    ``` r
    data <- read.csv("anonymous-data.csv")
    ```

## Skills demonstrated

`R` · `R Markdown` · `Linear Algebra` · `Covariance & Eigendecomposition` · `Principal Component Analysis` · `Feature Standardization` · `Dimensionality Reduction` · `Unsupervised Learning` · `K-Means Clustering` · `Data Visualization`

## Future improvements

- Exclude identifier variables from the PCA feature set and compare the component structure.
- Assess the number of clusters using silhouette scores or other clustering diagnostics.
- Explore how feature selection changes component loadings and cluster assignments.

------------------------------------------------------------------------

*Project by Mohammed Sharif · Statistical Analysis in R*
