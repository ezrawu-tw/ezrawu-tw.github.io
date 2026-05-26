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

# Python Pandas 資料分析
### 前言
#### Pandas 簡單來說就是我們生活中使用是試算表

首先要使用必須載入模組

```
import pandas as pd
```

# 如果是 "一維資料" ， 用Series
**串列資料**為底
```
import pandas as pd
s = pd.Series([1, 2, 3, 4])
print(s.max())
``` 
# 如果是 "雙維資料" ， 用DataFrame
**字典資料**為底

DataFrame 組成方法如下：
pandas.DataFrame( data, index, columns, dtype, copy)
参數說明：
data：一組數據(ndarray、series, map, lists, dict )。
index：索引值，或者可以稱為行標籤
columns：列標籤，默認為 RangeIndex (0, 1, 2, …, n) 。
dtype：数據類型。
copy：拷貝數據，默認為 False。

```
#範例1
from cgi import print_form
import pandas as pd
import numpy as np


df2 = pd.DataFrame({'A': 1.,
                    'B': pd.Timestamp('20130102'),
                    'C': pd.Series(1, index=list(range(8)), dtype='float32'),
                    'D': np.array([3] * 8, dtype='int32'),
                    'E': pd.Categorical(["test", "train", "test", "train","test", "train", "test", "train"]),
                    'F': 'foo'})

print(df2.head(2))#前二比
print(df2.tail(2))#後二比
```
![](https://i.imgur.com/5H1Jv0e.png)
# Pandas 對決 Json

```

import pandas as pd

df = pd.read_json('https://static.runoob.com/download/sites.json')
   
print(df.to_string())
```
![](https://i.imgur.com/z6jQjpH.png)


