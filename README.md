# ADCSI4SJ — CAHOOTS CAD Analysis (E. Andrae)

This repository contains an exploratory and descriptive analysis of Computer-Aided Dispatch (CAD) call data with a focus on CAHOOTS-related call signs. The workflow cleans raw CAD exports, establishes helper functions, and then produces a set of analyses that quantify CAHOOTS activity over time, assess relationships with overall call volume, and illustrate sampling-based summaries.

## Table of Contents

- [Introduction](#introduction)
- [Repository Structure](#repository-structure)
- [Requirements](#requirements)
- [Installation](#installation)
- [Data Expectations](#data-expectations)
- [Workflow & Usage](#workflow--usage)
- [Analyses Produced](#analyses-produced)
- [Reproducibility Notes](#reproducibility-notes)
- [Troubleshooting](#troubleshooting)
- [License](#license)
- [Contact](#contact)
- [Acknowledgments](#acknowledgments)

## Introduction

The project is organized as a sequence of Jupyter notebooks:

1) **Data Cleaning** → `data_cleaning_final.ipynb`  
2) **Helper Functions** → `establishing_functions.ipynb`  
3) **Analyses** → `cahoots_percentage_over_time.ipynb`, `cahoots_correlation_analysis.ipynb`, `cahoots_mean_sampling.ipynb`

Each stage builds on the previous, culminating in plots and tabulations that describe CAHOOTS call activity over time and relative to overall CAD volumes. A slide deck summarizing the work is included as `ADCSI4SJ_Final_Project_Slides.pdf`

## Repository Structure

```

.
├── ADCSI4SJ_Final_Project_Slides.pdf
├── README.md
├── establishing_functions.ipynb
├── data_cleaning_final.ipynb
├── cahoots_percentage_over_time.ipynb
├── cahoots_mean_sampling.ipynb
└── cahoots_correlation_analysis.ipynb

````

The notebooks are intended to be run in the order shown above.

## Requirements

- Python 3.x
- Jupyter (Notebook or JupyterLab)
- Python packages:
  - `pandas`
  - `numpy`
  - `scipy`
  - `matplotlib`

> The current README lists `pandas`, `numpy`, `scipy.stats`, and `matplotlib.pyplot`; installing `scipy` and `matplotlib` covers those modules.

## Installation

1. **Clone the Repository**
   ```bash
   git clone https://github.com/Elijah-Andrae56/ADCSI4SJ-EAndrae.git
   cd ADCSI4SJ-EAndrae
   ```

2. **(Recommended) Create a Virtual Environment**

   ```bash
   python -m venv .venv
   # Windows
   .venv\Scripts\activate
   # macOS/Linux
   source .venv/bin/activate
   ```

3. **Install Dependencies**

   ```bash
   pip install jupyter pandas numpy scipy matplotlib
   ```

4. **Launch Jupyter**

   ```bash
   jupyter lab
   # or
   jupyter notebook
   ```

## Data Expectations

The cleaning notebook expects a raw CAD export with at least the following fields (names will be normalized during cleaning):

* `Call_Created_Time` → parsed and renamed to **Call Time**
* `PrimaryUnitCallSign` → renamed to **Call Sign**
* `RespondingUnitCallSign` → renamed to **2 Call Sign**
* `InitialIncidentTypeDescription` → renamed to **Reason for Dispatch**
* `Disposition` (used to filter records where no action was taken)
  During cleaning, rows with missing incident type are removed, as are rows where both call sign fields are empty. A reduced set of relevant columns is retained to streamline analysis.

> **Privacy & Confidentiality**: Ensure you have the right to use the CAD data and that no personally identifiable information (PII) is exposed in outputs or version control history.

## Workflow & Usage

### 1) Data Cleaning — `data_cleaning_final.ipynb`

* Load the raw CAD CSV/extract.
* Run all cells to:

  * Parse **Call Time** as a datetime field.
  * Standardize column names.
  * Filter dispositions implying no action (removes most `CAHOT`-labelled calls).
  * Persist a cleaned dataset (the notebook is configured to save to the project folder). 

### 2) Helper Functions — `establishing_functions.ipynb`

* Load the cleaned dataset.
* Define the target call sign groups (e.g., CAHOOTS call signs) and record the first/last observed dates for each.
* Provide `calculate_counts(table, call_signs)` to produce monthly totals and call-sign-specific counts used downstream.

### 3) Analyses

Run any or all of the following:

* **Percent over Time** — `cahoots_percentage_over_time.ipynb`
  Produces monthly CAHOOTS percent of all CAD calls; labels first occurrences for each call sign; shows each call sign’s contribution to CAHOOTS totals; compares average percentages across selected call signs; and includes a stacked percentage view.

* **Correlation View** — `cahoots_correlation_analysis.ipynb`
  Visualizes total CAD calls vs. CAHOOTS monthly counts, with a zoomed view and per-call-sign counts; examines groupings by time period to assess whether relationships are driven by temporal regimes rather than aggregate volume.

* **Mean Sampling** — `cahoots_mean_sampling.ipynb`
  Assigns colors by time period, draws repeated samples (with replacement) from designated periods, and plots the distribution of average CAHOOTS percentages with the sample mean.

## Analyses Produced

Typical outputs include:

* Monthly time series plots (totals and percentages)
* Stacked percentage breakdowns by CAHOOTS call sign
* Scatter/relationship views of total CAD vs. CAHOOTS activity
* Sampling histograms with annotated means

All outputs are generated directly in the notebooks with `matplotlib`. Save figures from the notebook UI as needed.

## Reproducibility Notes

* **File Paths**: If the raw CAD data is outside this directory, adjust the input path cells at the top of `data_cleaning_final.ipynb`.
* **Call Sign Lists**: Update the `target_call_signs` / `cahoots_call_signs` lists in `establishing_functions.ipynb` to match your context.
* **Date Windows**: If you analyze sub-periods, set those filters consistently across notebooks.

## Troubleshooting

* **Datetime parsing errors**: Confirm the raw `Call_Created_Time` format and timezone; adjust the parsing directive if needed.
* **Empty plots or zero counts**: Verify that your call sign filters match the cleaned column names (**Call Sign**, **2 Call Sign**) and that dispositions weren’t over-filtered.
* **Module not found**: Re-install requirements into the active environment and restart the kernel.

## License


## Contact

For questions or suggestions, please open an issue or contact the maintainer.

## Acknowledgments

* Course: ADCSI4SJ.
* Thanks to collaborators and reviewers who provided feedback on the analysis workflow.
