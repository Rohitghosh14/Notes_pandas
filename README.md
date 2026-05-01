# 📊 NumPy & Pandas — Study Notes

Personal study notes and hands-on practice for **NumPy** and **Pandas** — two of the most essential libraries on any Python Data Science or AI/ML path.

This repo is a living reference I keep adding to as I learn. Not a polished tutorial — just real code, real comments, and real examples I wrote while learning.

---

## 📁 Repo Structure

```
numpy-pandas-notes/
│
├── numpy_file.ipynb      # All NumPy notes — arrays, operations, dimensions, statistics
├── pandas_file.ipynb     # All Pandas notes — DataFrames, filtering, updating, analysis
├── orders.csv            # Real dataset used for Pandas practice
├── main.py               # Entry point / scratch file
├── pyproject.toml        # uv project config (Python 3.14+, numpy, pandas)
├── uv.lock               # Locked dependency versions
└── README.md             # This file
```

---

## ⚙️ Setup

This project uses **`uv`** for fast, modern Python environment management.

```bash
# 1. Clone the repo
git clone https://github.com/Rohitghosh14/Notes_pandas.git
cd Notes_pandas

# 2. Create virtual environment
uv venv

# 3. Activate it
# Windows:
.venv\Scripts\activate
# Mac/Linux:
source .venv/bin/activate

# 4. Install dependencies
uv sync

# 5. Launch Jupyter
jupyter notebook
```

**Requirements:** Python 3.14+ · numpy >= 2.4.4 · pandas >= 3.0.2

---

## 🔢 NumPy — `numpy_file.ipynb`

> *NumPy is the backbone of scientific computing in Python. Every ML/Data Science library (pandas, scikit-learn, TensorFlow) is built on top of it.*

---

### 1. NumPy vs Python Lists

```python
python_list = [1, 2, 3, 4, 5]
numpy_array = np.array([1, 2, 3, 4, 5])

# Python list needs a loop to add
[i + 10 for i in python_list]      # ← loop required

# NumPy uses vectorization — operates on entire array at once
numpy_array + 10                    # ← no loop needed ✅
```

**Key difference:** NumPy uses **vectorized operations** — no Python loops, much faster, less code.

---

### 2. 9 Ways to Create Arrays

| Method | Code | Output |
|--------|------|--------|
| From list | `np.array([1,2,3])` | `[1 2 3]` |
| Range | `np.arange(0, 10, 2)` | `[0 2 4 6 8]` |
| Evenly spaced | `np.linspace(0, 1, 5)` | `[0. .25 .5 .75 1.]` |
| All zeros | `np.zeros(5)` | `[0. 0. 0. 0. 0.]` |
| All ones | `np.ones(5)` | `[1. 1. 1. 1. 1.]` |
| Filled value | `np.full(6, 7)` | `[7 7 7 7 7 7]` |
| Identity matrix | `np.eye(5)` | 5×5 diagonal matrix |
| Random (uniform) | `np.random.rand(3)` | values between 0–1 |
| Random integers | `np.random.randint(1,14,size=5)` | random ints |

---

### 3. Data Types (`dtype`)

```python
arr_int   = np.array([1, 2, 3])           # int64
arr_float = np.array([1.0, 2.0, 3.0])     # float64
arr_mix   = np.array([1, 2, 3.5])         # float64 (upcasted)

# Specifying dtype manually
arr = np.array([1, 2, 3], dtype=np.float64)

# Converting type
arr.astype(np.float32)
```

---

### 4. Multi-Dimensional Arrays

```
1D → [1, 2, 3]                          shape: (3,)
2D → [[1,2,3], [4,5,6]]                shape: (2, 3)
3D → [[[1,2],[3,4]], [[5,6],[7,8]]]    shape: (2, 2, 2)
```

```python
matrix_2d = np.array([[1,2,3],[4,5,6],[7,8,9]])

matrix_2d.shape      # (3, 3) → rows, columns
matrix_2d.ndim       # 2
matrix_2d.size       # 9 (total elements)
matrix_2d.dtype      # int64
matrix_2d.nbytes     # total bytes in memory
matrix_2d.T          # transpose
```

---

### 5. Indexing & Slicing

```python
# 1D — same as Python lists
arr[0]           # first element
arr[-1]          # last element
arr[0:5]         # slice
arr[6::-2]       # reverse step

# 2D — [row, column]
matrix[0, 0]     # row 0, col 0
matrix[0, :]     # entire first row
matrix[:, 0]     # entire first column
matrix[0:2, 1:3] # sub-matrix

# Boolean Indexing — very powerful!
arr[arr > 5]           # elements greater than 5
arr[arr % 2 == 0]      # even numbers only
```

---

### 6. Array Operations

```python
# Element-wise (a and b are same-shape arrays)
a + b       # addition
a * b       # multiplication
a - b       # subtraction
a / b       # division
a ** b      # power
np.sqrt(a)  # square root

# Scalar (broadcast a single value across the whole array)
a + 10
a * 2
a ** 3

# Comparison (returns a boolean array)
a > 2
a == 3
a <= 2
```

---

### 7. Array Manipulation

```python
arr = np.arange(12)

arr.reshape(4, 3)          # reshape to 4 rows, 3 cols
arr.reshape(2, 2, -1)      # -1 = let NumPy calculate that dimension
arr.flatten()              # collapse any shape back to 1D

matrix.T                   # transpose (flip rows and columns)

# Concatenation
np.vstack((a, b))          # vertical stack (add rows)
np.hstack((a, b))          # horizontal stack (add columns)
np.concatenate((a,b), axis=0)   # same as vstack
np.concatenate((a,b), axis=1)   # same as hstack
```

---

### 8. Dimensions & Axes Explained

```
Think of axes like directions:

2D array:
  axis=0 → collapse down rows    (one result per column)
  axis=1 → collapse across cols  (one result per row)

3D array: shape (2, 3, 4)
  axis=0 → across matrices (depth / pages)
  axis=1 → down rows
  axis=2 → across columns

Shape reading rule:
  (3, 4)       → 3 rows, 4 columns              (2D)
  (2, 3, 4)    → 2 matrices, 3 rows, 4 cols     (3D)
  (2, 2, 3, 4) → 2 tensors, 2 matrices, 3 rows  (4D)
```

---

### 9. Statistical Operations

```python
np.sum(arr)        # total sum
np.mean(arr)       # average
np.median(arr)     # middle value
np.std(arr)        # standard deviation
np.var(arr)        # variance
np.min(arr)        # minimum value
np.max(arr)        # maximum value
np.argmin(arr)     # index of minimum
np.argmax(arr)     # index of maximum

# On 2D arrays, use axis parameter:
np.sum(matrix, axis=0)     # sum of each column
np.mean(matrix, axis=1)    # mean of each row
```

---

### 10. Useful Array Methods

```python
np.sort(arr)               # returns sorted copy (original unchanged)
arr.sort()                 # sorts in-place (original changes)

np.where(arr > 5)          # indices where condition is True
arr[np.where(arr > 5)]     # values where condition is True

np.unique(arr)             # remove duplicates, return sorted unique values
```

---

### 11. Real Example — Student Score Analysis

```python
scores = np.array([
    [85, 95, 88],   # student 1
    [92, 87, 91],   # student 2
    [78, 82, 80],   # student 3
    [95, 98, 96],   # student 4
    [88, 85, 90],   # student 5
])

student_avg = np.mean(scores, axis=1)   # avg per student (collapse columns)
test_avg    = np.mean(scores, axis=0)   # avg per test (collapse rows)

np.argmax(student_avg)    # index of best student → student 4
np.argmin(test_avg)       # index of hardest test
```

---

## 🐼 Pandas — `pandas_file.ipynb`

> *Pandas is your toolkit for working with real-world tabular data — CSV files, Excel sheets, databases. Essential for data cleaning, exploration, and analysis.*

The practice dataset used: **`orders.csv`** — a sales orders dataset with columns `CustomerName`, `Product`, `Category`, `Country`, `Price`.

---

### 1. Loading Data

```python
import pandas as pd

df = pd.read_csv('orders.csv')       # from CSV file
df = pd.read_excel('orders.xlsx')    # from Excel file
df = pd.DataFrame(data_dict)         # from Python dictionary
```

---

### 2. Exploring a DataFrame

```python
df.head()        # first 5 rows
df.tail()        # last 5 rows
df.info()        # column names, types, null counts
df.describe()    # statistics (mean, std, min, max) for numeric columns
df.index         # row index labels
df.columns       # list of column names
```

---

### 3. Selecting Data

```python
df["Country"]                      # single column → returns a Series
df[["Country", "Product"]]         # multiple columns → returns a DataFrame

df.iloc[0:5]                       # rows 0–4 by integer position
df.iloc[4]["Product"]              # value at row 4, Product column
```

---

### 4. Filtering

```python
# Single condition
df[df["Price"] >= 100]

# AND condition (both must be true)
df[(df["Category"] == "Furniture") & (df["Country"] == "India")]

# OR condition (either can be true)
df[(df["Category"] == "Furniture") | (df["Country"] == "Japan")]

# String filter — names starting with "R"
df[df["CustomerName"].str.startswith("R")]

# isin — match any value from a list
df[df["Country"].isin(["India", "Japan"])]

# ~ to negate / flip the condition
df[~df["Country"].isin(["India", "Japan"])]   # everything EXCEPT India & Japan
```

---

### 5. Updating Data

```python
# Update a specific cell using loc
df.loc[df["CustomerName"] == "Raj Patel", "Product"] = "Box"

# Rename values in a column
df.loc[df["Country"] == "USA", "Country"] = "United States"

# Apply string transformation to entire column
df["Country"] = df["Country"].str.upper()
```

---

## 🗺️ Topics Roadmap

**NumPy**
- [x] Array creation (9 methods)
- [x] dtypes and type conversion
- [x] 1D, 2D, 3D, 4D arrays
- [x] Indexing, slicing, boolean indexing
- [x] Element-wise, scalar, comparison operations
- [x] reshape, transpose, concatenation
- [x] Axes and dimensions explained
- [x] Statistical operations
- [x] sort, where, unique
- [x] Real-world example (image brightness, student scores)
- [ ] Linear algebra (`np.linalg`)
- [ ] Broadcasting rules (deep dive)

**Pandas**
- [x] Loading DataFrames (CSV, Excel, dict)
- [x] Exploring with head/tail/info/describe
- [x] Column selection, iloc
- [x] Filtering with &, |, isin, str methods
- [x] Updating data with loc
- [ ] GroupBy & aggregation
- [ ] Merge & Join
- [ ] Handling missing values (NaN / fillna / dropna)
- [ ] Pandas plotting

---

## 🛠️ Tech Stack

| Tool | Version | Purpose |
|------|---------|---------|
| Python | 3.14+ | Core language |
| NumPy | ≥ 2.4.4 | Array computing |
| Pandas | ≥ 3.0.2 | Data analysis |
| Jupyter | latest | Interactive notebooks |
| uv | latest | Environment & package manager |

---

## 👨‍💻 Author

**Rohit** — Python learner on an AI/ML Engineering path.  
Writing my notes in code so I never forget what I learned.

---

> 💡 *These notes are written as I learn — if you spot a better way to do something, feel free to open an issue!*