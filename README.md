
# Movie Data Correlation Analysis

This project focuses on analyzing correlations in a movie dataset, specifically investigating the relationships between budget, gross earnings, company, and other factors. The analysis seeks to explore how these variables influence a movie's financial success.

## Project Steps

### Step 1: Importing Libraries
We start by importing all the necessary libraries for the project, including Pandas for data manipulation and Seaborn for data visualization.

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
```
### Step 2: Reading the Dataset
Next, we read the movie dataset into a Pandas DataFrame.

```python
df = pd.read_csv('movies.csv')
```

### Step 3: Preview the Data
We look at the first five rows of the data using the `.head()` method.

```python
df.head()
```

### Step 4: Checking for Missing Data
We check if there are any missing values in the dataset.

```python
df.isnull().sum()
```

As observed, there are no missing values in the dataset, so we are good to proceed.

### Step 5: Checking Data Types
We examine the data types for each column to ensure they are appropriate for analysis.

```python
df.dtypes
```

### Step 6: Creating the 'Year' Column
We add a new column called 'Year' by extracting the year from the relevant date-related column.

```python
df['Year'] = df['release_date'].apply(lambda x: x.split('-')[0])
```

### Step 7: Dropping Duplicates
We drop any duplicate rows to ensure data integrity.

```python
df.drop_duplicates(inplace=True)
```

### Step 8: Exploring Correlations
From our initial assumptions, we expect the 'Budget' and 'Company' to have a high correlation with gross earnings, as spending more money and working with successful companies should lead to higher earnings.

#### Scatter Plot: Budget vs Gross
We plot a scatter plot to visualize the relationship between budget and gross earnings.

```python
sns.scatterplot(x='budget', y='gross', data=df)
plt.show()
```

#### Correlation Analysis
To verify the correlation, we calculate the correlation matrix using different methods:

```python
# Pearson Correlation
df.corr(method='pearson')

# Kendall Correlation
df.corr(method='kendall')

# Spearman Correlation
df.corr(method='spearman')
```

### Step 9: Correlation Matrix Visualization
We create a heatmap to visualize the correlation matrix.

```python
correlation_matrix = df.corr()
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm')
plt.show()
```

### Step 10: Numerizing Categorical Data
Since 'Company' is a categorical variable, we convert it to numerical values for the correlation analysis.

```python
df['Company'] = df['Company'].factorize()[0]
```

### Step 11: Visualizing Correlation for 'Company'
We unstack the correlation matrix and look at the correlation involving 'Company.'

```python
company_corr = correlation_matrix.unstack().sort_values(ascending=False)
print(company_corr)
```

### Step 12: Conclusion
Contrary to our initial assumptions, the data reveals that **Votes** and **Budget** have a higher correlation with gross earnings than the **Company**. This shows that budget allocation and audience engagement (votes) are more critical factors in predicting a movie's success than the company that produced it.

## End of Project
This project helped explore and visualize how various factors, such as budget, votes, and company, impact a movie's gross earnings.

## Technologies Used
- Python
- Pandas for data manipulation
- Seaborn and Matplotlib for data visualization

## Conclusion
In the end, we found that budget and votes have the highest correlation with gross earnings, contradicting the assumption that the company would have a high correlation.

