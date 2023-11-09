# Project: High ROI Degrees

## Task 1: Load Data and Libraries
Load the required libraries and the degrees-that-pay-back.csv dataset.

1. Load the `tidyr`, `dplyr`, `readr`, `ggplot2`, `cluster`, and `factoextra` libraries.
2. Use `read_csv` (not `read.csv`) to read in `datasets/degrees-that-pay-back.csv` and use the `col_names` parameter to change the column names to the following: `College.Major`, `Starting.Median.Salary`, `Mid.Career.Median.Salary`, `Career.Percent.Growth`, `Percentile.10`, `Percentile.25`, `Percentile.75`, and `Percentile.90`. Assign the dataframe to `degrees`.
3. Display the first few rows of `degrees`.
4. Explore a summary of `degrees`.

## Task 2: Clean Data Types
Clean up the data types.

1. Use `mutate_at` to modify all columns except `College.Major`, using the `gsub` function to strip the dollar signs. The code is already there, but you'll be converting the result to numeric with `as.numeric` at the same time.
2. Use `mutate` to divide the `Career.Percent.Growth` values by 100.

## Task 3: Select Data for k-means and Apply Elbow Method
Select the relevant data for the k-means algorithm and apply the Elbow Method.

1. Select `Starting.Median.Salary`, `Mid.Career.Median.Salary`, `Percentile.10`, and `Percentile.90` columns from `degrees_clean` and assign to `k_means_data`.
2. Scale `k_means_data` using the `scale()` function.
3. Use `fviz_nbclust` on the `k_means_data` with `FUNcluster` set to `kmeans` and method set to "wss". Assign the results to `elbow_method`.

## Task 4: Apply Silhouette Method
Apply the Silhouette Method.

1. Run `fviz_nbclust` again but with "silhouette" as the method this time.

## Task 5: Apply Gap Statistic Method
Apply the Gap Statistic Method.

1. Apply the `clusGap()` function on the `k_means_data` with `FUN` set to `kmeans`, `nstart` set to 25, `K.max` set to 10, and `B` set to 50. Store the result as `gap_stat`.
2. Visualize the results by applying the `fviz_gap_stat()` function on `gap_stat`.

## Task 6: Run k-means Algorithm and Label Clusters
Run the k-means algorithm and label the clusters of the degrees data.

1. Set the seed to 111 using `set.seed()` to ensure reproducibility.
2. Set `num_clusters` equal to the recommended number of clusters, 3.
3. Run the `kmeans()` function on the `k_means_data` with `centers` set to `num_clusters`, `iter.max` set to 15, and `nstart` set to 25. Store the result as `k_means`.
4. Create a new data frame `degrees_labeled` by adding a new column `clusters` to `degrees_clean` equal to the cluster values in the object stored as `k_means`.

## Task 7: Plot Major vs. Salary
Plot each major by Starting Median Salary vs. Mid Career Median Salary.

1. Use `ggplot` to scatter plot `degrees_labeled` with `Mid.Career.Median.Salary` as a function of `Starting.Median.Salary` and color set to the `clusters` column as a factor.
2. Make your plot more readable by adding labels using `xlab`, `ylab`, and `ggtitle`.
3. Use both `scale_x_continuous` and `scale_y_continuous` with labels set to `scales::dollar` to format the axes as currency values.
4. Customize the transparency, shape, and colors of the scatter points, if you'd like.

## Task 8: Reshape Data
Reshape the data to prepare for the upcoming visualizations.

1. Select the `College.Major`, `Percentile.10`, `Percentile.25`, `Mid.Career.Median.Salary`, `Percentile.75`, `Percentile.90`, and `clusters` columns.
2. Apply the `gather()` function on all columns except `College.Major` and `clusters`, with `percentile` as the key and `salary` as the value, which will collapse the percentile columns into rows of one new column, `percentile`, with the respective salary values in the new column `salary`.
3. Use `mutate` to reorder the factor levels of the new `percentile` column from lowest to highest (such that `Mid.Career.Median.Salary` falls after `Percentile.25` and before `Percentile.75`).

## Task 9: Plot Majors of Cluster 1 by Percentile
Plot the majors of Cluster 1 by percentile.

1. Use `ggplot()` to plot `degrees_perc` (filtered such that `clusters` equals 1) with `salary` as a function of `percentile` as a scatter plot, and set group and color to `College.Major`.
2. Add lines to connect the points using `geom_line()`.
3. Set the title to "Cluster 1: The Liberal Arts".
4. Use the `theme()` and `element_text()` functions to set `axis.text.x` with a size of 7 and angle of 25 so the tick labels will be more readable.

## Task 10: Plot Majors of Cluster 2 by Percentile
Copy the code from Task 9, but where `clusters` is equal to 2. Change the title to "Cluster 2: The Goldilocks".

## Task 11: Plot Majors of Cluster 3 by Percentile
Copy the code from Task 10, but where `clusters` is equal to 3. Change the title to "Cluster 3: The Over Achievers".

## Task 12: Identify Majors with Highest Career Percent Growth
Identify the two majors with the highest career percent growth.

1. Use `arrange()` to sort the `degrees_labeled` data frame by `Career.Percent.Growth` in descending order (`desc`).
2. Assign the top two majors (they're tied!) to the list `highest_career_growth`.

