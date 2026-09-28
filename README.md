# Yingzhu Pan's Website

This repository contains my personal website for DSCI 521.

It includes two data analysis posts:

\- **Python:** comparing penguin body mass across species using summary statistics and visualizing by boxplots.

\- **R:** comparing female and male proportions within each penguin species using counts, percentages, and bar charts.

Live website: https://yingzhupan1823.github.io/

## Prerequisites

Install the following software before building the website:

- Git
- Quarto — version 1.10.18 used for this project
- uv — version 0.12.15 used during initial setup
- R — version 4.6.1 used for this project

Ensure that `git`, `quarto`, `uv`, and `Rscript` are available in your terminal.

The project specifies Python 3.14 in `.python-version`. uv can download a compatible Python version if needed.

Python package versions are recorded in `uv.lock`. R package versions are recorded in `renv.lock`. The project's `.Rprofile` activates renv, which bootstraps itself when needed.

## Build from a fresh clone

These instructions use Git Bash on Windows.

First, open Git Bash in a directory where you want to create a new copy of the repository. Run:

``` bash
git clone https://github.com/YingzhuPan1823/YingzhuPan1823.github.io.git
cd YingzhuPan1823.github.io
```

Run all remaining commands from this repository root, where `_quarto.yml` is located.

### 1. Restore the Python environment

``` bash
uv sync --locked
```

This creates the local `.venv` and installs the Python packages recorded in `uv.lock`, including Jupyter and ipykernel.

### 2. Restore the R environment

``` bash
Rscript -e 'renv::restore(prompt = FALSE)'
```

This restores the R packages recorded in `renv.lock`, including palmerpenguins, dplyr, tidyr, ggplot2, knitr, and rmarkdown.

### 3. Render the website

``` bash
uv run quarto render
```

Run this command from the repository root so that R activates the project's renv environment. The `uv run` prefix makes the project's Python environment available to Quarto.

The generated website is written to `docs/`.

## View the website locally

After rendering, open the homepage from Git Bash on Windows:

``` bash
start docs/index.html
```

Use the Blog page to open the Python and R posts.

Alternatively, start a local preview from the repository root:

``` bash
uv run quarto preview
```

Open the local URL printed in the terminal. Press Ctrl+C to stop the preview.

## Data and network requirements

Both posts use the [Palmer Penguins dataset](https://allisonhorst.github.io/palmerpenguins/), collected and made available by Dr. Kristen Gorman and Palmer Station Antarctica LTER.

The data are available under the [CC0 license](https://creativecommons.org/publicdomain/zero/1.0/). Both posts include a source link and the original study citation.

The Python post loads data from the Python `palmerpenguins` package. The R post loads data from the R `palmerpenguins` package. No separate data download is required during execution.

Internet access is required to clone the repository and download Python or package dependencies during environment restoration. Once the environments are restored, the two penguin analyses use the data bundled with their installed packages.

## Analysis details

### Python: body mass across species

The analysis drops observations with missing species or body mass. It reports sample sizes, means, and medians, and uses boxplots to compare body mass distributions.

Source: `posts/penguins-python/index.qmd`

### R: sex proportions across species

The analysis excludes records with missing species or sex. It calculates female and male percentages separately within each species and displays them in a grouped bar chart.

Source: `posts/penguins-r/index.qmd`

## Repository structure

- `_quarto.yml`: website configuration.
- `index.qmd`, `about.qmd`, `blog.qmd`: main website pages.
- `posts/`: blog post source files.
- `images/`: website images.
- `pyproject.toml`, `uv.lock`, `.python-version`: Python environment files.
- `renv.lock`, `.Rprofile`, `renv/activate.R`: R environment files.
- `docs/`: rendered website used by GitHub Pages.

Local environments and temporary files, including `.venv/`, `renv/library/`, `.quarto/`, `_site/`, and `.DS_Store`, should not be tracked by Git.
