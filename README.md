# Data Set Feature Selection  

By Luke Matsunaga  

Project completed as part of an Intro to Artificial Intelligence course.  

Focus: Implementing feature selection algorithms for improving classification performance.

This project implements feature selection techniques in C++ to evaluate and identify the most relevant features in a dataset using:

- Forward Selection  
- Backward Elimination  
- Nearest Neighbor evaluation (leave-one-out validation)

## Prerequisites
- C++17 compiler (GCC, Clang, or MSVC)

## Features
- Supports custom datasets (text file input)  
- Evaluates feature subsets using accuracy metrics  
- Outputs best feature subset and corresponding accuracy  
- Tracks performance across search steps  
- Modular and readable C++ implementation  

## Concepts Covered
- Feature selection in machine learning  
- Search strategies in feature space  
- Model evaluation using classification accuracy  
- Trade-offs between feature subset size and performance

## Dataset: UCI Wine
- I also ran Forward Selection and Backward Elimination a real public dataset
- Results and details can be found in the project report linked at the bottom
- Link to dataset: https://archive.ics.uci.edu/dataset/109/wine

## Interactive Demo
Below is a link to an interactive visual demo of the feature selection algorithms.
[Link here](https://ActualCookie88.github.io/Dataset-Feature-Selection/docs/visualizer.html)

## Building the Project
1. Clone the repo
```bash
git clone https://github.com/ActualCookie88/Dataset-Feature-Selection.git
```
2. Build executable
```bash
g++ -std=c++17 feature_selection.cpp -o feature_selection
```

## Running the Program
```bash
./feature_selection        # Linux/macOS
feature_selection.exe      # Windows
```

You will be prompted to:

Choose an existing dataset file or provide your own
Choose the algorithm (Forward Selection or Backward Elimination)

Note: the program may seem frozen for large datasets, but it is simply slow

## Output

The program displays:
- Accuracy of each feature subset
- Best feature subset found
- Final classification accuracy
- Program runtime

## Report
For detailed results and analysis, see project report:
[View Project Report](docs/Feature-SelectionProjectReport.pdf)
