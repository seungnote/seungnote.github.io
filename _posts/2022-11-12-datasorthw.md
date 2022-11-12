---
title:  "[Python] 데이터핸들링-데이터정렬(sort_value)QUIZ" 

categories:
  - Python
tags:
  - [Python,ADP,quiz,class101]

toc: true
toc_sticky: true

date: 2022-11-12

---

# 과제 2-4 

## players_20.csv데이터에서 height_cm, weight_kg 의 중위값(median)을 출력하세요.


```python
import pandas as pd 
```


```python
fifa_df = pd.read_csv("D:/anaconda/00.studying/data/players_20.csv")
fifa_df
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
      <th>player_url</th>
      <th>short_name</th>
      <th>long_name</th>
      <th>age</th>
      <th>dob</th>
      <th>height_cm</th>
      <th>weight_kg</th>
      <th>nationality</th>
      <th>club</th>
      <th>...</th>
      <th>lwb</th>
      <th>ldm</th>
      <th>cdm</th>
      <th>rdm</th>
      <th>rwb</th>
      <th>lb</th>
      <th>lcb</th>
      <th>cb</th>
      <th>rcb</th>
      <th>rb</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>158023</td>
      <td>https://sofifa.com/player/158023/lionel-messi/...</td>
      <td>L. Messi</td>
      <td>Lionel Andrés Messi Cuccittini</td>
      <td>32</td>
      <td>1987-06-24</td>
      <td>170</td>
      <td>72</td>
      <td>Argentina</td>
      <td>FC Barcelona</td>
      <td>...</td>
      <td>68+2</td>
      <td>66+2</td>
      <td>66+2</td>
      <td>66+2</td>
      <td>68+2</td>
      <td>63+2</td>
      <td>52+2</td>
      <td>52+2</td>
      <td>52+2</td>
      <td>63+2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20801</td>
      <td>https://sofifa.com/player/20801/c-ronaldo-dos-...</td>
      <td>Cristiano Ronaldo</td>
      <td>Cristiano Ronaldo dos Santos Aveiro</td>
      <td>34</td>
      <td>1985-02-05</td>
      <td>187</td>
      <td>83</td>
      <td>Portugal</td>
      <td>Juventus</td>
      <td>...</td>
      <td>65+3</td>
      <td>61+3</td>
      <td>61+3</td>
      <td>61+3</td>
      <td>65+3</td>
      <td>61+3</td>
      <td>53+3</td>
      <td>53+3</td>
      <td>53+3</td>
      <td>61+3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>190871</td>
      <td>https://sofifa.com/player/190871/neymar-da-sil...</td>
      <td>Neymar Jr</td>
      <td>Neymar da Silva Santos Junior</td>
      <td>27</td>
      <td>1992-02-05</td>
      <td>175</td>
      <td>68</td>
      <td>Brazil</td>
      <td>Paris Saint-Germain</td>
      <td>...</td>
      <td>66+3</td>
      <td>61+3</td>
      <td>61+3</td>
      <td>61+3</td>
      <td>66+3</td>
      <td>61+3</td>
      <td>46+3</td>
      <td>46+3</td>
      <td>46+3</td>
      <td>61+3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>200389</td>
      <td>https://sofifa.com/player/200389/jan-oblak/20/...</td>
      <td>J. Oblak</td>
      <td>Jan Oblak</td>
      <td>26</td>
      <td>1993-01-07</td>
      <td>188</td>
      <td>87</td>
      <td>Slovenia</td>
      <td>Atlético Madrid</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>183277</td>
      <td>https://sofifa.com/player/183277/eden-hazard/2...</td>
      <td>E. Hazard</td>
      <td>Eden Hazard</td>
      <td>28</td>
      <td>1991-01-07</td>
      <td>175</td>
      <td>74</td>
      <td>Belgium</td>
      <td>Real Madrid</td>
      <td>...</td>
      <td>66+3</td>
      <td>63+3</td>
      <td>63+3</td>
      <td>63+3</td>
      <td>66+3</td>
      <td>61+3</td>
      <td>49+3</td>
      <td>49+3</td>
      <td>49+3</td>
      <td>61+3</td>
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
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>18273</th>
      <td>245006</td>
      <td>https://sofifa.com/player/245006/shuai-shao/20...</td>
      <td>Shao Shuai</td>
      <td>邵帅</td>
      <td>22</td>
      <td>1997-03-10</td>
      <td>186</td>
      <td>79</td>
      <td>China PR</td>
      <td>Beijing Renhe FC</td>
      <td>...</td>
      <td>43+2</td>
      <td>42+2</td>
      <td>42+2</td>
      <td>42+2</td>
      <td>43+2</td>
      <td>45+2</td>
      <td>46+2</td>
      <td>46+2</td>
      <td>46+2</td>
      <td>45+2</td>
    </tr>
    <tr>
      <th>18274</th>
      <td>250995</td>
      <td>https://sofifa.com/player/250995/mingjie-xiao/...</td>
      <td>Xiao Mingjie</td>
      <td>Mingjie Xiao</td>
      <td>22</td>
      <td>1997-01-01</td>
      <td>177</td>
      <td>66</td>
      <td>China PR</td>
      <td>Shanghai SIPG FC</td>
      <td>...</td>
      <td>44+2</td>
      <td>43+2</td>
      <td>43+2</td>
      <td>43+2</td>
      <td>44+2</td>
      <td>46+2</td>
      <td>47+2</td>
      <td>47+2</td>
      <td>47+2</td>
      <td>46+2</td>
    </tr>
    <tr>
      <th>18275</th>
      <td>252332</td>
      <td>https://sofifa.com/player/252332/wei-zhang/20/...</td>
      <td>Zhang Wei</td>
      <td>张威</td>
      <td>19</td>
      <td>2000-05-16</td>
      <td>186</td>
      <td>75</td>
      <td>China PR</td>
      <td>Hebei China Fortune FC</td>
      <td>...</td>
      <td>47+2</td>
      <td>49+2</td>
      <td>49+2</td>
      <td>49+2</td>
      <td>47+2</td>
      <td>47+2</td>
      <td>49+2</td>
      <td>49+2</td>
      <td>49+2</td>
      <td>47+2</td>
    </tr>
    <tr>
      <th>18276</th>
      <td>251110</td>
      <td>https://sofifa.com/player/251110/haijian-wang/...</td>
      <td>Wang Haijian</td>
      <td>汪海健</td>
      <td>18</td>
      <td>2000-08-02</td>
      <td>185</td>
      <td>74</td>
      <td>China PR</td>
      <td>Shanghai Greenland Shenhua FC</td>
      <td>...</td>
      <td>48+2</td>
      <td>48+2</td>
      <td>48+2</td>
      <td>48+2</td>
      <td>48+2</td>
      <td>48+2</td>
      <td>49+2</td>
      <td>49+2</td>
      <td>49+2</td>
      <td>48+2</td>
    </tr>
    <tr>
      <th>18277</th>
      <td>233449</td>
      <td>https://sofifa.com/player/233449/ximing-pan/20...</td>
      <td>Pan Ximing</td>
      <td>潘喜明</td>
      <td>26</td>
      <td>1993-01-11</td>
      <td>182</td>
      <td>78</td>
      <td>China PR</td>
      <td>Hebei China Fortune FC</td>
      <td>...</td>
      <td>48+2</td>
      <td>49+2</td>
      <td>49+2</td>
      <td>49+2</td>
      <td>48+2</td>
      <td>48+2</td>
      <td>50+2</td>
      <td>50+2</td>
      <td>50+2</td>
      <td>48+2</td>
    </tr>
  </tbody>
</table>
<p>18278 rows × 104 columns</p>
</div>



## 데이터셋의 height_cm, weight_kg 이 중위값(median)보다 큰 선수를 출력하세요 


```python
# median 구하기 
print(fifa_df.median())
```

    sofifa_id                  226165.0
    age                            25.0
    height_cm                     181.0
    weight_kg                      75.0
    overall                        66.0
                                 ...   
    goalkeeping_diving             11.0
    goalkeeping_handling           11.0
    goalkeeping_kicking            11.0
    goalkeeping_positioning        11.0
    goalkeeping_reflexes           11.0
    Length: 61, dtype: float64
    

    C:\Windows\Temp\ipykernel_380\2581007142.py:1: FutureWarning: Dropping of nuisance columns in DataFrame reductions (with 'numeric_only=None') is deprecated; in a future version this will raise TypeError.  Select only valid columns before calling the reduction.
      print(fifa_df.median())
    


```python
# 선수 출력
fifa_df[(fifa_df['height_cm']>181.0)&(fifa_df['weight_kg']>75.0)]

# 해당 선수 이름만 출력 
fifa_df[['short_name']][(fifa_df['height_cm']>181.0)&(fifa_df['weight_kg']>75.0)]
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
      <th>short_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Cristiano Ronaldo</td>
    </tr>
    <tr>
      <th>3</th>
      <td>J. Oblak</td>
    </tr>
    <tr>
      <th>6</th>
      <td>M. ter Stegen</td>
    </tr>
    <tr>
      <th>7</th>
      <td>V. van Dijk</td>
    </tr>
    <tr>
      <th>11</th>
      <td>K. Koulibaly</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>18255</th>
      <td>C. Heath</td>
    </tr>
    <tr>
      <th>18262</th>
      <td>S. Callan</td>
    </tr>
    <tr>
      <th>18272</th>
      <td>P. Martin</td>
    </tr>
    <tr>
      <th>18273</th>
      <td>Shao Shuai</td>
    </tr>
    <tr>
      <th>18277</th>
      <td>Pan Ximing</td>
    </tr>
  </tbody>
</table>
<p>6863 rows × 1 columns</p>
</div>



## height_cm 기준으로 내림차순 정렬하세요


```python
# 값기준 정렬
fifa_df.sort_values(by=['height_cm'], ascending=False).head(10)
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
      <th>player_url</th>
      <th>short_name</th>
      <th>long_name</th>
      <th>age</th>
      <th>dob</th>
      <th>height_cm</th>
      <th>weight_kg</th>
      <th>nationality</th>
      <th>club</th>
      <th>...</th>
      <th>lwb</th>
      <th>ldm</th>
      <th>cdm</th>
      <th>rdm</th>
      <th>rwb</th>
      <th>lb</th>
      <th>lcb</th>
      <th>cb</th>
      <th>rcb</th>
      <th>rb</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>9208</th>
      <td>199321</td>
      <td>https://sofifa.com/player/199321/tomas-holy/20...</td>
      <td>T. Holý</td>
      <td>Tomáš Holý</td>
      <td>27</td>
      <td>1991-12-10</td>
      <td>205</td>
      <td>102</td>
      <td>Czech Republic</td>
      <td>Ipswich Town</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8200</th>
      <td>225050</td>
      <td>https://sofifa.com/player/225050/abdoul-ba/20/...</td>
      <td>A. Ba</td>
      <td>Abdoul Ba</td>
      <td>25</td>
      <td>1994-02-08</td>
      <td>203</td>
      <td>94</td>
      <td>Mauritania</td>
      <td>AJ Auxerre</td>
      <td>...</td>
      <td>56+2</td>
      <td>58+2</td>
      <td>58+2</td>
      <td>58+2</td>
      <td>56+2</td>
      <td>58+2</td>
      <td>66+2</td>
      <td>66+2</td>
      <td>66+2</td>
      <td>58+2</td>
    </tr>
    <tr>
      <th>12808</th>
      <td>215408</td>
      <td>https://sofifa.com/player/215408/aaron-chapman...</td>
      <td>A. Chapman</td>
      <td>Aaron Chapman</td>
      <td>29</td>
      <td>1990-05-29</td>
      <td>203</td>
      <td>92</td>
      <td>England</td>
      <td>Peterborough United</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3121</th>
      <td>192613</td>
      <td>https://sofifa.com/player/192613/costel-pantil...</td>
      <td>C. Pantilimon</td>
      <td>Costel Pantilimon</td>
      <td>32</td>
      <td>1987-02-01</td>
      <td>203</td>
      <td>96</td>
      <td>Romania</td>
      <td>Nottingham Forest</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>12864</th>
      <td>237015</td>
      <td>https://sofifa.com/player/237015/mikkel-mena-q...</td>
      <td>M. Qvist</td>
      <td>Mikkel Mena Qvist</td>
      <td>26</td>
      <td>1993-04-22</td>
      <td>203</td>
      <td>94</td>
      <td>Denmark</td>
      <td>AC Horsens</td>
      <td>...</td>
      <td>57+2</td>
      <td>60+2</td>
      <td>60+2</td>
      <td>60+2</td>
      <td>57+2</td>
      <td>57+2</td>
      <td>62+2</td>
      <td>62+2</td>
      <td>62+2</td>
      <td>57+2</td>
    </tr>
    <tr>
      <th>17365</th>
      <td>241870</td>
      <td>https://sofifa.com/player/241870/matt-casey/20...</td>
      <td>M. Casey</td>
      <td>Matt Casey</td>
      <td>19</td>
      <td>1999-11-13</td>
      <td>203</td>
      <td>80</td>
      <td>England</td>
      <td>Portsmouth</td>
      <td>...</td>
      <td>47+2</td>
      <td>48+2</td>
      <td>48+2</td>
      <td>48+2</td>
      <td>47+2</td>
      <td>49+2</td>
      <td>53+2</td>
      <td>53+2</td>
      <td>53+2</td>
      <td>49+2</td>
    </tr>
    <tr>
      <th>5451</th>
      <td>199074</td>
      <td>https://sofifa.com/player/199074/lacina-traore...</td>
      <td>L. Traoré</td>
      <td>Lacina Traoré</td>
      <td>29</td>
      <td>1990-05-20</td>
      <td>203</td>
      <td>87</td>
      <td>Ivory Coast</td>
      <td>CFR Cluj</td>
      <td>...</td>
      <td>46+2</td>
      <td>49+2</td>
      <td>49+2</td>
      <td>49+2</td>
      <td>46+2</td>
      <td>44+2</td>
      <td>48+2</td>
      <td>48+2</td>
      <td>48+2</td>
      <td>44+2</td>
    </tr>
    <tr>
      <th>17149</th>
      <td>243387</td>
      <td>https://sofifa.com/player/243387/samuel-brolin...</td>
      <td>S. Brolin</td>
      <td>Samuel Brolin</td>
      <td>18</td>
      <td>2000-09-29</td>
      <td>202</td>
      <td>85</td>
      <td>Sweden</td>
      <td>AIK</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4868</th>
      <td>224836</td>
      <td>https://sofifa.com/player/224836/vanja-milinko...</td>
      <td>V. Milinković-Savić</td>
      <td>Vanja Milinković-Savić</td>
      <td>22</td>
      <td>1997-02-20</td>
      <td>202</td>
      <td>92</td>
      <td>Serbia</td>
      <td>Standard de Liège</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7725</th>
      <td>243675</td>
      <td>https://sofifa.com/player/243675/kjell-scherpe...</td>
      <td>K. Scherpen</td>
      <td>Kjell Scherpen</td>
      <td>19</td>
      <td>2000-01-23</td>
      <td>202</td>
      <td>85</td>
      <td>Netherlands</td>
      <td>Ajax</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>10 rows × 104 columns</p>
</div>



## weight_kg 기준으로 내림차순 정렬하세요


```python
fifa_df.sort_values(by=['weight_kg'], ascending=True).head(10)
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
      <th>player_url</th>
      <th>short_name</th>
      <th>long_name</th>
      <th>age</th>
      <th>dob</th>
      <th>height_cm</th>
      <th>weight_kg</th>
      <th>nationality</th>
      <th>club</th>
      <th>...</th>
      <th>lwb</th>
      <th>ldm</th>
      <th>cdm</th>
      <th>rdm</th>
      <th>rwb</th>
      <th>lb</th>
      <th>lcb</th>
      <th>cb</th>
      <th>rcb</th>
      <th>rb</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>13070</th>
      <td>235600</td>
      <td>https://sofifa.com/player/235600/bandar-al-mut...</td>
      <td>B. Al Mutairi</td>
      <td>Bandar Al Mutairi</td>
      <td>29</td>
      <td>1990-03-14</td>
      <td>168</td>
      <td>50</td>
      <td>Saudi Arabia</td>
      <td>Al Fayha</td>
      <td>...</td>
      <td>62+2</td>
      <td>56+2</td>
      <td>56+2</td>
      <td>56+2</td>
      <td>62+2</td>
      <td>61+2</td>
      <td>56+2</td>
      <td>56+2</td>
      <td>56+2</td>
      <td>61+2</td>
    </tr>
    <tr>
      <th>17022</th>
      <td>252422</td>
      <td>https://sofifa.com/player/252422/mohsen-abdull...</td>
      <td>M. Abdullah</td>
      <td>Mohsen Abdullah</td>
      <td>24</td>
      <td>1995-04-13</td>
      <td>164</td>
      <td>52</td>
      <td>United Arab Emirates</td>
      <td>Al Ain FC</td>
      <td>...</td>
      <td>52+2</td>
      <td>49+2</td>
      <td>49+2</td>
      <td>49+2</td>
      <td>52+2</td>
      <td>50+2</td>
      <td>42+2</td>
      <td>42+2</td>
      <td>42+2</td>
      <td>50+2</td>
    </tr>
    <tr>
      <th>4982</th>
      <td>214919</td>
      <td>https://sofifa.com/player/214919/diego-rojas/2...</td>
      <td>D. Rojas</td>
      <td>Diego Nicolás Rojas Orellana</td>
      <td>24</td>
      <td>1995-02-15</td>
      <td>164</td>
      <td>52</td>
      <td>Chile</td>
      <td>Unión La Calera</td>
      <td>...</td>
      <td>54+2</td>
      <td>54+2</td>
      <td>54+2</td>
      <td>54+2</td>
      <td>54+2</td>
      <td>50+2</td>
      <td>43+2</td>
      <td>43+2</td>
      <td>43+2</td>
      <td>50+2</td>
    </tr>
    <tr>
      <th>10114</th>
      <td>234430</td>
      <td>https://sofifa.com/player/234430/isidro-ros-ri...</td>
      <td>Isi Ros</td>
      <td>Isidro Ros Ríos</td>
      <td>23</td>
      <td>1995-11-06</td>
      <td>165</td>
      <td>53</td>
      <td>Spain</td>
      <td>AD Alcorcón</td>
      <td>...</td>
      <td>51+2</td>
      <td>44+2</td>
      <td>44+2</td>
      <td>44+2</td>
      <td>51+2</td>
      <td>48+2</td>
      <td>37+2</td>
      <td>37+2</td>
      <td>37+2</td>
      <td>48+2</td>
    </tr>
    <tr>
      <th>17078</th>
      <td>246091</td>
      <td>https://sofifa.com/player/246091/jorge-garcia/...</td>
      <td>J. García</td>
      <td>Jorge García</td>
      <td>17</td>
      <td>2002-01-22</td>
      <td>165</td>
      <td>53</td>
      <td>Mexico</td>
      <td>Cruz Azul</td>
      <td>...</td>
      <td>51+2</td>
      <td>50+2</td>
      <td>50+2</td>
      <td>50+2</td>
      <td>51+2</td>
      <td>53+2</td>
      <td>53+2</td>
      <td>53+2</td>
      <td>53+2</td>
      <td>53+2</td>
    </tr>
    <tr>
      <th>12666</th>
      <td>232682</td>
      <td>https://sofifa.com/player/232682/abdulmajeed-a...</td>
      <td>A. Al Suwat</td>
      <td>Abdulmajeed Abdullah Al-Swat</td>
      <td>24</td>
      <td>1995-04-21</td>
      <td>168</td>
      <td>54</td>
      <td>Saudi Arabia</td>
      <td>Al Taawoun</td>
      <td>...</td>
      <td>54+2</td>
      <td>54+2</td>
      <td>54+2</td>
      <td>54+2</td>
      <td>54+2</td>
      <td>53+2</td>
      <td>50+2</td>
      <td>50+2</td>
      <td>50+2</td>
      <td>53+2</td>
    </tr>
    <tr>
      <th>10455</th>
      <td>239505</td>
      <td>https://sofifa.com/player/239505/patryk-kun/20...</td>
      <td>P. Kun</td>
      <td>Patryk Kun</td>
      <td>24</td>
      <td>1995-04-20</td>
      <td>165</td>
      <td>54</td>
      <td>Poland</td>
      <td>Raków Częstochowa</td>
      <td>...</td>
      <td>59+2</td>
      <td>54+2</td>
      <td>54+2</td>
      <td>54+2</td>
      <td>59+2</td>
      <td>57+2</td>
      <td>49+2</td>
      <td>49+2</td>
      <td>49+2</td>
      <td>57+2</td>
    </tr>
    <tr>
      <th>17817</th>
      <td>248551</td>
      <td>https://sofifa.com/player/248551/tomas-stabell...</td>
      <td>T. Stabell</td>
      <td>Tomas Stabell</td>
      <td>17</td>
      <td>2002-01-30</td>
      <td>167</td>
      <td>54</td>
      <td>Norway</td>
      <td>Tromsø IL</td>
      <td>...</td>
      <td>49+2</td>
      <td>47+2</td>
      <td>47+2</td>
      <td>47+2</td>
      <td>49+2</td>
      <td>49+2</td>
      <td>44+2</td>
      <td>44+2</td>
      <td>44+2</td>
      <td>49+2</td>
    </tr>
    <tr>
      <th>5680</th>
      <td>225964</td>
      <td>https://sofifa.com/player/225964/jorge-carrasc...</td>
      <td>J. Carrascal</td>
      <td>Jorge Carrascal</td>
      <td>21</td>
      <td>1998-05-25</td>
      <td>178</td>
      <td>54</td>
      <td>Colombia</td>
      <td>River Plate</td>
      <td>...</td>
      <td>52+2</td>
      <td>50+2</td>
      <td>50+2</td>
      <td>50+2</td>
      <td>52+2</td>
      <td>50+2</td>
      <td>45+2</td>
      <td>45+2</td>
      <td>45+2</td>
      <td>50+2</td>
    </tr>
    <tr>
      <th>13254</th>
      <td>235121</td>
      <td>https://sofifa.com/player/235121/bryan-lozano/...</td>
      <td>B. Lozano</td>
      <td>Brian Avelino Lozano Aparicio</td>
      <td>22</td>
      <td>1997-03-20</td>
      <td>167</td>
      <td>54</td>
      <td>Mexico</td>
      <td>U.N.A.M.</td>
      <td>...</td>
      <td>48+2</td>
      <td>42+2</td>
      <td>42+2</td>
      <td>42+2</td>
      <td>48+2</td>
      <td>45+2</td>
      <td>35+2</td>
      <td>35+2</td>
      <td>35+2</td>
      <td>45+2</td>
    </tr>
  </tbody>
</table>
<p>10 rows × 104 columns</p>
</div>



## height_cm 와 weight_kg 를 기준으로 오름차순 정렬하세요 


```python
fifa_df.sort_values(by=['height_cm','weight_kg'], ascending=True).head(10)
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
      <th>player_url</th>
      <th>short_name</th>
      <th>long_name</th>
      <th>age</th>
      <th>dob</th>
      <th>height_cm</th>
      <th>weight_kg</th>
      <th>nationality</th>
      <th>club</th>
      <th>...</th>
      <th>lwb</th>
      <th>ldm</th>
      <th>cdm</th>
      <th>rdm</th>
      <th>rwb</th>
      <th>lb</th>
      <th>lcb</th>
      <th>cb</th>
      <th>rcb</th>
      <th>rb</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4829</th>
      <td>237994</td>
      <td>https://sofifa.com/player/237994/nahuel-barrio...</td>
      <td>N. Barrios</td>
      <td>Cristian Nahuel Barrios</td>
      <td>21</td>
      <td>1998-05-07</td>
      <td>156</td>
      <td>58</td>
      <td>Argentina</td>
      <td>San Lorenzo de Almagro</td>
      <td>...</td>
      <td>56+2</td>
      <td>52+2</td>
      <td>52+2</td>
      <td>52+2</td>
      <td>56+2</td>
      <td>54+2</td>
      <td>44+2</td>
      <td>44+2</td>
      <td>44+2</td>
      <td>54+2</td>
    </tr>
    <tr>
      <th>3898</th>
      <td>202184</td>
      <td>https://sofifa.com/player/202184/joao-plata/20...</td>
      <td>J. Plata</td>
      <td>João Jimmy Plata Cotera</td>
      <td>27</td>
      <td>1992-03-01</td>
      <td>157</td>
      <td>71</td>
      <td>Ecuador</td>
      <td>Real Salt Lake</td>
      <td>...</td>
      <td>55+2</td>
      <td>52+2</td>
      <td>52+2</td>
      <td>52+2</td>
      <td>55+2</td>
      <td>52+2</td>
      <td>45+2</td>
      <td>45+2</td>
      <td>45+2</td>
      <td>52+2</td>
    </tr>
    <tr>
      <th>1496</th>
      <td>183895</td>
      <td>https://sofifa.com/player/183895/maxi-moralez/...</td>
      <td>M. Moralez</td>
      <td>Maximiliano Nicol Moralez</td>
      <td>32</td>
      <td>1987-02-27</td>
      <td>158</td>
      <td>56</td>
      <td>Argentina</td>
      <td>New York City FC</td>
      <td>...</td>
      <td>65+2</td>
      <td>62+2</td>
      <td>62+2</td>
      <td>62+2</td>
      <td>65+2</td>
      <td>62+2</td>
      <td>53+2</td>
      <td>53+2</td>
      <td>53+2</td>
      <td>62+2</td>
    </tr>
    <tr>
      <th>4243</th>
      <td>234698</td>
      <td>https://sofifa.com/player/234698/chanathip-son...</td>
      <td>C. Songkrasin</td>
      <td>Chanathip Songkrasin</td>
      <td>25</td>
      <td>1993-10-05</td>
      <td>158</td>
      <td>56</td>
      <td>Thailand</td>
      <td>Hokkaido Consadole Sapporo</td>
      <td>...</td>
      <td>54+2</td>
      <td>49+2</td>
      <td>49+2</td>
      <td>49+2</td>
      <td>54+2</td>
      <td>50+2</td>
      <td>37+2</td>
      <td>37+2</td>
      <td>37+2</td>
      <td>50+2</td>
    </tr>
    <tr>
      <th>16929</th>
      <td>247822</td>
      <td>https://sofifa.com/player/247822/josh-nisbet/2...</td>
      <td>J. Nisbet</td>
      <td>Josh Nisbet</td>
      <td>20</td>
      <td>1999-06-15</td>
      <td>158</td>
      <td>58</td>
      <td>Australia</td>
      <td>Central Coast Mariners</td>
      <td>...</td>
      <td>56+2</td>
      <td>54+2</td>
      <td>54+2</td>
      <td>54+2</td>
      <td>56+2</td>
      <td>55+2</td>
      <td>50+2</td>
      <td>50+2</td>
      <td>50+2</td>
      <td>55+2</td>
    </tr>
    <tr>
      <th>6789</th>
      <td>235714</td>
      <td>https://sofifa.com/player/235714/misael-doming...</td>
      <td>M. Domínguez</td>
      <td>Josué Misael Domínguez González</td>
      <td>19</td>
      <td>1999-10-27</td>
      <td>159</td>
      <td>58</td>
      <td>Mexico</td>
      <td>Cruz Azul</td>
      <td>...</td>
      <td>55+2</td>
      <td>51+2</td>
      <td>51+2</td>
      <td>51+2</td>
      <td>55+2</td>
      <td>53+2</td>
      <td>46+2</td>
      <td>46+2</td>
      <td>46+2</td>
      <td>53+2</td>
    </tr>
    <tr>
      <th>15878</th>
      <td>241046</td>
      <td>https://sofifa.com/player/241046/jonas-romero/...</td>
      <td>J. Romero</td>
      <td>Jonás Romero</td>
      <td>18</td>
      <td>2000-08-21</td>
      <td>159</td>
      <td>59</td>
      <td>Argentina</td>
      <td>Atlético Tucumán</td>
      <td>...</td>
      <td>45+2</td>
      <td>39+2</td>
      <td>39+2</td>
      <td>39+2</td>
      <td>45+2</td>
      <td>43+2</td>
      <td>36+2</td>
      <td>36+2</td>
      <td>36+2</td>
      <td>43+2</td>
    </tr>
    <tr>
      <th>4552</th>
      <td>190629</td>
      <td>https://sofifa.com/player/190629/daniel-villal...</td>
      <td>D. Villalva</td>
      <td>Daniel Alberto Villalba Barrios</td>
      <td>26</td>
      <td>1992-07-06</td>
      <td>159</td>
      <td>62</td>
      <td>Argentina</td>
      <td>Tiburones Rojos de Veracruz</td>
      <td>...</td>
      <td>55+2</td>
      <td>51+2</td>
      <td>51+2</td>
      <td>51+2</td>
      <td>55+2</td>
      <td>52+2</td>
      <td>41+2</td>
      <td>41+2</td>
      <td>41+2</td>
      <td>52+2</td>
    </tr>
    <tr>
      <th>6541</th>
      <td>222970</td>
      <td>https://sofifa.com/player/222970/erhun-oztumer...</td>
      <td>E. Oztumer</td>
      <td>Erhun Oztumer</td>
      <td>28</td>
      <td>1991-05-29</td>
      <td>160</td>
      <td>60</td>
      <td>England</td>
      <td>Charlton Athletic</td>
      <td>...</td>
      <td>53+2</td>
      <td>50+2</td>
      <td>50+2</td>
      <td>50+2</td>
      <td>53+2</td>
      <td>49+2</td>
      <td>40+2</td>
      <td>40+2</td>
      <td>40+2</td>
      <td>49+2</td>
    </tr>
    <tr>
      <th>3946</th>
      <td>214327</td>
      <td>https://sofifa.com/player/214327/vladimir-hern...</td>
      <td>V. Hernández</td>
      <td>Vladimir Javier Hernández Rivero</td>
      <td>30</td>
      <td>1989-04-23</td>
      <td>160</td>
      <td>61</td>
      <td>Colombia</td>
      <td>Atlético Nacional</td>
      <td>...</td>
      <td>55+2</td>
      <td>49+2</td>
      <td>49+2</td>
      <td>49+2</td>
      <td>55+2</td>
      <td>51+2</td>
      <td>39+2</td>
      <td>39+2</td>
      <td>39+2</td>
      <td>51+2</td>
    </tr>
  </tbody>
</table>
<p>10 rows × 104 columns</p>
</div>


