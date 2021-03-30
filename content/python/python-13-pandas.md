+++
title = "Pandas dataframes"
slug = "python-13-pandas"
weight = 13
+++

## Reading tabular data into dataframes

First, let's download the data. Open a terminal inside your Jupyter dashboard. Inside the terminal, type:

```sh
wget http://bit.ly/pythfiles -O pfiles.zip
unzip pfiles.zip && rm pfiles.zip        # this should unpack into the directory data-python/
```

You can now close the terminal panel. Let's switch back to our Python notebook and check our location:

```py
%pwd       # simply run a bash command with a prefix
%ls        # make sure you see data-python/
```

Pandas is a widely-used Python library for working with tabular data, borrows heavily from R's dataframes, built on top
of numpy. We will be reading the data we downloaded a minute ago into a pandas dataframe:

```py
import pandas as pd
data = pd.read_csv('data-python/gapminder_gdp_oceania.csv')
print(data)
data   # this prints out the table nicely in Jupyter Notebook!
```

```py
data.shape   # shape is a *member variable inside data*
data.info()    # info is a *member method inside data*
```

Use dir(data) to list all member variables and methods. Then call that name without (), and if it's a method it'll tell
you, so you'll need to use ().

Rows are observations, and columns are the observed variables. You can add new observations at any time.

Currently the rows are indexed by number. Let's index by country:

```py
data = pd.read_csv('data-python/gapminder_gdp_oceania.csv', index_col='country')
data
data.shape     # now 12 columns
data.info()    # it's a dataframe! show row/column names, precision, memory usage
print(data.columns)   # will list all the columns
print(data.T)   # this will transpose the dataframe; curously this is a variable
data.describe()   # will print some statistics of numerical columns (very useful for 1000s of rows!)
```

Quick question: how to list all country names? (try data.T.columns)

**[Quiz 12](./solaj.md):** explore Americas

**[Quiz 13](./solak.md):** first 3 rows and last 3 columns

**[Quiz 14](./solal.md):** navigating the filesystem from inside Jupyter Notebook

**[Quiz 15](./solam.md):** write a dataframe to disk

## Subsetting

```py
data = pd.read_csv('data-python/gapminder_gdp_europe.csv', index_col='country')
data.head()
```

Let's rename the columns:

```py
data.rename(columns={'gdpPercap_1952': '1952'})   # this renames only one but does not change `data`
```

Let's go through all columns and assign the new names:

```py
for col in data.columns:
    print(col, col[-4:])
    data = data.rename(columns={col: col[-4:]})

data
```

Printing one element:

```py
data.iloc[0,0]   # the very first element by position
data.loc['Albania','1952']    # exactly the same; the very first element by label
```

Printing a row:

```py
data.loc['Albania',:]   # usual Python's slicing notation - show all columns in that row
data.loc['Albania']     # exactly the same
data.loc['Albania',]    # exactly the same
```

Printing a column:

```py
data.loc[:,'1952']   # show all rows in that column
data['1952']   # exactly the same; single index refers to columns
data.1952      # exactly the same; most compact notation to access columns; does not work with numerical column names ...
```

Printing a range:

```py
data.loc['Italy':'Poland','1952':'1967']   # select multiple rows/columns
data.iloc[0:2,0:3]
```

Result of slicing can be used in further operations:

```py
data.loc['Italy':'Poland','1952':'1967'].max()   # max for each column
data.loc['Italy':'Poland','1952':'1967'].min()   # min for each column
```

Use comparisons to select data based on value:

```py
subset = data.loc['Italy':'Poland', '1962':'1972']
print(subset)
print(subset > 1e4)
```

Use a Boolean mask to print values (meeting the condition) or NaN (not meeting the condition):

```py
mask = subset > 1e4
print(mask)
print(subset[mask])   # will print numerical values only if the corresponding elements in mask are True
```

NaN's are ignored by statistical operations which is handy:

```py
subset[mask].describe()
subset[mask].max()
```

**[Quiz 16](./solan.md):** GDP of Serbia

**[Quiz 17](./solao.md):** study the script

**[Quiz 18](./solap.md):** study the script

How do you create a dataframe from scratch? Many ways; the easiest by defining columns:

```py
col1 = [1,2,3]
col2 = [4,5,6]
pd.DataFrame({'a': col1, 'b': col2})       # dataframe from a dictionary
```

Let's index the rows by hand:
```py
pd.DataFrame({'a': col1, 'b': col2}, index=['a1','a2','a3'])
```

## Looping over data sets

Let's say we want to read several files in data-python/. We can use **for** to loop through their list:

```py
for filename in ['data-python/gapminder_gdp_africa.csv', 'data-python/gapminder_gdp_asia.csv']:
    data = pd.read_csv(filename, index_col='country')
    print(filename, data.min())   # print min for each column
```

If we have many (10s or 100s) files, we want to specify them with a pattern:

```py
from glob import glob
print('all csv files in data directory:', glob('data-python/*.csv'))   # returns a list
print('all text files in data directory:', glob('data-python/*.txt'))   # empty list
list = glob('data-python/*.csv')
len(list)
```

```py
for filename in glob('data-python/*.csv'):
    data = pd.read_csv(filename)
    print(filename, data.gdpPercap_1952.min())
```

**Quiz 19:** glob's wildmask

<!-- The right answer is A. -->

**[Quiz 20](./solaq.md):** find the file with fewest records

<!-- **[Exercise](./solar.md):** add a curve for New Zealand. -->
<!-- **[Exercise](./solas.md):** do a scatter plot of Australia vs. New Zealand. -->
<!-- **[Quiz 21](./solat.md):** (more difficult) plot the average GDP vs. time in each region (each file) -->
