
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
  - [Numerical Data Operation](#Numerical-Operation)
  - [Text Data Operation](#Text-Operation)
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
|`df.dtypes`| This attribute returns the data types of each column in the DataFrame.|
|`df.values`| This attribute returns the NumPy representation of the DataFrame.|
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

**[🔼Back to Top](#table-of-contents)**

## Data cleaning

|Command | description|
|-------------|----------|
|`df.columns` = ['a','b','c'] | It rename the columns.|
|`pd.isnull()` | It checks for the null values and returns the Boolean array.|
|`pd.notnull()` | It is opposite of pd.isnull().|
|`df.dropna()`|It drops all the rows that contain the null values.|
|`df.dropna(axis= 1)`| It drops all the columns that contain null values.|
|`df.dropna(axis=1,thresh=n)`| It drops all the rows that have less than n non null values.|
|`df.fillna(x)`| It replaces all null values with x.|
|`s.fillna(s.mean())`| It replaces all the null values with the mean(the mean can be replaced with almost any function from the statistics module).|
|`s.astype(float)`| It converts the datatype of series to float.|
|`s.replace(1, 'one')`| It replaces all the values equal to 1 with 'one'.|
|`s.replace([1,3],[ 'one', 'three'])`|It replaces all 1 with 'one' and 3 with 'three'.|
|`df.rename(columns=lambda x: x+1)`|It rename mass of the columns.|
|`df.rename(columns={'old_name': 'new_ name'})`| It consist selective renaming.|
|`df.set_index('column_one')`| Used for changing the index.|
|`df.rename(index=lambda x: x+1)`| It rename mass of the index.|

**[🔼Back to Top](#table-of-contents)**

## Filter, Sort, and Groupby

|Command | description|
|-------------|----------|
|`df[df[col] > 0.5]` | Returns the rows where column col is greater than 0.5|
|`df[(df[col] > 0.5) & (df[col] < 0.7)]`| Returns the rows where 0.7 > col > 0.5|
|`df.sort_values(col1)` | It sorts the values by col1 in ascending order.|
|`df.sort_values(col2,ascending=False)` | It sorts the values by col2 in descending order.|
|`df.sort_values([col1,col2],ascending=[True,False])` | It sort the values by col1 in ascending order and col2 in descending order.|
|`df.groupby(col1)`| Returns a groupby object for the values from one column.|
|`df.groupby([col1,col2])`| Returns a groupby object for values from multiple columns.|
|`df.groupby(col1)[col2])` | Returns mean of the values in col2, grouped by the values in col1.|
|`df.pivot_table(index=col1,values=[col2,col3],aggfunc=mean)` | It creates the pivot table that groups by col1 and calculate mean of col2 and col3.|
|`df.groupby(col1).agg(np.mean`) | It calculates the average across all the columns for every unique col1 group.|
|`df.apply(np.mean)` | Its task is to apply the function np.mean() across each column.|
|`nf.apply(np.max,axis=1)`|Its task is to apply the function np.max() across each row.|

**[🔼Back to Top](#table-of-contents)**

## Join/Combine

|Command | description|
|-------------|----------|
|`df1.append(df2)`| Its task is to add the rows in df1 to the end of df2(columns should be identical).|
|`pd.concat([df1, df2], axis=1)`| Its task is to add the columns in df1 to the end of df2(rows should be identical).|
|`df1.join(df2,on=col1,how='inner')`| SQL-style join the columns in df1 with the columns on df2 where the rows for col have identical values, 'how' can be of 'left', 'right', 'outer', 'inner'.|

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
|`df.sum()`| Returns the sum of each column.|

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
|`df.groupby(['column_name'])['column_name'].cummax()` | It calculates the cumulative maximum value within each group defined by column_name in the DataFrame df.|
|`df.groupby(['column_name'])['column_name'].cummin()` | It calculates the cumulative minimum value within each group defined by column_name in the DataFrame df.|


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
