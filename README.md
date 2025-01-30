
# Transaction Pattern and Consumer Behavior Analysis

### Team Folder Name: AltDataGA2049_2024.sso9282_sk11297_zy2891
### Team Members: Simar Oberoi (sso9282), Soohan Kim (sk11297), Zehao Yang (zy2891)


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
