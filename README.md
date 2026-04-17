# Using ChatGPT and Python in Finance Education: A Portfolio Project for Accounting Majors

This repository contains the replication materials for the research article **“Using ChatGPT and Python in Finance Education: A Portfolio Project for Accounting Majors.”** It documents an AI-assisted, Python-based portfolio project used in an undergraduate finance course and provides the code, processed data, survey instrument, tables, figures, and supporting documentation needed to reproduce the article’s quantitative outputs.

## Author

**Veliota Drakopoulou**  
¹ Higher Colleges of Technology, UAE  
² Embry-Riddle Aeronautical University, USA  
**ORCID:** 0000-0002-1670-8033  
**Correspondence:** vdrakopoulou@yahoo.com

**GitHub repository:** <https://github.com/vdrakopoulou/FIN411X_ChatGPT_CoTutor_PortfolioProject>  
**Replication package (Zenodo):** <https://doi.org/10.5281/zenodo.18799045>
**Pre-Print:** https://www.researchsquare.com/article/rs-8988029/v1 

## Manuscript information

**Manuscript type:** Research article  
**Title:** *Using ChatGPT and Python in Finance Education: A Portfolio Project for Accounting Majors*

## Overview

The project examines the use of ChatGPT as a **co-tutor** in a Python-based CAPM portfolio assignment embedded in **FIN411X (Investment Analysis)**. The package supports replication of the study’s quantitative component, including:

- portfolio performance summaries for 30 student portfolios,
- ChatGPT survey responses linked through pseudonymous student IDs,
- notebooks for portfolio analysis and statistics,
- exported tables and figures used in the manuscript, and
- documentation for prompts and implementation notes.

## How the repository is organized

The public GitHub repository currently distributes most materials as ZIP archives. The most important file is:

- `Replication_Package.zip` — the complete working bundle

Additional component archives are also included for convenience:

- `code_capm.zip`
- `code_stats.zip`
- `data.zip`
- `figures.zip`
- `stat_output.zip`
- `tables.zip`

For most users, the recommended starting point is to **download and extract `Replication_Package.zip`**.

## Package structure after extraction

```text
Replication_Package/
  Readme.ipynb
  code_capm/
    capm_portfolio_project.ipynb
    portfolio_analysis.ipynb
  code_stats/
    FIN411X_Make_Tables_and_Figures.ipynb
    FIN411X_Stats_Analysis.ipynb
    run_FIN411X_#U2013_STATS_SCRIPT.ipynb
  data/
    chatgpt_survey_instrument.pdf
    chatgpt_survey_raw_id.csv
    summary_all_portfolios.csv
  documentation/
    ChatGPT Prompt Library for CAPM & Fixed#U2011Weight Portfolio (FIN411X Project).docx
    python_code_notes.docx
  figures/
    ai_literacy_vs_performance_scatterplot.png
    chatgpt_scales_boxplot.png
    portfolio_returns_histogram.png
  stat_output/
    fin411x_correlations.csv
    fin411x_descriptives.csv
  tables/
    table1_portfolio_performance.csv
    table2_ai_scales_reliability.csv
    table3_A2_frequency.csv
    table3_A3_frequency.csv
    table3_A5_frequency.csv
    table3_E1_frequency.csv
    table4_correlations_matrix.csv
    table5_ai_scales_vs_performance.csv
```

### Note on filenames

A small number of exported filenames preserve Unicode punctuation as code labels inside the ZIP archive, for example `#U2011` and `#U2013`. These are normal files and can be opened normally.

## What each part contains

### `data/`

This folder contains the core datasets used for replication.

- `summary_all_portfolios.csv` contains one row per student portfolio (`S01`–`S30`) with portfolio performance fields such as `alpha_daily`, `alpha_annual`, `beta`, `final_value_aed`, `pnl_aed`, and `total_return_pct`.
- `chatgpt_survey_raw_id.csv` contains the item-level survey export keyed by `Student_id`.
- `chatgpt_survey_instrument.pdf` is the survey instrument used in the study.

The raw survey export contains 31 rows, while the portfolio summary contains 30 rows; the analysis notebooks merge the two datasets by student ID and retain the 30 matched cases.

### `code_capm/`

These notebooks reproduce the portfolio construction and CAPM workflow.

- `capm_portfolio_project.ipynb` mirrors the student-facing workflow. It downloads market data with `yfinance`, computes returns, estimates CAPM alpha and beta, and exports a one-row summary for a selected student/portfolio combination.
- `portfolio_analysis.ipynb` aggregates individual portfolio summaries into `summary_all_portfolios.csv`.

The portfolio notebook is configured around:

- analysis window: `2025-01-02` to `2025-04-02`
- initial capital: `AED 600,000`
- benchmark: `^GSPC` (S&P 500)
- annual risk-free rate: `0.04`
- 30 predefined portfolios with a fixed 10-asset weight pattern

### `code_stats/`

These notebooks reproduce the article’s statistical analysis and publication outputs.

- `FIN411X_Stats_Analysis.ipynb` merges the portfolio and survey files, constructs three composite scales, computes descriptive statistics, and produces correlation analyses.
- `FIN411X_Make_Tables_and_Figures.ipynb` generates the main tables and figures used in the manuscript.
- `run_FIN411X_#U2013_STATS_SCRIPT.ipynb` is a helper notebook for regenerating the main figures from the merged analysis dataframe.

The three composite scales are:

- **B_scale** — learning and confidence
- **C_scale** — metacognitive strategies
- **D_scale** — AI literacy and critical awareness

### `tables/`, `figures/`, and `stat_output/`

These folders contain the bundled outputs used for the manuscript:

- summary statistics and correlations in `stat_output/`
- article tables in `tables/`
- exported PNG figures in `figures/`

### `documentation/`

This folder provides supporting teaching and implementation material:

- a prompt library used in the course project
- notes explaining the Python workflow and code organization

## Software requirements

The notebooks were designed for either:

- **Google Colab**, or
- a local **Jupyter** environment such as JupyterLab, VS Code, or Anaconda.

Recommended environment:

- Python 3.9 or later
- `numpy`
- `pandas`
- `scipy`
- `statsmodels`
- `matplotlib`
- `yfinance`
- `quantstats` (optional but used in the portfolio notebook)

Example installation:

```bash
pip install numpy pandas scipy statsmodels matplotlib yfinance quantstats
```

## Recommended replication workflow

### 1. Exact replication from the bundled data

For the closest reproduction of the manuscript outputs:

1. Download and extract `Replication_Package.zip`.
2. Open `code_stats/FIN411X_Stats_Analysis.ipynb`.
3. Make sure `summary_all_portfolios.csv` and `chatgpt_survey_raw_id.csv` are accessible to the notebook runtime.
4. Run the notebook from top to bottom.
5. Open `code_stats/FIN411X_Make_Tables_and_Figures.ipynb` and run all cells.

This workflow reproduces the descriptive statistics, reliability analyses, correlations, tables, and figures using the fixed CSV files distributed in the package.

### 2. Regenerating the portfolio summary from market data

If you want to reconstruct the portfolio summary rather than use the bundled CSV snapshot:

1. Open `code_capm/capm_portfolio_project.ipynb`.
2. Set the desired `student_id` and `portfolio_id`.
3. Run all cells to download prices, compute CAPM metrics, and export a one-row summary file.
4. Repeat for additional portfolios as needed.
5. Use `code_capm/portfolio_analysis.ipynb` to combine the portfolio summaries into a new `summary_all_portfolios.csv`.
6. Re-run the statistics notebooks.

## Important reproducibility notes

- The bundled CSV files provide the most stable route for exact replication.
- If you regenerate the portfolio data with `yfinance`, results may differ slightly over time if the data provider revises historical prices.
- The current notebooks save several outputs to the **current working directory**. The packaged folders `tables/`, `figures/`, and `stat_output/` contain the curated versions included with the replication package.
- Depending on your runtime, you may wish to edit file paths from bare filenames such as `summary_all_portfolios.csv` to explicit relative paths such as `../data/summary_all_portfolios.csv`.
- Raw ChatGPT transcripts are not included in this repository.

## Suggested use cases

This package may be useful for:

- researchers studying AI literacy, metacognition, and generative AI in higher education,
- instructors adapting Python-based finance assignments,
- replication studies in finance education, and
- classroom redesign projects that position AI as a guided learning support rather than a replacement for student thinking.

## Citation

If you use this repository or the replication files, please cite:

1. The manuscript:  
   **Drakopoulou, V.** *Using ChatGPT and Python in Finance Education: A Portfolio Project for Accounting Majors*.

2. The replication package DOI:  
   **Zenodo:** <https://doi.org/10.5281/zenodo.18799045>

## Contact

For correspondence, please contact **Veliota Drakopoulou** at **vdrakopoulou@yahoo.com**.

## License

Please refer to the `LICENSE` file in the repository root for licensing terms.
