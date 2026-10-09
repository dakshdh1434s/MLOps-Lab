# P04 — From Notebook to Package

**Course:** SCSE3040 — Machine Learning Operations  
**University:** Bennett University  
**Session:** 2026–27  
**Student:** Daksh Pratap Singh  
**Enrollment ID:** S24CSEU2285  
**Batch:** 80

## Overview

Practical 04 demonstrates how to refactor notebook code into a reusable Python package and run the workflow from the command line without relying on a notebook.

The practical uses a delivery-time dataset and a Linear Regression model to predict delivery duration. It separates responsibilities into modules so that data handling, feature utilities, model operations, and validation can be maintained independently.

## Learning objectives

- Understand the limitations of notebooks, including hidden state and cell execution order.
- Refactor notebook cells into functions and Python modules.
- Create and import a package using `__init__.py`.
- Train, evaluate, save, and reload a model.
- Run training and prediction scripts from the command line.
- Add utility functions and validate delivery-order inputs.

## Project structure

The practical builds the following structure inside the `work/` directory:

```text
work/
├── delivery/
│   ├── __init__.py
│   ├── data.py
│   ├── features.py
│   ├── model.py
│   └── validate.py
├── train.py
├── predict.py
└── model.joblib
```

- **`delivery/data.py`** — loads the delivery CSV and splits data into training and test sets.
- **`delivery/features.py`** — provides delivery feature utilities, including minutes per kilometre, order descriptions, and average speed in km/h.
- **`delivery/model.py`** — trains and evaluates the Linear Regression model and saves or loads it with `joblib`.
- **`delivery/validate.py`** — checks whether an order has valid distance, preparation time, traffic level, and rain values.
- **`delivery/__init__.py`** — marks `delivery` as a package and exposes selected functions.
- **`train.py`** — trains the model, reports its mean absolute error (MAE), and saves the model.
- **`predict.py`** — loads the saved model and predicts the delivery time for a sample order.
- **`model.joblib`** — stores the trained model for later use.

## Dataset

The practical uses `data/delivery_times.csv`, containing 600 generated food-delivery records. The input features are:

- `distance_km`
- `prep_time_min`
- `traffic_level`
- `rain`

The target column is `delivery_min`.

If the dataset is missing, the notebook includes code to recreate it using a fixed random seed.

## Model and evaluation

The notebook uses **Linear Regression**. The data is split into training and test sets with a test size of `0.2` and random seed `42`. Model performance is evaluated using **Mean Absolute Error (MAE)**, measured in minutes.

The notebook also saves the trained model with `joblib`, reloads it, and compares predictions from the original and reloaded models.

## Tasks completed in the practical

### T1 — Average speed function

Adds `average_speed_kmph(distance_km, delivery_min)` to `delivery/features.py`.

The function calculates speed in kilometres per hour:

```python
distance_km / (delivery_min / 60)
```

For example, 10 km in 30 minutes gives **20 km/h**.

### T2 — Order validation

Creates `delivery/validate.py` with `is_valid_order(order)`. An order is valid only when:

- `distance_km` is greater than `0`.
- `prep_time_min` is `0` or greater.
- `traffic_level` is `1`, `2`, or `3`.
- `rain` is `0` or `1`.

Invalid or incomplete inputs are rejected.

### T3 — Command-line prediction

Creates `predict.py`, which loads `model.joblib` and predicts the delivery duration for a sample order with:

- Distance: 7 km
- Preparation time: 25 minutes
- Traffic level: 3
- Rain: 0

The script prints a line beginning with `PREDICTION:`.

## How to run

Run the notebook cells from top to bottom first to create the package, dataset (if needed), trained model, and scripts.

From the `work/` directory, with the course virtual environment activated and the required dependencies installed:

```bash
python train.py
python predict.py
```

To provide a custom dataset path to the training script:

```bash
python train.py path/to/delivery_times.csv
```

Required libraries used by the notebook include `numpy`, `pandas`, `scikit-learn`, and `joblib`.

## Self-check

At the end of the notebook, run the **Self-check** cell. It checks the average-speed function, order validation rules, and successful command-line prediction. The notebook reports how many checks passed.

## Learning outcome

This practical turns exploratory notebook code into an importable, reusable package with a command-line training pipeline, persisted model, input validation, and prediction script. The structure is designed to support later practicals involving testing, serving, and containerization.

## References

- [Python documentation — Modules and packages](https://docs.python.org/3/tutorial/modules.html)
- [Python documentation — The module search path](https://docs.python.org/3/tutorial/modules.html#the-module-search-path)
- [joblib — Persistence](https://joblib.readthedocs.io/en/stable/persistence.html)
- [scikit-learn — Model persistence](https://scikit-learn.org/stable/model_persistence.html)

---
**Practical 04 — From Notebook to Package**
