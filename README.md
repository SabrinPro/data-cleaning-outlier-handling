# Data Cleaning & Outlier Handling

This repository contains a Python-based data cleaning assignment completed using **Pandas, NumPy, Matplotlib, and Seaborn**.

The assignment focuses on handling missing values and detecting and mitigating outliers using **trimming and capping techniques**.

## Objectives

The main objectives of this assignment are:

* Handle missing values in a categorical column.
* Detect outliers using the **IQR (Interquartile Range)** method.
* Mitigate outliers using **trimming**.
* Mitigate outliers using **capping**.
* Visualize outliers using boxplots.
* Practice data preprocessing using Pandas and NumPy.

## Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Kaggle Datasets

## Datasets Used

The assignment uses the following datasets:

1. **UCI Adult Census Dataset**

   * Used for missing-value imputation.
   * Target column: `Occupation`

2. **Diabetes Prediction Dataset**

   * Used for outlier detection and mitigation.
   * Target column: `age`

3. **House Price Dataset**

   * Used for outlier detection and mitigation.
   * Target column: `price`

## Assignment Tasks

### 1. Missing Value Imputation

Missing values in the `Occupation` column of the UCI Adult Census dataset are identified and replaced using the **mode** of the column.

The basic approach is:

```python
replaced_by = uci['Occupation'].mode()[0]
uci['Occupation'] = uci['Occupation'].fillna(replaced_by)
```

The number of missing values is checked before and after imputation.

---

### 2. Outliers in Diabetes Dataset

The `age` column of the Diabetes Prediction Dataset is analyzed for outliers.

The **IQR method** is used to calculate the lower and upper limits.

```python
Q1 = diabetes['age'].quantile(0.25)
Q3 = diabetes['age'].quantile(0.75)

IQR = Q3 - Q1

upper_limit = Q3 + 1.5 * IQR
lower_limit = Q1 - 1.5 * IQR
```

#### Trimming

In trimming, observations containing outlier values are removed from the dataset.

```python
new_dia_age = diabetes[
    (diabetes['age'] < upper_limit) &
    (diabetes['age'] > lower_limit)
]
```

#### Capping

In capping, outlier values are replaced by the calculated upper or lower limit instead of removing the observations.

```python
new_df_cap = diabetes.copy()

new_df_cap['age'] = np.where(
    new_df_cap['age'] > upper_limit,
    upper_limit,
    np.where(
        new_df_cap['age'] < lower_limit,
        lower_limit,
        new_df_cap['age']
    )
)
```

Boxplots are used to visualize the effect of outlier mitigation.

---

### 3. Outliers in House Price Dataset

The `price` column of the House Price Dataset is analyzed using the IQR method.

```python
Q1 = house['price'].quantile(0.25)
Q3 = house['price'].quantile(0.75)

IQR = Q3 - Q1

upper_limit = Q3 + 1.5 * IQR
lower_limit = Q1 - 1.5 * IQR
```

#### Trimming

```python
new_house = house[
    (house['price'] < upper_limit) &
    (house['price'] > lower_limit)
]
```

#### Capping

```python
new_house_cap = house.copy()

new_house_cap['price'] = np.where(
    new_house_cap['price'] > upper_limit,
    upper_limit,
    np.where(
        new_house_cap['price'] < lower_limit,
        lower_limit,
        new_house_cap['price']
    )
)
```

Boxplots are used before and after capping to observe the changes in the distribution.

## Methods Used

### Mode Imputation

Mode is used for the categorical `Occupation` column because it represents the most frequently occurring category.

### IQR Method

The Interquartile Range is calculated as:

```text
IQR = Q3 - Q1
```

The outlier boundaries are:

```text
Lower Limit = Q1 - 1.5 × IQR
Upper Limit = Q3 + 1.5 × IQR
```

Values outside these limits are considered potential outliers.

### Trimming

Trimming removes observations that contain outlier values.

### Capping

Capping keeps all observations but replaces values outside the acceptable range with the corresponding boundary value.

## Visualization

Boxplots are used to identify and compare outliers before and after mitigation.

The notebook contains visualizations for:

* Diabetes `age`
* Diabetes `age` after capping
* House `price`
* House `price` after capping

## Repository Contents

```text
├── assignment.ipynb
├── README.md
└── requirements.txt
```

## How to Run

1. Clone the repository.

2. Install the required libraries:

```bash
pip install -r requirements.txt
```

3. Open `assignment.ipynb` using Jupyter Notebook, JupyterLab, Google Colab, or Kaggle Notebook.

4. Make sure the required datasets are available in the expected Kaggle paths.

5. Run the notebook cells sequentially.

## Conclusion

This assignment demonstrates fundamental data preprocessing techniques using Python. Missing categorical values are handled using mode imputation, while numerical outliers are detected using the IQR method and mitigated through both trimming and capping.

The work provides practical experience with **data cleaning, statistical analysis, outlier detection, and data visualization** using Python libraries.
