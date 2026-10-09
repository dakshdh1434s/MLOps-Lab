# P05 — MLOps Configuration and Testing

**Course:** SCSE3040 — MLOps Practical  
**Student:** Daksh Pratap Singh  
**Enrollment ID:** S24CSEU2285  
**Batch:** 80

## Overview

This practical demonstrates configuration-driven setup and automated testing for a delivery-time prediction package. Model and data settings are kept in `config.yaml`, so key parameters can be changed in configuration rather than being hard-coded in the program.

## Repository

GitHub: https://github.com/dakshdh1434s/MLOps-Lab

## Configuration

The `config.yaml` file contains settings for the delivery-time model:

```yaml
# Settings for the delivery-time model.
# Change values here, never in the code.

data:
  path: ../data/delivery_times.csv
  features:
    - distance_km
    - prep_time_min
    - traffic_level
    - rain
  target: delivery_min

split:
  test_size: 0.2
  seed: 42

model:
  name: linear_regression

training:
  max_rows: 300
```

### Configuration fields

- `data.path`: Path to the delivery-time dataset.
- `data.features`: Input features used by the model.
- `data.target`: Target column to predict.
- `split.test_size`: Fraction of the data reserved for testing.
- `split.seed`: Seed used for reproducibility.
- `model.name`: Model selected for the practical.
- `training.max_rows`: Maximum number of rows used for training.

> Make sure the dataset path matches the directory structure on your machine.

## Running the tests

Run the test suite from the project environment. For example, if `pytest` is installed in your active Python environment:

```bash
python -m pytest -v
```

If the tests are located in a specific directory, pass that directory to pytest, for example:

```bash
python -m pytest work -v
```

A successful run should show the test summary at the end. Include a screenshot of your own terminal output in the practical submission.

## Package output before and after refactoring

- **Before refactor:** 1.92 minutes
- **After refactor:** 1.92 minutes

These are the values recorded in the practical reference submission; verify them against your own run before submitting.

## Submission checklist

- [ ] Confirm `config.yaml` is included in the repository.
- [ ] Run pytest and confirm the final summary line.
- [ ] Add the terminal screenshot to the submission PDF.
- [ ] Verify the before/after package output against your actual execution.

---
**Practical:** P05 — MLOps Configuration and Testing
