# Customer Segmentation

**Unsupervised Learning Project**\
**Author:** Joshua Ozoaka

## Overview

In this project, I carry out customer segmentation for a credit card provider, with the hypothetical goal of understanding and grouping customer behaviour to enable more personalised customer engagements.

Techniques used include exploratory data analysis (EDA), data preprocessing,
Principal Component Analysis (PCA), and two clustering algorithms:
K-Means and Agglomerative Hierarchical Clustering.

## Dataset

-   **File used:** `Customer Data.csv`
-   **Size:** 8,950 customer records and 18 features
-   **Content:** Numerical attributes describing customer tenure, credit
    limits, balances, purchases, cash advances, payments, and other
    measures of credit-card activity.
-   **Source:** Kaggle [here](https://www.kaggle.com/datasets/mahnazarjmand/customer-segmentation)

The notebook reports missing values in two variables, with most
concentrated in `MINIMUM_PAYMENTS`. It found no duplicate records. The
CSV is expected to be placed in the project directory before running the
notebook.

## Project Workflow

### 1. Data inspection

-   Reviewed the dataset's dimensions, data types, missing values, and
    duplicate records.
-   Used descriptive statistics to understand the range and spread of
    the variables.

### 2. Cleaning and preprocessing

-   Investigated missing values and compared relevant groups before
    deciding how to handle them.
-   Examined outliers and the strongly right-skewed distributions of
    many monetary variables.
-   Applied transformations and scaling to make the features more
    suitable for PCA and clustering.

### 3. Exploratory Data Analysis

Visualisations were used to investigate: - Distributions and outliers in
monetary variables. - Relationships between balances, purchases, cash
advances, payments, and credit limits. - Correlations among features,
many of which measure related aspects of financial activity.

### 4. Dimensionality reduction with PCA

Principal Component Analysis was used to combine correlated features and
reduce the number of dimensions before clustering. The final
representation retained **10 principal components**, accounting for
approximately **93% of the variance** in the processed data. Component
loadings were examined to help interpret the combined features.

### 5. Clustering

Two approaches were compared: - **K-Means:** The elbow method was used
to evaluate candidate K values. - **Agglomerative Hierarchical
Clustering:** A dendrogram and visual inspection were used to help
assess the grouping structure.

Both algorithms had optimal performance at **three clusters**.

### 6. Evaluation and interpretation

The clustering results were compared using: - **Silhouette score**, to
assess how well observations fit their assigned clusters relative to
neighbouring clusters. - **10-fold cross-validated Decision Tree
accuracy and macro F1**, using the cluster assignments as targets. These
served as supplementary measures of how consistently the assigned groups could
be predicted from the features; they are not ground-truth labels or
proof that the segments are objectively correct. - Visualisations and
summary statistics were used to describe the financial behaviours associated with
each cluster.

## Results

### Clustering comparison

| Method | Silhouette Score | Decision Tree CV Accuracy | Decison Tree CV Macro F1 |                                 
|--------|------------------|---------------------------|----------------------|
| K-Means | 0.2260 | 0.9558 | 0.9544 |
| Agglomerative Hierarchical | 0.2030 | 0.8902 | 0.8871   

K-Means performed better on all three reported metrics and showed
clearer separation in the two-dimensional Principal Component clustering visualisation. Based
on this comparison, K-Means was selected for the final segmentation.

### Interpreted customer segments

The cluster labels were encoded as **Cluster A, B, and C** as opposed to the integers they were initially assigned.

  ----------------------------------- -----------------------------------
  **Cluster A**                       Customers with a preference for
                                      cash advances, fairly high usage,
                                      comparatively weak debt clearance,
                                      and generally newer accounts.

  **Cluster B**                       Customers with relatively low
                                      overall usage, a preference for
                                      direct purchases---often in
                                      instalments---and stronger
                                      debt-clearance behaviour.

  **Cluster C**                       High-usage customers with frequent
                                      transactions, relatively high
                                      credit limits and payments, longer
                                      tenure, and a tendency toward full
                                      payments on direct purchases, while
                                      still making some cash advances.
  -----------------------------------------------------------------------

Note that these profiles are broad interpretations of cluster averages and
component loadings, not rules that describe every individual customer.
There is natural variation within each group.

## Tools and Libraries

-   Python
-   pandas and NumPy --- data handling and numerical operations
-   Matplotlib and Seaborn --- visualisation
-   scikit-learn --- preprocessing, PCA, clustering, cross-validation,
    and evaluation
-   SciPy --- hierarchical clustering and dendrogram support
-   Jupyter Notebook --- analysis workflow


## How to Run

1.  Clone or download the repository.

2.  Ensure Python and Jupyter Notebook are installed.

3.  Install the required libraries if necessary:

    ``` bash
    pip install pandas numpy matplotlib seaborn scikit-learn scipy jupyter
    ```

4.  Place `Customer Data.csv` in the directory expected by the notebook.

5.  Open the notebook and run the cells from top to bottom.

## Conclusion

This project applies an end-to-end unsupervised learning workflow to
credit-card customer data, from inspection and EDA through
preprocessing, PCA, clustering, and interpretation. The comparison
favoured K-Means with three clusters, producing three broad customer
profiles that differ in usage volume, transaction preferences,
debt-clearance behaviour, and account tenure.