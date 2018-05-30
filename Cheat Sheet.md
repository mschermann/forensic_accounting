# Some useful commands

**Important**: 
* `df` is the dataframe that you are using (i.e., the table of data that you are analyzing)
* `new_df` is the target variable that stores the result of your actions.

## Reducing a dataframe to a set of columns that are of interest
```
new_df = df.loc[:, ['COL_1_NAME', 'COL_2_NAME', 'COL_N_NAME']]
```

## Filtering a dataframe
* `new_df = df[df['COL_NAME']=='VALUE']` - filtering on string values
* `new_df = df[df['COL_NAME']==VALUE]` - filtering on numeric values
* `new_df = df_1[df_1['COL_NAME'].isin(df_2['COL_NAME'])]` - filtering on the values of a column in another table 


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
plt.scatter(df['COL_X_NAME'], df['COL_Y_NAME'])
```

## Faceted Bar charts plotting
```
chart = alt.Chart(data).mark_bar(stroke='transparent').encode(
    x=alt.X('<COL_NAME_1>', axis=alt.Axis(title='<Title>')),
    y=alt.Y('<COL_NAME_2>', scale=alt.Scale(domain=(<min>, <max>)), axis=alt.Axis(title='<Title>')),
    column='<COL_NAME_3>'
)
chart
```
The `column` command allows you to group the bar chart.

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

The following addendum sorts grouped data:
```
[..].sort_values('SORTING_COL', ascending=[True/False])
```

The following command allows you to apply multiple functions to multiple columns:
```
new_df = df.groupby(['COL_NAME_1','COL_NAME_2']).agg({'COL_NAME_1':'function','COL_NAME_2':'function'})
```

You can replace `function` with `mean` with `min`, `max`, `unique`, etc.

The following command allows you to count the number of occurences in a group.
```
new_df = df.groupby('COL_NAME_1')['COL_NAME_2'].value_counts().reset_index(name='count')
```
This tells you how often `COL_NAME_2` appears in each group of `COL_NAME_1`.

## Create dummy variables
Dummy variables help to understand the role of categorial variable. We can store the dummies back into the a dataframe.
```
new_df = df.join(df['COL_NAME'].str.get_dummies())
```

## Renaming values in a column
```
df['COL_NAME'] = df['COL_NAME'].map({VALUE_1: NEW_VALUE_1, VALUE_2: NEW_VALUE_2})
```
Use `''` to denote string variables (e.g., `'NEW_VALUE_1'`)

## Creating a pivot table
```
new_df = df.pivot_table(index=['COL_NAME_1','COL_NAME_2'], columns='KEY', values='AGGREGATE', aggfunc='sum').reset_index()
```
* `index` means the column(s) that become the pivot index.
* `columns` means the column(s) that become the keyed columns.
* `values` means the column(s) that contain the values of the pivot table.

## Row-wise operations
Average between two subsequent rows
```
df['mean'] = (df['value'] + df['value'].shift(1))/2
```

Growth-rate between two subsequent rows
```
df['rate'] = df['value'].pct_change(1)
```

## Convert formatted numbers into float values
Remove the `,`
```
df['value'] = df['value'].str.replace(',','')
```
Change the type of the column
```
df['value'] = df['value'].astype(float)
```
