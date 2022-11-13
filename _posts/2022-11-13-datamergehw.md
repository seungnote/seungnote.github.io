# 과제 2-5

##  players_19.csv와 players_20.csv 데이터를 행결합해서 master data를 만드세요 


```python
import pandas as pd 
```


```python
fifa_df19 = pd.read_csv("D:/anaconda/00.studying/data/players_19.csv")
fifa_df20 = pd.read_csv("D:/anaconda/00.studying/data/players_20.csv")
```

## fifa_df19 = players_19.csv에서 sofifa_id','short_name','overall' 컬럼만 추출


```python
# 꼭 한번 더 [ ]감싸줘야함 
fifa_d19=fifa_df19[['sofifa_id','short_name','overall']]
fifa_d19
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
      <th>sofifa_id</th>
      <th>short_name</th>
      <th>overall</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20801</td>
      <td>Cristiano Ronaldo</td>
      <td>94</td>
    </tr>
    <tr>
      <th>1</th>
      <td>158023</td>
      <td>L. Messi</td>
      <td>94</td>
    </tr>
    <tr>
      <th>2</th>
      <td>190871</td>
      <td>Neymar Jr</td>
      <td>92</td>
    </tr>
    <tr>
      <th>3</th>
      <td>193080</td>
      <td>De Gea</td>
      <td>91</td>
    </tr>
    <tr>
      <th>4</th>
      <td>192985</td>
      <td>K. De Bruyne</td>
      <td>91</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>17765</th>
      <td>238985</td>
      <td>P. Phillips</td>
      <td>47</td>
    </tr>
    <tr>
      <th>17766</th>
      <td>240160</td>
      <td>A. Kaltner</td>
      <td>47</td>
    </tr>
    <tr>
      <th>17767</th>
      <td>241304</td>
      <td>Ma Junliang</td>
      <td>47</td>
    </tr>
    <tr>
      <th>17768</th>
      <td>240158</td>
      <td>C. Ehlich</td>
      <td>47</td>
    </tr>
    <tr>
      <th>17769</th>
      <td>243961</td>
      <td>E. Tweed</td>
      <td>47</td>
    </tr>
  </tbody>
</table>
<p>17770 rows × 3 columns</p>
</div>



## fifa_df20 = players_20.csv 에서 sofifa_id와 overall만을 추출 


```python
fifa_d20=fifa_df20[['sofifa_id','overall']]
fifa_d20
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
      <th>sofifa_id</th>
      <th>overall</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>158023</td>
      <td>94</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20801</td>
      <td>93</td>
    </tr>
    <tr>
      <th>2</th>
      <td>190871</td>
      <td>92</td>
    </tr>
    <tr>
      <th>3</th>
      <td>200389</td>
      <td>91</td>
    </tr>
    <tr>
      <th>4</th>
      <td>183277</td>
      <td>91</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>18273</th>
      <td>245006</td>
      <td>48</td>
    </tr>
    <tr>
      <th>18274</th>
      <td>250995</td>
      <td>48</td>
    </tr>
    <tr>
      <th>18275</th>
      <td>252332</td>
      <td>48</td>
    </tr>
    <tr>
      <th>18276</th>
      <td>251110</td>
      <td>48</td>
    </tr>
    <tr>
      <th>18277</th>
      <td>233449</td>
      <td>48</td>
    </tr>
  </tbody>
</table>
<p>18278 rows × 2 columns</p>
</div>



## sofifa_id를 key값으로  위의 두 테이블을 innerjoin 하세요 


```python
df_inner1920=pd.merge(fifa_d19,fifa_d20,how='inner',on='sofifa_id')
df_inner1920
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
      <th>sofifa_id</th>
      <th>short_name</th>
      <th>overall_x</th>
      <th>overall_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20801</td>
      <td>Cristiano Ronaldo</td>
      <td>94</td>
      <td>93</td>
    </tr>
    <tr>
      <th>1</th>
      <td>158023</td>
      <td>L. Messi</td>
      <td>94</td>
      <td>94</td>
    </tr>
    <tr>
      <th>2</th>
      <td>190871</td>
      <td>Neymar Jr</td>
      <td>92</td>
      <td>92</td>
    </tr>
    <tr>
      <th>3</th>
      <td>193080</td>
      <td>De Gea</td>
      <td>91</td>
      <td>89</td>
    </tr>
    <tr>
      <th>4</th>
      <td>192985</td>
      <td>K. De Bruyne</td>
      <td>91</td>
      <td>91</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>13139</th>
      <td>238985</td>
      <td>P. Phillips</td>
      <td>47</td>
      <td>49</td>
    </tr>
    <tr>
      <th>13140</th>
      <td>240160</td>
      <td>A. Kaltner</td>
      <td>47</td>
      <td>53</td>
    </tr>
    <tr>
      <th>13141</th>
      <td>241304</td>
      <td>Ma Junliang</td>
      <td>47</td>
      <td>54</td>
    </tr>
    <tr>
      <th>13142</th>
      <td>240158</td>
      <td>C. Ehlich</td>
      <td>47</td>
      <td>57</td>
    </tr>
    <tr>
      <th>13143</th>
      <td>243961</td>
      <td>E. Tweed</td>
      <td>47</td>
      <td>48</td>
    </tr>
  </tbody>
</table>
<p>13144 rows × 4 columns</p>
</div>



## sofifa_id를 key값으로  위의 두 테이블을 outerjoin 하세요 


```python
df_outer1920=pd.merge(fifa_d19,fifa_d20,how='outer',on='sofifa_id')
df_outer1920
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
      <th>sofifa_id</th>
      <th>short_name</th>
      <th>overall_x</th>
      <th>overall_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20801</td>
      <td>Cristiano Ronaldo</td>
      <td>94.0</td>
      <td>93.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>158023</td>
      <td>L. Messi</td>
      <td>94.0</td>
      <td>94.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>190871</td>
      <td>Neymar Jr</td>
      <td>92.0</td>
      <td>92.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>193080</td>
      <td>De Gea</td>
      <td>91.0</td>
      <td>89.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>192985</td>
      <td>K. De Bruyne</td>
      <td>91.0</td>
      <td>91.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>22899</th>
      <td>245006</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>48.0</td>
    </tr>
    <tr>
      <th>22900</th>
      <td>250995</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>48.0</td>
    </tr>
    <tr>
      <th>22901</th>
      <td>252332</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>48.0</td>
    </tr>
    <tr>
      <th>22902</th>
      <td>251110</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>48.0</td>
    </tr>
    <tr>
      <th>22903</th>
      <td>233449</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>48.0</td>
    </tr>
  </tbody>
</table>
<p>22904 rows × 4 columns</p>
</div>



## outerjoin을 한 테이블 중 inner join을 한 테이블과 중복되는 행row을 삭제하세요 


```python
concat_1920=pd.concat([df_inner1920,df_outer1920])
concat_1920
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
      <th>sofifa_id</th>
      <th>short_name</th>
      <th>overall_x</th>
      <th>overall_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20801</td>
      <td>Cristiano Ronaldo</td>
      <td>94.0</td>
      <td>93.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>158023</td>
      <td>L. Messi</td>
      <td>94.0</td>
      <td>94.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>190871</td>
      <td>Neymar Jr</td>
      <td>92.0</td>
      <td>92.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>193080</td>
      <td>De Gea</td>
      <td>91.0</td>
      <td>89.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>192985</td>
      <td>K. De Bruyne</td>
      <td>91.0</td>
      <td>91.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>22899</th>
      <td>245006</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>48.0</td>
    </tr>
    <tr>
      <th>22900</th>
      <td>250995</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>48.0</td>
    </tr>
    <tr>
      <th>22901</th>
      <td>252332</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>48.0</td>
    </tr>
    <tr>
      <th>22902</th>
      <td>251110</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>48.0</td>
    </tr>
    <tr>
      <th>22903</th>
      <td>233449</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>48.0</td>
    </tr>
  </tbody>
</table>
<p>36048 rows × 4 columns</p>
</div>




```python
delete_du=concat_1920.drop_duplicates("sofifa_id")
delete_du
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
      <th>sofifa_id</th>
      <th>short_name</th>
      <th>overall_x</th>
      <th>overall_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20801</td>
      <td>Cristiano Ronaldo</td>
      <td>94.0</td>
      <td>93.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>158023</td>
      <td>L. Messi</td>
      <td>94.0</td>
      <td>94.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>190871</td>
      <td>Neymar Jr</td>
      <td>92.0</td>
      <td>92.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>193080</td>
      <td>De Gea</td>
      <td>91.0</td>
      <td>89.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>192985</td>
      <td>K. De Bruyne</td>
      <td>91.0</td>
      <td>91.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>22899</th>
      <td>245006</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>48.0</td>
    </tr>
    <tr>
      <th>22900</th>
      <td>250995</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>48.0</td>
    </tr>
    <tr>
      <th>22901</th>
      <td>252332</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>48.0</td>
    </tr>
    <tr>
      <th>22902</th>
      <td>251110</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>48.0</td>
    </tr>
    <tr>
      <th>22903</th>
      <td>233449</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>48.0</td>
    </tr>
  </tbody>
</table>
<p>22904 rows × 4 columns</p>
</div>


