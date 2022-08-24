# Cleaning Data in Python

## Chapter 1 - Common Data Problems

<b>Why do we need to clean data?</b><br>
<b>Answer:</b> Duplicate Values, Different spellings for the same word, Data Parsing etc/ may cause the data to become 'dirty' and if not cleaned the reports and insights generated from that data becomes compromized.

We also need to make sure that our variables have the correct data types. For example, integers in a data frame may be stored as strings.

### Converting strings to integers

Consider a column in a table which is supposed to contain integers but contains strings such as :- '123@456@789'.
To convert the column value strings to an integer we would first need to use the ```.strip()``` method to remove the character '@'.

```table['column name']  = table['column name'].str.strip('@')```

Now we can convert the resulting column values back to an integer.

```table['column name'] = table['column name'].astype('int')```

### Numerical or Categorical

Conside the column 'Marital Status' which has responses 0 or 1. Now both these numbers may be of the type integer but they represent two different categories. If the data type is treated as an integer, than the statistics of the column will give us unusual results. 

To treat these integers as categories we need to convert the column from ```integer``` data type to ```category``` data type.

```python
table['marital_status'] = table['marital_status'].astype('category')
```

To confirm the change it is good practise to ```assert``` the change.

```table['marital_status'].dtype == 'category'```

### Data information

- To get information related to the entire data frame we use ```df.info()```.

- To get summary statistics of individual columns in the data frame we use ```df['column name'].describe()```.

### Uniqueness contraints

#### Dropping data

It is important to note, that data should only be dropped when it is affecting a small set of out-of-range values. Dropping may result in loss of essential data. Hence, it should only be used when absolutely necessary.

##### How to drop data

1. <b>Filtering data</b>
Data can be dropped by applying simple masks/filters.
For example:-

```python
new_df = old_df[old_df['avg_rating'] < 5]
```

2. The ```.drop()``` method
We can also use the ```.drop()``` function to drop junk values.

```python
df.drop(df[df['avg_rating'] < 5].index, inplace = True)
```
To check if the drop has been made successfully we can use assertions.

```python
assert df['avg_rating'].max() <= 5
```

#### Replacing values

We can use the ```.loc[]``` location indexing method to replace values in the data frame.

```python
#         row argument        col argument
df.loc[df['avg_rating'] < 5, 'avg_rating'] = 5
assert df['avg_rating'].max() < 5
```

#### Date range example

Consider a data frame that has faulty dates, of registration that are greater than the present date. We would want to fix/remove those values.

To do so we first need to convert the pandas object value into a ```datetime``` data type.

```python
df['sub_date'] = pd.to_datetime(df['sub_date']).dt.date
assert df['sub_date'].dtype == 'datetime'
```


## Chapter 2



## Chapter 3



## Chapter 4

