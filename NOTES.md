# NumPy Tutorial Notebook

## Overview

This repository contains a Jupyter Notebook (`numpy.ipynb`) that serves as a comprehensive tutorial for the NumPy library in Python. It covers fundamental concepts, array manipulation techniques, mathematical operations, and practical examples, including data analysis and vector operations.

## Purpose

The primary goal of this notebook is to provide a hands-on learning experience for understanding and utilizing NumPy for numerical computing, data analysis, and scientific applications. It demonstrates key features and performance advantages of NumPy arrays over standard Python lists.

## Contents

The notebook is structured into several phases:

1.  **Phase I: NumPy Basics**
    *   Importing NumPy.
    *   Creating NumPy arrays from lists and using built-in functions (`zeros`, `ones`, `full`, `arange`, `random`).
    *   Comparison between Python lists and NumPy arrays (operations, performance).
    *   Understanding Vectors, Matrices, and Tensors.
    *   Exploring array properties (`shape`, `ndim`, `size`, `dtype`).
    *   Array reshaping (`reshape`, `flatten`, `ravel`, `T`).

2.  **Phase II: NumPy Array Operations**
    *   Indexing and slicing (1D and 2D arrays).
    *   Sorting arrays (`np.sort`, `axis` parameter).
    *   Filtering arrays using boolean indexing and masks.
    *   Fancy indexing and the `np.where()` function.
    *   Adding and removing data (`concatenate`, `vstack`, `hstack`, `delete`).
    *   Array compatibility basics.

3.  **Phase III: Advanced Operations with Business Examples**
    *   Applying NumPy for a sample sales data analysis (Zomato example).
    *   Calculating aggregations (`sum`, `min`, `max`, `mean`) along axes.
    *   Cumulative sums (`np.cumulative_sum`).
    *   Basic vector operations (addition, multiplication, dot product, angle).
    *   Vectorized operations using `np.vectorize` and direct array operations.
    *   Data visualization with Matplotlib.

4.  **Phase IV: File Operations**
    *   Saving NumPy arrays to `.npy` files using `np.save()`.
    *   Loading NumPy arrays from `.npy` files using `np.load()`.

## Usage

### Prerequisites

*   Python 3.x
*   Jupyter Notebook or JupyterLab
*   Required Libraries:
    *   NumPy
    *   Matplotlib

### Installation

You can install the necessary libraries using pip:

```bash
pip install numpy matplotlib jupyterlab
```

### Running the Notebook

1.  Clone this repository:
    ```bash
    git clone <repository-url>
    cd <repository-directory>
    ```
2.  Start JupyterLab:
    ```bash
    jupyter lab
    ```
3.  Open the `numpy.ipynb` file from the JupyterLab interface.
4.  Run the cells sequentially to follow the tutorial and execute the code examples.
