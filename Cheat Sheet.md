# Some useful commands

**Important**: 
* `df` is the dataframe that you are using (i.e., the table of data that you are analyzing)
* `new_df` is the target variable that stores the result of your actions.

## Reducing a dataframe to a set of columns that are of interest
```
new_df = df.loc[:, ['COL_1_NAME', 'COL_2_NAME', 'COL_N_NAME']]
```

## Filtering a dataframe
`new_df = df[df['COL_NAME']=='VALUE']` - filtering on string values
`new_df = df[df['COL_NAME']==VALUE]` - filtering on numeric values


## Display a dataframe
* `df.head()` shows the start of the dataframe
* `df.tail()` shows the end of the dataframe
* `df.sample(n)` shows a random sample of `n` rows

## Exploratory data analysis
* `df.describe()` shows descriptive statistics of the whole dataframe
* `df['COL_NAME'].describe()` shows descriptive statistics of one column of the dataframe
* `df[['COL_1_NAME','COL_2_NAME']].describe()` shows descriptive statistics of one column of the dataframe

Alternatively, you can ask for specific statistics:
* `df['COL_NAME'].mean()` shows the mean of a column
* You can replace `mean` with `min`, `max`, `unique`, etc.

## Changing column types
Sometimes you want to adjust the type of the values in a column. The following command changes the column type to `int`.
```
df['COL_NAME'] = df['COL_NAME'].astype(int)
```

## Simple plotting
A very quick look at the data often reveals important insights. The following command displays a scatterplot.
```
plt.scatter(df['COL_X_NAME, df['COL_Y_NAME'])
```

## Combining dataframes
Combining dataframes requires a shared column in both dataframes. The following command left-joins `df1` and `df2`.
```
new_df = pd.merge(df1, df2, on='SHARED_COL_NAME', how='left')
```

## Analysis of grouped data
You can generate descriptive statistics on group data. The following command groups the data on the values of `COL_NAME` and executes `function` on the groups:
```
df.groupby('COL_NAME')['COL_NAME'].function()
```
The following example shows the group-specific means for `COL_NAME`:
```
df.groupby('COL_NAME')['COL_NAME'].mean()
```
