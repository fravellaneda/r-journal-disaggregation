# Spatial Disaggregation Modeling with R-INLA for Air Pollution Applications

Code and data for the article *Spatial Disaggregation Modeling with R-INLA for Air Pollution Applications*, by Fernando Rodriguez Avellaneda and Paula Moraga (King Abdullah University of Science and Technology, KAUST), submitted to The R Journal.

The article shows how to fit a spatial disaggregation model with the SPDE approach in `INLA`. As an example, we disaggregate the mean PM2.5 concentration over Portugal in January 2019 from the CAMS reanalysis grid (0.1°, about 10 km) to a finer grid (0.02°, about 2 km), using elevation as a covariate.

## Files

| File | Description |
|---|---|
| `my-rjournal-paper.Rmd` | Source of the article |
| `my-rjournal-paper.R` | R code of the article, extracted from the Rmd |
| `my-rjournal-paper.pdf`, `my-rjournal-paper.html` | Rendered article |
| `my-rjournal-paper.tex` | LaTeX file generated when rendering |
| `styles.css` | Style for the HTML version |
| `data/pm2p5_portugal.csv` | Mean PM2.5 (μg/m³) on the CAMS grid over Portugal, January 2019 |
| `data/eurodemc.tif` | EuroDEM elevation (m), cropped to the study region and aggregated |

## Data

- **PM2.5:** CAMS European air quality reanalysis, from the [Atmosphere Data Store](https://ads.atmosphere.copernicus.eu/datasets/cams-europe-air-quality-reanalyses). The file in `data/` contains the monthly mean of the hourly values.
- **Elevation:** [EuroDEM](https://www.mapsforeurope.org/datasets/euro-dem), from EuroGeographics. The file in `data/` was cropped to the study region and aggregated.

The article includes the code used to build both files from the original downloads. These steps are not run by default (`eval=FALSE`), because the original files are large.

## Requirements

`INLA` is installed from its own repository, not from CRAN:

```r
install.packages(
  "INLA",
  repos = c(getOption("repos"), INLA = "https://inla.r-inla-download.org/R/stable"),
  dependencies = TRUE
)
```

The other packages are on CRAN:

```r
install.packages(c("fmesher", "terra", "sf", "exactextractr", "rnaturalearth",
                   "ggplot2", "patchwork", "viridis", "tidyterra", "kableExtra"))
```

The results in the article were obtained with R 4.6.0, `INLA` 26.8.7, `fmesher` 0.8.0, `terra` 1.9.34, `sf` 1.1.1, `exactextractr` 0.10.1 and `ggplot2` 4.0.3.

## Running the code

From the repository folder, run:

```r
source("my-rjournal-paper.R")
```

On a laptop with an Intel Core Ultra 9 285H (16 cores) and 63.5 GB of RAM, computing the projection matrix takes about 4 seconds and fitting the model, including the predictions on the 0.02° grid, takes about 20 seconds.
