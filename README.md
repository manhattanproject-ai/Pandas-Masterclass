
---
## Title: Pandas CheatSheet
## Description: The most commonly used pandas commands are given here.
## Created: 2025-1-3
---

## Table of Contents

- [Pandas CheatSheet for Developers](#pandas-cheatsheet-for-developers)
  - [Introduction-What-is-Pandas?](#introduction-what-is-pandas)
  - [Key and Imports](#key-and-imports)
  - [Importing Data](#importing-data)
  - [Exporting data](#exporting-data)
  - [Create Test objects](#create-test-objects)
  - [Viewing/Inspecting Data](#viewinginspecting-data)
  - [Selection](#selection)
  - [Data cleaning](#data-cleaning)
  - [Filter, Sort, and Groupby](#filter-sort-and-groupby)
  - [Join/Combine](#joincombine)
  - [Statistics](#statistics)
  - [Numerical Operation](#Numerical-Operation)
  - [Text Operation](#Text-Operation)
  - [Timeseries Operation](#Timeseries-Operations)
  - [Data Visualization with dataframe](#data-visualization-with-dataframe)
    - [Terminology And Definitions](#terminology-and-definitions)
    - [Type of plots](#type-of-plots)


# Pandas CheatSheet for Developers

## Introduction-What-is-Pandas?

> Pandas is a cornerstone library in the Python data science ecosystem, providing powerful and flexible data structures designed for efficient data manipulation and analysis. At its core, Pandas offers the DataFrame, a two-dimensional labeled data structure that resembles a spreadsheet or SQL table, enabling users to easily organize and work with structured data. This library simplifies tasks like data cleaning, transformation, aggregation, and exploration, making it indispensable for data scientists and analysts. Pandas excels at handling various data formats, including CSV, Excel, and SQL databases, and seamlessly integrates with other essential Python libraries like NumPy, Matplotlib, and scikit-learn, fostering a robust environment for comprehensive data analysis workflows.
> Pandas Cheat Sheet is a quick guide through the basics of Pandas that you will need to get started on wrangling your data with Python. If you want to begin your data science journey with Pandas, you can use it as a handy reference to deal with the data easily.

This cheat sheet will guide through the basics of the Pandas library from the data structure to I/O, selection, sorting and ranking, etc.

**[🔼Back to Top](#table-of-contents)**

## Key and Imports

> We use following shorthand in the cheat sheet:

|Command | description|
|----------|-------------|
|`pd`|import pandas library| 
|`df` | Refers to any Pandas Dataframe object.|
|`s` | Refers to any Pandas Series object.|

> You can use the following imports to get started:

**[🔼Back to Top](#table-of-contents)**

## Importing Dataset

|Command | description|
|---------|-------------|
|`pd.read_csv(filename)` | It read the data from CSV file.|
|`pd.read_table(filename)` | It is used to read the data from delimited text file.|
|`pd.read_excel(filename)` | It read the data from an Excel file.|
|`pd.read_sql(query,connection _object)`| It read the data from a SQL table/database.|
|`pd.read_json(json _string)` | It read the data from a JSON formatted string, URL or file.|
|`pd.read_html(url)` | It parses an html URL, string or the file and extract the tables to a list of dataframes.|
|`pd.read_clipboard()` | It takes the contents of clipboard and passes it to the read_table() function.|
|`pd.DataFrame(dict)` | From the dict, keys for the columns names, values for the data as lists.|
|`pd.read_feather(filename)` | Reads data from Feather file format, which is a fast, lightweight, and language-agnostic columnar file format.|
|`pd.read_parquet(filename)` | Reads data from Parquet file format, a columnar storage format known for its efficient storage and retrieval, especially for large datasets.|
|`pd.read_stata(filename)` | Reads data from Stata file format (.dta), commonly used in econometrics and social sciences.|
|`pd.read_sas(filename, format='xport' or 'sas7bdat')` | Reads data from SAS file formats (.xport or .sas7bdat)|
|`pd.read_pickle(filename)` | Reads data from a Python pickle file, which is a serialized Python object.|

**[🔼Back to Top](#table-of-contents)**

## Exporting data

|Command | description|
|-------------|----------|
|`df.to_csv(filename)`| It writes to a CSV file.|
|`df.to_excel(filename)`| It writes to an Excel file.|
|`df.to_sql(table_name, connection_object)`| It writes to a SQL table.|
|`df.to_json(filename)` | It write to a file in JSON format.|
|`df.to_parquet(filename)` | Writes the DataFrame to a Parquet file.|
|`df.to_feather(filename)` | Writes the DataFrame to a Feather file.|
|`df.to_stata(filename)` | Writes the DataFrame to a Stata .dta file.|
|`df.to_pickle(filename)` | Writes the DataFrame to a Python pickle file.|
|`df.to_html(filename)` | Writes the DataFrame to an HTML table.|
|`df.to_clipboard()` | Writes the DataFrame to the system clipboard.|
|`df.to_latex(filename)` | Writes the DataFrame to a LaTeX table.|


**[🔼Back to Top](#table-of-contents)**

## Create Test objects

> It is useful for testing the code segments.

|Command | description|
|-------------|----------|
|`pd.DataFrame(np.random.rand(7,18))`| Refers to 18 columns and 7 rows of random floats.|
|`pd.Series(my_list)`| It creates a Series from an iterable my_list.|
|`df.index= pd.date_range('1940/1/20', periods=df.shape[0])`|It adds the date index.|

**[🔼Back to Top](#table-of-contents)**

## Viewing/Inspecting Data

|Command | description|
|-------------|----------|
|`df.head(n)`| It returns first n rows of the DataFrame.By default it will return first 5 rows|
|`df.tail(n)` | It returns last n rows of the DataFrame.By default it will return last 5 rows|
|`df.shape` | It returns number of rows and columns.|
|`df.info()`| It returns index, Datatype, and memory information.|
|`df.index`| This attribute returns the index (row labels) of the DataFrame.|
|`df.columns`| This attribute returns the column labels of the DataFrame.|
|`df.dtypes`| This attribute returns the data types of each column in the DataFrame.|
|`df.values`| This attribute returns the NumPy representation of the DataFrame.|
|`df.describe()`| Generates descriptive statistics (count, mean, std, min, max, quartiles) for numerical columns.|
|`df.describe(include='all')`| Generates descriptive statistics for all columns, including non-numerical data.|
|`df.describe(include='object')`| Generates descriptive statistics for all non-numerical data.|
|`df.unique()`| (For a Series) Returns unique values in a Series in the order of appearance.|
|`df.nunique()`| This method returns the number of unique values in each column.|
|`s.value_counts(dropna=False)`| It views unique values and counts.|
|`df.apply(pd.Series.value_counts)`| It refers to the unique values and counts for all the columns.|
|`df.memory_usage(deep=True)`| This method returns the memory usage of each column in bytes. The deep=True argument is important for accurately calculating memory usage for object (string) columns.|


**[🔼Back to Top](#table-of-contents)**

## Selection

|Command | description|
|-------------|----------|
|`df[col1]` | It returns column with the label col as Series.|
|`df[[col1, col2]]`| It returns columns as a new DataFrame.|
|`s.iloc[0]` | It select by the position.|
|`s.loc['index_one']` | It select by the index.|
|`df.iloc[0,:]`| It returns first row.|
|`df.iloc[0,0]` | It returns the first element of first column.|
|`df.iloc[start:stop, step]`| Returns rows by position, with slicing similar to Python lists.|
|`df.loc[row_label, col_label]`| Returns a single value at the specified row and column label.|
|`df.loc[row_label, :]`| Returns a row by its label.|
|`df.loc[:, col_label]`| Returns a column by its label.|
|`df.at[row_label, col_label]`| Returns a single value at the specified row and column label, faster than df.loc[].|
|`df.iat[row_index, col_index]`| Returns a single value at the specified row and column index, faster than df.iloc[].|
|`df[df[col] > value]`| Returns rows where a column meets a specific condition (Boolean indexing).|
|`df[(df[col1] > value1) & (df[col2] == value2)]`| Returns rows based on multiple conditions using logical operators (&).|
|`df.query('col > value')`| Selects rows using a string expression for conditions (alternative to Boolean indexing).|
|`df.isin(values)`| Returns a DataFrame of Booleans indicating if each element is contained in values. Often used with df[] for filtering.|
|`df.filter(items=[], like='', regex='')`|Selects rows or columns based on specified item labels, partial string matches (like), or regular expressions (regex).|
|`df.loc[df['col'].isin(list_of_values)]`| Selects rows where a column's value is present in a list of allowed values.|
|`df.iloc[:, [0, 2, 5]]`| Selects columns by their integer positions (e.g., first, third, sixth columns).|

**[🔼Back to Top](#table-of-contents)**

## Data cleaning

|Command | description|
|-------------|----------|
|`df.columns = ['a','b','c']` | Renames all columns by assigning a new list of column names.|
|`pd.isnull(obj)` | Checks for null (NaN, None, NaT) values in a DataFrame or Series, returning a Boolean array/DataFrame.|
|`pd.notnull(obj)` | The inverse of pd.isnull(), checking for non-null values.|
|`df.dropna()`|It drops all the rows that contain the null values.|
|`df.dropna(axis= 1)`| It drops all the columns that contain null values.|
|`df.dropna(how='all')`| Drops rows where all values are null. (Often axis=0 is implied).|
|`df.dropna(axis=1, how='all')`| Drops columns where all values are null.|
|`df.dropna(how='all')`| Drops rows where all values are null. (Often axis=0 is implied).|
|`df.dropna(subset=['col1', 'col2'])`| Drops rows that have null values only in the specified subset of columns.|
|`df.dropna(thresh=n)`| Drops rows where all values are null. (Often axis=0 is implied).|
|`df.dropna(axis=1,thresh=n)`| Drops rows that have fewer than n non-null values.|
|`df.fillna(x)`| It replaces all null values with x.|
|`s.fillna(s.mean())`| It replaces all the null values with the mean(the mean can be replaced with almost any function from the statistics module).|
|`df.fillna({'col1': val1, 'col2': val2})`| Replaces null values with different specified values per column.|
|`df.fillna(method='ffill')`| Replaces null values by propagating the last valid observation forward to next valid observation (forward fill).|
|`df.fillna(method='bfill')`| Replaces null values by propagating the next valid observation backward to previous valid observation (backward fill).|
|`df.fillna(value=df.mean())`| Replaces null values in each column with that column's mean.|
|`s.astype(dtype)`| Converts the data type of a Series s to the specified dtype (e.g., 'float', 'int', 'str', datetime).|
|`df['col'].astype(dtype)`| Converts the data type of a specific column in a DataFrame.|
|`s.replace(old_value, new_value)`| Replaces all occurrences of old_value with new_value across the entire DataFrame.|
|`s.replace([val1, val2], [new_val1, new_val2])`| Replaces multiple old values with corresponding new values in a Series.|
|`df.replace(old_value, new_value)`| Replaces all occurrences of old_value with new_value across the entire DataFrame.|
|`df.replace({'col_name': {old_val: new_val}})`| Replaces values specifically within a designated column of a DataFrame.|
|`df.replace({'col1': {old_val1: new_val1}, 'col2': {old_val2: new_val2}})`|Replaces values differently across multiple specific columns.|
|`df.rename(columns=lambda x: x + '_new')`|Renames columns using a function (e.g., appending _new to each name).|
|`df.rename(columns={'old_name': 'new_name'})`| Renames specific columns using a dictionary mapping.|
|`df.set_index('column_one')`| Sets a specified column as the new DataFrame index.|
|`df.reset_index()`| Resets the index to the default integer index, optionally moving the current index to a column.|
|`df.rename(index=lambda x: x + 1)`| Renames index labels using a function.|
|`df.rename(index={old_label: new_label})`| Renames specific index labels using a dictionary mapping.|
|`df.drop_duplicates()`| Removes duplicate rows based on all columns.|
|`df.drop_duplicates(subset=['col1'])`| Removes duplicate rows based only on specified columns.|
|`df.drop_duplicates(keep='last')`| Removes duplicates, keeping the last occurrence. (Default is first).|
|`df.duplicated()`| Returns a Boolean Series indicating duplicate rows.|
|`df.duplicated(subset=['col1'])`| Returns a Boolean Series indicating duplicate rows based on specified columns.|
|`df.astype({'col1': 'int', 'col2': 'float'})`| Converts data types for multiple specific columns at once.|
|`pd.to_numeric(s, errors='coerce')`| Converts Series s to numeric, converting unparseable values to NaN.|
|`pd.to_datetime(s, errors='coerce')`| Converts Series s to datetime objects, converting unparseable values to NaT.|
|`pd.to_timedelta(s, errors='coerce')`| Converts Series s to timedelta objects.|
|`df.loc[df['col'].isin(['val1', 'val2'])]`| Filters rows where a column's value is in a given list.|
|`df.loc[~df['col'].isin(['val1', 'val2'])]`| Filters rows where a column's value is NOT in a given list.|
|`df.apply(function, axis=1)`| Applies a function along an axis of the DataFrame (e.g., row-wise operations).|
|`df.select_dtypes(include='number')`| Selects columns based on their data type (e.g., only numeric columns).|
|`df.drop(['col1', 'col2'], axis=1)`| Drops specified columns from the DataFrame.|
|`df.drop(index=[0, 1])`| Drops rows by their index labels.|
|`df.isnull().sum()`| Returns a Series with the count of null values per column.|
|`df.isnull().sum(axis=1)`| Returns a Series with the count of null values per row.|
|`df.interpolate()`| Fills NaN values using interpolation methods (e.g., linear, polynomial).|
|`df.clip(lower=min_val, upper=max_val)`| Clips values in the DataFrame to be within a specified range.|


**[🔼Back to Top](#table-of-contents)**

## Filter, Sort, and Groupby

|Command | description|
|-------------|----------|
|`df[df[col] > 0.5]` | Returns the rows where column col is greater than 0.5|
|`df[(df[col] > 0.5) & (df[col] < 0.7)]`| Returns the rows where 0.7 > col > 0.5|
|`df[df[col].isin(['val1', 'val2'])]`| Returns rows where col contains any of the specified values.|
|`df[df[col].notna()]`| Returns rows where col is not null/NaN.|
|`df[df[col].isna()]`| Returns rows where col is null/NaN.|
|`df.query('col > 0.5 and col < 0.7')`| Returns rows where 0.7 > col > 0.5 using a string expression.|
|`df.sort_values(col1)` | It sorts the values by col1 in ascending order.|
|`df.sort_values(col2,ascending=False)` | It sorts the values by col2 in descending order.|
|`df.sort_values([col1,col2],ascending=[True,False])` | It sort the values by col1 in ascending order and col2 in descending order.|
|`df.groupby(col1)`| Returns a groupby object for the values from one column.|
|`df.groupby([col1,col2])`| Returns a groupby object for values from multiple columns.|
|`df.groupby(col1)[col2].mean()` | Returns the mean of the values in col2, grouped by the values in col1.|
|`df.groupby(col1).agg(np.mean`) | It calculates the average across all the columns for every unique col1 group.|
|`df.groupby(col1).agg({'col2': 'sum', 'col3': 'max'})`|Calculates sum of col2 and max of col3, grouped by col1.|
|`df.groupby(col1).size()`|Returns the count of items in each group.|
|`df.groupby(col1).count()`|Returns the count of non-null items in each column for every group.|
|`df.groupby(col1).apply(custom_function)`|Applies a custom function to each group.|
|`df.groupby(col1).filter(lambda x: len(x) > N)`|Filters groups based on a condition (e.g., keeping groups with more than N rows).|
|`df.groupby(col1).filter(lambda x: x['col2'].mean() > X)`|Filters groups based on an aggregated condition within each group.|
|`df.groupby(col1).transform(lambda x: x - x.mean())`|Applies a function to each group and returns a DataFrame with the same shape as the original.|
|`df.groupby(col1).transform('mean')`|Fills values with the group's mean, aligning with the original DataFrame's index.|
|`df.pivot(index=col1, columns=col2, values=col3)` | Restructures a DataFrame by moving values from rows to columns. Does not aggregate.|
|`df.pivot_table(index=col1,values=[col2,col3],aggfunc=mean)` | It creates the pivot table that groups by col1 and calculate mean of col2 and col3.|
|`df.pivot_table(index=col1, columns=col2, values=col3, aggfunc='sum')` | Creates a pivot table summing col3, with col1 as index and col2 as columns.|
|`df.melt(id_vars=[col1], value_vars=[col2, col3], var_name='Metric', value_name='Value')` | "Unpivots" a DataFrame from wide to long format (inverse of pivot). unpivot is not a direct Pandas command; melt is used.|
|`df.stack()` | "Stacks" the (innermost) column level into the (innermost) row level, producing a Series.|
|`df.unstack()` | "Unstacks" the (innermost) row level into the (innermost) column level.|
|`df.T`|Transposes the DataFrame (swaps rows and columns).|
|`df.apply(np.mean)` | Its task is to apply the function np.mean() across each column.|
|`nf.apply(np.max,axis=1)`|Its task is to apply the function np.max() across each row.|
|`df.transform(func)`|Performs group-wise transformation where the result is broadcast to the original shape.|

**[🔼Back to Top](#table-of-contents)**

## Join/Combine

|Command | description|
|-------------|----------|
|`df1.append(df2)`| Its task is to add the rows in df1 to the end of df2(columns should be identical).|
|`pd.concat([df1, df2])`| Concatenates (stacks) DataFrames or Series along a particular axis (default is axis=0, meaning rows). It can add rows from df2 to the end of df1. Use axis=1 to add columns from df2 to df1. Handles non-matching indices based on join parameter ('outer' by default, 'inner' also available).|
|`pd.merge(df1, df2, on='key', how='inner')`| Combines DataFrames based on common values in specified columns or indices (keys). This is the most versatile and commonly used method for SQL-style joins. on specifies the column(s) to join on. how specifies the type of join ('inner', 'left', 'right', 'outer', 'cross').|
|`pd.merge(df1, df2, left_on='key_df1', right_on='key_df2')`| Combines DataFrames when the join keys have different names in df1 and df2.|
|`pd.merge(df1, df2, left_index=True, right_index=True)`| Combines DataFrames based on their indices. Use left_index=True and right_index=True when the index is the join key. Can be combined with left_on/right_on if one is an index and the other is a column.|
|`df1.join(df2, on='key', how='left')`| Combines DataFrames based on the index of the calling DataFrame (df1) and a specified column (or index) in the other DataFrame (df2). By default, it performs a left join (how='left'). Similar to pd.merge but optimized for joining on an index.|
|`df1.combine(df2, func)`| Combines two DataFrames by applying a function func to each element of the DataFrames. Elements are combined pairwise. Missing values can be handled.|
|`df1.combine_first(other)`| Combines two DataFrames by filling NaN values in df1 with corresponding non-NaN values from other, prioritizing df1's values where they exist.|
|`df1.update(other)`| Modifies df1 in place by updating its values with non-NaN values from other, aligning based on index and column labels.|

**[🔼Back to Top](#table-of-contents)**

## Statistics

> The statistics functions can be applied to a Series, which are as follows:

|Command | description|
|-------------|----------|
|`df.describe()`| It returns the summary statistics for the numerical columns.|
|`df.mean()` | It returns the mean of all the columns.|
|`df.corr()` | It returns the correlation between the columns in the dataframe.|
|`df.count()`| It returns the count of all the non-null values in each dataframe column.|
|`df.max()`| It returns the highest value from each of the columns.|
|`df.min()`| It returns the lowest value from each of the columns.|
|`df.median()`| It returns the median from each of the columns.|
|`df.std()`| It returns the standard deviation from each of the columns.|
|`df.var()`| Returns the variance of each column. Variance is a measure of the spread of data.|
|`df.quantile(q)`| Returns the quantiles of the DataFrame or Series. q is a value between 0 and 1, where 0 is the minimum and 1 is the maximum. This allows you to find percentiles (e.g., df.quantile(0.25) for the 25th percentile).|
|`df.skew()`| Returns the skewness of each column, a measure of the asymmetry of the data distribution.|
|`df.kurt()`| Returns the kurtosis of each column, a measure of the "tailedness" of the data distribution.|
|`df.mode()`| Returns the mode(s) (most frequent value(s)) of each column.|
|`df.abs()`| Returns the absolute numerical value of each element in the DataFrame.|
|`df.mad()`| Returns the mean absolute deviation of each column.|
|`df.prod()`| Returns the product of the values in each column.|
|`df.cumsum()`| Returns the cumulative sum along the specified axis (e.g., running total).|
|`df.cumprod()`| Returns the cumulative product along the specified axis (e.g., running product).|
|`df.pct_change()`| Returns the percentage change between the current and a prior element.|
|`df.cov()`| Returns the covariance between columns, indicating how two variables change together.|
|`df.sem()`| Returns the standard error of the mean for each column.|

**[🔼Back to Top](#table-of-contents)**

## Numerical Operation

> The Below  functions can be applied to Numerical Data:

|Command | description|
|-------------|----------|
|`df.add(s)`| It adds the specified scalar value to every element within the DataFrame df.|
|`df.sub(s)` | It subtracts the specified scalar value to every element within the DataFrame df.|
|`df.mul(s)` | It multiplies the specified scalar value to every element within the DataFrame df.|
|`df.div(s)` | It divides the specified scalar value to every element within the DataFrame df.|
|`df.floordiv(s)` | It gives you the integer quotient of a division, discarding any remainder..|
|`df.mod(s)` | It applies modulo operation to every element within the DataFrame df.|
|`df.pow(s)` | It applies power function to every element within the DataFrame df.|
|`df.eq(s)` | It compares each element of DataFrame df with the scalar value s and returns a DataFrame of boolean values indicating element-wise equality..|
|`df.ne(s)` | It compares each element of DataFrame df with the scalar value s and returns a DataFrame of boolean values indicating element-wise inequality..|
|`df.le(s)` | It compares each element in DataFrame df with scalar value s, returning a boolean DataFrame showing elements less than or equal to s.|
|`df.lt(s)` | It compares each element in DataFrame df with scalar value s, returning a boolean DataFrame showing elements strictly less than s.|
|`df.ge(s)` | It compares each element in DataFrame df with scalar value s, returning a boolean DataFrame showing elements greater than or equal to s.|
|`df.gt(s)` | It compares each element in DataFrame df with scalar value s, returning a boolean DataFrame showing elements strictly greater than s.|
|`df.nlargest(n=5, columns='column_name')` | It retrieves the five rows with the highest values in the specified column_name from the DataFrame df.|
|`df.nsmallest(n=5, columns='column_name')` | It retrieves the five rows with the lowest values in the specified column_name from the DataFrame df.|
|`df['column_name'].rank()` | It assigns a rank to each value in the specified column_name within the DataFrame df, based on their ascending order.|
|`pd.cut(df['column_name'], bins=4)` | It divides the values in the specified column_name into 4 equal-width bins and assigns each value to its corresponding bin.|
|`pd.cut(df['column_name'], bins=4, labels=['Low', 'Moderate', 'High', 'Extreme'])` | It categorizes the numerical data in specified column_name into four bins with the specified labels..|
|`pd.qcut(df['column_name'], q=4)` | It divides the values in the specified column_name into 4 quantiles, ensuring each bin has roughly the same number of data points.|
|`df['column_name'].clip(upper=20000)` | It caps the maximum value of elements in the column column_name within the DataFrame df to 20,000.|
|`df['column_name'].cumsum()` | It calculates the cumulative sum of the values in the column column_name within the DataFrame df.|
|`df['column_name'].cumprod()` | It calculates the cumulative product of the values in the column column_name within the DataFrame df.|
|`df.apply(lambda x: x.sum(), axis=0)` |  Applies a custom lambda function (here, sum) to each column of the DataFrame.|
|`df.apply(lambda x: x.mean(), axis=1)` | Applies a custom lambda function (here, mean) to each row of the DataFrame.|
|`df.apply(lambda x: pd.Series([x.min(), x.max()], index=['Min', 'Max']), axis=0, result_type='expand')` | Applies a custom lambda function to each column, returning a Series that expands into new columns in the resulting DataFrame.|
|`df.apply(lambda x: x / x.mean(), axis=0, result_type='broadcast')` | Applies a custom lambda function to each column, returning a DataFrame with the same shape as the original, broadcasting the result.|
|`df.apply(lambda x: x.sum() / x.count(), axis=0, result_type='reduce')` | Applies a custom lambda function to each column, returning a Series by reducing the result (this is the default behavior if not specified).|
|`df_scores.applymap(lambda x: x * 100 if pd.notna(x) else x)` | Applies a custom lambda function element-wise to every cell in the DataFrame.|
|`df_sales['Unit_Price_USD'].map(lambda x: x * 1.07 if pd.notna(x) else x)` | Applies a custom lambda function element-wise to each value in the specified Series (column).|
|`df['Sales_K_USD'] = df['Sales_Revenue'].apply(lambda x: x / 1000 if pd.notna(x) else x)` | Defines an anonymous inline function that is used here with .apply() to convert sales figures.|
|`df_performance['Profit_Category'] = df_performance['Profit_Margin_Pct'].apply(lambda x: 'High' if x > 0.15 else 'Low')` | Defines an anonymous inline function used with .apply() for conditional categorization based on a numerical value.|


**[🔼Back to Top](#table-of-contents)**

## Categorical Operation

> The Below  functions can be applied to Categorical Data:

|Command | description|
|-------------|----------|
|`df['column_name'].astype('category')`| Converts the data in the specified column to a pandas Categorical dtype, which is memory-efficient and enables categorical-specific methods.|
|`df['column_name'].value_counts()`| Counts the occurrences of each unique category in the specified column, returning a Series with categories as index and counts as values.|
|`df['column_name'].unique()`| Returns an array of all unique categories/values present in the specified column.|
|`df['column_name'].nunique()`| Returns the number of unique categories/values in the specified column.|
|`df['column_name'].mode()`| Returns the most frequently occurring category (or categories if there's a tie) in the specified column.|
|`df['categorical_column'].cat.categories`| Retrieves the list of all defined categories for a column that has already been converted to a Categorical dtype.|
|`df['categorical_column'].cat.reorder_categories(new_order, ordered=True)`| Reorders the existing categories of a categorical column according to new_order, optionally setting it as ordered.|
|`df['categorical_column'].cat.add_categories(new_cats)`| Adds new categories to the existing categories of a categorical column without changing the data.|
|`df['categorical_column'].cat.remove_categories(rem_cats)`| Removes specified categories from the existing categories of a categorical column, converting corresponding data points to NaN.|
|`df['categorical_column'].cat.remove_unused_categories()`| Removes any categories from a categorical column's metadata that are not actually present in the data.|
|`df['column_name'].isin(['value1', 'value2'])`| Checks if each element in the specified column is present within the given list of values, returning a boolean Series.|
|`pd.get_dummies(df['column_name'])`| Converts the specified categorical (or object) column into dummy/one-hot encoded variables (binary columns for each category).|


**[🔼Back to Top](#table-of-contents)**

## Text Operation

> The Below  functions can be applied to Text Data:

|Command | description|
|-------------|----------|
|`df.astype('string')`| It adds the specified scalar value to every element within the DataFrame df.|
|`df['column_name'].str.len()`| It obtains the number of characters in the string values within columns.|
|`df['column_name'].str.lower()`| It converts all strings in the column_name of the DataFrame df to lowercase.|
|`df['column_name'].str.upper()`| It converts all strings in the column_name of the DataFrame df to uppercase.|
|`df['column_name'].str.title()`| It returns a title-cased version of the string where every word starts with an uppercase character.|
|`df['column_name'].str.capitalize()`| It returns only uppercases the first character of the entire string, regardless of the number of words present.|
|`df['column_name'].str.swapcase()`| It is used to convert every character in a string to a case that is opposite of its current one.|
|`df['column_name'].str.casefold()`| It is used to returns a case-folded copy of the string, which can be useful for caseless matching.|
|`df['column_name'].str.isalnum()`| Checks whether all characters are alphanumeric in the column.|
|`df['column_name'].str.isalpha()`| Checks whether all characters are alphabetic in the column.|
|`df['column_name'].str.isdecimal()`| Checks whether all characters are decimal in the column.|
|`df['column_name'].str.isdigit()`| Checks whether all characters are digits in the column.|
|`df['column_name'].str.islower()`| Checks whether all characters are lowercase in the column.|
|`df['column_name'].str.isnumeric()`| Checks whether all characters are numeric in the column.|
|`df['column_name'].str.isspace()`| Checks whether all characters are whitespace in the column.|
|`df['column_name'].str.istitle()`| Checks whether all characters are titlecase in the column.|
|`df['column_name'].str.isupper()`| Checks whether all characters are uppercase in the column.|
|`df['column_name'].str.slice()`| It is a way of selecting a subset of characters from a string column.|
|`df['column_name'].str.slice_replace()`| It enables us to replace a positional slice of a string with another value.|
|`df['column_name'].str.split()`| It splits a string column into multiple columns based on a separator..|
|`df['column_name'].str.partition()`| It splits the string at the first occurrence of the separator.|
|`df['column_name'].str.cat()`| It helps in concatenating strings.|
|`df['column_name'].str.endswith()`| Checks  if each string value in the  column ends with the mentioned string.|
|`df['column_name'].str.contains()`| Checks  if each string value in the  column  match , can occur at any position within the string.|
|`df['column_name'].str.match()`| Checks  if each string value in the  column  match , must begin at the string's first character.|
|`df['column_name'].str.fullmatch()`| Checks  if each string value in the  column  match , the entire string must match the pattern.|
|`df['column_name'].str.find()`| It is used to search for a substring within each element of a DataFrame column and return the starting index of its first occurrence.|
|`df['column_name'].str.findall()`| It extracts all occurrences of the substring pattern so that the substring repetition count can be derived from the output..|
|`df['column_name'].str.extract()`| It is used to extract particular regex patterns that we want to extract from string values.|
|`df['column_name'].str.extractall()`| It is used to extract all particular regex patterns that we want to extract from string values.|
|`df['column_name'].str.replace()`| It is used to replacing each occurrence of a string or regex pattern.|
|`df['column_name'].str.pad()`| It is used for adding extra characters to the beginning or end of a string to make it up to a certain length.|
|`df['column_name'].str.rjust()`| Pads left side of strings with an arbitrary character. Equivalent to setting side='left' in pad().|
|`df['column_name'].str.ljust()`| Pads right side of strings with an arbitrary character. Equivalent to setting side='right' in pad().|
|`df['column_name'].str.center()`| Pads both sides of strings with an arbitrary character. Equivalent to setting side='both' in pad().|
|`df['column_name'].str.zfill()`| Pads left side of strings by prepending a 0 character. Equivalent to setting side='left' and fillchar='0' in pad(). |
|`df['column_name'].str.strip()`| It strips whitespaces (including newlines) or a set of specified characters from each string from the left and right sides.|
|`df['column_name'].str.rstrip()`| It is used if we only want to remove characters from the trailing side.|
|`df['column_name'].str.removeprefix()`| It is used if we’re dealing with string values that have a specific prefix.|
|`df['column_name'].str.removesuffix()`| It is used if we’re dealing with string values that have a specific suffix.|
|`df['column_name'].str.wrap()`| It is used to ensure that the text is wrapped across multiple lines to fit within the available width of the output display.|


**[🔼Back to Top](#table-of-contents)**

## Timeseries Operations

> The Below  functions can be applied to Timeseries Data:

|Command | description|
|-------------|----------|
|`pd.to_datetime(arg)`| Converts a scalar, array-like, Series, or DataFrame to datetime objects.|
|`pd.date_range(start=None, end=None, periods=None, freq='D')`| Generates a fixed-frequency DatetimeIndex.|
|`df.index.dt.year`| Extracts the year from a DatetimeIndex.|
|`df['date_col'].dt.month`| Extracts the month from a datetime Series.|
|`df.index.dt.day`| Extracts the day of the month from a DatetimeIndex|
|`df['time_col'].dt.hour`| Extracts the hour from a datetime Series.|
|`df.resample(rule)`| Used for frequency conversion (downsampling or upsampling) of time series data.|
|`df.resample(rule).mean()`| Aggregates resampled data by calculating the mean.|
|`df.resample(rule).sum()`| Aggregates resampled data by calculating the sum.|
|`df.resample(rule).first()`| Aggregates resampled data by taking the first value.|
|`df.resample(rule).last()`| Aggregates resampled data by taking the last value.|
|`df.resample(rule).ohlc()`| Aggregates resampled data to calculate Open, High, Low, Close (useful for financial data).|
|`df.asfreq(freq)`| Converts TimeSeries to specified frequency. Values are filled with NaN for new time points.|
|`df.shift(periods=1)`| Shifts the index by the desired number of periods.|
|`df.shift(freq='D')`| Shifts the index by a specified time frequency, respecting calendar gaps.|
|`df.pct_change(periods=1)`| Calculates the percentage change between the current and a prior element.|
|`df.rolling(window).mean()`| Calculates the rolling (moving) mean over a specified window.|
|`df.rolling(window).std()`| Calculates the rolling standard deviation over a specified window.|
|`df.expanding().sum()`|  Calculates the expanding (cumulative) sum from the beginning of the series up to the current point.|
|`df.expanding().mean()`| Calculates the expanding (cumulative) mean from the beginning of the series up to the current point.|
|`df.tz_localize(tz)`| Localizes a naive (timezone-unaware) DatetimeIndex to a specific timezone.|
|`df.tz_convert(tz)`| Converts an already timezone-aware DatetimeIndex to a different timezone.|
|`df.ffill()`| Fills NaN values by propagating the last valid observation forward to next valid observation.|
|`df.bfill()`| Fills NaN values by propagating the next valid observation backward to previous valid observation.|
|`df.interpolate(method='time')`| Fills NaN values by estimating based on time intervals, assuming linear progression.|

**[🔼Back to Top](#table-of-contents)**

## Data Visualization with dataframe

### Terminology And Definitions

|data| DataFrame|
|--------|------|
|`x`| label or position, default None|
|`y` | label, position or list of label, positions, default None Allows plotting of one column versus another|
|`ax `| matplotlib axes object, default None|
|`subplots`| boolean, default False Make separate subplots for each column|
|`sharex `| boolean, default True if ax is None else False. Be aware, that passing in both an ax and sharex=True will alter all x axis labels for all axis in a figure!|
|`sharey`| boolean, default False In case subplots=True, share y axis and set some y axis labels to invisible|
|`layout`|tuple (optional) (rows, columns) for the layout of subplots|
|`figsize`| a tuple (width, height) in inches|
|`use_index `| boolean, default True. Use index as ticks for x axis|
|`title `| string or list. Title to use for the plot. If a string is passed, print the string at the top of the figure. If a list is passed and subplots is True, print each item in the list above the corresponding subplot.|
|`grid `| boolean, default None (matlab style default). Axis grid lines|
|`legend`| False/True/’reverse’. Place legend on axis subplots|
|`style `| list or dict. Matplotlib line style per column|
|`logx `| boolean, default False. Use log scaling on x axis|
|`logy `| boolean, default False. Use log scaling on y axis|
|`loglog `| boolean, default False. Use log scaling on both x and y axes|
|`xticks `| sequence. Values to use for the xticks|
|`yticks `| sequence. Values to use for the yticks|
|`xlim `| 2-tuple/list|
|`ylim `| 2-tuple/list|
|`rot `| int, default None. Rotation for ticks (xticks for vertical, yticks for horizontal plots)|
|`fontsize `| int, default None. Font size for xticks and yticks|
|`colormap `| str or matplotlib colormap object, default None. Colormap to select colors from. If string, load colormap with that name from matplotlib.|
|`colorbar `| boolean, optional. If True, plot colorbar (only relevant for ‘scatter’ and ‘hexbin’ plots)|
|`position `| float. Specify relative alignments for bar plot layout. From 0 (left/bottom-end) to 1 (right/top-end). Default is 0.5 (center)|
|`table `| boolean, Series or DataFrame, default False. If True, draw a table using the data in the DataFrame and the data will be transposed to meet matplotlib’s default layout. If a Series or DataFrame is passed, use passed data to draw a table.|
|`yerr `| DataFrame, Series, array-like, dict and str. See Plotting with Error Bars for detail.|
|`xerr `| same types as yerr.|
|`stacked `| boolean, default False in line and bar plots, and True in area plot. If True, create stacked plot.|
|`sort_columns `| boolean, default False. Sort column names to determine plot ordering|
|`secondary_y `| boolean or sequence, default False. Whether to plot on the secondary y-axis If a list/tuple, which columns to plot on secondary y-axis|
|`mark_right `| boolean, default True. When using a secondary_y axis, automatically mark the column labels with “(right)” in the legend|
|`kwds`|  keywords .Options to pass to matplotlib plotting method|
|`axes`|  matplotlib.axes.Axes or numpy.ndarray of them|

**[🔼Back to Top](#table-of-contents)**

### Type of plots

`Note it is a part of data Visualization`

|king|type|
|-----|-----|
|`‘line’ `| line plot (default)|
|`‘bar’ `| vertical bar plot|
|`‘barh’ `| horizontal bar plot|
|`‘hist’ `| histogram|
|`‘box’ `| boxplot|
|`‘kde’ `| Kernel Density Estimation plot|
|`‘density’ `| same as ‘kde’|
|`‘area’`| area plot|
|`‘pie’ `| pie plot|
|`‘scatter’ `| scatter plot|
|`‘hexbin’ `| hexbin plot|

**[🔼Back to Top](#table-of-contents)**
