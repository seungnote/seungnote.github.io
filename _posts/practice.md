```python
import pandas as pd
import numpy as np
```


```python
customer1=pd.DataFrame({'id':['c01','c02','c03','c04'],
                       'last_name':['Lee','Kim','Choi','Park']},
                      index=[0,1,2,3])
customer1
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
      <th>last_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>c01</td>
      <td>Lee</td>
    </tr>
    <tr>
      <th>1</th>
      <td>c02</td>
      <td>Kim</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c03</td>
      <td>Choi</td>
    </tr>
    <tr>
      <th>3</th>
      <td>c04</td>
      <td>Park</td>
    </tr>
  </tbody>
</table>
</div>




```python
customer2=pd.DataFrame({'id':['c05','c06','c07'],
                       'Last_name':['Lim','Bae','Kim'],
                       'age':['23','34','45']},
                      index=[0,1,2])
customer2
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
      <th>Last_name</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>c05</td>
      <td>Lim</td>
      <td>23</td>
    </tr>
    <tr>
      <th>1</th>
      <td>c06</td>
      <td>Bae</td>
      <td>34</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c07</td>
      <td>Kim</td>
      <td>45</td>
    </tr>
  </tbody>
</table>
</div>




```python
customer2.columns=['id','last_name','age']
customer2
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
      <th>last_name</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>c05</td>
      <td>Lim</td>
      <td>23</td>
    </tr>
    <tr>
      <th>1</th>
      <td>c06</td>
      <td>Bae</td>
      <td>34</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c07</td>
      <td>Kim</td>
      <td>45</td>
    </tr>
  </tbody>
</table>
</div>




```python
new=pd.concat([customer1,customer2])
new
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
      <th>last_name</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>c01</td>
      <td>Lee</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>c02</td>
      <td>Kim</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c03</td>
      <td>Choi</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>c04</td>
      <td>Park</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>0</th>
      <td>c05</td>
      <td>Lim</td>
      <td>23</td>
    </tr>
    <tr>
      <th>1</th>
      <td>c06</td>
      <td>Bae</td>
      <td>34</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c07</td>
      <td>Kim</td>
      <td>45</td>
    </tr>
  </tbody>
</table>
</div>




```python
new2=new.reset_index(drop=True)
new2
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
      <th>last_name</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>c01</td>
      <td>Lee</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>c02</td>
      <td>Kim</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c03</td>
      <td>Choi</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>c04</td>
      <td>Park</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>c05</td>
      <td>Lim</td>
      <td>23</td>
    </tr>
    <tr>
      <th>5</th>
      <td>c06</td>
      <td>Bae</td>
      <td>34</td>
    </tr>
    <tr>
      <th>6</th>
      <td>c07</td>
      <td>Kim</td>
      <td>45</td>
    </tr>
  </tbody>
</table>
</div>




```python
new2.reset_index()
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
      <th>index</th>
      <th>id</th>
      <th>last_name</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>c01</td>
      <td>Lee</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>c02</td>
      <td>Kim</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>c03</td>
      <td>Choi</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>c04</td>
      <td>Park</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>c05</td>
      <td>Lim</td>
      <td>23</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>c06</td>
      <td>Bae</td>
      <td>34</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>c07</td>
      <td>Kim</td>
      <td>45</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
