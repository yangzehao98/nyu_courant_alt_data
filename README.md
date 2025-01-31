
# Transaction Pattern and Consumer Behavior Analysis

### Team Folder Name: AltDataGA2049_2024.sso9282_sk11297_zy2891
### Team Members: Zehao Yang (zy2891), Simar Oberoi (sso9282), Soohan Kim (sk11297)

## Dataset

- The dataset is stored in a compressed ZIP file: facteus_10k_user_panel.zip.

- It contains a CSV file: facteus_10k_user_panel.csv.

- Additional financial data is sourced from revenues_kpi.csv.

- The data includes transaction records with merchant names, locations, transaction details, and financial revenue data.

## 1. Regular Expressions

Use the RE module to:

- **a.** Isolate / find all variations of merchant strings belonging to merchant `MCDONALDS`, `AMAZON`, `APPLE`.
- **b.** Create regex to isolate the city where the transaction occurred.
- **c.** Use any method to remove the transaction ID if it is present in the transaction.
  - **i.** Evaluate 200 randomly selected rows manually and construct a confusion matrix to evaluate your error rates.

- Devise a minimum number of regular expressions to achieve the above.
- Try the regular expression on a sample of the rest of the data (or a uniform random sample of the data). Minimize false positives to 0 if possible.

## 2. Text Mining

1. Use `sklearn`
2. Filter in on the following merchants: `WALMART`, `MCDONALDS`, `AMAZON`, `APPLE`, `SHELL`, `WENDYS`, `TACO BELL`, `BURGER KING`, `DOLLAR GENERAL`, `ACE HARDWARE`.
3. Create a 1-3 gram vector space using no stemming, no stop words, and a word tokenizer with default settings. Strip non-alphanumeric characters and convert to all lowercase.
4. Create a vector space matrix from the above using `CountVectorizer` and `TfidfVectorizer`. Steps **c** and **d** could possibly be done in 1-2 lines of code. Try either or both for step **f** to maximize accuracy.
5. Remove n-grams which occur in less than ~3% of the strings. Try to minimize the number of columns while keeping the accuracy of the model in step **f** high.
6. Using the above matrix and a multi-label classification predictive model (recommend `xgboost` or `logistic`), predict the merchant.
7. Construct the model leaving some data out (10-fold cross-validation or a 20% random sample).
8. Evaluate your model on out-of-sample data and show out-of-sample error for each of the 10 merchants.
9. Please show your work with comments in your Jupyter notebook.

## 3. Clustering and Visualization

1. Reduce the matrix from section 2 to two (2) dimensions. Try `UMAP` first; if that doesn’t work, try `t-SNE`. You might need to normalize the matrix first for the below steps to work.
2. Draw a scatter plot for a sample of the data using the 2 dimensions in step 1.
3. Cluster using `k-means` k=10. Use line separations (like a Voronoi plot) to outline the cluster boundaries.  
   - See: [Voronoi Plot Example](http://msmbuilder.org/msmexplorer/development/examples/plot_voronoi.html)
   - If that doesn’t work, use different marker shapes for each cluster (i.e., 10 shapes).
4. Use marker colors to indicate the real merchant name from the dataset.
5. Ideally, the markers from steps **c** and **d** are the same, but even if they are not, as long as you show the work, you'll get full points.

## 4. Fiscal Calendar Mapping

1. Augments the main dataset by labeling each company-month into the correct fiscal calendar quarters.

2. Uses fiscal_calendar.csv mapping file, available at: Google Drive Link.

3. Maps using tickers and exchange to the main dataset.

4. Augments the main dataset with period start and end dates for fiscal quarters (not years).

5. Private companies are excluded from the mapping.

6. Since data is monthly, but some fiscal quarters do not align exactly with calendar months, adjustments are made:

- **a.** Start dates: Adjusted up or down to the closest month.

- **b.** End dates: Adjusted up or down to the closest month.

- **c.** Mapping Rule: The first month of the fiscal quarter is inclusive, while the final month is only inclusive up to the month prior to the end date. Example: NASDAQ:JACK 2020-Q3 starts on April 13 and ends on July 5th. Therefore, the months April, May, and June are mapped to 2020-Q3.

## 5. Revenue Data Integration & Analysis

1. Extracts total Consolidated Reported Revenues from revenues_kpi.csv.

2. Maps these revenues to the unique company-quarter dataset from the fiscal mapping.

3. Integrates total spend per user and reported revenues per quarter.

4. Standardizes exchange names across different datasets to ensure proper mapping.

5. Filters out outlier users and user-months to maintain data integrity.

6. Computes correlation coefficients between core data total spend per quarter and reported revenues for the top 15 companies by total sales in the main dataset.

7. Aggregates total spend on the ticker level, rather than the merchant level.

## 6. Walmart Fiscal Revenue Mapping:

1. For NYSE:WMT, identifies the correct reporting revenue segments for Fiscal 2020 using:

- **a.** 10-Q and 10-K filings

- **b.** Quarterly earnings presentations

- **c.** Other official financial sources

2. Focuses on U.S. operations, including Puerto Rico.

3. Creates a mapping table that aligns each fiscal quarter's "apples-to-apples" Net Sales to the core data's total spend per quarter.

4. Aggregates total spend for NYSE:WMT based on the correct segment combinations and fiscal quarters.

5. Ensures an accurate comparison between reported Net Sales and core transaction data.