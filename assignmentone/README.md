# Assignment-1
## Learning Probability Density Functions using Roll-Number-Parameterized Non-Linear Model

---

## Dataset

- **Feature Used:** NO₂ (Nitrogen Dioxide concentration)
- **Dataset Link:**  
  https://www.kaggle.com/datasets/shrutibhargava94/india-air-quality-data
- **Source:** Central Pollution Control Board (CPCB), India

---

## Objective

To learn a probability density function (PDF) for air quality data by applying a roll-number-dependent non-linear transformation and estimating the parameters of the resulting distribution.

---

## Problem Description

Given NO₂ concentration values \( x \), perform a non-linear transformation based on the university roll number and learn the parameters of the following probability density function:

\[
\hat{p}(z) = c \cdot e^{-\lambda (z - \mu)^2}
\]

---

## Methodology

---

### Step-1: Non-Linear Transformation

Each NO₂ value \( x \) is transformed into \( z \) using:

\[
z = Tr(x) = x + a_r \sin(b_r x)
\]

where,

\[
a_r = 0.05 \times (r \bmod 7)
\]

\[
b_r = 0.3 \times ((r \bmod 5) + 1)
\]

- \( r \) is the **University Roll Number**
- \( \bmod \) denotes the remainder operator

This transformation introduces roll-number-specific non-linearity into the data.

---

### Step-2: Learning the Probability Density Function

The transformed variable \( z \) is modeled using:

\[
\hat{p}(z) = c \cdot e^{-\lambda (z - \mu)^2}
\]

where:
- \( c \) — normalization constant
- \( \lambda \) — spread-controlling parameter
- \( \mu \) — mean of the distribution

---

## Parameter Estimation

- A **normalized histogram** is used to estimate the empirical probability density of \( z \).
- Parameters \( c \), \( \lambda \), and \( \mu \) are learned using **non-linear least squares curve fitting**.
- The learned PDF is compared with the empirical distribution for validation.

---

## Results

- The learned probability density function closely fits the empirical distribution of the transformed data.
- The model captures both the central tendency and dispersion of NO₂ values after transformation.
- Visualization includes:
  - Histogram of transformed data
  - Overlay of the fitted probability density function

---
## Histogram


<img width="877" height="579" alt="image" src="https://github.com/user-attachments/assets/0ef1e934-45bc-45a3-bf8b-e2832fe93c45" />






---
## Tools and Libraries

- Python
- NumPy
- Pandas
- Matplotlib
- SciPy

---

## Conclusion

This assignment demonstrates how roll-number-parameterized non-linear transformations can be used to personalize probability density learning tasks. The estimated PDF effectively models transformed air quality data and validates the application of non-linear parameter estimation techniques.

