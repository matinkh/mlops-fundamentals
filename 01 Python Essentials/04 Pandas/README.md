# 4. Pandas

What we'll cover here:

* Basic Pandas
* Working with DataFrames
* Numpy Basics

## 4.1 Basic Pandas Usage

### Key Terms

* **DataFrame:** A two-dimensional data structure inside Pandas; with rows and columns.
* **Series:** A one-dimensional array with axis label. (DataFrame column)
* **Loading:** Reading data into a DataFrame.
* **Exploratory analysis:** Initial investigation of data to understand its characteristics.
* **Exporting:** Saving data from a DataFrame to another format like CSV.



**DataFrame**

```python
import pandas as pd

data = [[1, 2, 3],
        [4, 5, 6],
        [7, 8, 9]]

colnames = ['apples', 'bananas', 'oranges']
index = ['Monday', 'Tuesday', 'Wednesday']

df = pd.DataFrame(data, index, colnames)
```

**Loading data**

```python
csv_url = "~/Desktop/my_data.csv"
df = pd.read_csv(csv_url, index_col=0)  # First column as index - optional
```

**Writing data**

```python
out_csv_url = "~/Desktop/processed_data.csv"
pd.to_csv(df, out_csv_url)
```

**Exploring data**

* **describe:** Statistics about each column
* **head:** Shows a few rows from the DataFrame
* **info:** Brief summary of the entire DataFrame



## 4.2 Working with DataFrames

### Key Terms

* **Manipulation:** Transforming, filtering, cleaning DataFrame after loading.
* **Visualization:** Creating charts and plots from DataFrame data.

### Common Operations

* Load data: `pd.read_csv()`

* Columns: `df["colname"]` or `df[["colname1", "colname2"]]`

* Rows - Filtering: `df[df["rating"] > 4]`

* Rows - Query: `df.query("rating > 93 & level == 'L5'")`

* Manipulation

  * Replace

    ```python
    df["variety_short"] = df["variety"].replace({"Red Wine": "R", "White Wine": "W"})
    ```

  * String Split

    ```python
    df["region_short"] = df["region"].str.split().str.get(-1)  # Get the last part
    ```

  * Apply (instead of loop)

    ```python
    def good_wine(value):
      return value > 94
    
    df["good"] = df["rating"].apply(good_wine)
    ```

* Visualization

  ```python
  from matplotlib import pyplot as plt
  
  # Plot everything
  df.plot()
  plt.show()
  
  # Plot one column
  df["rating"].plot()
  plt.show()
  
  # Scatter plot
  df.plot.scatter(x="rating", y="variety", alpha=0.5)
  plt.show()
  ```



## 4.3 NumPy Basics

### Key Terms

* **Array:** Primary data structure in NumPy; n-dimensional grid of values.
* **Reshape:** Transform an array into a new shape with the same elements.
* **Ravel:** Flatten an array into one dimensional shape.
* **Stack:** Vertically or horizontally concatenate arrays.
* **Slice:** Extract subset of array elements using indexing.

```python
# Array
array = np.array([1, 2, 3, 4, 5])

# 2D Array
array = np.array([[1, 2], [3, 4]])

# 2D random floats
array = np.random.rand(2, 2)

# A sequence
seq = np.arange(0, 27, 3)
```

**Array operations**

* Expanding

  ```python
  array = np.ones((4,))
  expanded = array[np.newaxis, :]  # expand one row
  ```

* Stacking

  ```python
  first = np.full((2, 12), 2)
  second = np.full((2, 7), 2)
  third = np.hstack((first, second))  # A (2, 19) array
  ```