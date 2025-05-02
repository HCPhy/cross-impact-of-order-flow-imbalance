# OFI Cross-Impact Analysis

This project calculates various types of **Order Flow Imbalance (OFI)** based on the methodology described in:

> Cont, Rama, Mihai Cucuringu, and Chao Zhang. "Cross-Impact of Order Flow Imbalance in Equity Markets," Quantitative Finance, 23(10), 1373–1393 (2023).

This repository was created as part of the Quantitative Internship trial project at **Blockhouse**.

---

## Table of Contents

1. [Project Structure](#project-structure)
2. [Features](#features)
3. [Getting Started](#getting-started)
4. [Usage](#usage)
5. [Results](#results)
6. [License & Acknowledgements](#license--acknowledgements)

---

## Project Structure

```
<repo root>
├── src/             # Source modules for OFI computation
├── data/            # Sample CSV data for benchmarks and demos
├── OFI.ipynb        # Jupyter notebook for end-to-end workflow
└── README.md        # This file
```

---

## Features

* **Best-Level OFI**: Net imbalance at the top of book (level 0).

* **Multi-Level OFI**: Imbalances across the first M levels (default M=10), normalized by total depth.

* **Integrated OFI**: Single scalar summarizing multi-level OFI via the first principal component (no mean subtraction).

* **Cross-Asset Impact**: Estimate contemporaneous and predictive cross-impact via LASSO:

  $r_{i,t}^{h} = \alpha_i + \sum_j \beta_{i,j}\,\mathrm{ofi}_{j,t}^h + \eta_{i,t}$

* **Log-Returns**: Event-level logarithmic returns:
  $\log\frac{P_{i,t}}{P_{i,t-h}}$

---

## Getting Started

1. **Clone the repository**

   ```bash
   gh repo clone HCPhy/cross-impact-of-order-flow-imbalance
   cd cross-impact-of-order-flow-imbalance
   ```

2. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

3. **Data**
   Place your raw order book CSV files in the `data/` directory.

---

## Usage

* **Notebook**: Open `OFI.ipynb` to follow a full example from data import to visualization.
* **Scripts**: Use modules in `src/`, for example:

  ```python
  from src.compute_mid_price import compute_mid_price
  from src.compute_ofi import compute_multi_level_ofi_rolling, compute_integrated_ofi
  from src.compute_cross_impact import fit_cross_impact_lasso
  ```

---

## Results

* Sample plots and benchmark metrics are in the notebook.
* Best-level OFI explains \~50–70% of next-tick price moves on large-cap stocks.
* Sparse cross-impact matrices reveal key inter-stock influences.

---

## License & Acknowledgements

* **License**: MIT
* Based on research by Cont, Cucuringu & Zhang (2023).
* Developed for the Blockhouse Quant Internship Trial.
