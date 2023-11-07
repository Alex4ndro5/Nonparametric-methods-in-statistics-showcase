# Nonparametric Methods in Statistics Showcase

This project consists of Jupyter Notebooks that showcase different nonparametric methods in statistics. It provides educational materials and code examples for understanding and applying these methods.

## Table of Contents

- [Introduction](#introduction)
- [Notebooks](#notebooks)
- [Sample Code](#sample-code)
- [Contributing](#contributing)
- [License](#license)

## Introduction

Nonparametric methods are essential tools in statistics for analyzing data when certain distributional assumptions are not met. This project aims to provide a comprehensive understanding of nonparametric methods and how to implement them using Python. Each notebook in the collection focuses on a specific nonparametric method and provides code examples, explanations, and demonstrations.

## Notebooks

Explore the collection of Jupyter Notebooks, each dedicated to a specific nonparametric method.
Each notebook includes explanations, code samples, and interactive elements to help you learn and apply nonparametric methods effectively.

## Sample Code

Here's a sample code snippet from one of the notebooks, showcasing a simulation of the t-distribution with different degrees of freedom and power calculations for nonparametric tests:

```python
# Symulacja rozkładu normalnego
def simulate_powers(n_samples, df_values):
    powers = []
    n_tests = 3

    for df in df_values:
        df_powers = np.zeros((n_tests, len(n_samples)))

        for i, n in enumerate(n_samples):
            data = stats.t.rvs(df, size=n)
            norm = stats.norm.rvs(size=n)
            data = (data - np.mean(data)) / np.std(data, ddof=1)

            # Test Shapiro-Wilka
            _, sw_pval = stats.shapiro(data)
            sw_power = 1 - sw_pval
            df_powers[0, i] = sw_power

            # Test Kolmogorov-Smirnova
            _, ks_pval = stats.kstest(data, 'norm')
            ks_power = 1 - ks_pval
            df_powers[1, i] = ks_power

            # Test Chi-squared 
            hist, _ = np.histogram(data, bins='auto')
            _, chi_pval = stats.chisquare(hist)
            chi_power = 1 - chi_pval
            df_powers[2, i] = chi_power

        powers.append(df_powers)

    return powers

np.random.seed(seed=411052)
n_samples = np.arange(5, 200, 3)
df_values = np.array([3, 5, 10, 50, 100])

powers = simulate_powers(n_samples, df_values)
```
## Contributing
We welcome contributions to this project. If you have additional nonparametric methods or improvements to the existing notebooks, please consider contributing. Follow our Contribution Guidelines to get started.

## License
This project is licensed under the MIT License. See the LICENSE file for more details.

For more information and access to all the notebooks, visit our GitHub repository.
