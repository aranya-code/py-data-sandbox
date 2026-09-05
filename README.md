# Python Data Sandbox

![Python](https://img.shields.io/badge/Python-3.9%2B-3776AB.svg?logo=python&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-array%20computing-013243?logo=numpy&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-data%20analysis-150458?logo=pandas&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-notebooks-F37626?logo=jupyter&logoColor=white)

A compact, hands-on Python workspace for learning the fundamentals of numerical computing and tabular data analysis with NumPy and Pandas. The repository combines focused scratchpad notebooks with a college-value dataset prepared for exploration and Tableau-oriented workflows.

The examples are intentionally direct: create arrays, inspect their shape and type, select and transform DataFrame data, filter rows, aggregate values, and practice the small operations that form the foundation of a larger data-analysis project.

## Contents

- [What is in this repository](#what-is-in-this-repository)
- [Repository layout](#repository-layout)
- [Learning path](#learning-path)
- [Data files](#data-files)
- [Getting started](#getting-started)
- [Working with the notebooks](#working-with-the-notebooks)
- [Example workflow](#example-workflow)
- [Data notes](#data-notes)
- [Project status](#project-status)

## What is in this repository

This repository currently contains two learning notebooks and a small set of related CSV files:

- **NumPy fundamentals**: array creation, indexing, slicing, dimensions, shapes, data types, initialization, arithmetic, statistics, reshaping, and stacking.
- **Pandas fundamentals**: DataFrame creation and inspection, CSV loading, column and row selection, sorting, filtering, string operations, column changes, grouping, aggregation, ranking, and cumulative calculations.
- **College-value data assets**: a Tableau-ready institution-level dataset and field-inventory files that describe the analytical and presentation fields available in the data.

This is an exploratory learning repository rather than a production Python package. There is currently no application entry point, package API, automated test suite, or data pipeline to run.

## Repository layout

```text
py-data-sandbox/
├── DataSet/
│   ├── college_value_analytical_field_inventory.csv
│   ├── college_value_tableau_field_inventory.csv
│   └── college_value_tableau_ready.csv
├── numpy_scratchpad.ipynb
├── pandas_scratchpad.ipynb
└── README.md
```

## Learning path

### 1. NumPy array operations

Open [`numpy_scratchpad.ipynb`](numpy_scratchpad.ipynb) to work through:

- One-, two-, and three-dimensional array creation
- Array dimensions, shapes, data types, and item sizes
- Element, row, column, and slice access
- Updating array values and using negative indexes
- Array initialization with `zeros`, `ones`, `full`, `full_like`, `identity`, and random-value helpers
- Element-wise arithmetic and powers
- Minimum, maximum, and sum calculations, including axis-based operations
- Reshaping arrays and vertically or horizontally stacking arrays

### 2. Pandas DataFrame operations

Continue with [`pandas_scratchpad.ipynb`](pandas_scratchpad.ipynb) to practice:

- Creating a DataFrame and inspecting its rows, columns, schema, and summary statistics
- Loading the Tableau-ready CSV with `pandas.read_csv`
- Selecting rows and columns with `loc` and `iloc`
- Sorting and filtering records
- Searching text with `str.contains`
- Querying records with `DataFrame.query`
- Adding, renaming, and dropping columns
- Creating derived values with string operations and conditional logic
- Counting values and grouping records by state
- Aggregating grouped data
- Ranking values and calculating cumulative totals

## Data files

### [`college_value_tableau_ready.csv`](DataSet/college_value_tableau_ready.csv)

The primary analysis file used by the Pandas notebook. It contains institution-level college data prepared for tabular exploration and Tableau use. The sample fields include:

| Field | Purpose |
| --- | --- |
| `UNITID` | Institution identifier |
| `INSTNM` | Institution name |
| `CITY`, `STABBR`, `ZIP` | Institution location |
| `LATITUDE`, `LONGITUDE` | Geographic coordinates |
| `institution_control_label` | Public or private control classification |
| `campus_status_label` | Campus status label |
| `admission_rate_status` | Availability status for admission-rate information |
| `region_label` | Geographic region |
| `locale_type_label`, `locale_detailed_label` | Locale classifications |
| `undergraduate_enrollment_primary` | Undergraduate enrollment value |
| `undergraduate_enrollment_size_band` | Enrollment-size grouping |

The complete column set is available in the CSV itself.

### [`college_value_analytical_field_inventory.csv`](DataSet/college_value_analytical_field_inventory.csv)

An analytical data dictionary describing project fields. It records field names, display labels, descriptions, dimensions, categories, units, data types, availability counts, missing counts, distinct-value counts, and source or derivation notes.

### [`college_value_tableau_field_inventory.csv`](DataSet/college_value_tableau_field_inventory.csv)

A Tableau-oriented field inventory organized by section and field order. It provides a concise view of field types, availability, missingness, and reported distinct values for presentation and dashboard preparation.

## Getting started

### Prerequisites

- Python 3.9 or newer
- A Jupyter-compatible environment, such as JupyterLab, Jupyter Notebook, or VS Code with the Jupyter extension
- `pip` or another Python package manager

### 1. Clone the repository

```bash
git clone https://github.com/<your-account>/py-data-sandbox.git
cd py-data-sandbox
```

Replace `<your-account>` with the GitHub account that hosts this repository.

### 2. Create and activate a virtual environment

Windows PowerShell:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

macOS or Linux:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install the notebook dependencies

```bash
python -m pip install --upgrade pip
python -m pip install numpy pandas jupyterlab
```

### 4. Launch the notebooks

```bash
jupyter lab
```

Open either notebook from the Jupyter interface. The Pandas notebook expects the repository layout to remain unchanged because it loads the dataset with the relative path `./DataSet/college_value_tableau_ready.csv`.

## Working with the notebooks

The notebooks are scratchpads, so cells can be run independently while experimenting. For a clean walkthrough:

1. Open the notebook in JupyterLab or VS Code.
2. Start at the first cell and run cells from top to bottom.
3. Inspect the output after each operation.
4. Change the examples and rerun cells to test how array shape, indexing, filtering, and aggregation affect the result.
5. Restart the kernel and rerun all cells when you need to confirm that the notebook works from a clean state.

Because the Pandas notebook adds temporary columns during exploration, restarting the kernel is useful when repeating the exercise from the original CSV state.

## Example workflow

The following small example mirrors the data-loading and filtering approach used in the Pandas notebook:

```python
import pandas as pd

data = pd.read_csv("DataSet/college_value_tableau_ready.csv")

available_admission_data = data.loc[
    data["admission_rate_status"] == "Available",
    ["UNITID", "INSTNM", "CITY", "STABBR"],
]

colleges_by_state = (
    data.groupby("STABBR", as_index=False)["INSTNM"]
    .count()
    .rename(columns={"INSTNM": "institution_count"})
    .sort_values("institution_count", ascending=False)
)

print(available_admission_data.head())
print(colleges_by_state.head())
```

For array practice, the NumPy notebook starts with the same basic progression used in many data workflows:

```python
import numpy as np

values = np.array([[1, 2, 3], [4, 5, 6]])
print(values.shape)
print(values[:, 1])
print(values.sum(axis=0))
```

## Data notes

- The CSV files are committed as repository data assets and can be opened directly from GitHub using the links above.
- The two inventory files are documentation and metadata companions to the Tableau-ready data file.
- Field availability and missing-value counts are recorded in the inventory files; inspect them before building an analysis or visualization that depends on a particular field.
- The notebooks demonstrate transformations for learning. They do not write a cleaned or transformed replacement dataset back to disk.
- The repository does not currently include a formal data-source citation, license statement, or automated freshness check. Add those details when the upstream source and redistribution terms are formally documented.

## Project status

This project is an active personal data-learning sandbox. The current focus is building fluency with NumPy arrays and Pandas DataFrames through small, inspectable examples. Future work may include adding visualizations, separating reusable analysis code from scratchpad exercises, introducing dependency pinning, and documenting the upstream data provenance.

## Contributing

Small improvements are welcome. Keep changes focused and reproducible:

1. Create a branch for the change.
2. Update the relevant notebook or documentation.
3. Run the affected notebook from a clean kernel.
4. Explain any dataset or dependency changes in the pull request.

## License

No license file is currently included. Until a license is added, treat the repository contents as all rights reserved and obtain permission before redistributing them.