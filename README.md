# Dataset Feature Selection

> Forward selection and backward elimination implemented in C++ to identify optimal feature subsets using 1-NN leave-one-out cross-validation.

**[Live Interactive Demo →](https://ActualCookie88.github.io/Dataset-Feature-Selection/visualizer.html)**

---

## Overview

This project implements two greedy search strategies for feature selection: forward selection and backward elimination. Both are evaluated using a 1-nearest-neighbor classifier with leave-one-out cross-validation (LOOCV). Applied to the UCI Wine dataset (178 samples, 13 features, 3 classes), forward selection identifies a 2-feature subset `{6, 15}` that achieves **95.8% accuracy**, compared to 72% using all 13 features, demonstrating that irrelevant features actively harm a nearest-neighbor classifier.

The project also includes an interactive browser-based visualizer for exploring algorithm behavior across feature subset sizes.

---

## Features

- **Forward selection** - greedily adds the single feature that most improves LOOCV accuracy at each step, from an empty set to the full feature set
- **Backward elimination** - starts with all features and greedily removes the least useful one per step
- **Precomputed distance matrix** - squared per-feature distances are cached before search, reducing redundant computation across LOOCV evaluations
- **Early termination** - Euclidean distance accumulation short-circuits when the running sum already exceeds the current nearest-neighbor distance
- **Custom dataset support** - accepts any whitespace-delimited text file where the first column is the class label
- **Run log output** - writes full per-level accuracy traces to `output/output.txt` for analysis

---

## Tech Stack

| | |
|---|---|
| Language | C++17 |
| Build | `g++` (no external dependencies) |
| Dataset | [UCI Wine (ID 109)](https://archive.ics.uci.edu/dataset/109/wine) |
| Visualizer | Vanilla HTML/CSS/JS + Chart.js |

---

## Getting Started

```bash
git clone https://github.com/ActualCookie88/Dataset-Feature-Selection.git
cd Dataset-Feature-Selection
g++ -std=c++17 feature_selection.cpp -o feature_selection
```

```bash
./feature_selection        # Linux/macOS
feature_selection.exe      # Windows
```

You will be prompted to select a dataset (small, large, or custom) and an algorithm. Results are printed to the terminal and saved to `output/output.txt`.

---

## How It Works

**Search strategy.** Both algorithms perform a greedy search over the feature power set. At each level of the search tree, every candidate feature is evaluated by temporarily adding or removing it and measuring LOOCV accuracy. The best-performing candidate is committed, and the process repeats until all features have been added (forward) or removed (backward).

**Evaluation.** LOOCV with 1-NN classifies each instance by finding its nearest neighbor among all other instances, using only the current candidate feature subset. Euclidean distance is computed over selected features only, with early termination once the accumulated distance exceeds the current best — a meaningful speedup on large feature sets.

**Distance precomputation.** Before search begins, squared per-feature distances between all instance pairs are stored in a 3D matrix `featureDistance[i][k][f]`. This avoids recomputing raw distances during the inner LOOCV loop, at the cost of O(n² · F) memory.

**Results on UCI Wine (16 features, small dataset):**

| Algorithm | Best subset | Accuracy |
|---|---|---|
| Forward selection | `{6, 15}` | **95.8%** |
| Backward elimination | `{6, 15, 2}` (3 features) | **94.0%** |
| Baseline (all features) | all 16 | 72.0% |

---

## Known Limitations

- Both algorithms are greedy and do not backtrack — they can miss globally optimal subsets
- Performance degrades on very large datasets (the large 64-feature dataset runs noticeably slowly)
- The visualizer uses representative data rather than being directly wired to program output

---

## Acknowledgements

Completed as part of **CS170: Introduction to Artificial Intelligence** at the University of California, Riverside. Dataset sourced from the [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/109/wine).
