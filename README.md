
## Finding the Philadelphia ZIP Code with the maximum ZHVI (Zillow Home Value Index) over time

First Homework Assignment of MUSA 620 Data Wrangling and Data Visualization at University of Pennsylvania


```python
import pandas as pd
```


```python
df = pd.read_csv('data/Zip_Zhvi_AllHomes.csv', engine='python')

df.head()
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
      <th>RegionID</th>
      <th>RegionName</th>
      <th>City</th>
      <th>State</th>
      <th>Metro</th>
      <th>CountyName</th>
      <th>SizeRank</th>
      <th>1996-04</th>
      <th>1996-05</th>
      <th>1996-06</th>
      <th>...</th>
      <th>2018-02</th>
      <th>2018-03</th>
      <th>2018-04</th>
      <th>2018-05</th>
      <th>2018-06</th>
      <th>2018-07</th>
      <th>2018-08</th>
      <th>2018-09</th>
      <th>2018-10</th>
      <th>2018-11</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>61639</td>
      <td>10025</td>
      <td>New York</td>
      <td>NY</td>
      <td>New York-Newark-Jersey City</td>
      <td>New York County</td>
      <td>1</td>
      <td>171600.0</td>
      <td>171600.0</td>
      <td>171400.0</td>
      <td>...</td>
      <td>1130500</td>
      <td>1123700</td>
      <td>1119500</td>
      <td>1116900</td>
      <td>1110100</td>
      <td>1098400</td>
      <td>1086900</td>
      <td>1080500</td>
      <td>1072200</td>
      <td>1064000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>84654</td>
      <td>60657</td>
      <td>Chicago</td>
      <td>IL</td>
      <td>Chicago-Naperville-Elgin</td>
      <td>Cook County</td>
      <td>2</td>
      <td>158400.0</td>
      <td>159700.0</td>
      <td>160700.0</td>
      <td>...</td>
      <td>351600</td>
      <td>352900</td>
      <td>351900</td>
      <td>350400</td>
      <td>348700</td>
      <td>347800</td>
      <td>348200</td>
      <td>349500</td>
      <td>351500</td>
      <td>354000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>61637</td>
      <td>10023</td>
      <td>New York</td>
      <td>NY</td>
      <td>New York-Newark-Jersey City</td>
      <td>New York County</td>
      <td>3</td>
      <td>347900.0</td>
      <td>349600.0</td>
      <td>351100.0</td>
      <td>...</td>
      <td>1516000</td>
      <td>1497900</td>
      <td>1497800</td>
      <td>1504600</td>
      <td>1489900</td>
      <td>1463300</td>
      <td>1438800</td>
      <td>1411600</td>
      <td>1389900</td>
      <td>1380100</td>
    </tr>
    <tr>
      <th>3</th>
      <td>91982</td>
      <td>77494</td>
      <td>Katy</td>
      <td>TX</td>
      <td>Houston-The Woodlands-Sugar Land</td>
      <td>Harris County</td>
      <td>4</td>
      <td>210400.0</td>
      <td>212200.0</td>
      <td>212200.0</td>
      <td>...</td>
      <td>326600</td>
      <td>330400</td>
      <td>332600</td>
      <td>334500</td>
      <td>335800</td>
      <td>336900</td>
      <td>338200</td>
      <td>338400</td>
      <td>336900</td>
      <td>336000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>84616</td>
      <td>60614</td>
      <td>Chicago</td>
      <td>IL</td>
      <td>Chicago-Naperville-Elgin</td>
      <td>Cook County</td>
      <td>5</td>
      <td>192500.0</td>
      <td>194500.0</td>
      <td>196100.0</td>
      <td>...</td>
      <td>429000</td>
      <td>430400</td>
      <td>429500</td>
      <td>428600</td>
      <td>428700</td>
      <td>430600</td>
      <td>431900</td>
      <td>430900</td>
      <td>430900</td>
      <td>433200</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 279 columns</p>
</div>




```python
df_phila = df[df['CountyName'] == 'Philadelphia County']

df_phila.head()
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
      <th>RegionID</th>
      <th>RegionName</th>
      <th>City</th>
      <th>State</th>
      <th>Metro</th>
      <th>CountyName</th>
      <th>SizeRank</th>
      <th>1996-04</th>
      <th>1996-05</th>
      <th>1996-06</th>
      <th>...</th>
      <th>2018-02</th>
      <th>2018-03</th>
      <th>2018-04</th>
      <th>2018-05</th>
      <th>2018-06</th>
      <th>2018-07</th>
      <th>2018-08</th>
      <th>2018-09</th>
      <th>2018-10</th>
      <th>2018-11</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>214</th>
      <td>65779</td>
      <td>19111</td>
      <td>Philadelphia</td>
      <td>PA</td>
      <td>Philadelphia-Camden-Wilmington</td>
      <td>Philadelphia County</td>
      <td>215</td>
      <td>84900.0</td>
      <td>84700.0</td>
      <td>84500.0</td>
      <td>...</td>
      <td>174300</td>
      <td>175500</td>
      <td>175700</td>
      <td>175800</td>
      <td>176400</td>
      <td>177300</td>
      <td>178400</td>
      <td>180300</td>
      <td>182800</td>
      <td>184800</td>
    </tr>
    <tr>
      <th>300</th>
      <td>65791</td>
      <td>19124</td>
      <td>Philadelphia</td>
      <td>PA</td>
      <td>Philadelphia-Camden-Wilmington</td>
      <td>Philadelphia County</td>
      <td>301</td>
      <td>43100.0</td>
      <td>43000.0</td>
      <td>42900.0</td>
      <td>...</td>
      <td>86200</td>
      <td>88000</td>
      <td>88900</td>
      <td>89900</td>
      <td>90800</td>
      <td>91400</td>
      <td>91900</td>
      <td>92800</td>
      <td>94200</td>
      <td>95700</td>
    </tr>
    <tr>
      <th>377</th>
      <td>65787</td>
      <td>19120</td>
      <td>Philadelphia</td>
      <td>PA</td>
      <td>Philadelphia-Camden-Wilmington</td>
      <td>Philadelphia County</td>
      <td>378</td>
      <td>46100.0</td>
      <td>46100.0</td>
      <td>46100.0</td>
      <td>...</td>
      <td>91100</td>
      <td>92100</td>
      <td>92400</td>
      <td>92400</td>
      <td>92600</td>
      <td>92800</td>
      <td>92800</td>
      <td>92900</td>
      <td>93500</td>
      <td>94200</td>
    </tr>
    <tr>
      <th>542</th>
      <td>65815</td>
      <td>19148</td>
      <td>Philadelphia</td>
      <td>PA</td>
      <td>Philadelphia-Camden-Wilmington</td>
      <td>Philadelphia County</td>
      <td>543</td>
      <td>41100.0</td>
      <td>41100.0</td>
      <td>41000.0</td>
      <td>...</td>
      <td>205700</td>
      <td>209500</td>
      <td>211800</td>
      <td>213400</td>
      <td>214900</td>
      <td>215500</td>
      <td>215700</td>
      <td>216900</td>
      <td>219800</td>
      <td>222500</td>
    </tr>
    <tr>
      <th>690</th>
      <td>65812</td>
      <td>19145</td>
      <td>Philadelphia</td>
      <td>PA</td>
      <td>Philadelphia-Camden-Wilmington</td>
      <td>Philadelphia County</td>
      <td>691</td>
      <td>41000.0</td>
      <td>41000.0</td>
      <td>41000.0</td>
      <td>...</td>
      <td>204100</td>
      <td>208400</td>
      <td>209500</td>
      <td>209100</td>
      <td>209600</td>
      <td>211100</td>
      <td>212600</td>
      <td>213800</td>
      <td>215100</td>
      <td>216700</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 279 columns</p>
</div>




```python
unwanted = ['SizeRank', 'RegionID', 'State', 'Metro', 'CountyName', 'City']
df_phila_final = df_phila.drop(unwanted, axis=1)

df_phila_final.head()
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
      <th>RegionName</th>
      <th>1996-04</th>
      <th>1996-05</th>
      <th>1996-06</th>
      <th>1996-07</th>
      <th>1996-08</th>
      <th>1996-09</th>
      <th>1996-10</th>
      <th>1996-11</th>
      <th>1996-12</th>
      <th>...</th>
      <th>2018-02</th>
      <th>2018-03</th>
      <th>2018-04</th>
      <th>2018-05</th>
      <th>2018-06</th>
      <th>2018-07</th>
      <th>2018-08</th>
      <th>2018-09</th>
      <th>2018-10</th>
      <th>2018-11</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>214</th>
      <td>19111</td>
      <td>84900.0</td>
      <td>84700.0</td>
      <td>84500.0</td>
      <td>84300.0</td>
      <td>84200.0</td>
      <td>84100.0</td>
      <td>83900.0</td>
      <td>83800.0</td>
      <td>83700.0</td>
      <td>...</td>
      <td>174300</td>
      <td>175500</td>
      <td>175700</td>
      <td>175800</td>
      <td>176400</td>
      <td>177300</td>
      <td>178400</td>
      <td>180300</td>
      <td>182800</td>
      <td>184800</td>
    </tr>
    <tr>
      <th>300</th>
      <td>19124</td>
      <td>43100.0</td>
      <td>43000.0</td>
      <td>42900.0</td>
      <td>42700.0</td>
      <td>42500.0</td>
      <td>42400.0</td>
      <td>42300.0</td>
      <td>42300.0</td>
      <td>42300.0</td>
      <td>...</td>
      <td>86200</td>
      <td>88000</td>
      <td>88900</td>
      <td>89900</td>
      <td>90800</td>
      <td>91400</td>
      <td>91900</td>
      <td>92800</td>
      <td>94200</td>
      <td>95700</td>
    </tr>
    <tr>
      <th>377</th>
      <td>19120</td>
      <td>46100.0</td>
      <td>46100.0</td>
      <td>46100.0</td>
      <td>46100.0</td>
      <td>46000.0</td>
      <td>45900.0</td>
      <td>45900.0</td>
      <td>45800.0</td>
      <td>45700.0</td>
      <td>...</td>
      <td>91100</td>
      <td>92100</td>
      <td>92400</td>
      <td>92400</td>
      <td>92600</td>
      <td>92800</td>
      <td>92800</td>
      <td>92900</td>
      <td>93500</td>
      <td>94200</td>
    </tr>
    <tr>
      <th>542</th>
      <td>19148</td>
      <td>41100.0</td>
      <td>41100.0</td>
      <td>41000.0</td>
      <td>40900.0</td>
      <td>40700.0</td>
      <td>40600.0</td>
      <td>40500.0</td>
      <td>40400.0</td>
      <td>40400.0</td>
      <td>...</td>
      <td>205700</td>
      <td>209500</td>
      <td>211800</td>
      <td>213400</td>
      <td>214900</td>
      <td>215500</td>
      <td>215700</td>
      <td>216900</td>
      <td>219800</td>
      <td>222500</td>
    </tr>
    <tr>
      <th>690</th>
      <td>19145</td>
      <td>41000.0</td>
      <td>41000.0</td>
      <td>41000.0</td>
      <td>40900.0</td>
      <td>40800.0</td>
      <td>40700.0</td>
      <td>40700.0</td>
      <td>40800.0</td>
      <td>40900.0</td>
      <td>...</td>
      <td>204100</td>
      <td>208400</td>
      <td>209500</td>
      <td>209100</td>
      <td>209600</td>
      <td>211100</td>
      <td>212600</td>
      <td>213800</td>
      <td>215100</td>
      <td>216700</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 273 columns</p>
</div>




```python
ZHVI = pd.melt(df_phila_final, id_vars=['RegionName'], 
                value_name='ZHVI', var_name='Date')

ZHVI.head()
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
      <th>RegionName</th>
      <th>Date</th>
      <th>ZHVI</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>19111</td>
      <td>1996-04</td>
      <td>84900.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>19124</td>
      <td>1996-04</td>
      <td>43100.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>19120</td>
      <td>1996-04</td>
      <td>46100.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>19148</td>
      <td>1996-04</td>
      <td>41100.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>19145</td>
      <td>1996-04</td>
      <td>41000.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
ZHVI['Date'] = pd.to_datetime(ZHVI['Date'])
ZHVI['Year'] = ZHVI['Date'].dt.year

ZHVI.head()
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
      <th>RegionName</th>
      <th>Date</th>
      <th>ZHVI</th>
      <th>Year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>19111</td>
      <td>1996-04-01</td>
      <td>84900.0</td>
      <td>1996</td>
    </tr>
    <tr>
      <th>1</th>
      <td>19124</td>
      <td>1996-04-01</td>
      <td>43100.0</td>
      <td>1996</td>
    </tr>
    <tr>
      <th>2</th>
      <td>19120</td>
      <td>1996-04-01</td>
      <td>46100.0</td>
      <td>1996</td>
    </tr>
    <tr>
      <th>3</th>
      <td>19148</td>
      <td>1996-04-01</td>
      <td>41100.0</td>
      <td>1996</td>
    </tr>
    <tr>
      <th>4</th>
      <td>19145</td>
      <td>1996-04-01</td>
      <td>41000.0</td>
      <td>1996</td>
    </tr>
  </tbody>
</table>
</div>




```python
annual_ZHVI = ZHVI.groupby(['RegionName', 'Year'])['ZHVI'].mean().reset_index()
annual_ZHVI
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
      <th>RegionName</th>
      <th>Year</th>
      <th>ZHVI</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>19102</td>
      <td>1996</td>
      <td>79966.666667</td>
    </tr>
    <tr>
      <th>1</th>
      <td>19102</td>
      <td>1997</td>
      <td>83166.666667</td>
    </tr>
    <tr>
      <th>2</th>
      <td>19102</td>
      <td>1998</td>
      <td>92550.000000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>19102</td>
      <td>1999</td>
      <td>114358.333333</td>
    </tr>
    <tr>
      <th>4</th>
      <td>19102</td>
      <td>2000</td>
      <td>145175.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>19102</td>
      <td>2001</td>
      <td>185016.666667</td>
    </tr>
    <tr>
      <th>6</th>
      <td>19102</td>
      <td>2002</td>
      <td>232733.333333</td>
    </tr>
    <tr>
      <th>7</th>
      <td>19102</td>
      <td>2003</td>
      <td>277475.000000</td>
    </tr>
    <tr>
      <th>8</th>
      <td>19102</td>
      <td>2004</td>
      <td>306200.000000</td>
    </tr>
    <tr>
      <th>9</th>
      <td>19102</td>
      <td>2005</td>
      <td>363100.000000</td>
    </tr>
    <tr>
      <th>10</th>
      <td>19102</td>
      <td>2006</td>
      <td>375008.333333</td>
    </tr>
    <tr>
      <th>11</th>
      <td>19102</td>
      <td>2007</td>
      <td>379058.333333</td>
    </tr>
    <tr>
      <th>12</th>
      <td>19102</td>
      <td>2008</td>
      <td>356275.000000</td>
    </tr>
    <tr>
      <th>13</th>
      <td>19102</td>
      <td>2009</td>
      <td>352541.666667</td>
    </tr>
    <tr>
      <th>14</th>
      <td>19102</td>
      <td>2010</td>
      <td>332583.333333</td>
    </tr>
    <tr>
      <th>15</th>
      <td>19102</td>
      <td>2011</td>
      <td>305283.333333</td>
    </tr>
    <tr>
      <th>16</th>
      <td>19102</td>
      <td>2012</td>
      <td>300250.000000</td>
    </tr>
    <tr>
      <th>17</th>
      <td>19102</td>
      <td>2013</td>
      <td>315650.000000</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19102</td>
      <td>2014</td>
      <td>333816.666667</td>
    </tr>
    <tr>
      <th>19</th>
      <td>19102</td>
      <td>2015</td>
      <td>329700.000000</td>
    </tr>
    <tr>
      <th>20</th>
      <td>19102</td>
      <td>2016</td>
      <td>344950.000000</td>
    </tr>
    <tr>
      <th>21</th>
      <td>19102</td>
      <td>2017</td>
      <td>354625.000000</td>
    </tr>
    <tr>
      <th>22</th>
      <td>19102</td>
      <td>2018</td>
      <td>363536.363636</td>
    </tr>
    <tr>
      <th>23</th>
      <td>19103</td>
      <td>1996</td>
      <td>114744.444444</td>
    </tr>
    <tr>
      <th>24</th>
      <td>19103</td>
      <td>1997</td>
      <td>120983.333333</td>
    </tr>
    <tr>
      <th>25</th>
      <td>19103</td>
      <td>1998</td>
      <td>130233.333333</td>
    </tr>
    <tr>
      <th>26</th>
      <td>19103</td>
      <td>1999</td>
      <td>150850.000000</td>
    </tr>
    <tr>
      <th>27</th>
      <td>19103</td>
      <td>2000</td>
      <td>189225.000000</td>
    </tr>
    <tr>
      <th>28</th>
      <td>19103</td>
      <td>2001</td>
      <td>246650.000000</td>
    </tr>
    <tr>
      <th>29</th>
      <td>19103</td>
      <td>2002</td>
      <td>300483.333333</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>798</th>
      <td>19153</td>
      <td>2012</td>
      <td>116675.000000</td>
    </tr>
    <tr>
      <th>799</th>
      <td>19153</td>
      <td>2013</td>
      <td>114541.666667</td>
    </tr>
    <tr>
      <th>800</th>
      <td>19153</td>
      <td>2014</td>
      <td>116016.666667</td>
    </tr>
    <tr>
      <th>801</th>
      <td>19153</td>
      <td>2015</td>
      <td>115541.666667</td>
    </tr>
    <tr>
      <th>802</th>
      <td>19153</td>
      <td>2016</td>
      <td>115375.000000</td>
    </tr>
    <tr>
      <th>803</th>
      <td>19153</td>
      <td>2017</td>
      <td>125816.666667</td>
    </tr>
    <tr>
      <th>804</th>
      <td>19153</td>
      <td>2018</td>
      <td>142827.272727</td>
    </tr>
    <tr>
      <th>805</th>
      <td>19154</td>
      <td>1996</td>
      <td>84022.222222</td>
    </tr>
    <tr>
      <th>806</th>
      <td>19154</td>
      <td>1997</td>
      <td>84591.666667</td>
    </tr>
    <tr>
      <th>807</th>
      <td>19154</td>
      <td>1998</td>
      <td>85766.666667</td>
    </tr>
    <tr>
      <th>808</th>
      <td>19154</td>
      <td>1999</td>
      <td>87191.666667</td>
    </tr>
    <tr>
      <th>809</th>
      <td>19154</td>
      <td>2000</td>
      <td>90233.333333</td>
    </tr>
    <tr>
      <th>810</th>
      <td>19154</td>
      <td>2001</td>
      <td>95991.666667</td>
    </tr>
    <tr>
      <th>811</th>
      <td>19154</td>
      <td>2002</td>
      <td>109833.333333</td>
    </tr>
    <tr>
      <th>812</th>
      <td>19154</td>
      <td>2003</td>
      <td>130116.666667</td>
    </tr>
    <tr>
      <th>813</th>
      <td>19154</td>
      <td>2004</td>
      <td>153566.666667</td>
    </tr>
    <tr>
      <th>814</th>
      <td>19154</td>
      <td>2005</td>
      <td>185741.666667</td>
    </tr>
    <tr>
      <th>815</th>
      <td>19154</td>
      <td>2006</td>
      <td>201358.333333</td>
    </tr>
    <tr>
      <th>816</th>
      <td>19154</td>
      <td>2007</td>
      <td>196650.000000</td>
    </tr>
    <tr>
      <th>817</th>
      <td>19154</td>
      <td>2008</td>
      <td>193591.666667</td>
    </tr>
    <tr>
      <th>818</th>
      <td>19154</td>
      <td>2009</td>
      <td>188708.333333</td>
    </tr>
    <tr>
      <th>819</th>
      <td>19154</td>
      <td>2010</td>
      <td>183775.000000</td>
    </tr>
    <tr>
      <th>820</th>
      <td>19154</td>
      <td>2011</td>
      <td>180700.000000</td>
    </tr>
    <tr>
      <th>821</th>
      <td>19154</td>
      <td>2012</td>
      <td>178500.000000</td>
    </tr>
    <tr>
      <th>822</th>
      <td>19154</td>
      <td>2013</td>
      <td>175441.666667</td>
    </tr>
    <tr>
      <th>823</th>
      <td>19154</td>
      <td>2014</td>
      <td>174100.000000</td>
    </tr>
    <tr>
      <th>824</th>
      <td>19154</td>
      <td>2015</td>
      <td>171233.333333</td>
    </tr>
    <tr>
      <th>825</th>
      <td>19154</td>
      <td>2016</td>
      <td>186883.333333</td>
    </tr>
    <tr>
      <th>826</th>
      <td>19154</td>
      <td>2017</td>
      <td>198741.666667</td>
    </tr>
    <tr>
      <th>827</th>
      <td>19154</td>
      <td>2018</td>
      <td>211436.363636</td>
    </tr>
  </tbody>
</table>
<p>828 rows × 3 columns</p>
</div>




```python
indices = annual_ZHVI.groupby(['Year'])['ZHVI'].idxmax()
```


```python
annual_max = annual_ZHVI.ix[indices]
annual_max
```

    C:\Users\MaiRZ\Anaconda3\envs\musa\lib\site-packages\ipykernel_launcher.py:1: DeprecationWarning: 
    .ix is deprecated. Please use
    .loc for label based indexing or
    .iloc for positional indexing
    
    See the documentation here:
    http://pandas.pydata.org/pandas-docs/stable/indexing.html#ix-indexer-is-deprecated
      """Entry point for launching an IPython kernel.
    




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
      <th>RegionName</th>
      <th>Year</th>
      <th>ZHVI</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>184</th>
      <td>19118</td>
      <td>1996</td>
      <td>182400.000000</td>
    </tr>
    <tr>
      <th>185</th>
      <td>19118</td>
      <td>1997</td>
      <td>184358.333333</td>
    </tr>
    <tr>
      <th>186</th>
      <td>19118</td>
      <td>1998</td>
      <td>187950.000000</td>
    </tr>
    <tr>
      <th>187</th>
      <td>19118</td>
      <td>1999</td>
      <td>207350.000000</td>
    </tr>
    <tr>
      <th>188</th>
      <td>19118</td>
      <td>2000</td>
      <td>239900.000000</td>
    </tr>
    <tr>
      <th>189</th>
      <td>19118</td>
      <td>2001</td>
      <td>274108.333333</td>
    </tr>
    <tr>
      <th>190</th>
      <td>19118</td>
      <td>2002</td>
      <td>311075.000000</td>
    </tr>
    <tr>
      <th>30</th>
      <td>19103</td>
      <td>2003</td>
      <td>353258.333333</td>
    </tr>
    <tr>
      <th>192</th>
      <td>19118</td>
      <td>2004</td>
      <td>411558.333333</td>
    </tr>
    <tr>
      <th>193</th>
      <td>19118</td>
      <td>2005</td>
      <td>474808.333333</td>
    </tr>
    <tr>
      <th>194</th>
      <td>19118</td>
      <td>2006</td>
      <td>489216.666667</td>
    </tr>
    <tr>
      <th>34</th>
      <td>19103</td>
      <td>2007</td>
      <td>492158.333333</td>
    </tr>
    <tr>
      <th>35</th>
      <td>19103</td>
      <td>2008</td>
      <td>489900.000000</td>
    </tr>
    <tr>
      <th>36</th>
      <td>19103</td>
      <td>2009</td>
      <td>497866.666667</td>
    </tr>
    <tr>
      <th>37</th>
      <td>19103</td>
      <td>2010</td>
      <td>466416.666667</td>
    </tr>
    <tr>
      <th>199</th>
      <td>19118</td>
      <td>2011</td>
      <td>436083.333333</td>
    </tr>
    <tr>
      <th>200</th>
      <td>19118</td>
      <td>2012</td>
      <td>425241.666667</td>
    </tr>
    <tr>
      <th>40</th>
      <td>19103</td>
      <td>2013</td>
      <td>425908.333333</td>
    </tr>
    <tr>
      <th>41</th>
      <td>19103</td>
      <td>2014</td>
      <td>449225.000000</td>
    </tr>
    <tr>
      <th>203</th>
      <td>19118</td>
      <td>2015</td>
      <td>472150.000000</td>
    </tr>
    <tr>
      <th>204</th>
      <td>19118</td>
      <td>2016</td>
      <td>499550.000000</td>
    </tr>
    <tr>
      <th>205</th>
      <td>19118</td>
      <td>2017</td>
      <td>520166.666667</td>
    </tr>
    <tr>
      <th>206</th>
      <td>19118</td>
      <td>2018</td>
      <td>535990.909091</td>
    </tr>
  </tbody>
</table>
</div>




```python
final_df = annual_max.loc[:, ['Year', 'RegionName', 'ZHVI']]

final_df
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
      <th>Year</th>
      <th>RegionName</th>
      <th>ZHVI</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>184</th>
      <td>1996</td>
      <td>19118</td>
      <td>182400.000000</td>
    </tr>
    <tr>
      <th>185</th>
      <td>1997</td>
      <td>19118</td>
      <td>184358.333333</td>
    </tr>
    <tr>
      <th>186</th>
      <td>1998</td>
      <td>19118</td>
      <td>187950.000000</td>
    </tr>
    <tr>
      <th>187</th>
      <td>1999</td>
      <td>19118</td>
      <td>207350.000000</td>
    </tr>
    <tr>
      <th>188</th>
      <td>2000</td>
      <td>19118</td>
      <td>239900.000000</td>
    </tr>
    <tr>
      <th>189</th>
      <td>2001</td>
      <td>19118</td>
      <td>274108.333333</td>
    </tr>
    <tr>
      <th>190</th>
      <td>2002</td>
      <td>19118</td>
      <td>311075.000000</td>
    </tr>
    <tr>
      <th>30</th>
      <td>2003</td>
      <td>19103</td>
      <td>353258.333333</td>
    </tr>
    <tr>
      <th>192</th>
      <td>2004</td>
      <td>19118</td>
      <td>411558.333333</td>
    </tr>
    <tr>
      <th>193</th>
      <td>2005</td>
      <td>19118</td>
      <td>474808.333333</td>
    </tr>
    <tr>
      <th>194</th>
      <td>2006</td>
      <td>19118</td>
      <td>489216.666667</td>
    </tr>
    <tr>
      <th>34</th>
      <td>2007</td>
      <td>19103</td>
      <td>492158.333333</td>
    </tr>
    <tr>
      <th>35</th>
      <td>2008</td>
      <td>19103</td>
      <td>489900.000000</td>
    </tr>
    <tr>
      <th>36</th>
      <td>2009</td>
      <td>19103</td>
      <td>497866.666667</td>
    </tr>
    <tr>
      <th>37</th>
      <td>2010</td>
      <td>19103</td>
      <td>466416.666667</td>
    </tr>
    <tr>
      <th>199</th>
      <td>2011</td>
      <td>19118</td>
      <td>436083.333333</td>
    </tr>
    <tr>
      <th>200</th>
      <td>2012</td>
      <td>19118</td>
      <td>425241.666667</td>
    </tr>
    <tr>
      <th>40</th>
      <td>2013</td>
      <td>19103</td>
      <td>425908.333333</td>
    </tr>
    <tr>
      <th>41</th>
      <td>2014</td>
      <td>19103</td>
      <td>449225.000000</td>
    </tr>
    <tr>
      <th>203</th>
      <td>2015</td>
      <td>19118</td>
      <td>472150.000000</td>
    </tr>
    <tr>
      <th>204</th>
      <td>2016</td>
      <td>19118</td>
      <td>499550.000000</td>
    </tr>
    <tr>
      <th>205</th>
      <td>2017</td>
      <td>19118</td>
      <td>520166.666667</td>
    </tr>
    <tr>
      <th>206</th>
      <td>2018</td>
      <td>19118</td>
      <td>535990.909091</td>
    </tr>
  </tbody>
</table>
</div>




```python
final_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 23 entries, 184 to 206
    Data columns (total 3 columns):
    Year          23 non-null int64
    RegionName    23 non-null int64
    ZHVI          23 non-null float64
    dtypes: float64(1), int64(2)
    memory usage: 736.0 bytes
    


```python
final_df['Year'] = final_df['Year'].astype(str)
final_df['RegionName'] = final_df['RegionName'].astype(str)


for i in range(len(final_df)):
    year = final_df.iloc[i][0]
    value = round(final_df.iloc[i][2], 2)
    zipcode = final_df.iloc[i][1]
    
    print("The maximum value for year {} equals {}, and the zipcode is {}.".format(year, value, zipcode), 
          end = '\n--------------------\n')
```

    The maximum value for year 1996 equals 182400.0, and the zipcode is 19118.
    --------------------
    The maximum value for year 1997 equals 184358.33, and the zipcode is 19118.
    --------------------
    The maximum value for year 1998 equals 187950.0, and the zipcode is 19118.
    --------------------
    The maximum value for year 1999 equals 207350.0, and the zipcode is 19118.
    --------------------
    The maximum value for year 2000 equals 239900.0, and the zipcode is 19118.
    --------------------
    The maximum value for year 2001 equals 274108.33, and the zipcode is 19118.
    --------------------
    The maximum value for year 2002 equals 311075.0, and the zipcode is 19118.
    --------------------
    The maximum value for year 2003 equals 353258.33, and the zipcode is 19103.
    --------------------
    The maximum value for year 2004 equals 411558.33, and the zipcode is 19118.
    --------------------
    The maximum value for year 2005 equals 474808.33, and the zipcode is 19118.
    --------------------
    The maximum value for year 2006 equals 489216.67, and the zipcode is 19118.
    --------------------
    The maximum value for year 2007 equals 492158.33, and the zipcode is 19103.
    --------------------
    The maximum value for year 2008 equals 489900.0, and the zipcode is 19103.
    --------------------
    The maximum value for year 2009 equals 497866.67, and the zipcode is 19103.
    --------------------
    The maximum value for year 2010 equals 466416.67, and the zipcode is 19103.
    --------------------
    The maximum value for year 2011 equals 436083.33, and the zipcode is 19118.
    --------------------
    The maximum value for year 2012 equals 425241.67, and the zipcode is 19118.
    --------------------
    The maximum value for year 2013 equals 425908.33, and the zipcode is 19103.
    --------------------
    The maximum value for year 2014 equals 449225.0, and the zipcode is 19103.
    --------------------
    The maximum value for year 2015 equals 472150.0, and the zipcode is 19118.
    --------------------
    The maximum value for year 2016 equals 499550.0, and the zipcode is 19118.
    --------------------
    The maximum value for year 2017 equals 520166.67, and the zipcode is 19118.
    --------------------
    The maximum value for year 2018 equals 535990.91, and the zipcode is 19118.
    --------------------
    
