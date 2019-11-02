---
layout: post
title:  "02. How Can Make DataFrame"
---

# DataFrame 생성
## 필요한 모듈 참조하기
> http://itpaper.co.kr/demo/python/sample.zip 에서 데이터셋 압축파일 다운로드

### ExcelFile 클래스가 의존하는 모듈 설치
> pip install openpyxl<br/>
> pip install xlrd


```python
from pandas import DataFrame    # 데이터프레임 클래스
from pandas import read_csv     # csv파일을 읽어들이기 위한 함수
from pandas import ExcelFile    # Excel 파일을 읽어들이기 위한 클래스
from sample import grade_list   # 리스트 형태의 샘플 데이터
from sample import grade_dic    # 딕셔너리 형태의 샘플 데이터
```


```python
grade_list # 2차원 리스트
```




    [[98, None, 88, 64],
     [88, 90, 62, 72],
     [92, 70, None, None],
     [63, 60, 31, 70],
     [120, 50, None, 88]]




```python
grade_dic # 리스트를 원소로 갖는 딕셔너리
```




    {'국어': [98, 88, 92, 63, 120],
     '영어': [None, 90, 70, 60, 50],
     '수학': [88, 62, None, 31, None],
     '과학': [64, 72, None, 70, 88]}



-----------------------------
## #01. 데이터프레임 만들기
### 2차원 리스트를 통한 생성
행과 열을 갖는 형태로 생성됨


```python
df = DataFrame(grade_list)
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
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>98</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>64.0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>88</td>
      <td>90.0</td>
      <td>62.0</td>
      <td>72.0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>92</td>
      <td>70.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>3</td>
      <td>63</td>
      <td>60.0</td>
      <td>31.0</td>
      <td>70.0</td>
    </tr>
    <tr>
      <td>4</td>
      <td>120</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>88.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 컬럼(열)이름을 지정하여 새로 생성 -> 컬럼의 이름을 갖고 있는 리스트를 지정한다
c_names = ['국어','영어','수학','과학']
df = DataFrame(grade_list, columns = c_names)
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
      <th>국어</th>
      <th>영어</th>
      <th>수학</th>
      <th>과학</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>98</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>64.0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>88</td>
      <td>90.0</td>
      <td>62.0</td>
      <td>72.0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>92</td>
      <td>70.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>3</td>
      <td>63</td>
      <td>60.0</td>
      <td>31.0</td>
      <td>70.0</td>
    </tr>
    <tr>
      <td>4</td>
      <td>120</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>88.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 인덱스(행)이름을 지정하여 새로 생성 -> 인덱스의 이름을 갖고 있는 리스트를 지정한다
i_names = ['철수','영희','민철','수현','호영']
df = DataFrame(grade_list, index=i_names)
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
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>철수</td>
      <td>98</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>64.0</td>
    </tr>
    <tr>
      <td>영희</td>
      <td>88</td>
      <td>90.0</td>
      <td>62.0</td>
      <td>72.0</td>
    </tr>
    <tr>
      <td>민철</td>
      <td>92</td>
      <td>70.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>수현</td>
      <td>63</td>
      <td>60.0</td>
      <td>31.0</td>
      <td>70.0</td>
    </tr>
    <tr>
      <td>호영</td>
      <td>120</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>88.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 인덱스와 컬럼이름 모두 지정하기
df = DataFrame(grade_list, index=i_names, columns=c_names)
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
      <th>국어</th>
      <th>영어</th>
      <th>수학</th>
      <th>과학</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>철수</td>
      <td>98</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>64.0</td>
    </tr>
    <tr>
      <td>영희</td>
      <td>88</td>
      <td>90.0</td>
      <td>62.0</td>
      <td>72.0</td>
    </tr>
    <tr>
      <td>민철</td>
      <td>92</td>
      <td>70.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>수현</td>
      <td>63</td>
      <td>60.0</td>
      <td>31.0</td>
      <td>70.0</td>
    </tr>
    <tr>
      <td>호영</td>
      <td>120</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>88.0</td>
    </tr>
  </tbody>
</table>
</div>



### 딕셔너리를 통한 데이터 프레임 생성
딕셔너리의 Key값이 데이터프레임의 컬럼이름이 된다. 리스트보다 딕셔너리가 간편함

열 -> Column,변수

행 -> index,row


```python
df = DataFrame(grade_dic)
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
      <th>국어</th>
      <th>영어</th>
      <th>수학</th>
      <th>과학</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>98</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>64.0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>88</td>
      <td>90.0</td>
      <td>62.0</td>
      <td>72.0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>92</td>
      <td>70.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>3</td>
      <td>63</td>
      <td>60.0</td>
      <td>31.0</td>
      <td>70.0</td>
    </tr>
    <tr>
      <td>4</td>
      <td>120</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>88.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 인덱스 이름을 지정한 데이터프레임 만들기
df = DataFrame(grade_dic, index=['철수','영희','민철','수현','호영'])
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
      <th>국어</th>
      <th>영어</th>
      <th>수학</th>
      <th>과학</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>철수</td>
      <td>98</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>64.0</td>
    </tr>
    <tr>
      <td>영희</td>
      <td>88</td>
      <td>90.0</td>
      <td>62.0</td>
      <td>72.0</td>
    </tr>
    <tr>
      <td>민철</td>
      <td>92</td>
      <td>70.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>수현</td>
      <td>63</td>
      <td>60.0</td>
      <td>31.0</td>
      <td>70.0</td>
    </tr>
    <tr>
      <td>호영</td>
      <td>120</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>88.0</td>
    </tr>
  </tbody>
</table>
</div>



-----------------------------------
## #02. 외부 파일 읽어오기
### csv파일 읽기


```python
df = read_csv('http://itpaper.co.kr/demo/python/grade.csv', encoding='euc-kr')
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
      <th>이름</th>
      <th>국어</th>
      <th>영어</th>
      <th>수학</th>
      <th>과학</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>학생1</td>
      <td>98.0</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>64.0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>학생2</td>
      <td>88.0</td>
      <td>90.0</td>
      <td>62.0</td>
      <td>72.0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>학생3</td>
      <td>92.0</td>
      <td>70.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>3</td>
      <td>학생4</td>
      <td>63.0</td>
      <td>60.0</td>
      <td>31.0</td>
      <td>70.0</td>
    </tr>
    <tr>
      <td>4</td>
      <td>학생5</td>
      <td>100.0</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>88.0</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>9995</td>
      <td>학생9996</td>
      <td>63.0</td>
      <td>60.0</td>
      <td>55.0</td>
      <td>70.0</td>
    </tr>
    <tr>
      <td>9996</td>
      <td>학생9997</td>
      <td>21.0</td>
      <td>50.0</td>
      <td>55.0</td>
      <td>88.0</td>
    </tr>
    <tr>
      <td>9997</td>
      <td>학생9998</td>
      <td>98.0</td>
      <td>90.0</td>
      <td>88.0</td>
      <td>64.0</td>
    </tr>
    <tr>
      <td>9998</td>
      <td>학생9999</td>
      <td>88.0</td>
      <td>90.0</td>
      <td>62.0</td>
      <td>72.0</td>
    </tr>
    <tr>
      <td>9999</td>
      <td>학생10000</td>
      <td>92.0</td>
      <td>70.0</td>
      <td>75.0</td>
      <td>85.0</td>
    </tr>
  </tbody>
</table>
<p>10000 rows × 5 columns</p>
</div>



### 엑셀파일 읽기


```python
# 엑셀파일을 객체 형태로 가져온다
xls = ExcelFile('http://itpaper.co.kr/demo/python/children_house.xlsx')
```


```python
# 엑셀파일의 sheet 이름에 대한 리스트
xls.sheet_names
```




    ['데이터', '메타정보']




```python
# 가져오고자 하는 sheet 이름을 지정하여 데이터프레임으로 변환
df = xls.parse(xls.sheet_names[0])
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
      <th>지역</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>전국(계)</td>
      <td>43742</td>
      <td>42517</td>
      <td>41084</td>
    </tr>
    <tr>
      <td>1</td>
      <td>서울</td>
      <td>6787</td>
      <td>6598</td>
      <td>6368</td>
    </tr>
    <tr>
      <td>2</td>
      <td>부산</td>
      <td>1957</td>
      <td>1971</td>
      <td>1937</td>
    </tr>
    <tr>
      <td>3</td>
      <td>대구</td>
      <td>1588</td>
      <td>1539</td>
      <td>1483</td>
    </tr>
    <tr>
      <td>4</td>
      <td>인천</td>
      <td>2308</td>
      <td>2278</td>
      <td>2231</td>
    </tr>
    <tr>
      <td>5</td>
      <td>광주</td>
      <td>1260</td>
      <td>1264</td>
      <td>1238</td>
    </tr>
    <tr>
      <td>6</td>
      <td>대전</td>
      <td>1698</td>
      <td>1669</td>
      <td>1584</td>
    </tr>
    <tr>
      <td>7</td>
      <td>울산</td>
      <td>946</td>
      <td>934</td>
      <td>895</td>
    </tr>
    <tr>
      <td>8</td>
      <td>세종</td>
      <td>160</td>
      <td>216</td>
      <td>250</td>
    </tr>
    <tr>
      <td>9</td>
      <td>경기</td>
      <td>13259</td>
      <td>12689</td>
      <td>12120</td>
    </tr>
    <tr>
      <td>10</td>
      <td>강원</td>
      <td>1257</td>
      <td>1227</td>
      <td>1180</td>
    </tr>
    <tr>
      <td>11</td>
      <td>충북</td>
      <td>1229</td>
      <td>1230</td>
      <td>1208</td>
    </tr>
    <tr>
      <td>12</td>
      <td>충남</td>
      <td>2053</td>
      <td>1988</td>
      <td>1974</td>
    </tr>
    <tr>
      <td>13</td>
      <td>전북</td>
      <td>1654</td>
      <td>1623</td>
      <td>1562</td>
    </tr>
    <tr>
      <td>14</td>
      <td>전남</td>
      <td>1242</td>
      <td>1238</td>
      <td>1251</td>
    </tr>
    <tr>
      <td>15</td>
      <td>경북</td>
      <td>2212</td>
      <td>2130</td>
      <td>2102</td>
    </tr>
    <tr>
      <td>16</td>
      <td>경남</td>
      <td>3533</td>
      <td>3349</td>
      <td>3158</td>
    </tr>
    <tr>
      <td>17</td>
      <td>제주</td>
      <td>599</td>
      <td>574</td>
      <td>543</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
