# Polynomial Degree Selection: Validation Split vs 5-Fold Cross-Validation

For *Machine Learning: Mathematical Basis* (D.B. Rokhlin, 2026).

## Overview

This project compares two strategies for selecting the degree of a polynomial
regression model:

1. A single random 70/30 train/validation split
2. 5-fold cross-validation

Both strategies are repeated across 30 different random seeds on the same
fixed dataset, and the resulting model quality is evaluated on a large
independent test set.

## Dataset

- n = 80 points, x ~ Uniform(-2, 2)
- True function: f*(x) = sin(2x) + 0.3x
- Gaussian noise, std = 0.3
- Test set: 2000 independent points from the same distribution

## Method

For each of 30 random seeds:

- **Validation split**: split the 80 points 70/30, fit polynomial degrees
  1–12 by least squares, pick the degree with the lowest validation RMSE.
- **5-fold CV**: run 5-fold cross-validation over the same 80 points for
  degrees 1–12, pick the degree with the lowest mean CV RMSE.

The selected degree is then refit on all 80 points and evaluated on the
2000-point test set.

## Key findings

- Validation split selected degrees ranging from 3 to 12 across the 30 seeds
  (std ≈ 2.0)
- 5-fold CV selected degree 5 in nearly every run (std ≈ 0.36)
- Test RMSE was more stable under CV (std ≈ 0.0002) than under the single
  split (std ≈ 0.020)

This matches the theoretical expectation that cross-validation gives a more
stable estimate of model quality than a single random split, at the cost of
roughly 5x more model fits.

## Files

- `HW1_PolynomialRegression.ipynb` — full notebook: dataset generation, both
  selection procedures, plots, and conclusion

## Requirements
numpy
scikit-learn
matplotlib

## Author

Goriola-Obafemi Babatunde Sukanmi — MSc Applied Mathematics and Informatics.
