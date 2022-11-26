---
title:  "[Python] 데이터핸들링-데이터 모양변경(pivot) QUIZ" 

categories:
  - quiz
tags:
  - [Python,ADP,quiz,class101]

toc: true
toc_sticky: true

date: 2022-11-26

---


<h1>Table of Contents<span class="tocSkip"></span></h1>
<div class="toc"><ul class="toc-item"><li><span><a href="#과제-3-2-melt-&amp;-pivot-table" data-toc-modified-id="과제-3-2-melt-&amp;-pivot-table-1"><span class="toc-item-num">1&nbsp;&nbsp;</span>과제 3-2 melt &amp; pivot table</a></span><ul class="toc-item"><li><span><a href="#데이터-:-'식품소비.csv'" data-toc-modified-id="데이터-:-'식품소비.csv'-1.1"><span class="toc-item-num">1.1&nbsp;&nbsp;</span>데이터 : '식품소비.csv'</a></span></li><li><span><a href="#y값을-id_vars로-놓고-column들이-category로-바뀌도록-테이블을-구성하세요" data-toc-modified-id="y값을-id_vars로-놓고-column들이-category로-바뀌도록-테이블을-구성하세요-1.2"><span class="toc-item-num">1.2&nbsp;&nbsp;</span>y값을 id_vars로 놓고 column들이 category로 바뀌도록 테이블을 구성하세요</a></span></li><li><span><a href="#아래와-같이-category,-y-값에-따른-평균을-구하세요" data-toc-modified-id="아래와-같이-category,-y-값에-따른-평균을-구하세요-1.3"><span class="toc-item-num">1.3&nbsp;&nbsp;</span>아래와 같이 category, y 값에 따른 평균을 구하세요</a></span></li><li><span><a href="#아래와-같이-category,-y-값에-따른-표준편차를-구하세요" data-toc-modified-id="아래와-같이-category,-y-값에-따른-표준편차를-구하세요-1.4"><span class="toc-item-num">1.4&nbsp;&nbsp;</span>아래와 같이 category, y 값에 따른 표준편차를 구하세요</a></span></li></ul></li></ul></div>

# 과제 3-2 melt & pivot table 

## 데이터 : '식품소비.csv' 
## y값을 id_vars로 놓고 column들이 category로 바뀌도록 테이블을 구성하세요 


```python
## 아래와 같이 테이블 구성하세요 
## 차후 통계분석 (Two-way ANOVA와 같은 모델에서는 아래와 같이 숫자형 변수를 범주형으로 변환시킬 수 있어야 합니다.)
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
      <th>y</th>
      <th>category</th>
      <th>purchase_mean</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>fruits</td>
      <td>1.990391</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>fruits</td>
      <td>0.399026</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>fruits</td>
      <td>-1.084450</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>fruits</td>
      <td>0.587832</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>fruits</td>
      <td>0.578841</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>3931</th>
      <td>0</td>
      <td>snack</td>
      <td>-0.074406</td>
    </tr>
    <tr>
      <th>3932</th>
      <td>0</td>
      <td>snack</td>
      <td>-0.941918</td>
    </tr>
    <tr>
      <th>3933</th>
      <td>0</td>
      <td>snack</td>
      <td>0.617562</td>
    </tr>
    <tr>
      <th>3934</th>
      <td>0</td>
      <td>snack</td>
      <td>-0.500739</td>
    </tr>
    <tr>
      <th>3935</th>
      <td>0</td>
      <td>snack</td>
      <td>0.442424</td>
    </tr>
  </tbody>
</table>
<p>3936 rows × 3 columns</p>
</div>




```python
import pandas as pd
import numpy as np

df1=pd.read_csv('D:/anaconda/00.studying/data/식품소비.csv')
df1.head(3)
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
      <th>fruits</th>
      <th>noodle</th>
      <th>bread</th>
      <th>sea_meat_proc</th>
      <th>seafood</th>
      <th>vegetables</th>
      <th>milk_product</th>
      <th>drink</th>
      <th>seasoned</th>
      <th>alcohol</th>
      <th>meat</th>
      <th>snack</th>
      <th>y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.990391</td>
      <td>-1.012199</td>
      <td>-0.352724</td>
      <td>-0.984753</td>
      <td>0.292604</td>
      <td>0.018439</td>
      <td>-0.741526</td>
      <td>-0.712569</td>
      <td>8.609079</td>
      <td>-0.481356</td>
      <td>-0.192308</td>
      <td>-0.787966</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.399026</td>
      <td>-1.130454</td>
      <td>-0.736949</td>
      <td>1.138270</td>
      <td>-0.355907</td>
      <td>-0.407597</td>
      <td>-0.103825</td>
      <td>-0.745347</td>
      <td>-0.912666</td>
      <td>-0.507464</td>
      <td>-0.037267</td>
      <td>-0.053419</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-1.084450</td>
      <td>-0.515528</td>
      <td>0.287652</td>
      <td>1.202120</td>
      <td>1.041995</td>
      <td>-0.211286</td>
      <td>0.762794</td>
      <td>-0.365113</td>
      <td>-0.842134</td>
      <td>-0.118748</td>
      <td>-0.466610</td>
      <td>0.346815</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
melt_df1=pd.melt(df1,id_vars='y',
                 value_vars=['fruits','noodle','bread',
                             'sea_meat_proc','seafood','vegetables',
                             'milk_product','drink','seasoned',
                             'alcohol','meat','snack'],
                var_name='category',value_name='purchase_mean',ignore_index=True)
melt_df1
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
      <th>y</th>
      <th>category</th>
      <th>purchase_mean</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>fruits</td>
      <td>1.990391</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>fruits</td>
      <td>0.399026</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>fruits</td>
      <td>-1.084450</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>fruits</td>
      <td>0.587832</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>fruits</td>
      <td>0.578841</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>3931</th>
      <td>0</td>
      <td>snack</td>
      <td>-0.074406</td>
    </tr>
    <tr>
      <th>3932</th>
      <td>0</td>
      <td>snack</td>
      <td>-0.941918</td>
    </tr>
    <tr>
      <th>3933</th>
      <td>0</td>
      <td>snack</td>
      <td>0.617562</td>
    </tr>
    <tr>
      <th>3934</th>
      <td>0</td>
      <td>snack</td>
      <td>-0.500739</td>
    </tr>
    <tr>
      <th>3935</th>
      <td>0</td>
      <td>snack</td>
      <td>0.442424</td>
    </tr>
  </tbody>
</table>
<p>3936 rows × 3 columns</p>
</div>



## 아래와 같이 category, y 값에 따른 평균을 구하세요 


```python
## 아래와 같이 category, y 값에 따른 평균을 구하세요 
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
      <th>category</th>
      <th>alcohol</th>
      <th>bread</th>
      <th>drink</th>
      <th>fruits</th>
      <th>meat</th>
      <th>milk_product</th>
      <th>noodle</th>
      <th>sea_meat_proc</th>
      <th>seafood</th>
      <th>seasoned</th>
      <th>snack</th>
      <th>vegetables</th>
    </tr>
    <tr>
      <th>y</th>
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
      <th>0</th>
      <td>-0.004521</td>
      <td>0.034998</td>
      <td>0.039269</td>
      <td>-0.030951</td>
      <td>0.004843</td>
      <td>0.025906</td>
      <td>0.040710</td>
      <td>0.048653</td>
      <td>-0.049477</td>
      <td>-0.061767</td>
      <td>0.031815</td>
      <td>-0.021682</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.023995</td>
      <td>-0.185758</td>
      <td>-0.208430</td>
      <td>0.164280</td>
      <td>-0.025703</td>
      <td>-0.137499</td>
      <td>-0.216079</td>
      <td>-0.258238</td>
      <td>0.262609</td>
      <td>0.327840</td>
      <td>-0.168866</td>
      <td>0.115079</td>
    </tr>
  </tbody>
</table>
</div>




```python
melt_df1.pivot_table(index=['y'],columns='category',values='purchase_mean',aggfunc='mean',margins=False)
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
      <th>category</th>
      <th>alcohol</th>
      <th>bread</th>
      <th>drink</th>
      <th>fruits</th>
      <th>meat</th>
      <th>milk_product</th>
      <th>noodle</th>
      <th>sea_meat_proc</th>
      <th>seafood</th>
      <th>seasoned</th>
      <th>snack</th>
      <th>vegetables</th>
    </tr>
    <tr>
      <th>y</th>
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
      <th>0</th>
      <td>-0.004521</td>
      <td>0.034998</td>
      <td>0.039269</td>
      <td>-0.030951</td>
      <td>0.004843</td>
      <td>0.025906</td>
      <td>0.040710</td>
      <td>0.048653</td>
      <td>-0.049477</td>
      <td>-0.061767</td>
      <td>0.031815</td>
      <td>-0.021682</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.023995</td>
      <td>-0.185758</td>
      <td>-0.208430</td>
      <td>0.164280</td>
      <td>-0.025703</td>
      <td>-0.137499</td>
      <td>-0.216079</td>
      <td>-0.258238</td>
      <td>0.262609</td>
      <td>0.327840</td>
      <td>-0.168866</td>
      <td>0.115079</td>
    </tr>
  </tbody>
</table>
</div>



## 아래와 같이 category, y 값에 따른 표준편차를 구하세요 


```python
## 아래와 같이 category, y 값에 따른 표준편차를 구하세요 
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
      <th>category</th>
      <th>alcohol</th>
      <th>bread</th>
      <th>drink</th>
      <th>fruits</th>
      <th>meat</th>
      <th>milk_product</th>
      <th>noodle</th>
      <th>sea_meat_proc</th>
      <th>seafood</th>
      <th>seasoned</th>
      <th>snack</th>
      <th>vegetables</th>
    </tr>
    <tr>
      <th>y</th>
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
      <th>0</th>
      <td>0.807697</td>
      <td>1.022185</td>
      <td>1.021704</td>
      <td>0.968966</td>
      <td>1.077321</td>
      <td>1.021463</td>
      <td>1.031713</td>
      <td>1.025004</td>
      <td>0.962507</td>
      <td>0.869678</td>
      <td>1.003254</td>
      <td>1.005114</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.706742</td>
      <td>0.869196</td>
      <td>0.866008</td>
      <td>1.155856</td>
      <td>0.415114</td>
      <td>0.884510</td>
      <td>0.797004</td>
      <td>0.827882</td>
      <td>1.162932</td>
      <td>1.490916</td>
      <td>0.984640</td>
      <td>0.983806</td>
    </tr>
  </tbody>
</table>
</div>




```python
melt_df1.pivot_table(index=['y'],columns='category',values='purchase_mean',aggfunc='std',margins=False)
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
      <th>category</th>
      <th>alcohol</th>
      <th>bread</th>
      <th>drink</th>
      <th>fruits</th>
      <th>meat</th>
      <th>milk_product</th>
      <th>noodle</th>
      <th>sea_meat_proc</th>
      <th>seafood</th>
      <th>seasoned</th>
      <th>snack</th>
      <th>vegetables</th>
    </tr>
    <tr>
      <th>y</th>
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
      <th>0</th>
      <td>0.807697</td>
      <td>1.022185</td>
      <td>1.021704</td>
      <td>0.968966</td>
      <td>1.077321</td>
      <td>1.021463</td>
      <td>1.031713</td>
      <td>1.025004</td>
      <td>0.962507</td>
      <td>0.869678</td>
      <td>1.003254</td>
      <td>1.005114</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.706742</td>
      <td>0.869196</td>
      <td>0.866008</td>
      <td>1.155856</td>
      <td>0.415114</td>
      <td>0.884510</td>
      <td>0.797004</td>
      <td>0.827882</td>
      <td>1.162932</td>
      <td>1.490916</td>
      <td>0.984640</td>
      <td>0.983806</td>
    </tr>
  </tbody>
</table>
</div>


