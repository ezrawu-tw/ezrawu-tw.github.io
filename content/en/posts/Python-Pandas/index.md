---
slug: Python-Pandas
title: Python_Pandas
date: 2025-10-28 12:29:55
tags:
- python
- data_analyist
categories:
  - Note
---
slug: Python-Pandas

# Python Pandas Data Analysis
### Introduction
#### Simply put, Pandas is like the spreadsheet software we use in everyday life.

First, you need to import the module to use it:

```
import pandas as pd
```

# For "one-dimensional data", use Series
Based on **list data**:
```
import pandas as pd
s = pd.Series([1, 2, 3, 4])
print(s.max())
``` 
# For "two-dimensional data", use DataFrame
Based on **dictionary data**.

The DataFrame constructor parameters are as follows:
pandas.DataFrame( data, index, columns, dtype, copy)
Parameter descriptions:
data: a set of data (ndarray, series, map, lists, dict).
index: index values, also known as row labels.
columns: column labels, defaults to RangeIndex (0, 1, 2, …, n).
dtype: data type.
copy: copy data, defaults to False.

```
# Example 1
from cgi import print_form
import pandas as pd
import numpy as np


df2 = pd.DataFrame({'A': 1.,
                    'B': pd.Timestamp('20130102'),
                    'C': pd.Series(1, index=list(range(8)), dtype='float32'),
                    'D': np.array([3] * 8, dtype='int32'),
                    'E': pd.Categorical(["test", "train", "test", "train","test", "train", "test", "train"]),
                    'F': 'foo'})

print(df2.head(2))  # first 2 rows
print(df2.tail(2))  # last 2 rows
```
![](https://i.imgur.com/5H1Jv0e.png)
# Pandas vs JSON

```

import pandas as pd

df = pd.read_json('https://static.runoob.com/download/sites.json')
   
print(df.to_string())
```
![](https://i.imgur.com/z6jQjpH.png)


