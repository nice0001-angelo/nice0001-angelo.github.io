---
layout: post
title:  "08. DataFrame Merge"
---

데이터프레임변합하기

필요한 모듈 참조


```python
import pandas as pd
from pandas import DataFrame
```

---------------------------------------
## #01. 행단위 병합

샘플 DataFrame 만들기


```python
df_top = pd.DataFrame({'국어':[90,82],'수학':[81,76]},index=['민철','철수'])
df_top
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
      <th>수학</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>민철</td>
      <td>90</td>
      <td>81</td>
    </tr>
    <tr>
      <td>철수</td>
      <td>82</td>
      <td>76</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_middle = pd.DataFrame({'국어':[70,62],'영어':[77,68]},index=['영민','정수'])
df_middle
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>영민</td>
      <td>70</td>
      <td>77</td>
    </tr>
    <tr>
      <td>정수</td>
      <td>62</td>
      <td>68</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_bottom = pd.DataFrame({'영어':[70,88],'과학':[81,76]},index=['민철','태영'])
df_bottom
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
      <th>영어</th>
      <th>과학</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>민철</td>
      <td>70</td>
      <td>81</td>
    </tr>
    <tr>
      <td>태영</td>
      <td>88</td>
      <td>76</td>
    </tr>
  </tbody>
</table>
</div>



A에 B를 이어 붙이기

- 단순히 헤로로 병합만 수행한다
- 데이터프레임간에 컬럼이 다르더라도 존재하지 않는 컬럼은 빈값(결측치)로 채워 넣는다


```python
df_a=df_top.append([df_middle,df_bottom],sort=False)
df_a
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
      <th>수학</th>
      <th>영어</th>
      <th>과학</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>민철</td>
      <td>90.0</td>
      <td>81.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>철수</td>
      <td>82.0</td>
      <td>76.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>영민</td>
      <td>70.0</td>
      <td>NaN</td>
      <td>77.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>정수</td>
      <td>62.0</td>
      <td>NaN</td>
      <td>68.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>민철</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>70.0</td>
      <td>81.0</td>
    </tr>
    <tr>
      <td>태영</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>76.0</td>
    </tr>
  </tbody>
</table>
</div>



A,B,C를 병합하기

append() 함수와 동일한 결과

- 단순히 세로 방향으로 덧붙이는 개념이므로 인덱스가 중복되는 경우도 발생한다
- sort파라미터를 생략하거나 True로 지정한 경우 컬럼 순서가 이름순으로 정렬된다
-(중요)병합되는 DataFrame간에 컬럼이 서로 다르다면 sort=False파라미터 필수 지정


```python
df_b=pd.concat([df_top,df_middle,df_bottom],sort=False)
df_b
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
      <th>수학</th>
      <th>영어</th>
      <th>과학</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>민철</td>
      <td>90.0</td>
      <td>81.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>철수</td>
      <td>82.0</td>
      <td>76.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>영민</td>
      <td>70.0</td>
      <td>NaN</td>
      <td>77.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>정수</td>
      <td>62.0</td>
      <td>NaN</td>
      <td>68.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>민철</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>70.0</td>
      <td>81.0</td>
    </tr>
    <tr>
      <td>태영</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>76.0</td>
    </tr>
  </tbody>
</table>
</div>



---------------------------------------
## #02. 열단위 병합

한번에 두 개의 객체만 병합 가능함

인덱스가 지정되지 않은 샘플 데이터 프레임


```python
df_left=pd.DataFrame({'고객번호':[1001,1002,1003,1004],'이름':['둘리','도우너','또치','길동']})
df_left
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
      <th>고객번호</th>
      <th>이름</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>1001</td>
      <td>둘리</td>
    </tr>
    <tr>
      <td>1</td>
      <td>1002</td>
      <td>도우너</td>
    </tr>
    <tr>
      <td>2</td>
      <td>1003</td>
      <td>또치</td>
    </tr>
    <tr>
      <td>3</td>
      <td>1004</td>
      <td>길동</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_right=pd.DataFrame({'고객번호':[1001,1002,1003,1005],'금액':[10000,20000,15000,5000]})
df_right
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
      <th>고객번호</th>
      <th>금액</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>1001</td>
      <td>10000</td>
    </tr>
    <tr>
      <td>1</td>
      <td>1002</td>
      <td>20000</td>
    </tr>
    <tr>
      <td>2</td>
      <td>1003</td>
      <td>15000</td>
    </tr>
    <tr>
      <td>3</td>
      <td>1005</td>
      <td>5000</td>
    </tr>
  </tbody>
</table>
</div>



두 데이터프레임의 공통 컬럼을 기준으로 병합하기

양쪽 데이터프레임에 모두 존재하는 데이터만 보여준다

> Database의 inner join과 같은 개념


```python
# 병합시 제외되는 항목들
# - df_left의 고객번호 1004번 데이터는 df_right의 고객번호 컬럼과 겹치지 않는다
# - df_right의 고객번호 1005번 데이터는 df_left의 고객번호 컬럼과 겹치지 않는다
pd.merge(df_left,df_right)
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
      <th>고객번호</th>
      <th>이름</th>
      <th>금액</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>1001</td>
      <td>둘리</td>
      <td>10000</td>
    </tr>
    <tr>
      <td>1</td>
      <td>1002</td>
      <td>도우너</td>
      <td>20000</td>
    </tr>
    <tr>
      <td>2</td>
      <td>1003</td>
      <td>또치</td>
      <td>15000</td>
    </tr>
  </tbody>
</table>
</div>



왼쪽 데이터프레임을 기준으로 오른쪽 프레임을 병합하기

how='left' 파라미터는 왼쪽 DataFrame의 모든 데이터를 보여준다

> Database의 left Outer join과 같은 개념


```python
# df_right의 고객번호 1005은 df_left에 존재하지 않기 때문에 병합되지 않는다
pd.merge(df_left,df_right,how='left')
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
      <th>고객번호</th>
      <th>이름</th>
      <th>금액</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>1001</td>
      <td>둘리</td>
      <td>10000.0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>1002</td>
      <td>도우너</td>
      <td>20000.0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>1003</td>
      <td>또치</td>
      <td>15000.0</td>
    </tr>
    <tr>
      <td>3</td>
      <td>1004</td>
      <td>길동</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# df_left의 고객번호 1004은 df_right에 존재하지 않기 때문에 병합되지 않는다
pd.merge(df_left,df_right,how='right')
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
      <th>고객번호</th>
      <th>이름</th>
      <th>금액</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>1001</td>
      <td>둘리</td>
      <td>10000</td>
    </tr>
    <tr>
      <td>1</td>
      <td>1002</td>
      <td>도우너</td>
      <td>20000</td>
    </tr>
    <tr>
      <td>2</td>
      <td>1003</td>
      <td>또치</td>
      <td>15000</td>
    </tr>
    <tr>
      <td>3</td>
      <td>1005</td>
      <td>NaN</td>
      <td>5000</td>
    </tr>
  </tbody>
</table>
</div>



양쪽 DataFrame을 모두 병합하기

how='outer' 파라미터를 추가하면 공통 컬럼의 값이 한쪽에만 있어도 데이터를 보여준다

> Database의 Full Outer join과 같은 개념


```python
pd.merge(df_left,df_right,how='outer')
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
      <th>고객번호</th>
      <th>이름</th>
      <th>금액</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>1001</td>
      <td>둘리</td>
      <td>10000.0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>1002</td>
      <td>도우너</td>
      <td>20000.0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>1003</td>
      <td>또치</td>
      <td>15000.0</td>
    </tr>
    <tr>
      <td>3</td>
      <td>1004</td>
      <td>길동</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>4</td>
      <td>1005</td>
      <td>NaN</td>
      <td>5000.0</td>
    </tr>
  </tbody>
</table>
</div>



중복되는 데이터가 존재하는 경우의 열단위 병합

모든 경우의 수를 따져서 조합을 만들어낸다


```python
df_first=pd.DataFrame({'아이디':['hello','world','python','hello'],'결재금액':[14000,13000,15000,13000]})
df_first
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
      <th>아이디</th>
      <th>결재금액</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>hello</td>
      <td>14000</td>
    </tr>
    <tr>
      <td>1</td>
      <td>world</td>
      <td>13000</td>
    </tr>
    <tr>
      <td>2</td>
      <td>python</td>
      <td>15000</td>
    </tr>
    <tr>
      <td>3</td>
      <td>hello</td>
      <td>13000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_second=pd.DataFrame({'아이디':['hello','python','python','world'],'적립금':[300,500,100,200]})
df_second
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
      <th>아이디</th>
      <th>적립금</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>hello</td>
      <td>300</td>
    </tr>
    <tr>
      <td>1</td>
      <td>python</td>
      <td>500</td>
    </tr>
    <tr>
      <td>2</td>
      <td>python</td>
      <td>100</td>
    </tr>
    <tr>
      <td>3</td>
      <td>world</td>
      <td>200</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.merge(df_first,df_second)
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
      <th>아이디</th>
      <th>결재금액</th>
      <th>적립금</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>hello</td>
      <td>14000</td>
      <td>300</td>
    </tr>
    <tr>
      <td>1</td>
      <td>hello</td>
      <td>13000</td>
      <td>300</td>
    </tr>
    <tr>
      <td>2</td>
      <td>world</td>
      <td>13000</td>
      <td>200</td>
    </tr>
    <tr>
      <td>3</td>
      <td>python</td>
      <td>15000</td>
      <td>500</td>
    </tr>
    <tr>
      <td>4</td>
      <td>python</td>
      <td>15000</td>
      <td>100</td>
    </tr>
  </tbody>
</table>
</div>



공통 컬럼이 두개 이상 존재하는 경우의 병합

두 데이터프레임에서 이름이 같은 열은 모두 키가 된다


```python
df_a=pd.DataFrame({'고객명':['민수','수영'],
                   '데이터':['2000','100000'],
                   '날짜':['2018-01-01','2018-01-01']})
df_a
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
      <th>고객명</th>
      <th>데이터</th>
      <th>날짜</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>민수</td>
      <td>2000</td>
      <td>2018-01-01</td>
    </tr>
    <tr>
      <td>1</td>
      <td>수영</td>
      <td>100000</td>
      <td>2018-01-01</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_b=pd.DataFrame({'고객명':['민수','수영'],'데이터':['21세','20세']})
df_b
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
      <th>고객명</th>
      <th>데이터</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>민수</td>
      <td>21세</td>
    </tr>
    <tr>
      <td>1</td>
      <td>수영</td>
      <td>20세</td>
    </tr>
  </tbody>
</table>
</div>




```python
# '고객'컬럼과 '데이터'컬럼이 동시에 일치하는 데이터를 찾아 병합한다
# df_a의 '데이터'는 금액을 의미하지만 df_b의 '데이터는'나이를 의미하므로 병합되어서는 안된다
# -> 존재하지 않으므로 결과 없음
pd.merge(df_a,df_b)
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
      <th>고객명</th>
      <th>데이터</th>
      <th>날짜</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>



on 파라미터를 사용하여 기준열 지정하기


```python
# 기준 열이 아니면서 이름이 같은 열에는 _x 또는 _y 와 같은 접미사가 붙는다
merge_tmp=pd.merge(df_a,df_b,on=['고객명'])
merge_tmp
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
      <th>고객명</th>
      <th>데이터_x</th>
      <th>날짜</th>
      <th>데이터_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>민수</td>
      <td>2000</td>
      <td>2018-01-01</td>
      <td>21세</td>
    </tr>
    <tr>
      <td>1</td>
      <td>수영</td>
      <td>100000</td>
      <td>2018-01-01</td>
      <td>20세</td>
    </tr>
  </tbody>
</table>
</div>




```python
merge_result=merge_tmp.rename(columns={"데이터_x":"금액","데이터_y":"나이"})
merge_result
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
      <th>고객명</th>
      <th>금액</th>
      <th>날짜</th>
      <th>나이</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>민수</td>
      <td>2000</td>
      <td>2018-01-01</td>
      <td>21세</td>
    </tr>
    <tr>
      <td>1</td>
      <td>수영</td>
      <td>100000</td>
      <td>2018-01-01</td>
      <td>20세</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.merge(df_a,df_b,how='left')
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
      <th>고객명</th>
      <th>데이터</th>
      <th>날짜</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>민수</td>
      <td>2000</td>
      <td>2018-01-01</td>
    </tr>
    <tr>
      <td>1</td>
      <td>수영</td>
      <td>100000</td>
      <td>2018-01-01</td>
    </tr>
  </tbody>
</table>
</div>



공통 컬럼이 존재하지 않는 경우의 병합

lift_on, right_on 파라미터를 사용하여 병합의 기준이 되는 열 이름을 명시해야 한다


```python
국어점수=DataFrame({'이름':['영희','철수'],'국어':[87,91]})
국어점수
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>영희</td>
      <td>87</td>
    </tr>
    <tr>
      <td>1</td>
      <td>철수</td>
      <td>91</td>
    </tr>
  </tbody>
</table>
</div>




```python
영어점수=DataFrame({'성명':['영희','철수'],'영어':[90,82]})
영어점수
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
      <th>성명</th>
      <th>영어</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>영희</td>
      <td>90</td>
    </tr>
    <tr>
      <td>1</td>
      <td>철수</td>
      <td>82</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 왼쪽의 이름 컬럼과 오른쪽의 성명 컬럼이 같은 데이터를 병합하라는 의미
국어영어=pd.merge(국어점수,영어점수,left_on=['이름'],right_on=['성명'])
국어영어
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
      <th>성명</th>
      <th>영어</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>영희</td>
      <td>87</td>
      <td>영희</td>
      <td>90</td>
    </tr>
    <tr>
      <td>1</td>
      <td>철수</td>
      <td>91</td>
      <td>철수</td>
      <td>82</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 중복되는 값을 갖는 '성명' 컬럼은 필요 없으므로 삭제
국어영어.drop('성명',axis=1,inplace=True)
국어영어
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>영희</td>
      <td>87</td>
      <td>90</td>
    </tr>
    <tr>
      <td>1</td>
      <td>철수</td>
      <td>91</td>
      <td>82</td>
    </tr>
  </tbody>
</table>
</div>



인덱스를 기준으로 하는 병합

left_index=True, right_index=True 파라미터를 선택적으로 사용한다


```python
수학점수=DataFrame({'수학':[90,82]},index=['민철','봉구'])
수학점수
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
      <th>수학</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>민철</td>
      <td>90</td>
    </tr>
    <tr>
      <td>봉구</td>
      <td>82</td>
    </tr>
  </tbody>
</table>
</div>




```python
과학점수=DataFrame({'과학':[90,82]},index=['민철','철수'])
과학점수
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
      <th>과학</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>민철</td>
      <td>90</td>
    </tr>
    <tr>
      <td>철수</td>
      <td>82</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 왼쪽에서 index를 기준으로 사용하고, 오른쪽에도 인덱스를 기준으로 사용함
# ->양쪽 데이터 프레임의 인덱스가 같은 행끼리 병합됨
수학과학=pd.merge(수학점수,과학점수,left_index=True,right_index=True)
수학과학
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
      <th>수학</th>
      <th>과학</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>민철</td>
      <td>90</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 인덱스가 겹치지 않더라도 병합하도록 how 파라미터를 적용
수학과학=pd.merge(수학점수,과학점수,left_index=True,right_index=True,how='outer')
수학과학
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
      <th>수학</th>
      <th>과학</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>민철</td>
      <td>90.0</td>
      <td>90.0</td>
    </tr>
    <tr>
      <td>봉구</td>
      <td>82.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>철수</td>
      <td>NaN</td>
      <td>82.0</td>
    </tr>
  </tbody>
</table>
</div>



왼쪽의 인덱스와 오른쪽의 컬럼을 기준으로 병합하기


```python
한국사=DataFrame({'한국사':[87,91]},index=['영희','철수'])
한국사
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
      <th>한국사</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>영희</td>
      <td>87</td>
    </tr>
    <tr>
      <td>철수</td>
      <td>91</td>
    </tr>
  </tbody>
</table>
</div>




```python
세계사=DataFrame({'세계사':[90,82],'이름':['영희','철수']})
세계사
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
      <th>세계사</th>
      <th>이름</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>90</td>
      <td>영희</td>
    </tr>
    <tr>
      <td>1</td>
      <td>82</td>
      <td>철수</td>
    </tr>
  </tbody>
</table>
</div>




```python
역사점수=pd.merge(한국사,세계사,left_index=True,right_on=['이름'])
역사점수
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
      <th>한국사</th>
      <th>세계사</th>
      <th>이름</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>87</td>
      <td>90</td>
      <td>영희</td>
    </tr>
    <tr>
      <td>1</td>
      <td>91</td>
      <td>82</td>
      <td>철수</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 이름 컬럼을 인덱스로 지정하고 삭제하기
name_list=list(역사점수['이름'])
name_dict={}

for i,v in enumerate(name_list):
    name_dict[i]=v

    
역사점수.rename(index=name_dict,inplace=True)
역사점수.drop('이름',axis=1,inplace=True)
역사점수
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
      <th>한국사</th>
      <th>세계사</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>영희</td>
      <td>87</td>
      <td>90</td>
    </tr>
    <tr>
      <td>철수</td>
      <td>91</td>
      <td>82</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
