---

layout: post
title: "Introduction to Data Transformation with Python and Pandas."
author: "Mario H. Gonzalez-Sauri"
date: "2022-10-04"
mermaid: true

---

================

## Importing Modules

``` python
import numpy as np

import pandas as pd
```

## Loading Data

For this tutorial you need to download the

-   The `avocados`, `homelessness.csv`, `sales_subset.csv` and
    `temperatures.csv` dataset from [Kaggle’s
    website.](https://www.kaggle.com/code/kakamana/datacamp-data-manipulation-with-pandas/data)

-   The `COVID19 Daily Updates`data from [Kaggle’s
    website.](https://www.kaggle.com/datasets/gpreda/coronavirus-2019ncov?select=covid-19-all.csv)

## Creating Dataframes

### A Dataframe from a list

``` python
a = [['a', '1.2', '4.2'], ['b', '70', '0.03'], ['x', '5', '0']]
df11 = pd.DataFrame(a, columns=['one', 'two', 'three'])
print(df11)
```

      one  two three
    0   a  1.2   4.2
    1   b   70  0.03
    2   x    5     0

### A Dataframe from Array

Example 1

``` python
dates = pd.date_range("20130101", periods=6) # pandas indexes
r_num = np.random.randn(6, 4) # array

df = pd.DataFrame(r_num, index=dates, columns=list("ABCD"))
print(df)
```

                       A         B         C         D
    2013-01-01  0.817994 -0.924007 -1.515711 -0.198598
    2013-01-02  0.673364 -1.914110 -0.126208 -0.282033
    2013-01-03  1.312579  0.340656 -0.300397 -0.838614
    2013-01-04 -0.732977 -0.560867 -0.515910 -0.768784
    2013-01-05 -2.045106 -0.929131 -0.029660  0.529883
    2013-01-06 -1.343257 -0.250821 -0.046303  0.944569

Example 2

``` python
r_num = np.array(range(1,26,1))
# Convert 1D array to a 2D numpy array of 5 rows and 5 columns
arr_2d = np.reshape(r_num, (5, 5))
df4 = pd.DataFrame(arr_2d)

print(df4)
print(type(df4))
```

        0   1   2   3   4
    0   1   2   3   4   5
    1   6   7   8   9  10
    2  11  12  13  14  15
    3  16  17  18  19  20
    4  21  22  23  24  25
    <class 'pandas.core.frame.DataFrame'>

### A Dataframe from a dictionary

``` python
dict = {
        "A": 1.0,
        "B": pd.Timestamp("20130102"),
        "C": pd.Series(1, index=list(range(4)), dtype="float32"),
        "D": np.array([3] * 4, dtype="int32"),
        "E": pd.Categorical(["test", "train", "test", "train"]),
        "F": "foo",
    }

df2 = pd.DataFrame(dict)

print(df2)
```

         A          B    C  D      E    F
    0  1.0 2013-01-02  1.0  3   test  foo
    1  1.0 2013-01-02  1.0  3  train  foo
    2  1.0 2013-01-02  1.0  3   test  foo
    3  1.0 2013-01-02  1.0  3  train  foo

### A Dataframe froma list of dictionaries

``` python
# Create a list of dictionaries with new data
df9 = [
    {"date": "2019-11-03", "small_sold": 10376832, "large_sold": 7835071},
    {"date": "2019-11-10", "small_sold": 10717154, "large_sold": 8561348},
]

# Convert list into DataFrame
df9 = pd.DataFrame(df9)

# Print the new DataFrame
print(df9)
```

             date  small_sold  large_sold
    0  2019-11-03    10376832     7835071
    1  2019-11-10    10717154     8561348

### A Dataframe from CSV

To print `df3` I use the `head()` method to print only the top rows.

``` python
# Read the csv from working directory
df3 = pd.read_csv("homelessness.csv")

print(df3.head())
```

       Unnamed: 0              region  ... family_members  state_pop
    0           0  East South Central  ...          864.0    4887681
    1           1             Pacific  ...          582.0     735139
    2           2            Mountain  ...         2606.0    7158024
    3           3  West South Central  ...          432.0    3009733
    4           4             Pacific  ...        20964.0   39461588

    [5 rows x 6 columns]

Another example of importing from csv.

``` python
df6 = pd.read_csv("sales_subset.csv")

print(df6.head())
```

       Unnamed: 0  store type  ...  temperature_c fuel_price_usd_per_l  unemployment
    0           0      1    A  ...       5.727778             0.679451         8.106
    1           1      1    A  ...       8.055556             0.693452         8.106
    2           2      1    A  ...      16.816667             0.718284         7.808
    3           3      1    A  ...      22.527778             0.748928         7.808
    4           4      1    A  ...      27.050000             0.714586         7.808

    [5 rows x 10 columns]

``` python
df7 = pd.read_csv("temperatures.csv")

print(df7.head())
```

       Unnamed: 0        date     city        country  avg_temp_c
    0           0  2000-01-01  Abidjan  Côte D'Ivoire      27.293
    1           1  2000-02-01  Abidjan  Côte D'Ivoire      27.685
    2           2  2000-03-01  Abidjan  Côte D'Ivoire      29.061
    3           3  2000-04-01  Abidjan  Côte D'Ivoire      28.162
    4           4  2000-05-01  Abidjan  Côte D'Ivoire      27.547

``` python
df8 = pd.read_csv("covid-19-all.csv")
print(df8.head())
```

    <string>:1: DtypeWarning: Columns (0,1) have mixed types. Specify dtype option on import or set low_memory=False.
      Country/Region Province/State  Latitude  ...  Recovered  Deaths        Date
    0            NaN            NaN       NaN  ...    41727.0  2191.0  2021-01-01
    1            NaN            NaN       NaN  ...    33634.0  1181.0  2021-01-01
    2            NaN            NaN       NaN  ...    67395.0  2762.0  2021-01-01
    3            NaN            NaN       NaN  ...     7463.0    84.0  2021-01-01
    4            NaN            NaN       NaN  ...    11146.0   405.0  2021-01-01

    [5 rows x 8 columns]

## Methods and Attributes of a DataFrame

In Python, there are specific `methods`, or operations that can be
performed for each data structure. Similarly, there are specific
characteristics of the data structures called `attributes`. We can
assess all the methods and attributes associated with a data structure
using the following lines:

``` python
att_meth = dir(df)
print(att_meth)
```

    ['A', 'B', 'C', 'D', 'T', '_AXIS_LEN', '_AXIS_ORDERS', '_AXIS_TO_AXIS_NUMBER', '_HANDLED_TYPES', '__abs__', '__add__', '__and__', '__annotations__', '__array__', '__array_priority__', '__array_ufunc__', '__array_wrap__', '__bool__', '__class__', '__contains__', '__copy__', '__deepcopy__', '__delattr__', '__delitem__', '__dict__', '__dir__', '__divmod__', '__doc__', '__eq__', '__finalize__', '__floordiv__', '__format__', '__ge__', '__getattr__', '__getattribute__', '__getitem__', '__getstate__', '__gt__', '__hash__', '__iadd__', '__iand__', '__ifloordiv__', '__imod__', '__imul__', '__init__', '__init_subclass__', '__invert__', '__ior__', '__ipow__', '__isub__', '__iter__', '__itruediv__', '__ixor__', '__le__', '__len__', '__lt__', '__matmul__', '__mod__', '__module__', '__mul__', '__ne__', '__neg__', '__new__', '__nonzero__', '__or__', '__pos__', '__pow__', '__radd__', '__rand__', '__rdivmod__', '__reduce__', '__reduce_ex__', '__repr__', '__rfloordiv__', '__rmatmul__', '__rmod__', '__rmul__', '__ror__', '__round__', '__rpow__', '__rsub__', '__rtruediv__', '__rxor__', '__setattr__', '__setitem__', '__setstate__', '__sizeof__', '__str__', '__sub__', '__subclasshook__', '__truediv__', '__weakref__', '__xor__', '_accessors', '_accum_func', '_add_numeric_operations', '_agg_by_level', '_agg_examples_doc', '_agg_summary_and_see_also_doc', '_align_frame', '_align_series', '_append', '_arith_method', '_as_manager', '_attrs', '_box_col_values', '_can_fast_transpose', '_check_inplace_and_allows_duplicate_labels', '_check_inplace_setting', '_check_is_chained_assignment_possible', '_check_label_or_level_ambiguity', '_check_setitem_copy', '_clear_item_cache', '_clip_with_one_bound', '_clip_with_scalar', '_cmp_method', '_combine_frame', '_consolidate', '_consolidate_inplace', '_construct_axes_dict', '_construct_axes_from_arguments', '_construct_result', '_constructor', '_constructor_sliced', '_convert', '_count_level', '_data', '_dir_additions', '_dir_deletions', '_dispatch_frame_op', '_drop_axis', '_drop_labels_or_levels', '_ensure_valid_index', '_find_valid_index', '_flags', '_from_arrays', '_from_mgr', '_get_agg_axis', '_get_axis', '_get_axis_name', '_get_axis_number', '_get_axis_resolvers', '_get_block_manager_axis', '_get_bool_data', '_get_cleaned_column_resolvers', '_get_column_array', '_get_index_resolvers', '_get_item_cache', '_get_label_or_level_values', '_get_numeric_data', '_get_value', '_getitem_bool_array', '_getitem_multilevel', '_gotitem', '_hidden_attrs', '_indexed_same', '_info_axis', '_info_axis_name', '_info_axis_number', '_info_repr', '_init_mgr', '_inplace_method', '_internal_names', '_internal_names_set', '_is_copy', '_is_homogeneous_type', '_is_label_or_level_reference', '_is_label_reference', '_is_level_reference', '_is_mixed_type', '_is_view', '_iset_item', '_iset_item_mgr', '_iset_not_inplace', '_item_cache', '_iter_column_arrays', '_ixs', '_join_compat', '_logical_func', '_logical_method', '_maybe_cache_changed', '_maybe_update_cacher', '_metadata', '_mgr', '_min_count_stat_function', '_needs_reindex_multi', '_protect_consolidate', '_reduce', '_reduce_axis1', '_reindex_axes', '_reindex_columns', '_reindex_index', '_reindex_multi', '_reindex_with_indexers', '_rename', '_replace_columnwise', '_repr_data_resource_', '_repr_fits_horizontal_', '_repr_fits_vertical_', '_repr_html_', '_repr_latex_', '_reset_cache', '_reset_cacher', '_sanitize_column', '_series', '_set_axis', '_set_axis_name', '_set_axis_nocheck', '_set_is_copy', '_set_item', '_set_item_frame_value', '_set_item_mgr', '_set_value', '_setitem_array', '_setitem_frame', '_setitem_slice', '_slice', '_stat_axis', '_stat_axis_name', '_stat_axis_number', '_stat_function', '_stat_function_ddof', '_take_with_is_copy', '_to_dict_of_blocks', '_typ', '_update_inplace', '_validate_dtype', '_values', '_where', 'abs', 'add', 'add_prefix', 'add_suffix', 'agg', 'aggregate', 'align', 'all', 'any', 'append', 'apply', 'applymap', 'asfreq', 'asof', 'assign', 'astype', 'at', 'at_time', 'attrs', 'axes', 'backfill', 'between_time', 'bfill', 'bool', 'boxplot', 'clip', 'columns', 'combine', 'combine_first', 'compare', 'convert_dtypes', 'copy', 'corr', 'corrwith', 'count', 'cov', 'cummax', 'cummin', 'cumprod', 'cumsum', 'describe', 'diff', 'div', 'divide', 'dot', 'drop', 'drop_duplicates', 'droplevel', 'dropna', 'dtypes', 'duplicated', 'empty', 'eq', 'equals', 'eval', 'ewm', 'expanding', 'explode', 'ffill', 'fillna', 'filter', 'first', 'first_valid_index', 'flags', 'floordiv', 'from_dict', 'from_records', 'ge', 'get', 'groupby', 'gt', 'head', 'hist', 'iat', 'idxmax', 'idxmin', 'iloc', 'index', 'infer_objects', 'info', 'insert', 'interpolate', 'isin', 'isna', 'isnull', 'items', 'iteritems', 'iterrows', 'itertuples', 'join', 'keys', 'kurt', 'kurtosis', 'last', 'last_valid_index', 'le', 'loc', 'lookup', 'lt', 'mad', 'mask', 'max', 'mean', 'median', 'melt', 'memory_usage', 'merge', 'min', 'mod', 'mode', 'mul', 'multiply', 'ndim', 'ne', 'nlargest', 'notna', 'notnull', 'nsmallest', 'nunique', 'pad', 'pct_change', 'pipe', 'pivot', 'pivot_table', 'plot', 'pop', 'pow', 'prod', 'product', 'quantile', 'query', 'radd', 'rank', 'rdiv', 'reindex', 'reindex_like', 'rename', 'rename_axis', 'reorder_levels', 'replace', 'resample', 'reset_index', 'rfloordiv', 'rmod', 'rmul', 'rolling', 'round', 'rpow', 'rsub', 'rtruediv', 'sample', 'select_dtypes', 'sem', 'set_axis', 'set_flags', 'set_index', 'shape', 'shift', 'size', 'skew', 'slice_shift', 'sort_index', 'sort_values', 'squeeze', 'stack', 'std', 'style', 'sub', 'subtract', 'sum', 'swapaxes', 'swaplevel', 'tail', 'take', 'to_clipboard', 'to_csv', 'to_dict', 'to_excel', 'to_feather', 'to_gbq', 'to_hdf', 'to_html', 'to_json', 'to_latex', 'to_markdown', 'to_numpy', 'to_parquet', 'to_period', 'to_pickle', 'to_records', 'to_sql', 'to_stata', 'to_string', 'to_timestamp', 'to_xarray', 'to_xml', 'transform', 'transpose', 'truediv', 'truncate', 'tz_convert', 'tz_localize', 'unstack', 'update', 'value_counts', 'values', 'var', 'where', 'xs']

All `methods` have parenthesis and typically they take arguments.
However `attributes` do no have parenthesis. Attributes and methods can
be called using the `.` notation.

### DataFrame Attributes

### Dimension and data types

``` python
# Print the dimension of the dataframe
print(df3.shape)

# Print the dataframe column types
print(df3.dtypes)
```

    (51, 6)
    Unnamed: 0          int64
    region             object
    state              object
    individuals       float64
    family_members    float64
    state_pop           int64
    dtype: object

### Columns and Rows

``` python
# Print the column index of dataframe
print(df3.columns)

# Print the row index of dataframe
print(df3.index)
```

    Index(['Unnamed: 0', 'region', 'state', 'individuals', 'family_members',
           'state_pop'],
          dtype='object')
    RangeIndex(start=0, stop=51, step=1)

### DataFrame Methods

### Describe the Data Frame

``` python
# First Rows
print(df.head())

# Last Rows
print(df.tail())
```

                       A         B         C         D
    2013-01-01  0.817994 -0.924007 -1.515711 -0.198598
    2013-01-02  0.673364 -1.914110 -0.126208 -0.282033
    2013-01-03  1.312579  0.340656 -0.300397 -0.838614
    2013-01-04 -0.732977 -0.560867 -0.515910 -0.768784
    2013-01-05 -2.045106 -0.929131 -0.029660  0.529883
                       A         B         C         D
    2013-01-02  0.673364 -1.914110 -0.126208 -0.282033
    2013-01-03  1.312579  0.340656 -0.300397 -0.838614
    2013-01-04 -0.732977 -0.560867 -0.515910 -0.768784
    2013-01-05 -2.045106 -0.929131 -0.029660  0.529883
    2013-01-06 -1.343257 -0.250821 -0.046303  0.944569

### Information

``` python
print(df.info())
```

    <class 'pandas.core.frame.DataFrame'>
    DatetimeIndex: 6 entries, 2013-01-01 to 2013-01-06
    Freq: D
    Data columns (total 4 columns):
     #   Column  Non-Null Count  Dtype  
    ---  ------  --------------  -----  
     0   A       6 non-null      float64
     1   B       6 non-null      float64
     2   C       6 non-null      float64
     3   D       6 non-null      float64
    dtypes: float64(4)
    memory usage: 240.0 bytes
    None

### Sort a DataFrame

``` python
# Sortdf3by individuals (ascending)
df3_ind = df3.sort_values("individuals") 

# Print the top few rows
print(df3_ind.head())

# Sortdf3by individuals (descending)
df3_ind = df3.sort_values("individuals", ascending=False) 

# Print the top few rows
print(df3_ind.head())


# Sortdf3by region ascending, then descending family members
df3_reg_fam = df3.sort_values(['region', 'family_members'], ascending=[True, False])

# Print the top few rows
print(df3_reg_fam.head())
```

        Unnamed: 0              region  ... family_members  state_pop
    50          50            Mountain  ...          205.0     577601
    34          34  West North Central  ...           75.0     758080
    7            7      South Atlantic  ...          374.0     965479
    39          39         New England  ...          354.0    1058287
    45          45         New England  ...          511.0     624358

    [5 rows x 6 columns]
        Unnamed: 0              region  ... family_members  state_pop
    4            4             Pacific  ...        20964.0   39461588
    32          32        Mid-Atlantic  ...        52070.0   19530351
    9            9      South Atlantic  ...         9587.0   21244317
    43          43  West South Central  ...         6111.0   28628666
    47          47             Pacific  ...         5880.0    7523869

    [5 rows x 6 columns]
        Unnamed: 0              region  ... family_members  state_pop
    13          13  East North Central  ...         3891.0   12723071
    35          35  East North Central  ...         3320.0   11676341
    22          22  East North Central  ...         3142.0    9984072
    49          49  East North Central  ...         2167.0    5807406
    14          14  East North Central  ...         1482.0    6695497

    [5 rows x 6 columns]

## Indexing

By default when we create a dataframe from scratch, Pandas assigns two
indexes for rows and columns using integers ranging from zero until the
last value, for instance, the `df4` that was created from a 2D array.

-   Column index

``` python
df4.columns
```

    RangeIndex(start=0, stop=5, step=1)

-   Row index

``` python
df4.index
```

    RangeIndex(start=0, stop=5, step=1)

However, in dataframes created from a `csv` we have column names by
default and whole numbers as indexes of the rows. For instance, the
dataframes `df6` and `df7`.

-   Column index

``` python
# Examples of column indexes
df6.columns

df7.columns
```

    Index(['Unnamed: 0', 'store', 'type', 'department', 'date', 'weekly_sales',
           'is_holiday', 'temperature_c', 'fuel_price_usd_per_l', 'unemployment'],
          dtype='object')
    Index(['Unnamed: 0', 'date', 'city', 'country', 'avg_temp_c'], dtype='object')

-   Row index

``` python
# Examples of row indexes
df6.index

df6.index
```

    RangeIndex(start=0, stop=10774, step=1)
    RangeIndex(start=0, stop=10774, step=1)

Changing column names is straightforward:

``` python
# Old
print(df9)


df9.columns = ['A', 'B', 'C']
# New
print(df9)
```

             date  small_sold  large_sold
    0  2019-11-03    10376832     7835071
    1  2019-11-10    10717154     8561348
                A         B        C
    0  2019-11-03  10376832  7835071
    1  2019-11-10  10717154  8561348

Is possible to use one column as a row index, as follows:

``` python
df7_1 = df7.set_index("city")
df7_1.head()
```

             Unnamed: 0        date        country  avg_temp_c
    city                                                      
    Abidjan           0  2000-01-01  Côte D'Ivoire      27.293
    Abidjan           1  2000-02-01  Côte D'Ivoire      27.685
    Abidjan           2  2000-03-01  Côte D'Ivoire      29.061
    Abidjan           3  2000-04-01  Côte D'Ivoire      28.162
    Abidjan           4  2000-05-01  Côte D'Ivoire      27.547

Dropping the index works as follows:

``` python
df7_1.reset_index().head()
```

          city  Unnamed: 0        date        country  avg_temp_c
    0  Abidjan           0  2000-01-01  Côte D'Ivoire      27.293
    1  Abidjan           1  2000-02-01  Côte D'Ivoire      27.685
    2  Abidjan           2  2000-03-01  Côte D'Ivoire      29.061
    3  Abidjan           3  2000-04-01  Côte D'Ivoire      28.162
    4  Abidjan           4  2000-05-01  Côte D'Ivoire      27.547

Once row-indexed, ideally, you would like to sort the dataframe
according to this index.

``` python
print(df7_1.sort_index())
```

             Unnamed: 0        date        country  avg_temp_c
    city                                                      
    Abidjan           0  2000-01-01  Côte D'Ivoire      27.293
    Abidjan         106  2008-11-01  Côte D'Ivoire      27.302
    Abidjan         107  2008-12-01  Côte D'Ivoire      27.472
    Abidjan         108  2009-01-01  Côte D'Ivoire      26.912
    Abidjan         109  2009-02-01  Côte D'Ivoire      28.224
    ...             ...         ...            ...         ...
    Xian          16391  2004-09-01          China      17.889
    Xian          16392  2004-10-01          China      11.229
    Xian          16393  2004-11-01          China       5.720
    Xian          16395  2005-01-01          China      -2.209
    Xian          16499  2013-09-01          China         NaN

    [16500 rows x 4 columns]

## Subsetting rows

To subset specific values of the dataframe we can filter columns using
relational operators (Boolean conditions) to return `True` of `False`
subsets of the dataframe. There are at least two common ways to achieve
this same objective. Imagine, you want to subset the rows from `df3`
where the column `individuals` is greater than 10000.

For example, passing the column as an attribute

``` python
df3[df3.individuals>10000]
```

        Unnamed: 0              region  ... family_members  state_pop
    4            4             Pacific  ...        20964.0   39461588
    9            9      South Atlantic  ...         9587.0   21244317
    32          32        Mid-Atlantic  ...        52070.0   19530351
    37          37             Pacific  ...         3337.0    4181886
    43          43  West South Central  ...         6111.0   28628666
    47          47             Pacific  ...         5880.0    7523869

    [6 rows x 6 columns]

Alternatively, we can directly subset passing
`df3["individuals"]>10000`, which is transformed into an object of
`<class 'pandas.core.series.Series'>`

``` python
print(type(df3["individuals"]>10000))

df3[df3["individuals"]>10000]
```

    <class 'pandas.core.series.Series'>
        Unnamed: 0              region  ... family_members  state_pop
    4            4             Pacific  ...        20964.0   39461588
    9            9      South Atlantic  ...         9587.0   21244317
    32          32        Mid-Atlantic  ...        52070.0   19530351
    37          37             Pacific  ...         3337.0    4181886
    43          43  West South Central  ...         6111.0   28628666
    47          47             Pacific  ...         5880.0    7523869

    [6 rows x 6 columns]

Another way to subset different rows is by using the method `loc`, which
takes advantage of the rows and columns indexes.

### Subsetting rows using the `loc`

-   We use the `[rows, columns]` brackets after the dataframe to
    distinguish between rows and columns.

-   Indexes of rows and columns are typically `strings` nested in `list`
    objects.

-   To subset range of rows or columns is easy with the `:` slicing
    operator

Let’s look a the `df7`, first we set the column `city` as a row index,
and then we pass the list `cities` to map all the rows of the cities
`"Moscow", "Saint Petersburg"`.

``` python
cities = ["Abidjan", "Xian"]
df7_1.loc[cities].head()
```

             Unnamed: 0        date        country  avg_temp_c
    city                                                      
    Abidjan           0  2000-01-01  Côte D'Ivoire      27.293
    Abidjan           1  2000-02-01  Côte D'Ivoire      27.685
    Abidjan           2  2000-03-01  Côte D'Ivoire      29.061
    Abidjan           3  2000-04-01  Côte D'Ivoire      28.162
    Abidjan           4  2000-05-01  Côte D'Ivoire      27.547

Going further we can specify multilevel indexes, that is, indexes nested
inside other indexes. Lets give an example were we nest the column
`country` inside the index of `city` from the dataset `df7`.

``` python
# Index df7 by country & city
df7_1 = df7.set_index(["country", "city"])

# List of tuples: Brazil, Rio De Janeiro & Pakistan, Lahore
rows_to_keep = [("Brazil", "Rio De Janeiro"), ("Pakistan", "Lahore")] # this is a list
print(df7_1.loc[rows_to_keep].head())
```

                            Unnamed: 0        date  avg_temp_c
    country city                                              
    Brazil  Rio De Janeiro       12540  2000-01-01      25.974
            Rio De Janeiro       12541  2000-02-01      26.699
            Rio De Janeiro       12542  2000-03-01      26.270
            Rio De Janeiro       12543  2000-04-01      25.750
            Rio De Janeiro       12544  2000-05-01      24.356

Now that we have two indexes is possible to sort the data accordingly

``` python
df7_1.sort_index(level=["country", "city"], ascending=[True, False]).head()
```

                       Unnamed: 0        date  avg_temp_c
    country     city                                     
    Afghanistan Kabul        7260  2000-01-01       3.326
                Kabul        7261  2000-02-01       3.454
                Kabul        7262  2000-03-01       9.612
                Kabul        7263  2000-04-01      17.925
                Kabul        7264  2000-05-01      24.658

Using the `loc` method is easy to slice blocks of values using the
indexes. For instance, in the `df7_1`, that was indexed and sorted, we
can pass the range `"Pakistan":"Russia"`, which will subset this set of
values from the dataframe. Is important to sort the data.frame before
passing the indexes of rows as follows:

``` python
df7_1 = df7_1.sort_index()
df7_1.loc["Pakistan":"Russia"]
```

                               Unnamed: 0        date  avg_temp_c
    country  city                                                
    Pakistan Faisalabad              4785  2000-01-01      12.792
             Faisalabad              4786  2000-02-01      14.339
             Faisalabad              4787  2000-03-01      20.309
             Faisalabad              4788  2000-04-01      29.072
             Faisalabad              4789  2000-05-01      34.845
    ...                               ...         ...         ...
    Russia   Saint Petersburg       13360  2013-05-01      12.355
             Saint Petersburg       13361  2013-06-01      17.185
             Saint Petersburg       13362  2013-07-01      17.234
             Saint Petersburg       13363  2013-08-01      17.153
             Saint Petersburg       13364  2013-09-01         NaN

    [1155 rows x 3 columns]

Finally, given that we have indexed the `df7_1` according to two
columns, we can subset pairs of index values and return a given set of
rows.

``` python
df7_1.loc[("Pakistan","Lahore"):("Russia", "Moscow")].head()
```

                     Unnamed: 0        date  avg_temp_c
    country  city                                      
    Pakistan Lahore        8415  2000-01-01      12.792
             Lahore        8416  2000-02-01      14.339
             Lahore        8417  2000-03-01      20.309
             Lahore        8418  2000-04-01      29.072
             Lahore        8419  2000-05-01      34.845

### Subsetting rows using the `iloc`

Using `iloc` with a Dataframe is similar to the `loc`:

-   We use the `[rows, columns]` brackets after the dataframe to
    distinguish between rows and columns.

-   Indexes of rows and columns are typically integers starting from
    zero.

-   To subset range of rows or columns is easy with the `:` slicing
    operator

Subset the first five rows

``` python
df7.iloc[:5, :]
```

       Unnamed: 0        date     city        country  avg_temp_c
    0           0  2000-01-01  Abidjan  Côte D'Ivoire      27.293
    1           1  2000-02-01  Abidjan  Côte D'Ivoire      27.685
    2           2  2000-03-01  Abidjan  Côte D'Ivoire      29.061
    3           3  2000-04-01  Abidjan  Côte D'Ivoire      28.162
    4           4  2000-05-01  Abidjan  Côte D'Ivoire      27.547

### Subsetting rows in two columns or more

A more complex example involves a subset involving filtering of two
columns. We are going to subset in two levels grouping each condition
inside `()` parenthesis as follows:

``` python
print(df3[(df3["state_pop"] > 5000000) & (df3["individuals"]> 5000)])
```

        Unnamed: 0              region  ... family_members  state_pop
    2            2            Mountain  ...         2606.0    7158024
    4            4             Pacific  ...        20964.0   39461588
    5            5            Mountain  ...         3250.0    5691287
    9            9      South Atlantic  ...         9587.0   21244317
    10          10      South Atlantic  ...         2556.0   10511131
    13          13  East North Central  ...         3891.0   12723071
    21          21         New England  ...        13257.0    6882635
    22          22  East North Central  ...         3142.0    9984072
    30          30        Mid-Atlantic  ...         3350.0    8886025
    32          32        Mid-Atlantic  ...        52070.0   19530351
    33          33      South Atlantic  ...         2817.0   10381615
    35          35  East North Central  ...         3320.0   11676341
    38          38        Mid-Atlantic  ...         5349.0   12800922
    42          42  East South Central  ...         1744.0    6771631
    43          43  West South Central  ...         6111.0   28628666
    47          47             Pacific  ...         5880.0    7523869

    [16 rows x 6 columns]

Another example, in `df3` filter for rows where family_members is less
than 1000 and region is Pacific.

``` python
df3[(df3.family_members < 1000) & (df3.region == "Pacific")]
```

       Unnamed: 0   region   state  individuals  family_members  state_pop
    1           1  Pacific  Alaska       1434.0           582.0     735139

Finally, we can subset from a list of options using the method `isin()`.

``` python
# The Mojave Desert states
canu = ["California", "Arizona", "Nevada", "Utah"]

# Filter for rows in the Mojave Desert states
df3[df3.state.isin(canu)].head()
```

        Unnamed: 0    region       state  individuals  family_members  state_pop
    2            2  Mountain     Arizona       7259.0          2606.0    7158024
    4            4   Pacific  California     109008.0         20964.0   39461588
    28          28  Mountain      Nevada       7058.0           486.0    3027341
    44          44  Mountain        Utah       1904.0           972.0    3153550

### Subsetting columns

To subset, it is necessary to know the column names of the dataframe.
For instance, the column names of the dataframe `df4` can be retrieved
using the attribute `df4.columns.values`, as follows:

``` python
print(df4.columns.values)
```

    [0 1 2 3 4]

Knowing the column index it is easy then to subset the dataframe:

``` python
# First column
df4[[0]]

# Last column
df4[[4]]
```

        0
    0   1
    1   6
    2  11
    3  16
    4  21
        4
    0   5
    1  10
    2  15
    3  20
    4  25

Another example using the dataframe `df3` whose column indexes are

``` python
print(df3.columns.values)
```

    ['Unnamed: 0' 'region' 'state' 'individuals' 'family_members' 'state_pop']

We can pass a list of column names to subset the `state` and
`family_members` columns as follows:

``` python
# select two columns
df3[["state", "family_members"]].head()
```

            state  family_members
    0     Alabama           864.0
    1      Alaska           582.0
    2     Arizona          2606.0
    3    Arkansas           432.0
    4  California         20964.0

To subset columns using the `loc` method we have to select the rows and
columns that we are selecting. If we intend to select all the rows and
we only are subsetting columns, we have to pass the `:` slice operator.

``` python
df3.loc[:, ["state", "family_members"]].head()
```

            state  family_members
    0     Alabama           864.0
    1      Alaska           582.0
    2     Arizona          2606.0
    3    Arkansas           432.0
    4  California         20964.0

Another example using the `df7`

``` python
df7.loc[:, ["city", "country"]].head()
```

          city        country
    0  Abidjan  Côte D'Ivoire
    1  Abidjan  Côte D'Ivoire
    2  Abidjan  Côte D'Ivoire
    3  Abidjan  Côte D'Ivoire
    4  Abidjan  Côte D'Ivoire

Similarly, to the `loc` method, subsetting columns with the `iloc`
method uses integers to map columns. For instance subsetting the columns
`["city", "country"]` from `df7`. The slice operators `:` using the
`iloc` method states that we are calling all the rows or columns.

``` python
df7.columns
df7.iloc[:, [1,3]].head()
```

    Index(['Unnamed: 0', 'date', 'city', 'country', 'avg_temp_c'], dtype='object')
             date        country
    0  2000-01-01  Côte D'Ivoire
    1  2000-02-01  Côte D'Ivoire
    2  2000-03-01  Côte D'Ivoire
    3  2000-04-01  Côte D'Ivoire
    4  2000-05-01  Côte D'Ivoire

## Subsetting rows and columns

First, locate the rows of the second column that comply with the rule.
In this example, we locate elements that are divisible by `2`.

``` python
# Subset elements of the second column that are divisible by two
rows = df4[1] % 2 == 0
print(type(rows))
```

    <class 'pandas.core.series.Series'>

Notice that Python creates an object of type
`pandas.core.series.Series`. Next, we use this object to subset the
elements of the second column in the following way:

``` python
df5 = df4[[1]][rows]

print(df5.shape)
print(type(df5))
print(df5)
```

    (3, 1)
    <class 'pandas.core.frame.DataFrame'>
        1
    0   2
    2  12
    4  22

Another method of subsetting rows and columns is by using indexes and
the `loc` method. Recall that this method works only if the dataset
contains indexes and is sorted accordingly. To refresh these steps,
let’s perform the following operations:

``` python
df7_1 = df7.set_index(["country", "city"]) # set the indexes
df7_1 = df7_1.sort_index() # sort the dataframe descending
```

Now we can subset all rows that contain the country `Zimbabwe` on the
column `date`, as follows:

``` python
df7_1.loc["Zimbabwe", "date"].head()

type(df7_1.index.values)
```

    city
    Harare    2000-01-01
    Harare    2000-02-01
    Harare    2000-03-01
    Harare    2000-04-01
    Harare    2000-05-01
    Name: date, dtype: object
    <class 'numpy.ndarray'>

### Subsetting rows and columns using the `iloc`

This method is similar to the `loc` method, but instead of using
`strings` as indexes, we use integers to call rows and columns. We
follow these two rules:

-   We use the `[rows, columns]` brackets to distinguish between rows
    and columns.

-   Indexes of rows and columns are numbers that typically start in `0`.

Recall `df4`

``` python
print(df4)
```

        0   1   2   3   4
    0   1   2   3   4   5
    1   6   7   8   9  10
    2  11  12  13  14  15
    3  16  17  18  19  20
    4  21  22  23  24  25

Subset the first and last element of `df4`

``` python
# Subset the first element of df4
print(df4.iloc[0,0])

# Subset the last element of df4
print(df4.iloc[4,4])
```

    1
    25

Extract the first column

``` python
df4.iloc[:,[0]]
```

        0
    0   1
    1   6
    2  11
    3  16
    4  21

Extract the first row

``` python
df4.iloc[[0],:]
```

       0  1  2  3  4
    0  1  2  3  4  5

Extract the last 10 elements of the second column

``` python
df7.iloc[(df7.shape[0]-11):(df7.shape[0]-1), [1]]
```

                 date
    16489  2012-11-01
    16490  2012-12-01
    16491  2013-01-01
    16492  2013-02-01
    16493  2013-03-01
    16494  2013-04-01
    16495  2013-05-01
    16496  2013-06-01
    16497  2013-07-01
    16498  2013-08-01

Get the first 5 rows of columns 3 and 4.

``` python
df7.iloc[:4, 2:4]
```

          city        country
    0  Abidjan  Côte D'Ivoire
    1  Abidjan  Côte D'Ivoire
    2  Abidjan  Côte D'Ivoire
    3  Abidjan  Côte D'Ivoire

Extract all elements in the first row that comply with a condition. For
this example we are going to nest the condition of all the values in the
first row greater than two, `df4.iloc[0,:]>2`. Then we are using the
`np.where` method to locate the indexes of elements that contain a
`True` boolean.

``` python
df4.iloc[[0], np.where(df4.iloc[0,:]>2)[0]]
```

       2  3  4
    0  3  4  5

## Transforming

### Describe (Summary Statistics)

``` python
# mean
print(df3.state_pop.mean())

# median
print(df3.state_pop.median())

# variance
print(df3.state_pop.var())

# standard deviation
print(df3.state_pop.std())

# min value
# standard deviation
print(df3.state_pop.min())

# max value
print(df3.state_pop.min())

# all together
print(df3.describe())
```

    6405637.274509804
    4461153.0
    53688706994844.23
    7327257.808678784
    577601
    577601
           Unnamed: 0    individuals  family_members     state_pop
    count   51.000000      51.000000       51.000000  5.100000e+01
    mean    25.000000    7225.784314     3504.882353  6.405637e+06
    std     14.866069   15991.025083     7805.411811  7.327258e+06
    min      0.000000     434.000000       75.000000  5.776010e+05
    25%     12.500000    1446.500000      592.000000  1.777414e+06
    50%     25.000000    3082.000000     1482.000000  4.461153e+06
    75%     37.500000    6781.500000     3196.000000  7.340946e+06
    max     50.000000  109008.000000    52070.000000  3.946159e+07

If the dataframe contains integers or real numbers is easy to perform
the operations across the columns or rows.

``` python
# Mean of rows across columns
df4.mean(axis=1)

# Mean of columns across columns
df4.mean(axis=0)
```

    0     3.0
    1     8.0
    2    13.0
    3    18.0
    4    23.0
    dtype: float64
    0    11.0
    1    12.0
    2    13.0
    3    14.0
    4    15.0
    dtype: float64

### Column operations

The main column operations are:

-   Sum

``` python
print(df3.state_pop.sum())
```

    326687501

-   Cumulative sum

``` python
print(df3.state_pop.cumsum())
```

    0       4887681
    1       5622820
    2      12780844
    3      15790577
    4      55252165
    5      60943452
    6      64514972
    7      65480451
    8      66181998
    9      87426315
    10     97937446
    11     99358039
    12    101108575
    13    113831646
    14    120527143
    15    123675761
    16    126587120
    17    131048273
    18    135707963
    19    137047020
    20    143082822
    21    149965457
    22    159949529
    23    165555778
    24    168536798
    25    174658421
    26    175719086
    27    177644700
    28    180672041
    29    182025506
    30    190911531
    31    193004272
    32    212534623
    33    222916238
    34    223674318
    35    235350659
    36    239290894
    37    243472780
    38    256273702
    39    257331989
    40    262416145
    41    263294843
    42    270066474
    43    298695140
    44    301848690
    45    302473048
    46    310974334
    47    318498203
    48    320302494
    49    326109900
    50    326687501
    Name: state_pop, dtype: int64

-   Cumulative product

``` python
print(df3.state_pop.cumprod())
```

    0                 4887681
    1           3593124922659
    2     7272930357681714200
    3     7903566051232904824
    4    -6717292260295177376
    5     8873061169631614368
    6     8148294484792166400
    7     5819023669836478464
    8    -1205241372944291840
    9    -6292177132517226496
    10    6622373097463437312
    11    4962005595153618944
    12    3470577629245915136
    13   -8423188867997155328
    14   -2225371326546493440
    15    3946997816422858752
    16    5096266778097451008
    17    1136688303390556160
    18    1494541717077688320
    19    7730232222543446016
    20    8113663438137196544
    21   -1654939752842264576
    22    6166687450565443584
    23    1500558237656678400
    24    6253697334853500928
    25   -8790508571491041280
    26   -7109132568401805312
    27   -5744006173422518272
    28   -2284299832833081344
    29   -8673003558171312128
    30   -3504656614122586112
    31   -5377308965807849472
    32   -4878392185126387712
    33    1709610911523667968
    34    8941421250245296128
    35    9215048314536329216
    36   -8334418405679431680
    37    4198662944055099392
    38   -8723413785341067264
    39     581225513859678208
    40    1910243011917250560
    41    2130586611002376192
    42   -2684937009104945152
    43   -2708850407756529664
    44    7509713552135946240
    45   -6781182851288137728
    46   -6382118816838582272
    47   -4484145143506534400
    48    2332118313460563968
    49   -4719128645426216960
    50   -8733419210157326336
    Name: state_pop, dtype: int64

### Adding new columns

To add new columns we can take a dataframe, for instance `df4`, write
the new index (or column name) and then pass the values on the left of
`=` as follows

``` python
# add columns 3 and 4 and save them on a new column
df4[5] = df4[2] + df4[3]

# estimate column 3 as a proportion of column 5 and add the result in a new column
df4[6] = df4[2] / df4[5]

print(df4)
```

        0   1   2   3   4   5         6
    0   1   2   3   4   5   7  0.428571
    1   6   7   8   9  10  17  0.470588
    2  11  12  13  14  15  27  0.481481
    3  16  17  18  19  20  37  0.486486
    4  21  22  23  24  25  47  0.489362

If the columns do not have a numeric index, but a string name, the
procedure to add a new column is by passing a string with the name of
the new column, as follows:

``` python
# Create indiv_per_10k col as homeless individuals per 10k state pop
df3["indiv_per_10k"] = 10000 * df3.individuals / df3.state_pop   
```

### Converting column types

Transform the first column into a `datetime64[ns]`

``` python
# Print class of object
print(df7["date"].dtypes) # column date is an object

# transform 
df7["date"] = pd.to_datetime(df7["date"])

# Print the new class of object
print(df7["date"].dtypes)  # column date is an object
```

    object
    datetime64[ns]

Now that `date` is of class `datetime64[ns]`, we can create new columns
of year, month or day

``` python
# Add a year column to temperatures
df7["year"] = df7["date"].dt.year
df7["month"] = df7["date"].dt.month
df7["day"] = df7["date"].dt.day

df7.head()
print(df7.dtypes)
```

       Unnamed: 0       date     city        country  avg_temp_c  year  month  day
    0           0 2000-01-01  Abidjan  Côte D'Ivoire      27.293  2000      1    1
    1           1 2000-02-01  Abidjan  Côte D'Ivoire      27.685  2000      2    1
    2           2 2000-03-01  Abidjan  Côte D'Ivoire      29.061  2000      3    1
    3           3 2000-04-01  Abidjan  Côte D'Ivoire      28.162  2000      4    1
    4           4 2000-05-01  Abidjan  Côte D'Ivoire      27.547  2000      5    1
    Unnamed: 0             int64
    date          datetime64[ns]
    city                  object
    country               object
    avg_temp_c           float64
    year                   int64
    month                  int64
    day                    int64
    dtype: object

Here is another example using `df11`, columns two and three are strings
that can be transformed into numeric elements.

``` python
print(df11.dtypes)


df11[['two', 'three']] = df11[['two', 'three']].astype(float)
```

    one      object
    two      object
    three    object
    dtype: object

### Aggregating

The aggregate method works by defining a function that latter is going
to be called on each column of a dataframe using the method `agg()`

For instance, consider the following function that computes the 75% and
the 25% quantiles

``` python
def iqr(column):
    return column.quantile(0.75) - column.quantile(0.25)
```

We can use this function on columns one and three of the `df4` dataframe
as follows:

``` python
print(df4[[0, 2]].agg(iqr))
```

    0    10.0
    2    10.0
    dtype: float64

`agg()` can take more than one function, for instance

``` python
print(df4[[0, 2]].agg([iqr, np.median, np.mean]))
```

               0     2
    iqr     10.0  10.0
    median  11.0  13.0
    mean    11.0  13.0

### Grouping

For grouping, we use the method `.groupby()` from the `pandas` library
that splits a dataframe according to a certain categorical variable. The
following snipped splits the dataframe using the variable `type` in two
categories, and then computes the `sum()` of the column `weekly_sales`.

``` python
df6.groupby("type")["weekly_sales"].sum()
```

    type
    A    2.337163e+08
    B    2.317840e+07
    Name: weekly_sales, dtype: float64

We can even take more than one category

``` python
df6.groupby(["type", "is_holiday"])["weekly_sales"].sum()
```

    type  is_holiday
    A     False         2.336927e+08
          True          2.360181e+04
    B     False         2.317678e+07
          True          1.621410e+03
    Name: weekly_sales, dtype: float64

Now we can use the `.groupby` together with the `agg` functions to
calculate the min, max, mean and median of a variable.

``` python
df6.groupby("type")[["unemployment", "fuel_price_usd_per_l"]].agg([np.mean, np.median, np.max, np.min])
```

         unemployment                ... fuel_price_usd_per_l                    
                 mean median   amax  ...               median      amax      amin
    type                             ...                                         
    A        7.972611  8.067  8.992  ...             0.735455  1.107410  0.664129
    B        9.279323  9.199  9.765  ...             0.803348  1.107674  0.760023

    [2 rows x 8 columns]

### Dealing with NaN values

``` python
# Initial number of rows
na_rows = df8.shape[0]

# Report the sum of NaN values in each column
df8.isna().sum()

# Report the sum of NaN values in each column as a proportion 
df8.isna().sum()/df8.shape[0]
```

    Country/Region    171061
    Province/State    223208
    Latitude          171062
    Longitude         171062
    Confirmed             19
    Recovered            386
    Deaths               432
    Date                   0
    dtype: int64
    Country/Region    0.137736
    Province/State    0.179724
    Latitude          0.137736
    Longitude         0.137736
    Confirmed         0.000015
    Recovered         0.000311
    Deaths            0.000348
    Date              0.000000
    dtype: float64

Imputing `NaN` values with zero

``` python
#Impute NaN with Zero
df8_1 = df8.fillna(0)

#Display no NaNs
df8_1.isna().any()
```

    Country/Region    False
    Province/State    False
    Latitude          False
    Longitude         False
    Confirmed         False
    Recovered         False
    Deaths            False
    Date              False
    dtype: bool

Removing rows with missing values

``` python
# Drop Na values
df8 = df8.dropna()

# How many rows were dropped?
na_rows - df8.shape[0]
```

    223572

### Pivot Tables

The pivot table is another method to transform data using categorical
variables to split the dataframe. By default, the `.pivot_table` method
computes the mean of a variable.

``` python
# Pivot for mean weekly_sales for each store type
df6.pivot_table(values="weekly_sales", index="type")
```

          weekly_sales
    type              
    A     23674.667242
    B     25696.678370

An example selecting two variables

``` python
# Pivot for mean weekly_sales for each store type
df6.pivot_table(values=["weekly_sales", "unemployment"], index="type")
```

          unemployment  weekly_sales
    type                            
    A         7.972611  23674.667242
    B         9.279323  25696.678370

We can extend the pivot table capabilities by passing two functions
instead of one, as follows

``` python
# Pivot for mean weekly_sales for each store type
df6.pivot_table(values="weekly_sales", index="type", aggfunc=[np.mean, np.median])
```

                  mean       median
          weekly_sales weekly_sales
    type                           
    A     23674.667242     11943.92
    B     25696.678370     13336.08

We can split the dataframe passing one variable as `index` and another
as `columns`

``` python
df6.pivot_table(values="weekly_sales", index="type", columns="is_holiday")
```

    is_holiday         False       True
    type                               
    A           23768.583523  590.04525
    B           25751.980533  810.70500

Create a pivot table adding the `avg_temp_c` column from `df7`, with
`country` and `city` as rows, and `year` as columns.

``` python
df7["year"] = df7["date"].dt.year
```

Compute over two variables and replaces the `NaN` values, adding a `sum`
of the columns and rows with the argument `margins=True`.

``` python
df6.pivot_table(values="weekly_sales", index="department", columns=["store", "type"], fill_value=0, margins=True)
```

    store                  1             2  ...            39           All
    type                   A             A  ...             A              
    department                              ...                            
    1           23491.755000  32392.588333  ...  21423.068333  32052.467153
    2           47421.124167  68156.664167  ...  60768.638333  71380.022778
    3           12872.590000  17012.000000  ...  16847.852500  18278.390625
    4           38382.255833  47650.447500  ...  41670.077500  44863.253681
    5           23761.120000  30331.717500  ...  23466.439167  37189.000000
    ...                  ...           ...  ...           ...           ...
    96          27897.153333  33841.960833  ...  24947.875833  20337.607681
    97          33771.761667  40757.997500  ...  23002.670000  26584.400833
    98          10853.782500  14009.203333  ...   9089.097500  11820.590278
    99            466.364545    455.516364  ...    317.189091    379.123659
    All         20896.941787  26517.435162  ...  18414.938423  23843.950149

    [81 rows x 13 columns]

## Exporting

### DataFrame to CSV

The most common format to export data is by saving the dataframe on a
`csv` file

``` python
df9.to_csv("df9.csv")
```

### DataFrame to Latex

``` python
print(df.style.to_latex())
```

    \begin{tabular}{lrrrr}
     & A & B & C & D \\
    2013-01-01 00:00:00 & 0.817994 & -0.924007 & -1.515711 & -0.198598 \\
    2013-01-02 00:00:00 & 0.673364 & -1.914110 & -0.126208 & -0.282033 \\
    2013-01-03 00:00:00 & 1.312579 & 0.340656 & -0.300397 & -0.838614 \\
    2013-01-04 00:00:00 & -0.732977 & -0.560867 & -0.515910 & -0.768784 \\
    2013-01-05 00:00:00 & -2.045106 & -0.929131 & -0.029660 & 0.529883 \\
    2013-01-06 00:00:00 & -1.343257 & -0.250821 & -0.046303 & 0.944569 \\
    \end{tabular}

## References

-   Stack Overflow (2022)

-   Data Camp (2022)

<div id="refs" class="references csl-bib-body hanging-indent">

<div id="ref-datacamp1" class="csl-entry">

Data Camp. 2022. “<span class="nocase">Data Manipulation with pandas -
DataCamp Learn</span>.”
<https://app.datacamp.com/learn/courses/data-manipulation-with-pandas>.

</div>

<div id="ref-stackover1" class="csl-entry">

Stack Overflow. 2022. “<span class="nocase">Change column type in
pandas</span>.”
<https://stackoverflow.com/questions/15891038/change-column-type-in-pandas>.

</div>

</div>
