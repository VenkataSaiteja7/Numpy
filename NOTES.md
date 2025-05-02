# NumPy Tutorial Notes

This document contains notes based on the `numpy.ipynb` Jupyter Notebook, covering fundamental and advanced concepts of the NumPy library in Python.

## Phase I: NumPy Basics

### Introduction

Import the NumPy library, typically aliased as `np`.

```python
import numpy as np
import time
import matplotlib.pyplot as plt
```

### Creating Arrays

#### From Lists

NumPy arrays can be created from Python lists using `np.array()`.

-   **1D Array:**
    ```python
    arr_1d  = np.array([1,2,3,4,5])
    print("1D array : ",arr_1d)
    # Output: 1D array :  [1 2 3 4 5]
    ```
-   **2D Array:** Note that for multi-dimensional arrays, the list must be nested correctly.
    ```python
    arr_2d = np.array([[1,2,3],[4,5,6]])
    print("2D array : \n",arr_2d)
    # Output:
    # 2D array :
    #  [[1 2 3]
    #  [4 5 6]]
    ```

#### List vs. NumPy Array

-   **Operations:** Standard Python list multiplication duplicates the list, while NumPy array multiplication performs element-wise operations.
    ```python
    py_list = [1,2,3]
    print("python list multiplication : ", py_list*2)
    # Output: python list multiplication :  [1, 2, 3, 1, 2, 3]

    np_array = np.array([1,2,3])
    print("python numpy multiplication : ", np_array*2)
    # Output: python numpy multiplication :  [2 4 6]
    ```
-   **Performance:** NumPy operations are generally much faster than equivalent operations on standard Python lists, especially for large datasets.
    ```python
    # Timing comparison (example)
    start = time.time()
    py_list = [i*2 for i in range(1000000)]
    print("\n List operation time : ", time.time() - start)

    start = time.time()
    np_array = np.arange(1000000)*2
    print("\n np array operation time : ", time.time() - start)
    # Output (example times):
    #  List operation time :  0.085...
    #  np array operation time :  0.023...
    ```

#### Creating Arrays from Scratch

NumPy provides functions to create arrays with initial placeholder content:

-   `np.zeros()`: Creates an array filled with zeros.
    ```python
    zeros = np.zeros((3,4))
    print("zeros array : \n", zeros)
    # Output:
    # zeros array :
    #  [[0. 0. 0. 0.]
    #  [0. 0. 0. 0.]
    #  [0. 0. 0. 0.]]
    ```
-   `np.ones()`: Creates an array filled with ones.
    ```python
    ones = np.ones((2,3))
    print("ones array : \n", ones)
    # Output:
    # ones array :
    #  [[1. 1. 1.]
    #  [1. 1. 1.]]
    ```
-   `np.full()`: Creates an array filled with a specified value.
    ```python
    full = np.full((2,2),7)
    print("full array : \n", full)
    # Output:
    # full array :
    #  [[7 7]
    #  [7 7]]
    ```
-   `np.random.random()`: Creates an array with random values between 0 and 1.
    ```python
    random = np.random.random((2,3))
    print("random array : \n", random)
    # Output: (Example random values)
    # random array :
    #  [[0.40... 0.49... 0.45...]
    #  [0.51... 0.22... 0.78...]]
    ```
-   `np.arange()`: Creates an array with a sequence of numbers (similar to Python's `range`, but returns an array).
    ```python
    sequence = np.arange(0,11,2) # end is exclusive
    print("sequence array : \n", sequence)
    # Output: sequence array :  [ 0  2  4  6  8 10]
    ```

### Vector, Matrix, and Tensor

NumPy arrays can represent these mathematical concepts:

-   **Vector (1D Array):**
    ```python
    vector = np.array([1,2,3])
    print("Vector : \n", vector)
    ```
-   **Matrix (2D Array):**
    ```python
    matrix = np.array([[1,2,3],
                       [4,5,6]])
    print("matrix : \n", matrix)
    ```
-   **Tensor (3D+ Array):**
    ```python
    tensor = np.array([[[1,2],[3,4]],
                        [[5,6],[7,8]]])
    print("Tensor : \n",tensor)
    ```

### Array Properties

Key attributes of NumPy arrays:

-   `shape`: Returns a tuple representing the dimensions (rows, columns, ...).
-   `ndim`: Returns the number of dimensions.
-   `size`: Returns the total number of elements.
-   `dtype`: Returns the data type of the elements.

```python
arr = np.array([[1,2,3],
                [4,5,6]])

print("Shape : ",arr.shape)       # Output: Shape :  (2, 3)
print("Dimension : ",arr.ndim)     # Output: Dimension :  2
print("Size : ",arr.size)         # Output: Size :  6
print("DataType : ",arr.dtype)     # Output: DataType :  int64
```

### Array Reshaping

Modifying the shape of an array:

-   `reshape()`: Returns a new array with the specified shape. The total size must remain the same.
    ```python
    arr = np.arange(12)
    reshaped = arr.reshape((3,4))
    print("Reshaped array : \n", reshaped)
    # Output:
    # Reshaped array :
    #  [[ 0  1  2  3]
    #  [ 4  5  6  7]
    #  [ 8  9 10 11]]
    ```
-   `flatten()`: Returns a 1D copy of the array.
    ```python
    flattened = reshaped.flatten()
    print("flattened array : \n", flattened)
    # Output: flattened array : [ 0  1  2  3  4  5  6  7  8  9 10 11]
    ```
-   `ravel()`: Returns a 1D view of the array (modifying the raveled array might modify the original).
    ```python
    raveled = reshaped.ravel()
    print("\n raveled array : ",raveled)
    # Output: raveled array :  [ 0  1  2  3  4  5  6  7  8  9 10 11]
    ```
-   `.T` (Transpose): Swaps rows and columns.
    ```python
    transpose = reshaped.T
    print("\n Transpose array : \n", transpose)
    # Output:
    #  Transpose array :
    #  [[ 0  4  8]
    #  [ 1  5  9]
    #  [ 2  6 10]
    #  [ 3  7 11]]
    ```

## Phase II: NumPy Array Operations

### Indexing and Slicing

#### 1D Arrays

Similar to Python lists, but with extended capabilities.

-   **Basic Slicing:** `arr[start:stop:step]`
    ```python
    arr = np.array([1,2,3,4,5,6,7,8,9,10])
    print("Basic Slicing : ", arr[2:7])     # Output: [3 4 5 6 7]
    print("With Step :", arr[1:8:2])        # Output: [2 4 6 8]
    ```
-   **Negative Indexing:** Access elements from the end.
    ```python
    print("Negative indexing : ", arr[-4])   # Output: 7
    ```

#### 2D Arrays

Use comma-separated indices for dimensions `arr[row, column]`.

```python
arr_2d = np.array([[1,2,3],
                   [4,5,6],
                   [7,8,9]])

print("Specific Element : ", arr_2d[1,2]) # Output: 6 (row 1, col 2)
print("Entire Row : ", arr_2d[1])         # Output: [4 5 6] (row 1)
print("Entire Row (alt): ", arr_2d[1,:])   # Output: [4 5 6]
print("Entire Col : ", arr_2d[:,1])       # Output: [2 5 8] (col 1)
```

### Sorting

-   `np.sort()`: Returns a sorted copy of the array.
    ```python
    unsortedArr = np.array([2,4,2,77,44,78,23,45,67,23,12,34,64])
    print("Sorted Array : ", np.sort(unsortedArr))
    # Output: [ 2  2  4 12 23 23 34 44 45 64 67 77 78]
    ```
-   **Sorting 2D Arrays:** Use the `axis` parameter:
    -   `axis=0`: Sort along columns.
    -   `axis=1`: Sort along rows.
    ```python
    arr_2d_unsorted = np.array([[3,4],
                                [90,56],
                                [34,6]])
    print("Sort 2D array by column (axis=0) : \n", np.sort(arr_2d_unsorted,axis=0))
    # Output:
    # [[ 3  4]
    #  [34  6]
    #  [90 56]]
    print("Sort 2D array by row (axis=1) : \n", np.sort(arr_2d_unsorted,axis=1))
    # Output:
    # [[ 3  4]
    #  [56 90]
    #  [ 6 34]]
    ```

### Filtering Arrays (Boolean Indexing)

Create new arrays by filtering based on conditions.

-   **Direct Boolean Expression:**
    ```python
    numbers = np.array([1,2,3,4,5,49,34,56,75,34])
    even_numbers = numbers [numbers % 2 == 0]
    print("even numbers : ", even_numbers)
    # Output: [ 2  4 34 56 34]
    ```
-   **Using a Mask:** A mask is a boolean array created from a condition.
    ```python
    mask = numbers > 5
    print("Numbers greater than 5 : ", numbers[mask])
    # Output: [49 34 56 75 34]
    ```

### Fancy Indexing vs. `np.where()`

-   **Fancy Indexing:** Accessing multiple array elements using a list or array of indices.
    ```python
    indices = [0,2,4]
    print("Accessed values using index list: ", numbers[indices])
    # Output: [1 3 5]
    ```
-   **`np.where(condition)`:** Returns the *indices* of elements where the condition is True.
    ```python
    where_result = np.where(numbers > 5) # Returns a tuple containing an array of indices
    print("where condition output (indices) : ", where_result)
    # Output: (array([5, 6, 7, 8, 9]),)
    print("Accessing array values using where indices : ", numbers[where_result])
    # Output: [49 34 56 75 34]
    ```
-   **`np.where(condition, x, y)`:** Returns elements from `x` where `condition` is True, and elements from `y` where it's False.
    ```python
    # Example: Multiply numbers > 5 by 5, keep others the same
    example_array = np.where(numbers > 5 , numbers * 5, numbers)
    print(example_array)
    # Output: [  1   2   3   4   5 245 170 280 375 170]
    ```

### Adding and Removing Data

-   **Concatenating:** Combine arrays. Use `np.concatenate()`. Direct addition `+` performs element-wise addition.
    ```python
    arr1 = np.array([1,2,3])
    arr2 = np.array([4,5,6])

    # Incorrect (element-wise addition): arr1 + arr2 -> [5 7 9]

    # Correct way to combine:
    combined_arr = np.concatenate((arr1,arr2))
    print("combined array : ", combined_arr)
    # Output: [1 2 3 4 5 6]
    ```
-   **Stacking:** Combine arrays along a new axis.
    -   `np.vstack()`: Stack vertically (add rows). Shapes must be compatible except for the first axis.
    -   `np.hstack()`: Stack horizontally (add columns). Shapes must be compatible except for the second axis.
    ```python
    original_arr = np.array([[1,2],[3,4]])
    new_row = np.array([[5,6]])
    with_new_row = np.vstack((original_arr,new_row))
    print("row added vertically : \n" , with_new_row)
    # Output:
    # [[1 2]
    #  [3 4]
    #  [5 6]]

    new_col = np.array([[7],[8]])
    with_new_col = np.hstack((original_arr,new_col))
    print("\n column added horizontally: \n", with_new_col)
    # Output:
    # [[1 2 7]
    #  [3 4 8]]
    ```
-   **Deleting:** Remove elements using `np.delete()`.
    ```python
    arr = np.array([1,2,3,4,5,6,7,8,9,10])
    new_arr = np.delete(arr, 2) # Delete element at index 2
    print("new array after deleting index 2 : ", new_arr)
    # Output: [ 1  2  4  5  6  7  8  9 10]
    ```

### Array Compatibility (Broadcasting)

NumPy allows operations on arrays of different but compatible shapes. (The notebook only checks shape equality, but broadcasting is a broader concept).

```python
arr1 = np.array([1,2,3])
arr2 = np.array([4,5,6])
print("Compatibility Shapes : ", arr1.shape == arr2.shape) # Output: True
```
*Note: Broadcasting rules allow operations like adding a scalar to an array or adding a (1, n) array to an (m, n) array.*

## Phase III: Advanced Operations with Examples

### Business Example: Zomato Sales Analysis

Using NumPy for data analysis on sample sales data.

```python
# Data structure: [restaurant_id, 2021, 2022, 2023, 2024]
sales_data = np.array([
    [1, 150000, 180000, 220000, 250000],   # Paradise Biryani
    [2, 120000, 140000, 160000, 190000],   # Beijing Bites
    [3, 200000, 230000, 260000, 300000],   # Pizza Hub
    [4, 180000, 210000, 240000, 270000],   # Burger Point
    [5, 160000, 185000, 205000, 230000]    # Chai Point
])

print("Sales data shape", sales_data.shape) # Output: (5, 5)

# Accessing Data
print("\n Sampled data for 1st 3 restaurants : \n", sales_data[:3])
print("\n Sales data (all rows, columns 1 onwards) : \n", sales_data[:,1:])
```

#### Aggregations (`sum`, `min`, `max`, `mean`)

Use the `axis` parameter to control aggregation direction:

-   `axis=0`: Aggregate down the columns.
-   `axis=1`: Aggregate across the rows.

```python
# Extract sales figures only
sales_figures = sales_data[:,1:]

# Total Sales per Year (sum down columns)
yearly_total = np.sum(sales_figures, axis=0)
print("Yearly Sales (Column wise sum) : \n", yearly_total)
# Output: [ 810000  945000 1085000 1240000]

# Total Sales per Restaurant (sum across rows)
restaurant_total = np.sum(sales_figures, axis=1)
print("Total Sales per Restaurant (Row wise sum) : \n", restaurant_total)
# Output: [800000 610000 990000 900000 780000]

# Minimum Sales per Year (min down columns)
min_sales_yearly = np.min(sales_figures, axis=0)
print("Minimum sales per year (column wise min) : ",min_sales_yearly)
# Output: [120000 140000 160000 190000]

# Maximum Sales per Year (max down columns)
max_sales_yearly = np.max(sales_figures, axis=0)
print("Max Sales per year (column wise max) : ", max_sales_yearly)
# Output: [200000 230000 260000 300000]

# Average Sales per Restaurant (mean across rows)
avg_sales_restaurant = np.mean(sales_figures, axis=1)
print("Average sales per restaurant : ", avg_sales_restaurant)
# Output: [200000. 152500. 247500. 225000. 195000.]
```

#### Cumulative Sum

`np.cumulative_sum()` calculates the cumulative sum along an axis.

```python
cum_sum_sales = np.cumulative_sum(sales_figures, axis=1)
print("Cumulative Sales per Restaurant : \n", cum_sum_sales)
# Output:
# [[150000 330000 550000 800000]
#  [120000 260000 420000 610000]
#  [200000 430000 690000 990000]
#  [180000 390000 630000 900000]
#  [160000 345000 550000 780000]]

# Plotting average cumulative sales
plt.figure(figsize=(10,6))
plt.plot(np.mean(cum_sum_sales, axis=0)) # Mean of cumulative sums per year
plt.title("Average Cumulative Sales across all restaurants ")
plt.xlabel("Years (Index: 0=2021, 1=2022, etc.)") # Corrected label
plt.ylabel("Sales")
plt.grid(True)
plt.show()
```

### Vector Operations

Performing operations between vectors (1D arrays).

```python
vector1 = np.array([1,2,3,4,5])
vector2 = np.array([6,7,8,9,10])

# Vector addition (element-wise)
print("Vector addition : \n ",vector1 + vector2)
# Output: [ 7  9 11 13 15]

# Vector multiplication (element-wise)
print("Vector Multiplication : \n ",vector1 * vector2)
# Output: [ 6 14 24 36 50]

# Dot Product
dot_product = np.dot(vector1, vector2)
# print(dot_product) # Output: 130

# Angle between vectors (using dot product and norms)
norm_v1 = np.linalg.norm(vector1)
norm_v2 = np.linalg.norm(vector2)
cos_angle = dot_product / (norm_v1 * norm_v2)
angle_radians = np.arccos(np.clip(cos_angle, -1.0, 1.0)) # Clip for precision issues
print("Angle (radians): ", angle_radians)
# Output: 0.2655...
```

### Vectorized Operations

Applying functions element-wise to arrays efficiently without explicit loops.

-   `np.vectorize()`: Creates a vectorized function from a standard Python function.
    ```python
    restaurant_types = np.array(["biryani",'chinese','pizza','burger',"cafe"])
    vectorized_upper = np.vectorize(str.upper)
    print("Vectorized Upper : ", vectorized_upper(restaurant_types))
    # Output: ['BIRYANI' 'CHINESE' 'PIZZA' 'BURGER' 'CAFE']
    ```
-   **Direct Operations:** Many NumPy functions and standard operators are already vectorized.
    ```python
    monthly_avg = (sales_data[:,1:] / 12).round(2)
    print("Monthly Average : \n ", monthly_avg)
    # Output: (Calculated monthly averages)
    ```

## Phase IV: File Operations

### Saving NumPy Arrays

-   `np.save()`: Saves a single array to a binary file (`.npy`).
    ```python
    arr1 = np.array([[1,2,3],[4,5,6]])
    arr2 = np.random.rand(3,3)
    np.save('arr1.npy', arr1)
    np.save('arr2.npy', arr2)
    ```
-   `np.savez()`: Saves multiple arrays into a single uncompressed archive (`.npz`).
-   `np.savez_compressed()`: Saves multiple arrays into a single compressed archive (`.npz`).

### Loading NumPy Arrays

-   `np.load()`: Loads arrays from `.npy` or `.npz` files.
    ```python
    loaded_array = np.load('arr1.npy')
    print("loaded array : ", loaded_array)
    # Output: [[1 2 3] [4 5 6]]
    ```
    *Note: The notebook example loads `arr1.npy` but prints a 1D array `[1 2 3 4 5]`, suggesting the file might have been overwritten or the example output is incorrect.*
