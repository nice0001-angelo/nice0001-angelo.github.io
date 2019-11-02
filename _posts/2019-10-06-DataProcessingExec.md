---
layout: post
title:  "06. Data Pre-Processing Exercise"
---

# 데이터 전처리 연습문제
- 모듈 참조


```python
import numpy
from pandas import DataFrame
from pandas import ExcelFile
```

샘플 데이터 가져오기


```python
xlsx = ExcelFile("http://itpaper.co.kr/demo/python/mpg.xlsx")
mpg_df = xlsx.parse(xlsx.sheet_names[0])
mpg_df
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
      <th>Unnamed: 0</th>
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>class</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>1</td>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>18</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <td>1</td>
      <td>2</td>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <td>2</td>
      <td>3</td>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>20</td>
      <td>31</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <td>3</td>
      <td>4</td>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(av)</td>
      <td>f</td>
      <td>21</td>
      <td>30</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <td>4</td>
      <td>5</td>
      <td>audi</td>
      <td>a4</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
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
      <td>229</td>
      <td>230</td>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>19</td>
      <td>28</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <td>230</td>
      <td>231</td>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <td>231</td>
      <td>232</td>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <td>232</td>
      <td>233</td>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>18</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <td>233</td>
      <td>234</td>
      <td>volkswagen</td>
      <td>passat</td>
      <td>3.6</td>
      <td>2008</td>
      <td>6</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>17</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
  </tbody>
</table>
<p>234 rows × 12 columns</p>
</div>



문제

Q1)자동차 배기량에 따라 고속도로 연비가 다른지 알아보려고 한다. displ(배기량)이 4 이하인 자동차와 5이상인 자동차 중 어떤 자동차의 hwy(고속도로 연비)가 평균적으로 더 높은지 알아보아라


```python
# 정답(1)
배기량_4이하 = mpg_df.query('displ <=4')
배기량_4이하['hwy'].mean()
```




    25.96319018404908




```python
# 정답(1)
배기량_5이상 = mpg_df.query('displ >=5')
배기량_5이상['hwy'].mean()
```




    18.07894736842105




```python
자동차별_평균_displ = mpg_df.groupby(mpg_df['model']).mean()
자동차별_평균_displ
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
      <th>Unnamed: 0</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>cty</th>
      <th>hwy</th>
    </tr>
    <tr>
      <th>model</th>
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
      <td>4runner 4wd</td>
      <td>176.5</td>
      <td>3.483333</td>
      <td>2002.000000</td>
      <td>5.666667</td>
      <td>15.166667</td>
      <td>18.833333</td>
    </tr>
    <tr>
      <td>a4</td>
      <td>4.0</td>
      <td>2.328571</td>
      <td>2002.857143</td>
      <td>4.857143</td>
      <td>18.857143</td>
      <td>28.285714</td>
    </tr>
    <tr>
      <td>a4 quattro</td>
      <td>11.5</td>
      <td>2.425000</td>
      <td>2003.500000</td>
      <td>5.000000</td>
      <td>17.125000</td>
      <td>25.750000</td>
    </tr>
    <tr>
      <td>a6 quattro</td>
      <td>17.0</td>
      <td>3.366667</td>
      <td>2005.000000</td>
      <td>6.666667</td>
      <td>16.000000</td>
      <td>24.000000</td>
    </tr>
    <tr>
      <td>altima</td>
      <td>144.5</td>
      <td>2.800000</td>
      <td>2005.000000</td>
      <td>4.666667</td>
      <td>20.666667</td>
      <td>28.666667</td>
    </tr>
    <tr>
      <td>c1500 suburban 2wd</td>
      <td>21.0</td>
      <td>5.520000</td>
      <td>2006.200000</td>
      <td>8.000000</td>
      <td>12.800000</td>
      <td>17.800000</td>
    </tr>
    <tr>
      <td>camry</td>
      <td>183.0</td>
      <td>2.671429</td>
      <td>2002.857143</td>
      <td>4.857143</td>
      <td>19.857143</td>
      <td>28.285714</td>
    </tr>
    <tr>
      <td>camry solara</td>
      <td>190.0</td>
      <td>2.642857</td>
      <td>2002.857143</td>
      <td>4.857143</td>
      <td>19.857143</td>
      <td>28.142857</td>
    </tr>
    <tr>
      <td>caravan 2wd</td>
      <td>43.0</td>
      <td>3.390909</td>
      <td>2003.090909</td>
      <td>5.818182</td>
      <td>15.818182</td>
      <td>22.363636</td>
    </tr>
    <tr>
      <td>civic</td>
      <td>104.0</td>
      <td>1.711111</td>
      <td>2003.000000</td>
      <td>4.000000</td>
      <td>24.444444</td>
      <td>32.555556</td>
    </tr>
    <tr>
      <td>corolla</td>
      <td>196.0</td>
      <td>1.800000</td>
      <td>2002.600000</td>
      <td>4.000000</td>
      <td>25.600000</td>
      <td>34.000000</td>
    </tr>
    <tr>
      <td>corvette</td>
      <td>26.0</td>
      <td>6.160000</td>
      <td>2004.400000</td>
      <td>8.000000</td>
      <td>15.400000</td>
      <td>24.800000</td>
    </tr>
    <tr>
      <td>dakota pickup 4wd</td>
      <td>53.0</td>
      <td>4.411111</td>
      <td>2004.000000</td>
      <td>7.111111</td>
      <td>12.777778</td>
      <td>17.000000</td>
    </tr>
    <tr>
      <td>durango 4wd</td>
      <td>61.0</td>
      <td>4.971429</td>
      <td>2004.142857</td>
      <td>7.714286</td>
      <td>11.857143</td>
      <td>16.000000</td>
    </tr>
    <tr>
      <td>expedition 2wd</td>
      <td>76.0</td>
      <td>5.133333</td>
      <td>2002.000000</td>
      <td>8.000000</td>
      <td>11.333333</td>
      <td>17.333333</td>
    </tr>
    <tr>
      <td>explorer 4wd</td>
      <td>80.5</td>
      <td>4.266667</td>
      <td>2002.000000</td>
      <td>6.666667</td>
      <td>13.666667</td>
      <td>18.000000</td>
    </tr>
    <tr>
      <td>f150 pickup 4wd</td>
      <td>87.0</td>
      <td>4.714286</td>
      <td>2001.571429</td>
      <td>7.428571</td>
      <td>13.000000</td>
      <td>16.428571</td>
    </tr>
    <tr>
      <td>forester awd</td>
      <td>162.5</td>
      <td>2.500000</td>
      <td>2005.000000</td>
      <td>4.000000</td>
      <td>18.833333</td>
      <td>25.000000</td>
    </tr>
    <tr>
      <td>grand cherokee 4wd</td>
      <td>126.5</td>
      <td>4.575000</td>
      <td>2005.750000</td>
      <td>7.250000</td>
      <td>13.500000</td>
      <td>17.625000</td>
    </tr>
    <tr>
      <td>grand prix</td>
      <td>157.0</td>
      <td>3.960000</td>
      <td>2002.600000</td>
      <td>6.400000</td>
      <td>17.000000</td>
      <td>26.400000</td>
    </tr>
    <tr>
      <td>gti</td>
      <td>210.0</td>
      <td>2.160000</td>
      <td>2002.600000</td>
      <td>4.400000</td>
      <td>20.000000</td>
      <td>27.400000</td>
    </tr>
    <tr>
      <td>impreza awd</td>
      <td>169.5</td>
      <td>2.425000</td>
      <td>2003.500000</td>
      <td>4.000000</td>
      <td>19.625000</td>
      <td>26.000000</td>
    </tr>
    <tr>
      <td>jetta</td>
      <td>217.0</td>
      <td>2.277778</td>
      <td>2003.000000</td>
      <td>4.666667</td>
      <td>21.222222</td>
      <td>29.111111</td>
    </tr>
    <tr>
      <td>k1500 tahoe 4wd</td>
      <td>30.5</td>
      <td>5.700000</td>
      <td>2003.500000</td>
      <td>8.000000</td>
      <td>12.500000</td>
      <td>16.250000</td>
    </tr>
    <tr>
      <td>land cruiser wagon 4wd</td>
      <td>199.5</td>
      <td>5.200000</td>
      <td>2003.500000</td>
      <td>8.000000</td>
      <td>12.000000</td>
      <td>16.500000</td>
    </tr>
    <tr>
      <td>malibu</td>
      <td>35.0</td>
      <td>3.000000</td>
      <td>2004.400000</td>
      <td>5.200000</td>
      <td>18.800000</td>
      <td>27.600000</td>
    </tr>
    <tr>
      <td>maxima</td>
      <td>149.0</td>
      <td>3.166667</td>
      <td>2002.000000</td>
      <td>6.000000</td>
      <td>18.666667</td>
      <td>25.333333</td>
    </tr>
    <tr>
      <td>mountaineer 4wd</td>
      <td>139.5</td>
      <td>4.400000</td>
      <td>2003.500000</td>
      <td>7.000000</td>
      <td>13.250000</td>
      <td>18.000000</td>
    </tr>
    <tr>
      <td>mustang</td>
      <td>95.0</td>
      <td>4.377778</td>
      <td>2004.000000</td>
      <td>7.111111</td>
      <td>15.888889</td>
      <td>23.222222</td>
    </tr>
    <tr>
      <td>navigator 2wd</td>
      <td>136.0</td>
      <td>5.400000</td>
      <td>2002.000000</td>
      <td>8.000000</td>
      <td>11.333333</td>
      <td>17.000000</td>
    </tr>
    <tr>
      <td>new beetle</td>
      <td>224.5</td>
      <td>2.133333</td>
      <td>2002.000000</td>
      <td>4.333333</td>
      <td>24.000000</td>
      <td>32.833333</td>
    </tr>
    <tr>
      <td>passat</td>
      <td>231.0</td>
      <td>2.400000</td>
      <td>2002.857143</td>
      <td>4.857143</td>
      <td>18.571429</td>
      <td>27.571429</td>
    </tr>
    <tr>
      <td>pathfinder 4wd</td>
      <td>152.5</td>
      <td>4.050000</td>
      <td>2003.500000</td>
      <td>6.500000</td>
      <td>13.750000</td>
      <td>18.000000</td>
    </tr>
    <tr>
      <td>ram 1500 pickup 4wd</td>
      <td>69.5</td>
      <td>5.020000</td>
      <td>2005.300000</td>
      <td>8.000000</td>
      <td>11.400000</td>
      <td>15.300000</td>
    </tr>
    <tr>
      <td>range rover</td>
      <td>132.5</td>
      <td>4.300000</td>
      <td>2003.500000</td>
      <td>8.000000</td>
      <td>11.500000</td>
      <td>16.500000</td>
    </tr>
    <tr>
      <td>sonata</td>
      <td>112.0</td>
      <td>2.557143</td>
      <td>2002.857143</td>
      <td>4.857143</td>
      <td>19.000000</td>
      <td>27.714286</td>
    </tr>
    <tr>
      <td>tiburon</td>
      <td>119.0</td>
      <td>2.300000</td>
      <td>2005.428571</td>
      <td>4.857143</td>
      <td>18.285714</td>
      <td>26.000000</td>
    </tr>
    <tr>
      <td>toyota tacoma 4wd</td>
      <td>204.0</td>
      <td>3.271429</td>
      <td>2002.857143</td>
      <td>5.142857</td>
      <td>15.571429</td>
      <td>19.428571</td>
    </tr>
  </tbody>
</table>
</div>




```python
result = 자동차별_평균_displ.groupby(자동차별_평균_displ['hwy']).max()
```


```python
result
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
      <th>Unnamed: 0</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>cty</th>
    </tr>
    <tr>
      <th>hwy</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>15.300000</td>
      <td>69.5</td>
      <td>5.020000</td>
      <td>2005.300000</td>
      <td>8.000000</td>
      <td>11.400000</td>
    </tr>
    <tr>
      <td>16.000000</td>
      <td>61.0</td>
      <td>4.971429</td>
      <td>2004.142857</td>
      <td>7.714286</td>
      <td>11.857143</td>
    </tr>
    <tr>
      <td>16.250000</td>
      <td>30.5</td>
      <td>5.700000</td>
      <td>2003.500000</td>
      <td>8.000000</td>
      <td>12.500000</td>
    </tr>
    <tr>
      <td>16.428571</td>
      <td>87.0</td>
      <td>4.714286</td>
      <td>2001.571429</td>
      <td>7.428571</td>
      <td>13.000000</td>
    </tr>
    <tr>
      <td>16.500000</td>
      <td>199.5</td>
      <td>5.200000</td>
      <td>2003.500000</td>
      <td>8.000000</td>
      <td>12.000000</td>
    </tr>
    <tr>
      <td>17.000000</td>
      <td>136.0</td>
      <td>5.400000</td>
      <td>2004.000000</td>
      <td>8.000000</td>
      <td>12.777778</td>
    </tr>
    <tr>
      <td>17.333333</td>
      <td>76.0</td>
      <td>5.133333</td>
      <td>2002.000000</td>
      <td>8.000000</td>
      <td>11.333333</td>
    </tr>
    <tr>
      <td>17.625000</td>
      <td>126.5</td>
      <td>4.575000</td>
      <td>2005.750000</td>
      <td>7.250000</td>
      <td>13.500000</td>
    </tr>
    <tr>
      <td>17.800000</td>
      <td>21.0</td>
      <td>5.520000</td>
      <td>2006.200000</td>
      <td>8.000000</td>
      <td>12.800000</td>
    </tr>
    <tr>
      <td>18.000000</td>
      <td>152.5</td>
      <td>4.400000</td>
      <td>2003.500000</td>
      <td>7.000000</td>
      <td>13.750000</td>
    </tr>
    <tr>
      <td>18.833333</td>
      <td>176.5</td>
      <td>3.483333</td>
      <td>2002.000000</td>
      <td>5.666667</td>
      <td>15.166667</td>
    </tr>
    <tr>
      <td>19.428571</td>
      <td>204.0</td>
      <td>3.271429</td>
      <td>2002.857143</td>
      <td>5.142857</td>
      <td>15.571429</td>
    </tr>
    <tr>
      <td>22.363636</td>
      <td>43.0</td>
      <td>3.390909</td>
      <td>2003.090909</td>
      <td>5.818182</td>
      <td>15.818182</td>
    </tr>
    <tr>
      <td>23.222222</td>
      <td>95.0</td>
      <td>4.377778</td>
      <td>2004.000000</td>
      <td>7.111111</td>
      <td>15.888889</td>
    </tr>
    <tr>
      <td>24.000000</td>
      <td>17.0</td>
      <td>3.366667</td>
      <td>2005.000000</td>
      <td>6.666667</td>
      <td>16.000000</td>
    </tr>
    <tr>
      <td>24.800000</td>
      <td>26.0</td>
      <td>6.160000</td>
      <td>2004.400000</td>
      <td>8.000000</td>
      <td>15.400000</td>
    </tr>
    <tr>
      <td>25.000000</td>
      <td>162.5</td>
      <td>2.500000</td>
      <td>2005.000000</td>
      <td>4.000000</td>
      <td>18.833333</td>
    </tr>
    <tr>
      <td>25.333333</td>
      <td>149.0</td>
      <td>3.166667</td>
      <td>2002.000000</td>
      <td>6.000000</td>
      <td>18.666667</td>
    </tr>
    <tr>
      <td>25.750000</td>
      <td>11.5</td>
      <td>2.425000</td>
      <td>2003.500000</td>
      <td>5.000000</td>
      <td>17.125000</td>
    </tr>
    <tr>
      <td>26.000000</td>
      <td>169.5</td>
      <td>2.425000</td>
      <td>2005.428571</td>
      <td>4.857143</td>
      <td>19.625000</td>
    </tr>
    <tr>
      <td>26.400000</td>
      <td>157.0</td>
      <td>3.960000</td>
      <td>2002.600000</td>
      <td>6.400000</td>
      <td>17.000000</td>
    </tr>
    <tr>
      <td>27.400000</td>
      <td>210.0</td>
      <td>2.160000</td>
      <td>2002.600000</td>
      <td>4.400000</td>
      <td>20.000000</td>
    </tr>
    <tr>
      <td>27.571429</td>
      <td>231.0</td>
      <td>2.400000</td>
      <td>2002.857143</td>
      <td>4.857143</td>
      <td>18.571429</td>
    </tr>
    <tr>
      <td>27.600000</td>
      <td>35.0</td>
      <td>3.000000</td>
      <td>2004.400000</td>
      <td>5.200000</td>
      <td>18.800000</td>
    </tr>
    <tr>
      <td>27.714286</td>
      <td>112.0</td>
      <td>2.557143</td>
      <td>2002.857143</td>
      <td>4.857143</td>
      <td>19.000000</td>
    </tr>
    <tr>
      <td>28.142857</td>
      <td>190.0</td>
      <td>2.642857</td>
      <td>2002.857143</td>
      <td>4.857143</td>
      <td>19.857143</td>
    </tr>
    <tr>
      <td>28.285714</td>
      <td>183.0</td>
      <td>2.671429</td>
      <td>2002.857143</td>
      <td>4.857143</td>
      <td>19.857143</td>
    </tr>
    <tr>
      <td>28.666667</td>
      <td>144.5</td>
      <td>2.800000</td>
      <td>2005.000000</td>
      <td>4.666667</td>
      <td>20.666667</td>
    </tr>
    <tr>
      <td>29.111111</td>
      <td>217.0</td>
      <td>2.277778</td>
      <td>2003.000000</td>
      <td>4.666667</td>
      <td>21.222222</td>
    </tr>
    <tr>
      <td>32.555556</td>
      <td>104.0</td>
      <td>1.711111</td>
      <td>2003.000000</td>
      <td>4.000000</td>
      <td>24.444444</td>
    </tr>
    <tr>
      <td>32.833333</td>
      <td>224.5</td>
      <td>2.133333</td>
      <td>2002.000000</td>
      <td>4.333333</td>
      <td>24.000000</td>
    </tr>
    <tr>
      <td>34.000000</td>
      <td>196.0</td>
      <td>1.800000</td>
      <td>2002.600000</td>
      <td>4.000000</td>
      <td>25.600000</td>
    </tr>
  </tbody>
</table>
</div>



Q2) 자동차 제조회사에 따라 도시 연비가 다른지 알아보려고 한다. "audi"와 "toyota"중 어느 manufacturer(자동차 제조 회사)의 cty(도시연비)가 평균적으로 더 높은지 알아보아라


```python
# 정답(2)
아우디 = mpg_df.query("manufacturer == 'audi'")
아우디['cty'].mean()
```




    17.61111111111111




```python
토요타 = mpg_df.query("manufacturer == 'toyota'")
토요타['cty'].mean()
```




    18.529411764705884




```python
혼다 = mpg_df.query("manufacturer == 'honda'")
혼다['cty'].mean()
```




    24.444444444444443




```python

```


```python

```

Q3)"chevrolet", "ford", "honda" 자동차의 고속도로 연비 평균을 알아보려고 한다. 이 회사들의 데이터를 추출한 후 hwy 전체 평균을 구해 보세요


```python
#정담(3)
추출데이터 = mpg_df.query("manufacturer == 'chevelot' or manufacturer == 'honda' or manufacturer == 'ford'")
추출데이터['hwy'].mean()
```




    22.852941176470587




```python
# 집계 대상을 추출
filter_df1 = mpg_df.filter(['manufacturer','cty'])
filter_df1
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
      <th>manufacturer</th>
      <th>cty</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>audi</td>
      <td>18</td>
    </tr>
    <tr>
      <td>1</td>
      <td>audi</td>
      <td>21</td>
    </tr>
    <tr>
      <td>2</td>
      <td>audi</td>
      <td>20</td>
    </tr>
    <tr>
      <td>3</td>
      <td>audi</td>
      <td>21</td>
    </tr>
    <tr>
      <td>4</td>
      <td>audi</td>
      <td>16</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>229</td>
      <td>volkswagen</td>
      <td>19</td>
    </tr>
    <tr>
      <td>230</td>
      <td>volkswagen</td>
      <td>21</td>
    </tr>
    <tr>
      <td>231</td>
      <td>volkswagen</td>
      <td>16</td>
    </tr>
    <tr>
      <td>232</td>
      <td>volkswagen</td>
      <td>18</td>
    </tr>
    <tr>
      <td>233</td>
      <td>volkswagen</td>
      <td>17</td>
    </tr>
  </tbody>
</table>
<p>234 rows × 2 columns</p>
</div>




```python
평균 = filter_df1.mean(axis=1)

결과치1 = filter_df1.copy()
결과치1['평균'] = 평균
결과치1
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
      <th>manufacturer</th>
      <th>cty</th>
      <th>평균</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>audi</td>
      <td>18</td>
      <td>18.0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>audi</td>
      <td>21</td>
      <td>21.0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>audi</td>
      <td>20</td>
      <td>20.0</td>
    </tr>
    <tr>
      <td>3</td>
      <td>audi</td>
      <td>21</td>
      <td>21.0</td>
    </tr>
    <tr>
      <td>4</td>
      <td>audi</td>
      <td>16</td>
      <td>16.0</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>229</td>
      <td>volkswagen</td>
      <td>19</td>
      <td>19.0</td>
    </tr>
    <tr>
      <td>230</td>
      <td>volkswagen</td>
      <td>21</td>
      <td>21.0</td>
    </tr>
    <tr>
      <td>231</td>
      <td>volkswagen</td>
      <td>16</td>
      <td>16.0</td>
    </tr>
    <tr>
      <td>232</td>
      <td>volkswagen</td>
      <td>18</td>
      <td>18.0</td>
    </tr>
    <tr>
      <td>233</td>
      <td>volkswagen</td>
      <td>17</td>
      <td>17.0</td>
    </tr>
  </tbody>
</table>
<p>234 rows × 3 columns</p>
</div>




```python
결과치2 = 결과치1.filter(['manufacturer' == 'chevrolet' or 'manufacturer' == 'toyota' or 'manufacturer' == 'honda'])
결과치2
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
    </tr>
    <tr>
      <td>1</td>
    </tr>
    <tr>
      <td>2</td>
    </tr>
    <tr>
      <td>3</td>
    </tr>
    <tr>
      <td>4</td>
    </tr>
    <tr>
      <td>...</td>
    </tr>
    <tr>
      <td>229</td>
    </tr>
    <tr>
      <td>230</td>
    </tr>
    <tr>
      <td>231</td>
    </tr>
    <tr>
      <td>232</td>
    </tr>
    <tr>
      <td>233</td>
    </tr>
  </tbody>
</table>
<p>234 rows × 0 columns</p>
</div>



문제 4)
mpg데이터의 fl변수는 자동차에 사용하는 연료(fuel)를 의미한다(각 연료 이름의 첫 글자만 저장)

mpg데이터에는 연료 종류를 나타낸 fl변수는 있지만 연료 가격을 나타낸 변수는 없다

다음의 가격정보를 이용해 mpg데이터에 price_fl(연료가격) 변수를 추가하라

추가한 결과에서 model,fl,price_fl 추출하여 출력하세요

fl : 연료 종류
    값:의미-가격
> c:CNG/가스 - 2.35<br>
> d:디젤/diesel - 2.38<br>
> e:에탄올 혼합연료/ethanol E85 - 2.11<br>
> p:고급휘발유/premium - 2.76<br>
> r:보통휘발유/regular -2.22


```python
# 연료의 종류를 판별하기 위한 조건 나열
conditions = [(mpg_df['fl'] == 'c'), #가스
              (mpg_df['fl'] == 'd'), #디젤
              (mpg_df['fl'] == 'e'), #에탄올 혼합연료
              (mpg_df['fl'] == 'p'), #고급 휘발유
              (mpg_df['fl'] == 'r')] #보통 휘발유

# 연료별 가격 나열
price = [2.35,2.38,2.11,2.76,2.22]
```


```python
# 조건에 따른 가격열 추가하기
mpg_df['price_fl'] = numpy.select(conditions, price)
mpg_df
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
      <th>Unnamed: 0</th>
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>class</th>
      <th>price_fl</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>1</td>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>18</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
      <td>2.76</td>
    </tr>
    <tr>
      <td>1</td>
      <td>2</td>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
      <td>2.76</td>
    </tr>
    <tr>
      <td>2</td>
      <td>3</td>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>20</td>
      <td>31</td>
      <td>p</td>
      <td>compact</td>
      <td>2.76</td>
    </tr>
    <tr>
      <td>3</td>
      <td>4</td>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(av)</td>
      <td>f</td>
      <td>21</td>
      <td>30</td>
      <td>p</td>
      <td>compact</td>
      <td>2.76</td>
    </tr>
    <tr>
      <td>4</td>
      <td>5</td>
      <td>audi</td>
      <td>a4</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>compact</td>
      <td>2.76</td>
    </tr>
    <tr>
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
      <td>229</td>
      <td>230</td>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>19</td>
      <td>28</td>
      <td>p</td>
      <td>midsize</td>
      <td>2.76</td>
    </tr>
    <tr>
      <td>230</td>
      <td>231</td>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>midsize</td>
      <td>2.76</td>
    </tr>
    <tr>
      <td>231</td>
      <td>232</td>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
      <td>2.76</td>
    </tr>
    <tr>
      <td>232</td>
      <td>233</td>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>18</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
      <td>2.76</td>
    </tr>
    <tr>
      <td>233</td>
      <td>234</td>
      <td>volkswagen</td>
      <td>passat</td>
      <td>3.6</td>
      <td>2008</td>
      <td>6</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>17</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
      <td>2.76</td>
    </tr>
  </tbody>
</table>
<p>234 rows × 13 columns</p>
</div>




```python
#모델별 연료가격
mpg_df.filter(['model','fl','price_fl'])
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
      <th>model</th>
      <th>fl</th>
      <th>price_fl</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>a4</td>
      <td>p</td>
      <td>2.76</td>
    </tr>
    <tr>
      <td>1</td>
      <td>a4</td>
      <td>p</td>
      <td>2.76</td>
    </tr>
    <tr>
      <td>2</td>
      <td>a4</td>
      <td>p</td>
      <td>2.76</td>
    </tr>
    <tr>
      <td>3</td>
      <td>a4</td>
      <td>p</td>
      <td>2.76</td>
    </tr>
    <tr>
      <td>4</td>
      <td>a4</td>
      <td>p</td>
      <td>2.76</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>229</td>
      <td>passat</td>
      <td>p</td>
      <td>2.76</td>
    </tr>
    <tr>
      <td>230</td>
      <td>passat</td>
      <td>p</td>
      <td>2.76</td>
    </tr>
    <tr>
      <td>231</td>
      <td>passat</td>
      <td>p</td>
      <td>2.76</td>
    </tr>
    <tr>
      <td>232</td>
      <td>passat</td>
      <td>p</td>
      <td>2.76</td>
    </tr>
    <tr>
      <td>233</td>
      <td>passat</td>
      <td>p</td>
      <td>2.76</td>
    </tr>
  </tbody>
</table>
<p>234 rows × 3 columns</p>
</div>




```python

```
