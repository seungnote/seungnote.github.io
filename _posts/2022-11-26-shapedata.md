---
title:  "[Python] 데이터핸들링-데이터 모양변경(pivot)" 

categories:
  - Python
tags:
  - [Python,ADP,class101]

toc: true
toc_sticky: true

date: 2022-11-26

---

# 데이터 모양 변경(pivot)

## 데이터 재구조화(melt) 행으로 전환

피벗테이블 쉽게 만들기 위해서 재구조함 

pd.melt(df, id_vars=['A','D], value_vars=['B','E'],
var_name='myVarname', value_name='myValname', ignore_index=False)


```python
import pandas as pd
import numpy as np

df_student=pd.DataFrame({'id':['S01','S02','S03','S04','S05'], 
                        'kor':[80,75,56,69,90],
                        'math':[84,70,90,60,45],
                        'eng':[55,90,85,90,80]})
df_student
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
      <th>id</th>
      <th>kor</th>
      <th>math</th>
      <th>eng</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>S01</td>
      <td>80</td>
      <td>84</td>
      <td>55</td>
    </tr>
    <tr>
      <th>1</th>
      <td>S02</td>
      <td>75</td>
      <td>70</td>
      <td>90</td>
    </tr>
    <tr>
      <th>2</th>
      <td>S03</td>
      <td>56</td>
      <td>90</td>
      <td>85</td>
    </tr>
    <tr>
      <th>3</th>
      <td>S04</td>
      <td>69</td>
      <td>60</td>
      <td>90</td>
    </tr>
    <tr>
      <th>4</th>
      <td>S05</td>
      <td>90</td>
      <td>45</td>
      <td>80</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_student.info()

# id에는 object 
# value_vars는 집계 가능한 함수 
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 5 entries, 0 to 4
    Data columns (total 4 columns):
     #   Column  Non-Null Count  Dtype 
    ---  ------  --------------  ----- 
     0   id      5 non-null      object
     1   kor     5 non-null      int64 
     2   math    5 non-null      int64 
     3   eng     5 non-null      int64 
    dtypes: int64(3), object(1)
    memory usage: 288.0+ bytes
    


```python
melt_st=pd.melt(df_student,id_vars=['id'], value_vars=['kor','math','eng'],var_name='subject',
               value_name='score',ignore_index=False)
melt_st
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
      <th>id</th>
      <th>subject</th>
      <th>score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>S01</td>
      <td>kor</td>
      <td>80</td>
    </tr>
    <tr>
      <th>1</th>
      <td>S02</td>
      <td>kor</td>
      <td>75</td>
    </tr>
    <tr>
      <th>2</th>
      <td>S03</td>
      <td>kor</td>
      <td>56</td>
    </tr>
    <tr>
      <th>3</th>
      <td>S04</td>
      <td>kor</td>
      <td>69</td>
    </tr>
    <tr>
      <th>4</th>
      <td>S05</td>
      <td>kor</td>
      <td>90</td>
    </tr>
    <tr>
      <th>0</th>
      <td>S01</td>
      <td>math</td>
      <td>84</td>
    </tr>
    <tr>
      <th>1</th>
      <td>S02</td>
      <td>math</td>
      <td>70</td>
    </tr>
    <tr>
      <th>2</th>
      <td>S03</td>
      <td>math</td>
      <td>90</td>
    </tr>
    <tr>
      <th>3</th>
      <td>S04</td>
      <td>math</td>
      <td>60</td>
    </tr>
    <tr>
      <th>4</th>
      <td>S05</td>
      <td>math</td>
      <td>45</td>
    </tr>
    <tr>
      <th>0</th>
      <td>S01</td>
      <td>eng</td>
      <td>55</td>
    </tr>
    <tr>
      <th>1</th>
      <td>S02</td>
      <td>eng</td>
      <td>90</td>
    </tr>
    <tr>
      <th>2</th>
      <td>S03</td>
      <td>eng</td>
      <td>85</td>
    </tr>
    <tr>
      <th>3</th>
      <td>S04</td>
      <td>eng</td>
      <td>90</td>
    </tr>
    <tr>
      <th>4</th>
      <td>S05</td>
      <td>eng</td>
      <td>80</td>
    </tr>
  </tbody>
</table>
</div>




```python
melt_st=pd.melt(df_student,id_vars=['id'], value_vars=['kor','math','eng'],var_name='subject',
               value_name='score',ignore_index=True)
melt_st
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
      <th>id</th>
      <th>subject</th>
      <th>score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>S01</td>
      <td>kor</td>
      <td>80</td>
    </tr>
    <tr>
      <th>1</th>
      <td>S02</td>
      <td>kor</td>
      <td>75</td>
    </tr>
    <tr>
      <th>2</th>
      <td>S03</td>
      <td>kor</td>
      <td>56</td>
    </tr>
    <tr>
      <th>3</th>
      <td>S04</td>
      <td>kor</td>
      <td>69</td>
    </tr>
    <tr>
      <th>4</th>
      <td>S05</td>
      <td>kor</td>
      <td>90</td>
    </tr>
    <tr>
      <th>5</th>
      <td>S01</td>
      <td>math</td>
      <td>84</td>
    </tr>
    <tr>
      <th>6</th>
      <td>S02</td>
      <td>math</td>
      <td>70</td>
    </tr>
    <tr>
      <th>7</th>
      <td>S03</td>
      <td>math</td>
      <td>90</td>
    </tr>
    <tr>
      <th>8</th>
      <td>S04</td>
      <td>math</td>
      <td>60</td>
    </tr>
    <tr>
      <th>9</th>
      <td>S05</td>
      <td>math</td>
      <td>45</td>
    </tr>
    <tr>
      <th>10</th>
      <td>S01</td>
      <td>eng</td>
      <td>55</td>
    </tr>
    <tr>
      <th>11</th>
      <td>S02</td>
      <td>eng</td>
      <td>90</td>
    </tr>
    <tr>
      <th>12</th>
      <td>S03</td>
      <td>eng</td>
      <td>85</td>
    </tr>
    <tr>
      <th>13</th>
      <td>S04</td>
      <td>eng</td>
      <td>90</td>
    </tr>
    <tr>
      <th>14</th>
      <td>S05</td>
      <td>eng</td>
      <td>80</td>
    </tr>
  </tbody>
</table>
</div>



## 데이터 재구조화(pivot_table)

pd.pivot_table(data,index,columns,values,aggfunc,margins) 

만약에 margin=True 넣으면 총합도 알 수 있음


```python
# 원래 데이터로 바꾸기 
pd.pivot_table(melt_st,index='id',columns='subject',values='score').head(10)
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
      <th>subject</th>
      <th>eng</th>
      <th>kor</th>
      <th>math</th>
    </tr>
    <tr>
      <th>id</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>S01</th>
      <td>55</td>
      <td>80</td>
      <td>84</td>
    </tr>
    <tr>
      <th>S02</th>
      <td>90</td>
      <td>75</td>
      <td>70</td>
    </tr>
    <tr>
      <th>S03</th>
      <td>85</td>
      <td>56</td>
      <td>90</td>
    </tr>
    <tr>
      <th>S04</th>
      <td>90</td>
      <td>69</td>
      <td>60</td>
    </tr>
    <tr>
      <th>S05</th>
      <td>80</td>
      <td>90</td>
      <td>45</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_fruits=pd.read_csv("D:/anaconda/00.studying/data/Fruits.csv")
df_fruits

#id: Fruit
# var: Sales, Expenses, Profit
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
      <th>Fruit</th>
      <th>Year</th>
      <th>Location</th>
      <th>Sales</th>
      <th>Expenses</th>
      <th>Profit</th>
      <th>Date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Apples</td>
      <td>2008</td>
      <td>West</td>
      <td>98</td>
      <td>78</td>
      <td>20</td>
      <td>2008-12-31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Apples</td>
      <td>2009</td>
      <td>West</td>
      <td>111</td>
      <td>79</td>
      <td>32</td>
      <td>2009-12-31</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Apples</td>
      <td>2010</td>
      <td>West</td>
      <td>89</td>
      <td>76</td>
      <td>13</td>
      <td>2010-12-31</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Oranges</td>
      <td>2008</td>
      <td>East</td>
      <td>96</td>
      <td>81</td>
      <td>15</td>
      <td>2008-12-31</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Bananas</td>
      <td>2008</td>
      <td>East</td>
      <td>85</td>
      <td>76</td>
      <td>9</td>
      <td>2008-12-31</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Oranges</td>
      <td>2009</td>
      <td>East</td>
      <td>93</td>
      <td>80</td>
      <td>13</td>
      <td>2009-12-31</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Bananas</td>
      <td>2009</td>
      <td>East</td>
      <td>94</td>
      <td>78</td>
      <td>16</td>
      <td>2009-12-31</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Oranges</td>
      <td>2010</td>
      <td>East</td>
      <td>98</td>
      <td>91</td>
      <td>7</td>
      <td>2010-12-31</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Bananas</td>
      <td>2010</td>
      <td>East</td>
      <td>81</td>
      <td>71</td>
      <td>10</td>
      <td>2010-12-31</td>
    </tr>
  </tbody>
</table>
</div>




```python
melt_fruits=pd.melt(df_fruits,id_vars=['Fruit'],
                    value_vars=['Sales','Expenses','Profit'])
melt_fruits
#27개의 데이터가 27개의 행이됨 
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
      <th>Fruit</th>
      <th>variable</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Apples</td>
      <td>Sales</td>
      <td>98</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Apples</td>
      <td>Sales</td>
      <td>111</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Apples</td>
      <td>Sales</td>
      <td>89</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Oranges</td>
      <td>Sales</td>
      <td>96</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Bananas</td>
      <td>Sales</td>
      <td>85</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Oranges</td>
      <td>Sales</td>
      <td>93</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Bananas</td>
      <td>Sales</td>
      <td>94</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Oranges</td>
      <td>Sales</td>
      <td>98</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Bananas</td>
      <td>Sales</td>
      <td>81</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Apples</td>
      <td>Expenses</td>
      <td>78</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Apples</td>
      <td>Expenses</td>
      <td>79</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Apples</td>
      <td>Expenses</td>
      <td>76</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Oranges</td>
      <td>Expenses</td>
      <td>81</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Bananas</td>
      <td>Expenses</td>
      <td>76</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Oranges</td>
      <td>Expenses</td>
      <td>80</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Bananas</td>
      <td>Expenses</td>
      <td>78</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Oranges</td>
      <td>Expenses</td>
      <td>91</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Bananas</td>
      <td>Expenses</td>
      <td>71</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Apples</td>
      <td>Profit</td>
      <td>20</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Apples</td>
      <td>Profit</td>
      <td>32</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Apples</td>
      <td>Profit</td>
      <td>13</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Oranges</td>
      <td>Profit</td>
      <td>15</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Bananas</td>
      <td>Profit</td>
      <td>9</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Oranges</td>
      <td>Profit</td>
      <td>13</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Bananas</td>
      <td>Profit</td>
      <td>16</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Oranges</td>
      <td>Profit</td>
      <td>7</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Bananas</td>
      <td>Profit</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>




```python
melt_fruits.pivot_table(index=['Fruit'],columns='variable',values='value',aggfunc='mean',margins=False)
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
      <th>variable</th>
      <th>Expenses</th>
      <th>Profit</th>
      <th>Sales</th>
    </tr>
    <tr>
      <th>Fruit</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Apples</th>
      <td>77.666667</td>
      <td>21.666667</td>
      <td>99.333333</td>
    </tr>
    <tr>
      <th>Bananas</th>
      <td>75.000000</td>
      <td>11.666667</td>
      <td>86.666667</td>
    </tr>
    <tr>
      <th>Oranges</th>
      <td>84.000000</td>
      <td>11.666667</td>
      <td>95.666667</td>
    </tr>
  </tbody>
</table>
</div>




```python
melt_fruits.pivot_table(index=['Fruit'],columns='variable',values='value',aggfunc='sum',margins=True)
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
      <th>variable</th>
      <th>Expenses</th>
      <th>Profit</th>
      <th>Sales</th>
      <th>All</th>
    </tr>
    <tr>
      <th>Fruit</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Apples</th>
      <td>233</td>
      <td>65</td>
      <td>298</td>
      <td>596</td>
    </tr>
    <tr>
      <th>Bananas</th>
      <td>225</td>
      <td>35</td>
      <td>260</td>
      <td>520</td>
    </tr>
    <tr>
      <th>Oranges</th>
      <td>252</td>
      <td>35</td>
      <td>287</td>
      <td>574</td>
    </tr>
    <tr>
      <th>All</th>
      <td>710</td>
      <td>135</td>
      <td>845</td>
      <td>1690</td>
    </tr>
  </tbody>
</table>
</div>



## 데이터 행 열 변경(transpose)

데이터의 행과 열을 바꿔준다 


```python
df_fruits
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
      <th>Fruit</th>
      <th>Year</th>
      <th>Location</th>
      <th>Sales</th>
      <th>Expenses</th>
      <th>Profit</th>
      <th>Date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Apples</td>
      <td>2008</td>
      <td>West</td>
      <td>98</td>
      <td>78</td>
      <td>20</td>
      <td>2008-12-31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Apples</td>
      <td>2009</td>
      <td>West</td>
      <td>111</td>
      <td>79</td>
      <td>32</td>
      <td>2009-12-31</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Apples</td>
      <td>2010</td>
      <td>West</td>
      <td>89</td>
      <td>76</td>
      <td>13</td>
      <td>2010-12-31</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Oranges</td>
      <td>2008</td>
      <td>East</td>
      <td>96</td>
      <td>81</td>
      <td>15</td>
      <td>2008-12-31</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Bananas</td>
      <td>2008</td>
      <td>East</td>
      <td>85</td>
      <td>76</td>
      <td>9</td>
      <td>2008-12-31</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Oranges</td>
      <td>2009</td>
      <td>East</td>
      <td>93</td>
      <td>80</td>
      <td>13</td>
      <td>2009-12-31</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Bananas</td>
      <td>2009</td>
      <td>East</td>
      <td>94</td>
      <td>78</td>
      <td>16</td>
      <td>2009-12-31</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Oranges</td>
      <td>2010</td>
      <td>East</td>
      <td>98</td>
      <td>91</td>
      <td>7</td>
      <td>2010-12-31</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Bananas</td>
      <td>2010</td>
      <td>East</td>
      <td>81</td>
      <td>71</td>
      <td>10</td>
      <td>2010-12-31</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_fruits.transpose()
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
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Fruit</th>
      <td>Apples</td>
      <td>Apples</td>
      <td>Apples</td>
      <td>Oranges</td>
      <td>Bananas</td>
      <td>Oranges</td>
      <td>Bananas</td>
      <td>Oranges</td>
      <td>Bananas</td>
    </tr>
    <tr>
      <th>Year</th>
      <td>2008</td>
      <td>2009</td>
      <td>2010</td>
      <td>2008</td>
      <td>2008</td>
      <td>2009</td>
      <td>2009</td>
      <td>2010</td>
      <td>2010</td>
    </tr>
    <tr>
      <th>Location</th>
      <td>West</td>
      <td>West</td>
      <td>West</td>
      <td>East</td>
      <td>East</td>
      <td>East</td>
      <td>East</td>
      <td>East</td>
      <td>East</td>
    </tr>
    <tr>
      <th>Sales</th>
      <td>98</td>
      <td>111</td>
      <td>89</td>
      <td>96</td>
      <td>85</td>
      <td>93</td>
      <td>94</td>
      <td>98</td>
      <td>81</td>
    </tr>
    <tr>
      <th>Expenses</th>
      <td>78</td>
      <td>79</td>
      <td>76</td>
      <td>81</td>
      <td>76</td>
      <td>80</td>
      <td>78</td>
      <td>91</td>
      <td>71</td>
    </tr>
    <tr>
      <th>Profit</th>
      <td>20</td>
      <td>32</td>
      <td>13</td>
      <td>15</td>
      <td>9</td>
      <td>13</td>
      <td>16</td>
      <td>7</td>
      <td>10</td>
    </tr>
    <tr>
      <th>Date</th>
      <td>2008-12-31</td>
      <td>2009-12-31</td>
      <td>2010-12-31</td>
      <td>2008-12-31</td>
      <td>2008-12-31</td>
      <td>2009-12-31</td>
      <td>2009-12-31</td>
      <td>2010-12-31</td>
      <td>2010-12-31</td>
    </tr>
  </tbody>
</table>
</div>


