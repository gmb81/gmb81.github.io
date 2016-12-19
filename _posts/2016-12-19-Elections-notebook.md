
```python
This is notebook to the election post from earlier this month.
```


```python
import pandas as pd
import numpy as np

```


```python
twenty_sixteen = pd.read_csv('/media/gates/Data1/data/election/election/2016.csv')
```


```python
eighty_four = pd.read_csv('/media/gates/Data1/data/election/election/county.csv')
```


```python
combined = twenty_sixteen
```


```python
combined['STCOU']
```




    0        2013
    1        2016
    2        2020
    3        2050
    4        2060
    5        2068
    6        2070
    7        2090
    8        2100
    9        2105
    10       2110
    11       2122
    12       2130
    13       2150
    14       2164
    15       2170
    16       2180
    17       2185
    18       2188
    19       2195
    20       2198
    21       2220
    22       2230
    23       2240
    24       2261
    25       2270
    26       2275
    27       2282
    28       2290
    29       1001
            ...  
    3111    54097
    3112    54099
    3113    54101
    3114    54103
    3115    54105
    3116    54107
    3117    54109
    3118    56001
    3119    56003
    3120    56005
    3121    56007
    3122    56009
    3123    56011
    3124    56013
    3125    56015
    3126    56017
    3127    56019
    3128    56021
    3129    56023
    3130    56025
    3131    56027
    3132    56029
    3133    56031
    3134    56033
    3135    56035
    3136    56037
    3137    56039
    3138    56041
    3139    56043
    3140    56045
    Name: STCOU, dtype: int64




```python
combined = combined.merge(eighty_four, on=['STCOU'])
```


```python
combined.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>votesDem</th>
      <th>votesGOP</th>
      <th>total</th>
      <th>demPer</th>
      <th>gopPer</th>
      <th>diff</th>
      <th>diffPer</th>
      <th>state</th>
      <th>county</th>
      <th>STCOU</th>
      <th>Areaname</th>
      <th>1984 results Democrat</th>
      <th>1984 election result Republican</th>
      <th>1984 votes other</th>
      <th>Total cal</th>
      <th>Total reported</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>93003</td>
      <td>130413</td>
      <td>246588</td>
      <td>0.377159</td>
      <td>0.52887</td>
      <td>37410</td>
      <td>15.17+ACU-</td>
      <td>AK</td>
      <td>Alaska</td>
      <td>2013</td>
      <td>Aleutians East, AK</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>93003</td>
      <td>130413</td>
      <td>246588</td>
      <td>0.377159</td>
      <td>0.52887</td>
      <td>37410</td>
      <td>15.17+ACU-</td>
      <td>AK</td>
      <td>Alaska</td>
      <td>2016</td>
      <td>Aleutians West, AK</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>93003</td>
      <td>130413</td>
      <td>246588</td>
      <td>0.377159</td>
      <td>0.52887</td>
      <td>37410</td>
      <td>15.17+ACU-</td>
      <td>AK</td>
      <td>Alaska</td>
      <td>2020</td>
      <td>Anchorage, AK</td>
      <td>25403</td>
      <td>62049</td>
      <td>2702</td>
      <td>90154</td>
      <td>90154</td>
    </tr>
    <tr>
      <th>3</th>
      <td>93003</td>
      <td>130413</td>
      <td>246588</td>
      <td>0.377159</td>
      <td>0.52887</td>
      <td>37410</td>
      <td>15.17+ACU-</td>
      <td>AK</td>
      <td>Alaska</td>
      <td>2050</td>
      <td>Bethel, AK</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>93003</td>
      <td>130413</td>
      <td>246588</td>
      <td>0.377159</td>
      <td>0.52887</td>
      <td>37410</td>
      <td>15.17+ACU-</td>
      <td>AK</td>
      <td>Alaska</td>
      <td>2060</td>
      <td>Bristol Bay, AK</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
combined['1984 Diff']= combined['1984 election result Republican']-combined['1984 results Democrat']
```


```python
combined['2016 Diff'] = combined['votesGOP']-combined['votesDem']
```


```python
combined_data = combined[['votesDem', 'votesGOP', 'state', 'county', 'STCOU', '1984 results Democrat',
                          '1984 election result Republican', '1984 Diff','2016 Diff']]
```


```python
sum_1984_Dem = sum(combined['1984 results Democrat'])
sum_1984_Reb = sum(combined['1984 election result Republican'])
sum_2016_Dem = sum(combined['votesDem'])
sum_2016_Reb = sum(combined['votesGOP'])
```


```python
print('1984 Dem', sum_1984_Dem)
print('1984 Rep', sum_1984_Reb)
print('2016 Dem', sum_2016_Dem)
print('2016 Rep', sum_2016_Reb)
```

    1984 Dem 37537186
    1984 Rep 54372639
    2016 Dem 63571033
    2016 Rep 63979765



```python
sum_1984_Reb - sum_1984_Dem
```




    16835453




```python
avg_diff_1984 = np.mean(combined['1984 Diff'])
avg_diff_2016 = np.mean(combined['2016 Diff'])
```


```python
avg_diff_1984
```




    5359.902260426616




```python
avg_diff_2016
```




    130.1279847182426




```python
max_dif_1984 = np.max(combined['1984 Diff'])
max_dif_2016 = np.max(combined['2016 Diff'])
```


```python
max_dif_1984
```




    428741




```python
max_dif_2016
```




    104444




```python
combined.columns.values
```




    array(['votesDem', 'votesGOP', 'total', 'demPer', 'gopPer', 'diff',
           'diffPer', 'state', 'county', 'STCOU', 'Areaname',
           '1984 results Democrat', '1984 election result Republican',
           '1984 votes other', 'Total cal', 'Total reported', '1984 Diff',
           '2016 Diff'], dtype=object)




```python
combined_data = combined[['votesDem', 'votesGOP', '1984 results Democrat', '1984 election result Republican',
                         'STCOU', 'state', 'county', '1984 Diff', '2016 Diff']]
```

Need to make the STCOU a five digit string in order to break it apart accurately


```python
def add_zero(county):
    if len(county)<5:
        while len(county)<5:
            county = '0'+county
        return county
            
    else:
        return county
```


```python
combined_data['STCOU'] = combined_data['STCOU'].apply(str)
```

    /home/gates/anaconda3/envs/math/lib/python3.5/site-packages/ipykernel/__main__.py:1: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      if __name__ == '__main__':



```python
combined_data['STCOU'] = combined_data['STCOU'].apply(add_zero)
```

    /home/gates/anaconda3/envs/math/lib/python3.5/site-packages/ipykernel/__main__.py:1: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      if __name__ == '__main__':



```python
combined_data['AFFGEOID'] = '0500000US'+combined_data['STCOU']
```

    /home/gates/anaconda3/envs/math/lib/python3.5/site-packages/ipykernel/__main__.py:1: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      if __name__ == '__main__':



```python
no_AK = combined_data[combined_data['state']!='AK']
```


```python
no_AK.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>votesDem</th>
      <th>votesGOP</th>
      <th>1984 results Democrat</th>
      <th>1984 election result Republican</th>
      <th>STCOU</th>
      <th>state</th>
      <th>county</th>
      <th>1984 Diff</th>
      <th>2016 Diff</th>
      <th>AFFGEOID</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>29</th>
      <td>5908</td>
      <td>18110</td>
      <td>3366</td>
      <td>8350</td>
      <td>01001</td>
      <td>AL</td>
      <td>Autauga County</td>
      <td>4984</td>
      <td>12202</td>
      <td>0500000US01001</td>
    </tr>
    <tr>
      <th>30</th>
      <td>18409</td>
      <td>72780</td>
      <td>7272</td>
      <td>24964</td>
      <td>01003</td>
      <td>AL</td>
      <td>Baldwin County</td>
      <td>17692</td>
      <td>54371</td>
      <td>0500000US01003</td>
    </tr>
    <tr>
      <th>31</th>
      <td>4848</td>
      <td>5431</td>
      <td>4591</td>
      <td>5459</td>
      <td>01005</td>
      <td>AL</td>
      <td>Barbour County</td>
      <td>868</td>
      <td>583</td>
      <td>0500000US01005</td>
    </tr>
    <tr>
      <th>32</th>
      <td>1874</td>
      <td>6733</td>
      <td>2167</td>
      <td>3487</td>
      <td>01007</td>
      <td>AL</td>
      <td>Bibb County</td>
      <td>1320</td>
      <td>4859</td>
      <td>0500000US01007</td>
    </tr>
    <tr>
      <th>33</th>
      <td>2150</td>
      <td>22808</td>
      <td>3738</td>
      <td>8508</td>
      <td>01009</td>
      <td>AL</td>
      <td>Blount County</td>
      <td>4770</td>
      <td>20658</td>
      <td>0500000US01009</td>
    </tr>
  </tbody>
</table>
</div>




```python
sum_1984_Dem = sum(no_AK['1984 results Democrat'])
sum_1984_Reb = sum(no_AK['1984 election result Republican'])
sum_2016_Dem = sum(no_AK['votesDem'])
sum_2016_Reb = sum(no_AK['votesGOP'])
```


```python
print('1984 Dem', sum_1984_Dem)
print('1984 Rep', sum_1984_Reb)
print('2016 Dem', sum_2016_Dem)
print('2016 Rep', sum_2016_Reb)
```

    1984 Dem 37511783
    1984 Rep 54310590
    2016 Dem 60873946
    2016 Rep 60197788



```python
no_AK.to_csv('/media/gates/Data1/data/election/election/no_AK.csv')
```


```python
no_AK.columns.values
```




    array(['votesDem', 'votesGOP', '1984 results Democrat',
           '1984 election result Republican', 'STCOU', 'state', 'county',
           '1984 Diff', '2016 Diff', 'AFFGEOID'], dtype=object)




```python
Diff_1984 = np.mean(no_AK['1984 Diff'])
Diff_2016 = np.mean(no_AK['2016 Diff'])
```


```python
print(Diff_1984)
print(Diff_2016)
```

    5398.074228791774
    -217.27442159383034



```python
max_1984 = np.max(no_AK['1984 Diff'])
max_2016 = np.max(no_AK['2016 Diff'])
print(max_1984)
print(max_2016)
```

    428741
    104444



```python
no_AK.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>votesDem</th>
      <th>votesGOP</th>
      <th>1984 results Democrat</th>
      <th>1984 election result Republican</th>
      <th>STCOU</th>
      <th>state</th>
      <th>county</th>
      <th>1984 Diff</th>
      <th>2016 Diff</th>
      <th>AFFGEOID</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>29</th>
      <td>5908</td>
      <td>18110</td>
      <td>3366</td>
      <td>8350</td>
      <td>01001</td>
      <td>AL</td>
      <td>Autauga County</td>
      <td>4984</td>
      <td>12202</td>
      <td>0500000US01001</td>
    </tr>
    <tr>
      <th>30</th>
      <td>18409</td>
      <td>72780</td>
      <td>7272</td>
      <td>24964</td>
      <td>01003</td>
      <td>AL</td>
      <td>Baldwin County</td>
      <td>17692</td>
      <td>54371</td>
      <td>0500000US01003</td>
    </tr>
    <tr>
      <th>31</th>
      <td>4848</td>
      <td>5431</td>
      <td>4591</td>
      <td>5459</td>
      <td>01005</td>
      <td>AL</td>
      <td>Barbour County</td>
      <td>868</td>
      <td>583</td>
      <td>0500000US01005</td>
    </tr>
    <tr>
      <th>32</th>
      <td>1874</td>
      <td>6733</td>
      <td>2167</td>
      <td>3487</td>
      <td>01007</td>
      <td>AL</td>
      <td>Bibb County</td>
      <td>1320</td>
      <td>4859</td>
      <td>0500000US01007</td>
    </tr>
    <tr>
      <th>33</th>
      <td>2150</td>
      <td>22808</td>
      <td>3738</td>
      <td>8508</td>
      <td>01009</td>
      <td>AL</td>
      <td>Blount County</td>
      <td>4770</td>
      <td>20658</td>
      <td>0500000US01009</td>
    </tr>
  </tbody>
</table>
</div>




```python
combined_no_AK = combined[combined['state']!='AK']
```


```python
#realized I didn't include the initial totals for the elections
no_AK['2016 total'] = combined_no_AK['total']
no_AK['1984 total'] = combined_no_AK['Total cal']
```

    /home/gates/anaconda3/envs/math/lib/python3.5/site-packages/ipykernel/__main__.py:2: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      from ipykernel import kernelapp as app
    /home/gates/anaconda3/envs/math/lib/python3.5/site-packages/ipykernel/__main__.py:3: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      app.launch_new_instance()



```python

```


```python
no_AK.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>votesDem</th>
      <th>votesGOP</th>
      <th>1984 results Democrat</th>
      <th>1984 election result Republican</th>
      <th>STCOU</th>
      <th>state</th>
      <th>county</th>
      <th>1984 Diff</th>
      <th>2016 Diff</th>
      <th>AFFGEOID</th>
      <th>2016 total</th>
      <th>1984 total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>29</th>
      <td>5908</td>
      <td>18110</td>
      <td>3366</td>
      <td>8350</td>
      <td>01001</td>
      <td>AL</td>
      <td>Autauga County</td>
      <td>4984</td>
      <td>12202</td>
      <td>0500000US01001</td>
      <td>24661</td>
      <td>11917</td>
    </tr>
    <tr>
      <th>30</th>
      <td>18409</td>
      <td>72780</td>
      <td>7272</td>
      <td>24964</td>
      <td>01003</td>
      <td>AL</td>
      <td>Baldwin County</td>
      <td>17692</td>
      <td>54371</td>
      <td>0500000US01003</td>
      <td>94090</td>
      <td>33045</td>
    </tr>
    <tr>
      <th>31</th>
      <td>4848</td>
      <td>5431</td>
      <td>4591</td>
      <td>5459</td>
      <td>01005</td>
      <td>AL</td>
      <td>Barbour County</td>
      <td>868</td>
      <td>583</td>
      <td>0500000US01005</td>
      <td>10390</td>
      <td>10161</td>
    </tr>
    <tr>
      <th>32</th>
      <td>1874</td>
      <td>6733</td>
      <td>2167</td>
      <td>3487</td>
      <td>01007</td>
      <td>AL</td>
      <td>Bibb County</td>
      <td>1320</td>
      <td>4859</td>
      <td>0500000US01007</td>
      <td>8748</td>
      <td>5687</td>
    </tr>
    <tr>
      <th>33</th>
      <td>2150</td>
      <td>22808</td>
      <td>3738</td>
      <td>8508</td>
      <td>01009</td>
      <td>AL</td>
      <td>Blount County</td>
      <td>4770</td>
      <td>20658</td>
      <td>0500000US01009</td>
      <td>25384</td>
      <td>12482</td>
    </tr>
  </tbody>
</table>
</div>




```python
total_2016 = sum(no_AK['2016 total'])
total_1984 = sum(no_AK['1984 total'])
print(total_2016)
print(total_1984)
```

    127269327
    92434275



```python
Trump_wins = no_AK[no_AK['2016 Diff']>0]
```


```python
Trump_wins.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>votesDem</th>
      <th>votesGOP</th>
      <th>1984 results Democrat</th>
      <th>1984 election result Republican</th>
      <th>STCOU</th>
      <th>state</th>
      <th>county</th>
      <th>1984 Diff</th>
      <th>2016 Diff</th>
      <th>AFFGEOID</th>
      <th>2016 total</th>
      <th>1984 total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>29</th>
      <td>5908</td>
      <td>18110</td>
      <td>3366</td>
      <td>8350</td>
      <td>01001</td>
      <td>AL</td>
      <td>Autauga County</td>
      <td>4984</td>
      <td>12202</td>
      <td>0500000US01001</td>
      <td>24661</td>
      <td>11917</td>
    </tr>
    <tr>
      <th>30</th>
      <td>18409</td>
      <td>72780</td>
      <td>7272</td>
      <td>24964</td>
      <td>01003</td>
      <td>AL</td>
      <td>Baldwin County</td>
      <td>17692</td>
      <td>54371</td>
      <td>0500000US01003</td>
      <td>94090</td>
      <td>33045</td>
    </tr>
    <tr>
      <th>31</th>
      <td>4848</td>
      <td>5431</td>
      <td>4591</td>
      <td>5459</td>
      <td>01005</td>
      <td>AL</td>
      <td>Barbour County</td>
      <td>868</td>
      <td>583</td>
      <td>0500000US01005</td>
      <td>10390</td>
      <td>10161</td>
    </tr>
    <tr>
      <th>32</th>
      <td>1874</td>
      <td>6733</td>
      <td>2167</td>
      <td>3487</td>
      <td>01007</td>
      <td>AL</td>
      <td>Bibb County</td>
      <td>1320</td>
      <td>4859</td>
      <td>0500000US01007</td>
      <td>8748</td>
      <td>5687</td>
    </tr>
    <tr>
      <th>33</th>
      <td>2150</td>
      <td>22808</td>
      <td>3738</td>
      <td>8508</td>
      <td>01009</td>
      <td>AL</td>
      <td>Blount County</td>
      <td>4770</td>
      <td>20658</td>
      <td>0500000US01009</td>
      <td>25384</td>
      <td>12482</td>
    </tr>
  </tbody>
</table>
</div>




```python
Trump_loss = no_AK[no_AK['2016 Diff']<0]
```


```python
Trump_loss.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>votesDem</th>
      <th>votesGOP</th>
      <th>1984 results Democrat</th>
      <th>1984 election result Republican</th>
      <th>STCOU</th>
      <th>state</th>
      <th>county</th>
      <th>1984 Diff</th>
      <th>2016 Diff</th>
      <th>AFFGEOID</th>
      <th>2016 total</th>
      <th>1984 total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <td>3530</td>
      <td>1139</td>
      <td>3537</td>
      <td>1697</td>
      <td>01011</td>
      <td>AL</td>
      <td>Bullock County</td>
      <td>-1840</td>
      <td>-2391</td>
      <td>0500000US01011</td>
      <td>4701</td>
      <td>5299</td>
    </tr>
    <tr>
      <th>52</th>
      <td>12826</td>
      <td>5784</td>
      <td>10955</td>
      <td>9585</td>
      <td>01047</td>
      <td>AL</td>
      <td>Dallas County</td>
      <td>-1370</td>
      <td>-7042</td>
      <td>0500000US01047</td>
      <td>18730</td>
      <td>20718</td>
    </tr>
    <tr>
      <th>60</th>
      <td>4006</td>
      <td>838</td>
      <td>3675</td>
      <td>1361</td>
      <td>01063</td>
      <td>AL</td>
      <td>Greene County</td>
      <td>-2314</td>
      <td>-3168</td>
      <td>0500000US01063</td>
      <td>4862</td>
      <td>5209</td>
    </tr>
    <tr>
      <th>61</th>
      <td>4772</td>
      <td>3172</td>
      <td>3289</td>
      <td>2691</td>
      <td>01065</td>
      <td>AL</td>
      <td>Hale County</td>
      <td>-598</td>
      <td>-1600</td>
      <td>0500000US01065</td>
      <td>8010</td>
      <td>6056</td>
    </tr>
    <tr>
      <th>65</th>
      <td>151581</td>
      <td>130614</td>
      <td>107506</td>
      <td>158362</td>
      <td>01073</td>
      <td>AL</td>
      <td>Jefferson County</td>
      <td>50856</td>
      <td>-20967</td>
      <td>0500000US01073</td>
      <td>290111</td>
      <td>266547</td>
    </tr>
  </tbody>
</table>
</div>




```python
np.mean(Trump_loss['2016 Diff']) 
#Remember that negative numbers are Clinton's votes, since we are subtracting her numbers from Trumps.
```




    -37052.85010266941




```python
len(Trump_loss)
```




    487




```python
len(Trump_wins)
```




    2625




```python
Reagan_wins = no_AK[no_AK['1984 Diff']>0]
Reagan_loss = no_AK[no_AK['1984 Diff']<0]
```


```python
len(Reagan_wins)
```




    2777




```python
len(Reagan_loss)
```




    333




```python

```
