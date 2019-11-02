---
layout: post
title:  "05. Data Pre-Processing(3)"
---

# 데이터 전처리(3) - 집계함수 활용
- 모듈 참조 및 샘플데이터 가져오기


```python
import numpy
from pandas import DataFrame
from sample import grade_dic
```


```python
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



---------------------------------------
## #01. 집계함수 사용

데이터프레임에서 집계함수를 사용하면 열단위(세로방향)에 대해 수행된다

전체 열에 대한 집계


```python
# 과목별 총점
df.sum()
```




    국어    461.0
    영어    270.0
    수학    181.0
    과학    294.0
    dtype: float64




```python
# 과목별 평균
df.mean()
```




    국어    92.200000
    영어    67.500000
    수학    60.333333
    과학    73.500000
    dtype: float64



특정 열에 대한 집계


```python
# 국어 과목에서 최고점수
df['국어'].max()
```




    120



행 단위 집계

집계함수에 axis = 1 파라미터를 지정한다

- axis=0:y축, 열단위, 기본값
- axis=1:x축, 행단위, 필요한 경우 명시


```python
#학생별 총점
df.sum(axis=1)
```




    철수    250.0
    영희    312.0
    민철    162.0
    수현    224.0
    호영    258.0
    dtype: float64




```python
#학생별 평균
df.mean(axis=1)
```




    철수    83.333333
    영희    78.000000
    민철    81.000000
    수현    56.000000
    호영    86.000000
    dtype: float64




```python
#특정행에 대한 집계
df.loc['영희'].mean()
```




    78.0




```python
#특정행에 대한 집계
df.loc['철수'].max()
```




    98.0



행단위 집계 결과를 새로운 열로 추가하기


```python
# 학생별 총점과 평균 산출
총점 = df.sum(axis=1)
평균 = df.mean(axis=1)
```


```python
#데이터프레임의 복사본을 생성한 후 산출한 집계 결과를 새로운 열로 추가
성적표 = df.copy()
성적표['총점'] = 총점
성적표['평균'] = 평균
성적표
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
      <th>총점</th>
      <th>평균</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>철수</td>
      <td>98</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>64.0</td>
      <td>250.0</td>
      <td>83.333333</td>
    </tr>
    <tr>
      <td>영희</td>
      <td>88</td>
      <td>90.0</td>
      <td>62.0</td>
      <td>72.0</td>
      <td>312.0</td>
      <td>78.000000</td>
    </tr>
    <tr>
      <td>민철</td>
      <td>92</td>
      <td>70.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>162.0</td>
      <td>81.000000</td>
    </tr>
    <tr>
      <td>수현</td>
      <td>63</td>
      <td>60.0</td>
      <td>31.0</td>
      <td>70.0</td>
      <td>224.0</td>
      <td>56.000000</td>
    </tr>
    <tr>
      <td>호영</td>
      <td>120</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>258.0</td>
      <td>86.000000</td>
    </tr>
  </tbody>
</table>
</div>



---------------------------------------
## #02. 조건에 따른 선택적인 값을 추가하기

조건이 참인 경우 A, 그렇지 않은 경우 B


```python
성적표['결과'] = numpy.where(성적표['평균'] >=70, '합격','불합격')
성적표
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
      <th>총점</th>
      <th>평균</th>
      <th>결과</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>철수</td>
      <td>98</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>64.0</td>
      <td>250.0</td>
      <td>83.333333</td>
      <td>합격</td>
    </tr>
    <tr>
      <td>영희</td>
      <td>88</td>
      <td>90.0</td>
      <td>62.0</td>
      <td>72.0</td>
      <td>312.0</td>
      <td>78.000000</td>
      <td>합격</td>
    </tr>
    <tr>
      <td>민철</td>
      <td>92</td>
      <td>70.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>162.0</td>
      <td>81.000000</td>
      <td>합격</td>
    </tr>
    <tr>
      <td>수현</td>
      <td>63</td>
      <td>60.0</td>
      <td>31.0</td>
      <td>70.0</td>
      <td>224.0</td>
      <td>56.000000</td>
      <td>불합격</td>
    </tr>
    <tr>
      <td>호영</td>
      <td>120</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>258.0</td>
      <td>86.000000</td>
      <td>합격</td>
    </tr>
  </tbody>
</table>
</div>



여러개의 조건중에서 선택적인 값을 추가하기


```python
# 학점을 부여하기 위한 점수의 구간을 설정하는 조건들을 리스트로 설정
conditions = [(성적표['평균'] >= 90), #A
              (성적표['평균'] >= 80), #B
              (성적표['평균'] >= 70), #C
              (성적표['평균'] < 70)] #D

# 조건에 따라 부여될 학점
grade = ['A','B','C','F']

# 조건에 따른 학점열 추가하기
성적표['학점'] = numpy.select(conditions, grade)
성적표
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
      <th>총점</th>
      <th>평균</th>
      <th>결과</th>
      <th>학점</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>철수</td>
      <td>98</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>64.0</td>
      <td>250.0</td>
      <td>83.333333</td>
      <td>합격</td>
      <td>B</td>
    </tr>
    <tr>
      <td>영희</td>
      <td>88</td>
      <td>90.0</td>
      <td>62.0</td>
      <td>72.0</td>
      <td>312.0</td>
      <td>78.000000</td>
      <td>합격</td>
      <td>C</td>
    </tr>
    <tr>
      <td>민철</td>
      <td>92</td>
      <td>70.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>162.0</td>
      <td>81.000000</td>
      <td>합격</td>
      <td>B</td>
    </tr>
    <tr>
      <td>수현</td>
      <td>63</td>
      <td>60.0</td>
      <td>31.0</td>
      <td>70.0</td>
      <td>224.0</td>
      <td>56.000000</td>
      <td>불합격</td>
      <td>F</td>
    </tr>
    <tr>
      <td>호영</td>
      <td>120</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>258.0</td>
      <td>86.000000</td>
      <td>합격</td>
      <td>B</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
