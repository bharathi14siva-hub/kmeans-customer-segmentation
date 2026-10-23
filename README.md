# Customer Segmentation Using K-Means Clustering

## Project Overview

This project applies **K-Means Clustering**, an unsupervised Machine Learning algorithm, to segment customers based on their purchasing behavior. The objective is to identify groups of customers with similar spending patterns, order frequency, and purchase quantities to support data-driven business decisions.

## Dataset

- **Dataset:** Online Retail
- **Source:** [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/352/online+retail)
- **Original transaction records:** 541,909
- **Cleaned transaction records:** 392,692
- **Unique customers analyzed:** 4,338

The dataset contains transactions from a UK-based online retailer between December 2010 and December 2011.

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- Jupyter Notebook

## Project Workflow

1. **Data Loading:** Imported the Excel dataset using Pandas.
2. **Data Exploration:** Examined column names, data types, missing values, duplicates, cancellations, and numerical distributions.
3. **Data Cleaning:** Removed duplicate records, transactions without customer IDs, cancelled invoices, and records with non-positive quantities or unit prices.
4. **Feature Engineering:** Aggregated transaction records into customer-level features:
   - Total Spending
   - Total Orders
   - Total Quantity Purchased
5. **Log Transformation:** Applied `numpy.log1p()` to reduce the influence of highly skewed feature distributions.
6. **Feature Scaling:** Used `StandardScaler` to standardize the transformed features.
7. **Model Selection:** Used the Elbow Method and compared Silhouette Scores for cluster counts from 2 to 8.
8. **Model Training:** Trained the K-Means model using `k=2`.
9. **Evaluation:** Evaluated cluster separation using the Silhouette Score.
10. **Visualization:** Visualized customer segments using spending and order frequency.

## Model Results

| Metric | Result |
|---|---:|
| Original transaction records | 541,909 |
| Cleaned transaction records | 392,692 |
| Customers analyzed | 4,338 |
| Selected clusters | 2 |
| Cluster 0 | 1,677 customers |
| Cluster 1 | 2,661 customers |
| Silhouette Score | 0.4987 |

The two-cluster model achieved the highest Silhouette Score among the tested values of `k` from 2 to 8. This indicates better separation according to this metric among the tested options, but does not establish that two clusters are best for every business objective.

## Customer Segments

### Cluster 0 — Higher-Spending, More-Frequent Customers

- **Customers:** 1,677
- **Average spending:** 4,616.60
- **Average orders:** 8.39
- **Average quantity:** 2,681.42

This segment has higher average spending, order frequency, and purchase quantity. Businesses could explore loyalty programs and retention strategies for these customers.

### Cluster 1 — Lower-Spending, Less-Frequent Customers

- **Customers:** 2,661
- **Average spending:** 430.35
- **Average orders:** 1.68
- **Average quantity:** 246.25

This segment has lower average spending and order frequency. Businesses could test targeted promotions and product recommendations to encourage repeat purchases.

*Note: Cluster names are interpretations of observed feature averages. The dataset does not provide predefined customer-segment labels. Spending values are in the dataset's monetary units.*

## Project Structure

```text
kmeans-customer-segmentation/
├── README.md
├── data/
│   └── Online Retail.xlsx
├── notebooks/
│   ├── customer_segmentation_real_data.ipynb
│   └── kmeans_practice.ipynb
└── results/
    └── customer_segmentation_results.csv
```

## How to Run the Project

1. Clone or download this repository.
2. Install the required libraries:

   ```bash
   pip install pandas numpy matplotlib scikit-learn openpyxl jupyter
   ```

3. Ensure `Online Retail.xlsx` is inside the `data/` directory.
4. Open `notebooks/customer_segmentation_real_data.ipynb` in VS Code or Jupyter Notebook.
5. Run the notebook cells in order.

**Important:** The notebook's dataset loading and CSV-saving paths must match the folder structure above. If you run the notebook with `notebooks/` as the working directory, use:

```python
df = pd.read_excel("../data/Online Retail.xlsx")
```

Save the results using:

```python
customer_data.to_csv(
    "../results/customer_segmentation_results.csv",
    index=False
)
```

If your notebook contains an existing `customer_data` DataFrame, retain your current variable names and apply these paths to the corresponding cells.

## Limitations

- K-Means requires the number of clusters to be specified in advance.
- Results depend on feature selection, scaling, initialization, and the chosen number of clusters.
- The Silhouette Score of 0.4987 indicates some cluster separation, but the groups are not perfectly separated.
- The analysis excludes cancelled invoices, transactions without customer IDs, and non-positive quantities or unit prices.
- The dataset covers a historical period, so its patterns may not represent current customer behavior.
- Business recommendations are hypotheses that require validation.
- The model was evaluated on the same dataset used for clustering; further stability analysis would strengthen the evaluation.

## Conclusion

This project demonstrates an end-to-end unsupervised Machine Learning workflow using real retail transaction data. It transforms transaction records into customer-level features, applies K-Means clustering, evaluates the resulting groups, and interprets customer purchasing patterns for potential business use.

The project provided practical experience in data cleaning, feature engineering, log transformation, standardization, clustering, model evaluation, and data visualization.
