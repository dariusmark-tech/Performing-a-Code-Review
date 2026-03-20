# 📱 Smartphone Data Analysis — Code Review Project

> **Role:** Senior Data Scientist reviewing a Junior Data Scientist's code before shipping to production.

---

## 📋 Project Overview

This project prepares and visualizes smartphone data to help a university procurement team decide the best mobile phone to offer to employees. The workflow ingests raw CSV data, cleans it, and produces scatter plot visualizations comparing various specs against price.

---

## 📁 Project Structure

```
project/
│
├── data/
│   └── smartphones.csv        # Raw smartphone dataset
│
├── notebook.ipynb             # Main Jupyter notebook
│   ├── Cell 1 — prepare_smartphone_data()
│   ├── Cell 2 — column_to_label() & visualize_versus_price()
│   └── Cell 3 — Unit Tests (pytest + ipytest)
│
└── README.md
```

---

## ⚙️ Functions

### `prepare_smartphone_data(file_path)`
Reads raw smartphone CSV data and returns a cleaned DataFrame:
- Keeps only relevant columns
- Removes rows missing `battery_capacity` or `os` values
- Converts `price` from cents to dollars (divides by 100)

### `column_to_label(column_name)`
Converts a snake_case DataFrame column name into a human-readable plot label.
- Example: `"processor_speed"` → `"Processor Speed"`

### `visualize_versus_price(clean_data, x)`
Generates a seaborn scatter plot of any given column versus `price`, colored by operating system.

---

## 🧪 Running Tests

Tests are written with `pytest` and run inside the notebook using `ipytest`.

```python
ipytest.run("-qq")
```

Expected output:
```
..                        [100%]
2 passed
```

---

## 🛠️ Code Review Changes Made

| Area | Issue | Fix |
|------|-------|-----|
| PEP-8 | `rawData`, `trimmedData`, `reducedData` (camelCase) | Renamed to `raw_data`, `trimmed_data`, `reduced_data` |
| PEP-8 | Variable name too long: `columns_to_keep_in_clean_data` | Renamed to `columns_to_keep` |
| DRY | Label logic repeated twice in `visualize_versus_price()` | Replaced with `column_to_label()` calls |
| Unit Test | `assert not ... == 0` logic was inverted | Removed `not` so test correctly checks for zero NaN values |
| Docstring | Mentioned only `battery_capacity` in drop logic | Updated to reflect both `battery_capacity` and `os` |

---

## 📦 Requirements

```
pandas
seaborn
matplotlib
pytest
ipytest
```

---

## 🚀 How to Run

1. Place `smartphones.csv` in the `./data/` folder
2. Open `notebook.ipynb` in Jupyter
3. Run all cells in order
4. Confirm `2 passed` in the test cell output
5. Remove the `print(raw_data.head())` debug line before final submission
[
  "t_68f073a852d14dae99d6b8c10c9450b3.py::test_columns_kept",
  "t_68f073a852d14dae99d6b8c10c9450b3.py::test_data_not_empty",
  "t_68f073a852d14dae99d6b8c10c9450b3.py::test_nan_values",
  "t_68f073a852d14dae99d6b8c10c9450b3.py::test_price_conversion"
]
