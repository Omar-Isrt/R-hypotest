# R‑HypoTest

**Hypothesis Testing Toolkit in R**  
*Group 7 · 27 January 2024*

---

## 📖 Table of Contents

1. [Project Overview](#project-overview)  
2. [Features](#features)  
3. [Installation](#installation)  
4. [Usage](#usage)  
5. [Function Reference](#function-reference)  
6. [Examples](#examples)  
7. [Group Members](#group-members)  
8. [License](#license)  

---

## 🚀 Project Overview

**R‑HypoTest** is an R package (or script) that provides a single, unified function for performing a variety of hypothesis tests—both parametric and non‑parametric. It computes test statistics, _p_-values, and confidence intervals, helping you draw statistical conclusions from your sample data with ease.

---

## ✨ Features

- **Parametric tests**  
  - One‑sample Z and T tests  
  - Two‑sample (independent and paired) T tests  
  - One‑way ANOVA (more than two means)  
  - Pearson’s Chi‑Square test  

- **Non‑parametric tests**  
  - Bootstrap hypothesis test  

- **Robust output**  
  - Test statistic  
  - _p_-value  
  - Confidence interval  
  - Degrees of freedom (where applicable)  

- **Flexible input**  
  - Supports vectors, matrices, factors  
  - Specify population standard deviations or estimate from data  
  - Adjustable significance level (_α_) and bootstrap replicates  

---

## 🛠 Installation

1. **Clone this repository**  
   ```bash
   git clone https://github.com/<your‑username>/R‑HypoTest.git
   cd R‑HypoTest
   ```

2. **Source the script**  
   ```r
   source("test_of_hypothesis.R")
   ```

> _If you package it as an R package, you could also use_  
> ```r
> devtools::install_local("path/to/R-HypoTest")
> ```

---

## 🎯 Usage

Load the function into your R session:

```r
source("test_of_hypothesis.R")

# Example: one‑sample Z‑test
x      <- rnorm(50, mean = 3.5, sd = 1.7)
sigma  <- 1        # known population sd
mu_0   <- 3        # hypothesized mean
alpha  <- 0.05     # significance level
H1     <- "mu>mu_0"

result <- test_of_hypothesis(
  approach  = "parametric",
  x         = x,
  sigma_x   = sigma,
  mu_0      = mu_0,
  alpha     = alpha,
  H1        = H1
)

print(result)
```

---

## 📑 Function Reference

`test_of_hypothesis(approach, independent = NULL, x, y = NULL, mu_0 = NULL,  
                   sigma_x = NULL, sigma_y = NULL, sigma_d = NULL,  
                   n1 = NULL, n2 = NULL, B = NULL, alpha, H1)`

| Argument     | Description                                                                                   |
|--------------|-----------------------------------------------------------------------------------------------|
| `approach`   | `"parametric"` or `"non_parametric"`                                                          |
| `independent`| `TRUE` for independent two-sample tests, `FALSE` for paired tests (only for parametric)     |
| `x`          | Numeric vector, data for group 1 (or only sample for one-sample tests)                       |
| `y`          | Numeric vector, data for group 2 (if applicable)                                             |
| `mu_0`       | Hypothesized population mean (for one-sample tests)                                          |
| `sigma_x`    | Known population SD of `x` (for Z‑tests)                                                      |
| `sigma_y`    | Known population SD of `y` (for two-sample Z‑tests)                                          |
| `sigma_d`    | Known SD of paired differences (for paired Z‑tests)                                          |
| `n1`, `n2`   | Sample sizes or group counts (for ANOVA or chi‑square tests)                                 |
| `B`          | Number of bootstrap replicates (for non‑parametric tests)                                    |
| `alpha`      | Significance level (e.g., `0.05`)                                                             |
| `H1`         | Alternative hypothesis as a string, e.g. `"mu>mu_0"`, `"means differ"`, or `"association"`   |

---

## 🧪 Examples

### One‑Sample T‑Test

```r
x     <- rnorm(20, mean = 5, sd = 2)
mu_0  <- 4.5
alpha <- 0.05
H1    <- "mu<mu_0"

test_of_hypothesis(
  approach = "parametric",
  x        = x,
  mu_0     = mu_0,
  alpha    = alpha,
  H1       = H1
)
```

### Paired Two‑Sample T‑Test

```r
pre  <- rnorm(30, mean = 100, sd = 15)
post <- pre + rnorm(30, mean = 5, sd = 10)

test_of_hypothesis(
  approach     = "parametric",
  independent  = FALSE,
  x            = pre,
  y            = post,
  alpha        = 0.01,
  H1           = "mu>mu_0"
)
```

### One‑Way ANOVA

```r
scores <- c(22, 42, 44, 52, 45, 37, 52, 33, 8, 47, 43, 32, 16, 24, 19, 18, 34, 39)
group  <- rep(c("A","B","C"), each = 6)

test_of_hypothesis(
  approach = "parametric",
  x        = group,
  y        = scores,
  n1       = 3,
  n2       = 6,
  alpha    = 0.05,
  H1       = "means differ"
)
```

### Bootstrap Test

```r
x <- rnorm(12, 10, 1)
y <- rnorm(1000, 20, 5)

test_of_hypothesis(
  approach = "non_parametric",
  x        = x,
  y        = y,
  B        = 1000,
  alpha    = 0.05,
  H1       = "treatment effect exists"
)
```

---

## 👥 Group Members

- Fahmida Akter Keya  
- Kazi Anika Hayder  
- Shafrin Mardia  
- Md Omar Faruk  
- Montasir Affan 

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

