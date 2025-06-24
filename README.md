# Vasicek Bond Pricing: Analytical, Monte Carlo, and PDE Approaches

## Overview

This repository presents a comprehensive implementation of zero-coupon bond pricing under the **Vasicek interest rate model** using three distinct methodologies:

1. **Analytical Formula** – Closed-form solution for zero-coupon bonds
2. **Monte Carlo Simulation** – Simulated short-rate paths using Ornstein-Uhlenbeck process
3. **Finite Difference Method (PDE Approach)** – Backward time-stepping to solve the Vasicek pricing PDE

These approaches are implemented in Python and benchmarked against each other to demonstrate accuracy, convergence, and numerical stability in modeling stochastic interest rate environments.

---

## Table of Contents

* [Background](#background)
* [Mathematical Formulation](#mathematical-formulation)
* [Methodologies](#methodologies)

  * [Analytical Bond Pricing](#1-analytical-bond-pricing)
  * [Monte Carlo Simulation](#2-monte-carlo-simulation)
  * [PDE Finite Difference Method](#3-pde-finite-difference-method)
* [Dependencies](#dependencies)
* [Usage](#usage)
* [Results](#results)
* [Visualizations](#visualizations)
* [Applications](#applications)
* [Author](#author)
* [License](#license)

---

## Background

The Vasicek model is a foundational short-rate model used extensively in fixed income analytics. It assumes that the short-term interest rate evolves according to a **mean-reverting Ornstein-Uhlenbeck (OU) process**:

$dr_t = \kappa (\theta - r_t) dt + \sigma dW_t$

where:

* $r_t$ is the instantaneous short rate
* $\kappa$ is the rate of mean reversion
* $\theta$ is the long-term mean level
* $\sigma$ is the volatility
* $W_t$ is a standard Wiener process

This model provides analytical tractability, especially for pricing zero-coupon bonds and interest rate derivatives.

---

## Mathematical Formulation

The price of a zero-coupon bond maturing at time $T$, given the current short rate $r_t$, is:

$P(t,T) = A(t,T) \cdot e^{-B(t,T) \cdot r_t}$

Where:

* $B(t,T) = \frac{1 - e^{-\kappa (T - t)}}{\kappa}$
* $( A(t,T) = \exp \left\[ \left( \theta - \frac{\sigma^2}{2\kappa^2} \right)(B(t,T) - (T - t)) - \frac{\sigma^2}{4\kappa} B(t,T)^2 \right] ]$

---

## Methodologies

### 1. Analytical Bond Pricing

Implements the closed-form Vasicek solution for zero-coupon bonds. This method serves as the benchmark for the simulation and PDE methods.

### 2. Monte Carlo Simulation

* Simulates thousands of paths of the short rate using the OU process.
* Uses the average discount factor to approximate bond price:
  $P(T) \approx \mathbb{E}[e^{-\int_0^T r_t dt}]$
* Includes computation of standard error to measure Monte Carlo variance.

### 3. PDE Finite Difference Method

* Solves the backward Kolmogorov equation:
  $\frac{\partial V}{\partial t} + \kappa(\theta - r) \frac{\partial V}{\partial r} + \frac{1}{2}\sigma^2 \frac{\partial^2 V}{\partial r^2} - rV = 0$
* Implements an implicit finite difference scheme using a tridiagonal sparse matrix.
* Handles boundary and terminal conditions appropriately.
* Interpolates bond price at given $r_0$.

---

## Dependencies

* Python 3.8+
* numpy
* scipy
* matplotlib

Install all dependencies using:

```bash
pip install -r requirements.txt
```

---

## Usage

Clone the repository:

```bash
git clone https://github.com/Mkhan2317/Vasicek-Bond-Pricing
cd Vasicek-Bond-Pricing
```


Run the script:

```bash
python vasicek_bond_pricing.py
```

---

## Results

| Method           | Estimated Bond Price | Notes                         |
| ---------------- | -------------------- | ----------------------------- |
| Analytical       | 0.883xx              | Closed-form, baseline result  |
| Monte Carlo (MC) | 0.882xx ± 0.001xx    | Mean with standard error      |
| PDE Finite Diff  | 0.883xx              | High accuracy, grid converged |

---

## Visualizations

* Yield curve visualization of simulated Vasicek process
* Initial bond price curve at $t = 0$
* 3D surface plot of bond price over time and short rate

All plots are automatically generated and displayed upon script execution.

---

## Applications

* Interest rate risk modeling
* Government and corporate bond pricing
* Asset Liability Management (ALM)
* Fixed income trading strategy development
* Quantitative research in stochastic interest rate models

---

## Author

**MD Amir Khan**
Master’s in Financial Engineering – Stevens Institute of Technology
Focus: Interest Rate Derivatives, Fixed Income Analytics, Quantitative Investing

Connect with me on [LinkedIn](https://www.linkedin.com/in/amirkhan2317/)

---

## License

This project is open-source and licensed under the MIT License.
See the `LICENSE` file for details.
