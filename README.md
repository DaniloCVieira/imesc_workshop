# Applied Machine Learning for Environmental Sciences — iMESc workshop

Course material for the hands-on workshop **"Applied Machine Learning for Environmental Sciences"**, a specialist course by the Ghent University Doctoral School.

**Instructors:** Prof. Gustavo Fonseca (Instituto do Mar, UNIFESP, Brazil) and Prof. Danilo C. Vieira (Instituto Oceanográfico, USP, Brazil)

All analyses are done in **iMESc** (*interactive Machine Learning app for Environmental Sciences*), a free Shiny app that runs in R. You do not need to write code.

## What is in this repository

```
imesc_workshop/
├── handbook/
│   └── iMESc_workshop_handbook.pdf      Participant handbook: step-by-step guide to the three examples
└── datasets/
    ├── ex1_estuary/                     Example 1: finding groups along an estuarine gradient
    ├── ex2_shelf/                       Example 2: predicting benthic richness and quality
    └── ex3_chla/                        Example 3: forecasting coastal chlorophyll-a
```

Start with the **handbook**. It explains each example, which files to load and every step in iMESc. Each example has its own dataset folder.

## Getting the files

Download everything at once: on the repository page, click the green **Code** button, then **Download ZIP**, and unzip the file on your computer. If you use Git, you can clone the repository instead:

```
git clone https://github.com/DaniloCVieira/imesc_workshop.git
```

To download a single file, open it on GitHub and click **Download raw file**.

## Before the workshop: install and start iMESc

1. Install a recent version of [R](https://cran.r-project.org/) and [RStudio](https://posit.co/download/rstudio-desktop/).
2. In RStudio, install Shiny:

   ```r
   install.packages("shiny")
   ```

3. Start iMESc:

   ```r
   options(timeout = 1200)
   shiny::runGitHub("iMESc", "DaniloCVieira")
   ```

The first launch installs all the packages that iMESc needs and can take several minutes. Later launches are faster. `options(timeout = 1200)` gives R more time to download iMESc on a slow connection; without it, R stops after 60 seconds.

Please run these steps **before the first session**, so that the installation does not take time from the exercises. If the installation fails, send the instructors the error message (the last lines printed in the R console) before the workshop.

iMESc needs a screen resolution of at least 1377 × 768 pixels. If panels overlap, maximise the browser window or zoom out.

### Linux and macOS

**Windows** needs no extra step: R installs ready-built (binary) packages.

**Linux.** On Linux, R packages are compiled from source, and several of the packages used by iMESc (for maps, spatial data and some models) need system libraries. You need administrator (`sudo`) rights to install them.

- **Ubuntu / Debian:** run this command in a terminal before starting iMESc. If a library is missing, iMESc stops and prints the same command with the missing ones.

  ```bash
  sudo apt update && sudo apt install -y build-essential gfortran cmake pkg-config \
    libfontconfig1-dev libfreetype-dev libssl-dev libabsl-dev libnlopt-dev \
    libgdal-dev gdal-bin libgeos-dev libproj-dev libsqlite3-dev libudunits2-dev \
    libcurl4-openssl-dev libglpk-dev libmagick++-dev gsfonts libpng-dev zlib1g-dev pandoc
  ```

- **Other distributions** (Fedora, Arch, ...): install the equivalent development packages of your distribution (C/C++ and Fortran compilers, CMake, GDAL, GEOS, PROJ, SQLite, udunits2, curl, OpenSSL, fontconfig, FreeType, GLPK, NLopt, ImageMagick++, libpng, zlib and Pandoc), then start iMESc. If you are unsure, contact the instructors before the workshop.

**macOS.** R installs ready-built packages, so usually no extra step is needed. If the installation complains about a missing compiler, install the Xcode Command Line Tools in the Terminal and start iMESc again:

```bash
xcode-select --install
```

## Datasets

All datasets are **synthetic**. They were generated to resemble real environmental data and contain a known, hidden structure, so that you can check whether the methods recover it.

Every file is a CSV with the observation ID in the first column and the variable names in the first row. The handbook says which files to upload as the Numeric-, Factor- and Coords-Attribute of each Datalist.

### Example 1: Finding groups along an estuarine gradient (`datasets/ex1_estuary`)

Unsupervised learning (Self-Organizing Maps and hierarchical clustering). 240 water and sediment samples: 120 stations, each sampled in summer and in winter.

| File | Load as | Content |
|---|---|---|
| `ex1_numeric.csv` | Numeric-Attribute | 16 environmental variables (salinity, turbidity, nutrients, oxygen, sediment, ...) |
| `ex1_factors.csv` | Factor-Attribute | Season, Campaign |
| `ex1_coords.csv` | Coords-Attribute | Longitude, Latitude |

### Example 2: Predicting benthic richness and quality (`datasets/ex2_shelf`)

Supervised regression and classification with spatial validation. Training area: 400 stations. Transfer area: 100 stations, deeper and about 100 km away, used only for the final test.

| File | Content |
|---|---|
| `ex2_train_X_numeric.csv` | 15 environmental and contamination predictors (training area) |
| `ex2_train_Y_numeric.csv` | Richness (training area) |
| `ex2_train_factors.csv` | Quality_class, Sampling_design (training area) |
| `ex2_train_coords.csv` | Longitude, Latitude (training area) |
| `ex2_transfer_X_numeric.csv` | The same 15 predictors (transfer area) |
| `ex2_transfer_Y_numeric.csv` | Observed Richness (transfer area) |
| `ex2_transfer_factors.csv` | Quality_class, Sampling_design (transfer area) |
| `ex2_transfer_coords.csv` | Longitude, Latitude (transfer area) |

### Example 3: Forecasting coastal chlorophyll-a (`datasets/ex3_chla`)

Supervised forecasting of a time series. Daily data from 1 January 2020 to 31 December 2024 (1827 days) at one coastal station.

| File | Load as | Content |
|---|---|---|
| `ex3_chla_numeric.csv` | Numeric-Attribute | Chla, SST, Wind_along, Rain, Discharge, PAR, Tide_range (the date is the ID) |
| `ex3_chla_factors.csv` | Factor-Attribute | Year, Month, Season, Days |

All the forecasting features (targets with lead, 7-day means) are built inside iMESc during the exercise, as described in the handbook.

## Using your own data

At the end of the workshop you will apply the same workflow to your own data. If you want to, bring a dataset prepared with the same file rules:

- The first column holds a unique ID; the first row holds the variable names.
- Variable names must be unique, have no spaces or special symbols, and must not start with a number.
- Use a dot as the decimal separator, and write missing values as `NA`.
- All files of one Datalist must use the same IDs.

## More help

- iMESc help pages: <https://danilocvieira.github.io/iMESc_help/>
- iMESc source code: <https://github.com/DaniloCVieira/iMESc>

## How to cite iMESc

Vieira, D. C., Paula, F. S., Yaginuma, L. E. & Fonseca, G. (2025). iMESc – an interactive machine learning app for environmental sciences. *Frontiers in Environmental Science*, 13, 1533292. <https://doi.org/10.3389/fenvs.2025.1533292>
