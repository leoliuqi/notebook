

```python
import pandas as pd
```

### 一、2002 年-2018 年上海机动车拍照拍卖
### 问题
(1) 哪一次拍卖的中标率首次小于5%？


```python
df = pd.read_csv('数据集/2002年-2018年上海机动车拍照拍卖.csv')
df['rate'] = df['Total number of license issued']/df['Total number of applicants']*100
df[df.rate < 5].head(1)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Total number of license issued</th>
      <th>lowest price</th>
      <th>avg price</th>
      <th>Total number of applicants</th>
      <th>rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>159</th>
      <td>15-May</td>
      <td>7482</td>
      <td>79000</td>
      <td>79099</td>
      <td>156007</td>
      <td>4.795939</td>
    </tr>
  </tbody>
</table>
</div>



(2) 按年统计拍卖最低价的下列统计量：最大值、均值、0.75 分位数，要求显示在同一张表上。


```python
df = pd.concat([df,df['Date'].str.split('-', expand=True)], axis=1)
df[0]=df[0].apply(lambda x:str(int(x)+2000))
df.groupby(0)['lowest price '].describe().drop(columns=['count', 'std', 'min', '25%', '50%'])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>mean</th>
      <th>75%</th>
      <th>max</th>
    </tr>
    <tr>
      <th>0</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2002</th>
      <td>20316.666667</td>
      <td>24300.0</td>
      <td>30800.0</td>
    </tr>
    <tr>
      <th>2003</th>
      <td>31983.333333</td>
      <td>36300.0</td>
      <td>38500.0</td>
    </tr>
    <tr>
      <th>2004</th>
      <td>29408.333333</td>
      <td>38400.0</td>
      <td>44200.0</td>
    </tr>
    <tr>
      <th>2005</th>
      <td>31908.333333</td>
      <td>35600.0</td>
      <td>37900.0</td>
    </tr>
    <tr>
      <th>2006</th>
      <td>37058.333333</td>
      <td>39525.0</td>
      <td>39900.0</td>
    </tr>
    <tr>
      <th>2007</th>
      <td>45691.666667</td>
      <td>48950.0</td>
      <td>53800.0</td>
    </tr>
    <tr>
      <th>2008</th>
      <td>29945.454545</td>
      <td>34150.0</td>
      <td>37300.0</td>
    </tr>
    <tr>
      <th>2009</th>
      <td>31333.333333</td>
      <td>34150.0</td>
      <td>36900.0</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>38008.333333</td>
      <td>41825.0</td>
      <td>44900.0</td>
    </tr>
    <tr>
      <th>2011</th>
      <td>47958.333333</td>
      <td>51000.0</td>
      <td>53800.0</td>
    </tr>
    <tr>
      <th>2012</th>
      <td>61108.333333</td>
      <td>65325.0</td>
      <td>68900.0</td>
    </tr>
    <tr>
      <th>2013</th>
      <td>79125.000000</td>
      <td>82550.0</td>
      <td>90800.0</td>
    </tr>
    <tr>
      <th>2014</th>
      <td>73816.666667</td>
      <td>74000.0</td>
      <td>74600.0</td>
    </tr>
    <tr>
      <th>2015</th>
      <td>80575.000000</td>
      <td>83450.0</td>
      <td>85300.0</td>
    </tr>
    <tr>
      <th>2016</th>
      <td>85733.333333</td>
      <td>87475.0</td>
      <td>88600.0</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>90616.666667</td>
      <td>92350.0</td>
      <td>93500.0</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>87825.000000</td>
      <td>88150.0</td>
      <td>89000.0</td>
    </tr>
  </tbody>
</table>
</div>



(3) 将第一列时间列拆分成两个列，一列为年份（格式为20××），另一列为月份（英语缩写），添加到列表作为第一第二列，并将原表第一列删除，其他列依次向后顺延。


```python
df = df[[0,1,'Total number of license issued','lowest price ','avg price','Total number of applicants','rate']]
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>Total number of license issued</th>
      <th>lowest price</th>
      <th>avg price</th>
      <th>Total number of applicants</th>
      <th>rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2002</td>
      <td>Jan</td>
      <td>1400</td>
      <td>13600</td>
      <td>14735</td>
      <td>3718</td>
      <td>37.654653</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2002</td>
      <td>Feb</td>
      <td>1800</td>
      <td>13100</td>
      <td>14057</td>
      <td>4590</td>
      <td>39.215686</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2002</td>
      <td>Mar</td>
      <td>2000</td>
      <td>14300</td>
      <td>14662</td>
      <td>5190</td>
      <td>38.535645</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2002</td>
      <td>Apr</td>
      <td>2300</td>
      <td>16000</td>
      <td>16334</td>
      <td>4806</td>
      <td>47.856846</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2002</td>
      <td>May</td>
      <td>2350</td>
      <td>17800</td>
      <td>18357</td>
      <td>4665</td>
      <td>50.375134</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>198</th>
      <td>2018</td>
      <td>Aug</td>
      <td>10402</td>
      <td>88300</td>
      <td>88365</td>
      <td>192755</td>
      <td>5.396488</td>
    </tr>
    <tr>
      <th>199</th>
      <td>2018</td>
      <td>Sep</td>
      <td>12712</td>
      <td>87300</td>
      <td>87410</td>
      <td>189142</td>
      <td>6.720876</td>
    </tr>
    <tr>
      <th>200</th>
      <td>2018</td>
      <td>Oct</td>
      <td>10728</td>
      <td>88000</td>
      <td>88070</td>
      <td>181861</td>
      <td>5.899011</td>
    </tr>
    <tr>
      <th>201</th>
      <td>2018</td>
      <td>Nov</td>
      <td>11766</td>
      <td>87300</td>
      <td>87374</td>
      <td>177355</td>
      <td>6.634152</td>
    </tr>
    <tr>
      <th>202</th>
      <td>2018</td>
      <td>Dec</td>
      <td>12850</td>
      <td>87400</td>
      <td>87508</td>
      <td>165442</td>
      <td>7.767072</td>
    </tr>
  </tbody>
</table>
<p>203 rows × 7 columns</p>
</div>



(4) 现在将表格行索引设为多级索引，外层为年份，内层为原表格第二至第五列的变量名，列索引为月份。


```python
df_p = df.pivot(index=0,columns=1, values=['Total number of license issued','lowest price ','avg price','Total number of applicants','rate'])
df_p.stack(0)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>1</th>
      <th>Apr</th>
      <th>Aug</th>
      <th>Dec</th>
      <th>Feb</th>
      <th>Jan</th>
      <th>Jul</th>
      <th>Jun</th>
      <th>Mar</th>
      <th>May</th>
      <th>Nov</th>
      <th>Oct</th>
      <th>Sep</th>
    </tr>
    <tr>
      <th>0</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">2002</th>
      <th>Total number of applicants</th>
      <td>4806.000000</td>
      <td>4640.000000</td>
      <td>3525.000000</td>
      <td>4590.000000</td>
      <td>3718.000000</td>
      <td>3774.000000</td>
      <td>4502.000000</td>
      <td>5190.000000</td>
      <td>4665.000000</td>
      <td>4021.000000</td>
      <td>4661.000000</td>
      <td>4393.000000</td>
    </tr>
    <tr>
      <th>Total number of license issued</th>
      <td>2300.000000</td>
      <td>3000.000000</td>
      <td>3600.000000</td>
      <td>1800.000000</td>
      <td>1400.000000</td>
      <td>3000.000000</td>
      <td>2800.000000</td>
      <td>2000.000000</td>
      <td>2350.000000</td>
      <td>3200.000000</td>
      <td>3200.000000</td>
      <td>3200.000000</td>
    </tr>
    <tr>
      <th>avg price</th>
      <td>16334.000000</td>
      <td>21601.000000</td>
      <td>27848.000000</td>
      <td>14057.000000</td>
      <td>14735.000000</td>
      <td>20904.000000</td>
      <td>20178.000000</td>
      <td>14662.000000</td>
      <td>18357.000000</td>
      <td>31721.000000</td>
      <td>27040.000000</td>
      <td>24040.000000</td>
    </tr>
    <tr>
      <th>lowest price</th>
      <td>16000.000000</td>
      <td>21000.000000</td>
      <td>27800.000000</td>
      <td>13100.000000</td>
      <td>13600.000000</td>
      <td>19800.000000</td>
      <td>19600.000000</td>
      <td>14300.000000</td>
      <td>17800.000000</td>
      <td>30800.000000</td>
      <td>26400.000000</td>
      <td>23600.000000</td>
    </tr>
    <tr>
      <th>rate</th>
      <td>47.856846</td>
      <td>64.655172</td>
      <td>102.127660</td>
      <td>39.215686</td>
      <td>37.654653</td>
      <td>79.491256</td>
      <td>62.194580</td>
      <td>38.535645</td>
      <td>50.375134</td>
      <td>79.582193</td>
      <td>68.654795</td>
      <td>72.843160</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">2018</th>
      <th>Total number of applicants</th>
      <td>204980.000000</td>
      <td>192755.000000</td>
      <td>165442.000000</td>
      <td>220831.000000</td>
      <td>226316.000000</td>
      <td>202337.000000</td>
      <td>209672.000000</td>
      <td>217056.000000</td>
      <td>198627.000000</td>
      <td>177355.000000</td>
      <td>181861.000000</td>
      <td>189142.000000</td>
    </tr>
    <tr>
      <th>Total number of license issued</th>
      <td>11916.000000</td>
      <td>10402.000000</td>
      <td>12850.000000</td>
      <td>11098.000000</td>
      <td>12183.000000</td>
      <td>10395.000000</td>
      <td>10775.000000</td>
      <td>9855.000000</td>
      <td>10216.000000</td>
      <td>11766.000000</td>
      <td>10728.000000</td>
      <td>12712.000000</td>
    </tr>
    <tr>
      <th>avg price</th>
      <td>87089.000000</td>
      <td>88365.000000</td>
      <td>87508.000000</td>
      <td>87660.000000</td>
      <td>87936.000000</td>
      <td>88380.000000</td>
      <td>87900.000000</td>
      <td>88176.000000</td>
      <td>89018.000000</td>
      <td>87374.000000</td>
      <td>88070.000000</td>
      <td>87410.000000</td>
    </tr>
    <tr>
      <th>lowest price</th>
      <td>86900.000000</td>
      <td>88300.000000</td>
      <td>87400.000000</td>
      <td>87600.000000</td>
      <td>87900.000000</td>
      <td>88300.000000</td>
      <td>87800.000000</td>
      <td>88100.000000</td>
      <td>89000.000000</td>
      <td>87300.000000</td>
      <td>88000.000000</td>
      <td>87300.000000</td>
    </tr>
    <tr>
      <th>rate</th>
      <td>5.813250</td>
      <td>5.396488</td>
      <td>7.767072</td>
      <td>5.025563</td>
      <td>5.383181</td>
      <td>5.137469</td>
      <td>5.138979</td>
      <td>4.540303</td>
      <td>5.143309</td>
      <td>6.634152</td>
      <td>5.899011</td>
      <td>6.720876</td>
    </tr>
  </tbody>
</table>
<p>85 rows × 12 columns</p>
</div>



(5) 一般而言某个月最低价与上月最低价的差额，会与该月均值与上月均值的差额具有相同的正负号，哪些拍卖时间不具有这个特点？


```python
df['cha1'] = df['lowest price ']- df['lowest price '].shift(1)
df['cha2'] = df['avg price'] - df['avg price'].shift(1)
df[df['cha1']*df['cha2']<0]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>Total number of license issued</th>
      <th>lowest price</th>
      <th>avg price</th>
      <th>Total number of applicants</th>
      <th>rate</th>
      <th>cha1</th>
      <th>cha2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>21</th>
      <td>2003</td>
      <td>Oct</td>
      <td>4500</td>
      <td>32800</td>
      <td>34842</td>
      <td>9383</td>
      <td>47.959075</td>
      <td>4000.0</td>
      <td>-3886.0</td>
    </tr>
    <tr>
      <th>22</th>
      <td>2003</td>
      <td>Nov</td>
      <td>5042</td>
      <td>33100</td>
      <td>34284</td>
      <td>9849</td>
      <td>51.193015</td>
      <td>300.0</td>
      <td>-558.0</td>
    </tr>
    <tr>
      <th>29</th>
      <td>2004</td>
      <td>Jun</td>
      <td>6233</td>
      <td>17800</td>
      <td>21001</td>
      <td>19233</td>
      <td>32.407841</td>
      <td>7000.0</td>
      <td>-13225.0</td>
    </tr>
    <tr>
      <th>36</th>
      <td>2005</td>
      <td>Jan</td>
      <td>5500</td>
      <td>28500</td>
      <td>32520</td>
      <td>6208</td>
      <td>88.595361</td>
      <td>-800.0</td>
      <td>2238.0</td>
    </tr>
    <tr>
      <th>37</th>
      <td>2005</td>
      <td>Feb</td>
      <td>3800</td>
      <td>31700</td>
      <td>32425</td>
      <td>8949</td>
      <td>42.462845</td>
      <td>3200.0</td>
      <td>-95.0</td>
    </tr>
    <tr>
      <th>44</th>
      <td>2005</td>
      <td>Sep</td>
      <td>6700</td>
      <td>26500</td>
      <td>28927</td>
      <td>10972</td>
      <td>61.064528</td>
      <td>1500.0</td>
      <td>-6978.0</td>
    </tr>
    <tr>
      <th>52</th>
      <td>2006</td>
      <td>May</td>
      <td>4500</td>
      <td>37700</td>
      <td>38139</td>
      <td>8301</td>
      <td>54.210336</td>
      <td>200.0</td>
      <td>-187.0</td>
    </tr>
    <tr>
      <th>56</th>
      <td>2006</td>
      <td>Sep</td>
      <td>6500</td>
      <td>37000</td>
      <td>41601</td>
      <td>7064</td>
      <td>92.015855</td>
      <td>-2900.0</td>
      <td>1142.0</td>
    </tr>
    <tr>
      <th>60</th>
      <td>2007</td>
      <td>Jan</td>
      <td>6000</td>
      <td>38500</td>
      <td>40974</td>
      <td>6587</td>
      <td>91.088508</td>
      <td>-1300.0</td>
      <td>456.0</td>
    </tr>
    <tr>
      <th>61</th>
      <td>2007</td>
      <td>Feb</td>
      <td>3500</td>
      <td>39100</td>
      <td>40473</td>
      <td>5056</td>
      <td>69.224684</td>
      <td>600.0</td>
      <td>-501.0</td>
    </tr>
    <tr>
      <th>71</th>
      <td>2007</td>
      <td>Dec</td>
      <td>7500</td>
      <td>50000</td>
      <td>56042</td>
      <td>10356</td>
      <td>72.421784</td>
      <td>-3800.0</td>
      <td>1725.0</td>
    </tr>
    <tr>
      <th>128</th>
      <td>2012</td>
      <td>Oct</td>
      <td>9500</td>
      <td>65200</td>
      <td>66708</td>
      <td>19921</td>
      <td>47.688369</td>
      <td>-500.0</td>
      <td>283.0</td>
    </tr>
  </tbody>
</table>
</div>



(6) 将某一个月牌照发行量与其前两个月发行量均值的差额定义为发行增益，最初的两个月用0 填充，求发行增益极值出现的时间。


```python
df['zengyi'] = df['Total number of license issued']-((df['Total number of license issued'].shift(1)+df['Total number of license issued'].shift(2))/2)
df['zengyi'] = df['zengyi'].fillna(0)
```


```python
df.loc[df['zengyi'].idxmax()]
```




    0                                    2008
    1                                     Jan
    Total number of license issued      16000
    lowest price                         8100
    avg price                           23370
    Total number of applicants          20539
    rate                              77.9006
    cha1                               -41900
    cha2                               -32672
    zengyi                               8500
    Name: 72, dtype: object




```python
df.loc[df['zengyi'].idxmin()]
```




    0                                    2008
    1                                     Apr
    Total number of license issued       9000
    lowest price                        37300
    avg price                           37659
    Total number of applicants          37072
    rate                              24.2771
    cha1                                 6000
    cha2                                 5490
    zengyi                              -3650
    Name: 74, dtype: object



### 二、2007 年-2019 年俄罗斯机场货运航班运载量
### 问题
(1) 求每年货运航班总运量。


```python

```

(2) 每年记录的机场都是相同的吗？
(3) 按年计算2010 年-2015 年全年货运量记录为0 的机场航班比例。
(4) 若某机场至少存在5 年或以上满足所有月运量记录都为0，则将其所有
年份的记录信息从表中删除，并返回处理后的表格
(5) 采用一种合理的方式将所有机场划分为东南西北四个分区，并给出2017
年-2019 年货运总量最大的区域。
(6) 在统计学中常常用秩代表排名，现在规定某个机场某年某个月的秩为该
机场该月在当年所有月份中货运量的排名（例如*** 机场19 年1 月运
量在整个19 年12 个月中排名第一，则秩为1），那么判断某月运量情
况的相对大小的秩方法为将所有机场在该月的秩排名相加，并将这个量
定义为每一个月的秩综合指数，请根据上述定义计算2016 年12 个月
的秩综合指数。

### 三、新冠肺炎在美国的传播
### 问题
(1) 用corr() 函数计算县（每行都是一个县）人口与表中最后一天记录日期
死亡数的相关系数。
(2) 截止到4 月1 日，统计每个州零感染县的比例。
(3) 请找出最早出确证病例的三个县。
(4) 按州统计单日死亡增加数，并给出哪个州在哪一天确诊数增加最大（这
里指的是在所有州和所有天两个指标一起算，不是分别算）。
(5) 现需对每个州编制确证与死亡表，第一列为时间，并且起始时间为该州
开始出现死亡比例的那一天，第二列和第三列分别为确证数和死亡数，
每个州需要保存为一个单独的csv 文件，文件名为“州名.csv”。
(6) 现需对4 月1 日至4 月10 日编制新增确证数与新增死亡数表，第一列
为州名，第二列和第三列分别为新增确证数和新增死亡数，分别保存为
十个单独的csv 文件，文件名为“日期.csv”。
