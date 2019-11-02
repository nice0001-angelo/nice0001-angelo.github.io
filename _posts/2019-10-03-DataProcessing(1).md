---
layout: post
title:  "03. Data Pre-Processing(1)"
---

# 데이터 전처리(1)
- 분석에 적합하게 데이터를 가공하는 작업
- 데이터가공(Data manupulation), 데이터 핸들링(Data Handling), 데이터 클리닝(Data Cleanging)

## 데이터 전 처리에서 수행되는 작업들

- 개별값에 접근하기
- 행 혹은 열(변수)추출
- 행 혹은 열추가, 삭제
- 정렬
- 기술통계 산출
- 다른 데이터프레임과 데이터 합치기(행,열)
- 집단별 나누기

-----------------------------
## #01. 필요한 모듈 참조


```python
from pandas import DataFrame
from sample import grade_dic
```

-----------------------------------------------------------
## #02. 샘플 데이터프레임 만들기


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



------------------------------------------------
## #03. 데이터 추출하기


```python
# 데이터프레임은 '열' 우선 접근이다.
df['국어']
```




    철수     98
    영희     88
    민철     92
    수현     63
    호영    120
    Name: 국어, dtype: int64




```python
# '철수'라는 이름의 열은 없으므로 에러
df['철수']
```


    ---------------------------------------------------------------------------

    KeyError                                  Traceback (most recent call last)

    c:\users\administrator\appdata\local\programs\python\python37\lib\site-packages\pandas\core\indexes\base.py in get_loc(self, key, method, tolerance)
       2896             try:
    -> 2897                 return self._engine.get_loc(key)
       2898             except KeyError:
    

    pandas\_libs\index.pyx in pandas._libs.index.IndexEngine.get_loc()
    

    pandas\_libs\index.pyx in pandas._libs.index.IndexEngine.get_loc()
    

    pandas\_libs\hashtable_class_helper.pxi in pandas._libs.hashtable.PyObjectHashTable.get_item()
    

    pandas\_libs\hashtable_class_helper.pxi in pandas._libs.hashtable.PyObjectHashTable.get_item()
    

    KeyError: '철수'

    
    During handling of the above exception, another exception occurred:
    

    KeyError                                  Traceback (most recent call last)

    <ipython-input-4-ba74e3c322b2> in <module>
          1 # '철수'라는 이름의 열은 없으므로 에러
    ----> 2 df['철수']
    

    c:\users\administrator\appdata\local\programs\python\python37\lib\site-packages\pandas\core\frame.py in __getitem__(self, key)
       2978             if self.columns.nlevels > 1:
       2979                 return self._getitem_multilevel(key)
    -> 2980             indexer = self.columns.get_loc(key)
       2981             if is_integer(indexer):
       2982                 indexer = [indexer]
    

    c:\users\administrator\appdata\local\programs\python\python37\lib\site-packages\pandas\core\indexes\base.py in get_loc(self, key, method, tolerance)
       2897                 return self._engine.get_loc(key)
       2898             except KeyError:
    -> 2899                 return self._engine.get_loc(self._maybe_cast_indexer(key))
       2900         indexer = self.get_indexer([key], method=method, tolerance=tolerance)
       2901         if indexer.ndim > 1 or indexer.size > 1:
    

    pandas\_libs\index.pyx in pandas._libs.index.IndexEngine.get_loc()
    

    pandas\_libs\index.pyx in pandas._libs.index.IndexEngine.get_loc()
    

    pandas\_libs\hashtable_class_helper.pxi in pandas._libs.hashtable.PyObjectHashTable.get_item()
    

    pandas\_libs\hashtable_class_helper.pxi in pandas._libs.hashtable.PyObjectHashTable.get_item()
    

    KeyError: '철수'



```python
# '행'단위로 접근하기 위해서는 'loc'이라는 속성을 통해 접근한다
df.loc['철수']
```




    국어    98.0
    영어     NaN
    수학    88.0
    과학    64.0
    Name: 철수, dtype: float64




```python
# 개별 값에 접근하고자 할 때도 '열>행' 순으로 접근
#df['국어']['철수']
df.loc['철수','국어']
```




    98




```python
# 행 우선 접근시 'loc'을 통해 접근한다. 단 하나의 괄호안에 [행,열] 순으로 이름을 넣는다
df.loc['철수','국어'] = 100
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
      <td>100</td>
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
# 조건검색
df.query('국어> 80')
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
      <td>100</td>
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
# 다중조건에 맞는 행 조회(1) -> And
df.query('국어> 80 and 수학 > 80')
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
      <td>100</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>64.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 다중조건에 맞는 행 조회(2) -> Or
df.query('국어< 70 or 수학 < 70')
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
      <td>영희</td>
      <td>88</td>
      <td>90.0</td>
      <td>62.0</td>
      <td>72.0</td>
    </tr>
    <tr>
      <td>수현</td>
      <td>63</td>
      <td>60.0</td>
      <td>31.0</td>
      <td>70.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 열 필터링 --> 추출할 컬럼의 이름을 리스트로 전달한다
df.filter(['국어','영어'])
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
      <td>철수</td>
      <td>100</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>영희</td>
      <td>88</td>
      <td>90.0</td>
    </tr>
    <tr>
      <td>민철</td>
      <td>92</td>
      <td>70.0</td>
    </tr>
    <tr>
      <td>수현</td>
      <td>63</td>
      <td>60.0</td>
    </tr>
    <tr>
      <td>호영</td>
      <td>120</td>
      <td>50.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 전치 구하기(가로,세로가 바뀜)
df2 = df.T
df2
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
      <th>철수</th>
      <th>영희</th>
      <th>민철</th>
      <th>수현</th>
      <th>호영</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>국어</td>
      <td>100.0</td>
      <td>88.0</td>
      <td>92.0</td>
      <td>63.0</td>
      <td>120.0</td>
    </tr>
    <tr>
      <td>영어</td>
      <td>NaN</td>
      <td>90.0</td>
      <td>70.0</td>
      <td>60.0</td>
      <td>50.0</td>
    </tr>
    <tr>
      <td>수학</td>
      <td>88.0</td>
      <td>62.0</td>
      <td>NaN</td>
      <td>31.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>과학</td>
      <td>64.0</td>
      <td>72.0</td>
      <td>NaN</td>
      <td>70.0</td>
      <td>88.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 조건 검색(영희의 점수가 80 이상인 과목 찾기)
df2.filter(['영희']).query('영희 > 80')

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
      <th>영희</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>국어</td>
      <td>88.0</td>
    </tr>
    <tr>
      <td>영어</td>
      <td>90.0</td>
    </tr>
  </tbody>
</table>
</div>



수집                           처리                         분석                  시각화
--------------------------------------------------------------------------------------------

프로그래밍                 형식을 통일시킴                   통계                   그래프
java, PHP, Node                                          (Python,R)  
R,Python                   분산처리 시스템                           
                    
사용자들의 활동            Hadoop                           여기서 
내역을 텍스트로 저장       & 맵리듀스                       분석한걸 
-->로그                                                     제안하면
                           정형데이터로               -->머신러닝(Knn알고리즘)             
온라인 데이터 수집         가공 후 저장함                
                          (DB,xslx)
형식이 제각각
-->비정형 데이터

------------------------------------------------
## #04. 행 추가하기


```python
#  데이터프레임 복제
cp = df.copy()
```


```python
# 새로운 행 추가하기(원본 자체가 수정됨)
# -> 추가될 행의 인덱스 이름을 지정해 준다.
# -> 리스트로 추가할 경우 DataFrame의 컬럼 순서에 맞게 지정한다.
# -> 누락되는 값이 있거나 값의 수가 초과될 경우 에러
cp.loc['정호'] = [90,80,70,60]
cp
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
      <td>100</td>
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
    <tr>
      <td>정호</td>
      <td>90</td>
      <td>80.0</td>
      <td>70.0</td>
      <td>60.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# -> 딕셔너리 형태로 추가할 경우 컬럼의 순서는 상관없다
# -> 누락되는 값이 있거나 값의 수가 초과될 경우 에러
cp.loc['민정'] = { '국어':81,'영어':72,'과학':90,'수학':84}
cp
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
      <td>100</td>
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
    <tr>
      <td>정호</td>
      <td>90</td>
      <td>80.0</td>
      <td>70.0</td>
      <td>60.0</td>
    </tr>
    <tr>
      <td>민정</td>
      <td>81</td>
      <td>72.0</td>
      <td>84.0</td>
      <td>90.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 기존의 행 복사하기
cp.loc['철민'] = cp.loc['철수']
cp
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
      <td>100.0</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>64.0</td>
    </tr>
    <tr>
      <td>영희</td>
      <td>88.0</td>
      <td>90.0</td>
      <td>62.0</td>
      <td>72.0</td>
    </tr>
    <tr>
      <td>민철</td>
      <td>92.0</td>
      <td>70.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>수현</td>
      <td>63.0</td>
      <td>60.0</td>
      <td>31.0</td>
      <td>70.0</td>
    </tr>
    <tr>
      <td>호영</td>
      <td>120.0</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>88.0</td>
    </tr>
    <tr>
      <td>정호</td>
      <td>90.0</td>
      <td>80.0</td>
      <td>70.0</td>
      <td>60.0</td>
    </tr>
    <tr>
      <td>민정</td>
      <td>81.0</td>
      <td>72.0</td>
      <td>84.0</td>
      <td>90.0</td>
    </tr>
    <tr>
      <td>철민</td>
      <td>100.0</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>64.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 다른 데이터프레임을 병합
# -> 제외된 열에 대해서는 NaN(결측치)로 설정됨
# -> sort : 열을 이름순으ㅗㄹ 정렬함(기본값 true)
tmp = DataFrame({'국어':81,'수학':84,'과학':90}, index=['상호'])
tmp
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
      <th>과학</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>상호</td>
      <td>81</td>
      <td>84</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>




```python
new_cf = cp.append(tmp,sort=False)
new_cf
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
      <td>100.0</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>64.0</td>
    </tr>
    <tr>
      <td>영희</td>
      <td>88.0</td>
      <td>90.0</td>
      <td>62.0</td>
      <td>72.0</td>
    </tr>
    <tr>
      <td>민철</td>
      <td>92.0</td>
      <td>70.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>수현</td>
      <td>63.0</td>
      <td>60.0</td>
      <td>31.0</td>
      <td>70.0</td>
    </tr>
    <tr>
      <td>호영</td>
      <td>120.0</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>88.0</td>
    </tr>
    <tr>
      <td>정호</td>
      <td>90.0</td>
      <td>80.0</td>
      <td>70.0</td>
      <td>60.0</td>
    </tr>
    <tr>
      <td>민정</td>
      <td>81.0</td>
      <td>72.0</td>
      <td>84.0</td>
      <td>90.0</td>
    </tr>
    <tr>
      <td>철민</td>
      <td>100.0</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>64.0</td>
    </tr>
    <tr>
      <td>상호</td>
      <td>81.0</td>
      <td>NaN</td>
      <td>84.0</td>
      <td>90.0</td>
    </tr>
  </tbody>
</table>
</div>



---------------------------------
## #05. 행 삭제하기


```python
# 데이터프레임 복제
cp=df.copy()
cp
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
      <td>100</td>
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
# -> 추가는 원본 자체가 변하지만 삭제는 결과가 반영된 새로운 복사본이 생성된다
k1 = cp.drop("철수")
k1
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
cp
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
      <td>100</td>
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
# 한번에 여러 행 삭제하기
k2 = cp.drop(['철수','영희','호영'])
k2
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
  </tbody>
</table>
</div>




```python
# ->인덱싱을 통한 0번째행 삭제하기
k3 = cp.drop(cp.index[0])
k3
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
# ->슬라이싱을 통한 3번째 행 부터 7번째 행 전까지 삭제하기
k4 = cp.drop(cp.index[3:7])
k4
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
      <td>100</td>
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
  </tbody>
</table>
</div>




```python
cp
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
      <td>100</td>
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
# drop 함수에 inplace = True 파라미터를 추가하면 원본 자체에서 삭제된다.
# 그러므로 이미 삭제된 행이라면 에러 발생
k5=cp.drop(['영희','수현'], inplace=True)
k5
```


```python
cp
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
      <td>100</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>64.0</td>
    </tr>
    <tr>
      <td>민철</td>
      <td>92</td>
      <td>70.0</td>
      <td>NaN</td>
      <td>NaN</td>
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



-------------------------------------
## #06. 열 추가하기


```python
cp = df.copy()
cp
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
      <td>100</td>
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
# 열 추가하기
# -> 리스트 형식으로 추가할 경우 행의 수에 맞게 추가되어야 한다
cp['한국사']=['92','83','72','None','80']
cp
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
      <th>한국사</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>철수</td>
      <td>100</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>64.0</td>
      <td>92</td>
    </tr>
    <tr>
      <td>영희</td>
      <td>88</td>
      <td>90.0</td>
      <td>62.0</td>
      <td>72.0</td>
      <td>83</td>
    </tr>
    <tr>
      <td>민철</td>
      <td>92</td>
      <td>70.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>72</td>
    </tr>
    <tr>
      <td>수현</td>
      <td>63</td>
      <td>60.0</td>
      <td>31.0</td>
      <td>70.0</td>
      <td>None</td>
    </tr>
    <tr>
      <td>호영</td>
      <td>120</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>80</td>
    </tr>
  </tbody>
</table>
</div>




```python
# -> 새로운 열에 하나의 값을 지정하면 모든 행이 동일한 값을 갖는다
cp['세계사']=100
cp
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
      <th>한국사</th>
      <th>세계사</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>철수</td>
      <td>100</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>64.0</td>
      <td>92</td>
      <td>100</td>
    </tr>
    <tr>
      <td>영희</td>
      <td>88</td>
      <td>90.0</td>
      <td>62.0</td>
      <td>72.0</td>
      <td>83</td>
      <td>100</td>
    </tr>
    <tr>
      <td>민철</td>
      <td>92</td>
      <td>70.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>72</td>
      <td>100</td>
    </tr>
    <tr>
      <td>수현</td>
      <td>63</td>
      <td>60.0</td>
      <td>31.0</td>
      <td>70.0</td>
      <td>None</td>
      <td>100</td>
    </tr>
    <tr>
      <td>호영</td>
      <td>120</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>80</td>
      <td>100</td>
    </tr>
  </tbody>
</table>
</div>




```python
from pandas import Series
# 시리즈를 통한 열 추가
# -> 각 값이 연결될 행의 이름(index)를 지정해야 한다.
# -> 이 경우는 부분적으로 값을 비워 둘 수 있다
# (여기서는 호영의 데이터 생략)
cp['사회'] = Series([82,90,92,64],index=['철수','영희','민철','수현'])
cp
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
      <th>한국사</th>
      <th>세계사</th>
      <th>사회</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>철수</td>
      <td>100</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>64.0</td>
      <td>92</td>
      <td>100</td>
      <td>82.0</td>
    </tr>
    <tr>
      <td>영희</td>
      <td>88</td>
      <td>90.0</td>
      <td>62.0</td>
      <td>72.0</td>
      <td>83</td>
      <td>100</td>
      <td>90.0</td>
    </tr>
    <tr>
      <td>민철</td>
      <td>92</td>
      <td>70.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>72</td>
      <td>100</td>
      <td>92.0</td>
    </tr>
    <tr>
      <td>수현</td>
      <td>63</td>
      <td>60.0</td>
      <td>31.0</td>
      <td>70.0</td>
      <td>None</td>
      <td>100</td>
      <td>64.0</td>
    </tr>
    <tr>
      <td>호영</td>
      <td>120</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>80</td>
      <td>100</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 딕셔너리는 행(?)을 추가 할 수 없음..학인필요
```

-----------------------------
## #07. 열 삭제하기


```python
cp=df.copy()
cp
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
      <td>100</td>
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
# 열 삭제하기
# -> 컬럼 이름을 통한 열 삭제
# -> inplace=True 파라미터를 추가할 경우 원본 자체에서 삭제되고 리턴되는 객체는 없다(여기서는 사용안함)
# axis=0(x축,행,기본값), axis=1(y축,열,optional)
k1=cp.drop('국어',axis=1)
k1
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
      <th>수학</th>
      <th>과학</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>철수</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>64.0</td>
    </tr>
    <tr>
      <td>영희</td>
      <td>90.0</td>
      <td>62.0</td>
      <td>72.0</td>
    </tr>
    <tr>
      <td>민철</td>
      <td>70.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>수현</td>
      <td>60.0</td>
      <td>31.0</td>
      <td>70.0</td>
    </tr>
    <tr>
      <td>호영</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>88.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 여러 열을 동시에 삭제하기 -> 열 이름을 리스트로 지정
k2=cp.drop(['영어','수학','과학'],axis=1)
k2
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>철수</td>
      <td>100</td>
    </tr>
    <tr>
      <td>영희</td>
      <td>88</td>
    </tr>
    <tr>
      <td>민철</td>
      <td>92</td>
    </tr>
    <tr>
      <td>수현</td>
      <td>63</td>
    </tr>
    <tr>
      <td>호영</td>
      <td>120</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 인덱싱을 통한 3번째(0부터 카운트)열 삭제하기
# -> axis = 0:행삭제(기본값), axis=1 :열삭제
k3 = cp.drop(cp.columns[3],axis=1)
k3
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>철수</td>
      <td>100</td>
      <td>NaN</td>
      <td>88.0</td>
    </tr>
    <tr>
      <td>영희</td>
      <td>88</td>
      <td>90.0</td>
      <td>62.0</td>
    </tr>
    <tr>
      <td>민철</td>
      <td>92</td>
      <td>70.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>수현</td>
      <td>63</td>
      <td>60.0</td>
      <td>31.0</td>
    </tr>
    <tr>
      <td>호영</td>
      <td>120</td>
      <td>50.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# -> 슬라이싱을 통한 2번째 열부터 4번째 열전까지 삭제하기
k4 =cp.drop(cp.columns[2:4],axis=1)
k4
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
      <td>철수</td>
      <td>100</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>영희</td>
      <td>88</td>
      <td>90.0</td>
    </tr>
    <tr>
      <td>민철</td>
      <td>92</td>
      <td>70.0</td>
    </tr>
    <tr>
      <td>수현</td>
      <td>63</td>
      <td>60.0</td>
    </tr>
    <tr>
      <td>호영</td>
      <td>120</td>
      <td>50.0</td>
    </tr>
  </tbody>
</table>
</div>



----------------------------------
## #08. 데이터 정렬


```python
cp=df.copy()
cp
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
      <td>100</td>
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
# 특정 열을 기준으로 오름차순(순차정렬) 정렬
# -> inplace=True 인 경우 원본 자체를 정렬함
# -> inplace=False 인 경우 정렬된 결과를 리턴하고 원본은 변화 없음(기본값)
cp.sort_values('국어',inplace=True)
cp
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
      <td>수현</td>
      <td>63</td>
      <td>60.0</td>
      <td>31.0</td>
      <td>70.0</td>
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
      <td>철수</td>
      <td>100</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>64.0</td>
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
# 두 개 이상의 열로 정렬할 경우 리스트로 설정
# -> 국어 점수가 동일할 경우 수학점수 순으로 정렬된다(앞의 리스트가 동점일 경우만 뒤에 리스트가 order 결정요소가 됨)
cp.sort_values(['국어','수학'], inplace=True)
cp
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
      <td>수현</td>
      <td>63</td>
      <td>60.0</td>
      <td>31.0</td>
      <td>70.0</td>
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
      <td>철수</td>
      <td>100</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>64.0</td>
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
## #09. 컬럼인덱스 변경


```python
cp=df.copy()
cp
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
      <td>100</td>
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
# 컬럼 순서 변경
# -> 지정된 순서대로 열이 재정렬 된 결과가 반환된다.
# -> inplace 파라미터 지원 안함
# -> 원본은 변화 없음. 결과가 적용된 복사본이 생성된다
a = cp.reindex(columns=['국어','수학','과학','영어'])
a
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
      <th>과학</th>
      <th>영어</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>철수</td>
      <td>100</td>
      <td>88.0</td>
      <td>64.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>영희</td>
      <td>88</td>
      <td>62.0</td>
      <td>72.0</td>
      <td>90.0</td>
    </tr>
    <tr>
      <td>민철</td>
      <td>92</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>70.0</td>
    </tr>
    <tr>
      <td>수현</td>
      <td>63</td>
      <td>31.0</td>
      <td>70.0</td>
      <td>60.0</td>
    </tr>
    <tr>
      <td>호영</td>
      <td>120</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>50.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 인덱스(행) 순서 변경
# -> 지정된 순서대로 행이 재정렬 된 결과가 반환된다
# -> inplace 파라미터 지원 안함
# -> 원본은 변화 없음. 결과가 적용된 복사본이 생성된다.
b = cp.reindex(index=['철수','민철','호영','영희','수현'])
b
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
      <td>100</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>64.0</td>
    </tr>
    <tr>
      <td>민철</td>
      <td>92</td>
      <td>70.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>호영</td>
      <td>120</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>88.0</td>
    </tr>
    <tr>
      <td>영희</td>
      <td>88</td>
      <td>90.0</td>
      <td>62.0</td>
      <td>72.0</td>
    </tr>
    <tr>
      <td>수현</td>
      <td>63</td>
      <td>60.0</td>
      <td>31.0</td>
      <td>70.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 컬럼, 인덱스 이름 변경
# -> '기존이름:새이름' 형식의 딕셔너리로 지정
# -> columns와 index중 변경을 원하는 하나만 설정 가능
# -> 원본은 변화없음. 결과가 적용된 복사본이 생성된다.
# -> inplace 파라미터 '지원함'
c=cp.rename(
    columns={'국어':'kor','영어':'eng','수학':'math','과학':'sci'},
    index={'영희':'yh','수현':'sh','호영':'hy','철수':'cs','민철':'mc'})
c
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
      <th>kor</th>
      <th>eng</th>
      <th>math</th>
      <th>sci</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>cs</td>
      <td>100</td>
      <td>NaN</td>
      <td>88.0</td>
      <td>64.0</td>
    </tr>
    <tr>
      <td>yh</td>
      <td>88</td>
      <td>90.0</td>
      <td>62.0</td>
      <td>72.0</td>
    </tr>
    <tr>
      <td>mc</td>
      <td>92</td>
      <td>70.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>sh</td>
      <td>63</td>
      <td>60.0</td>
      <td>31.0</td>
      <td>70.0</td>
    </tr>
    <tr>
      <td>hy</td>
      <td>120</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>88.0</td>
    </tr>
  </tbody>
</table>
</div>



## 향후 커리큐럼

데이터프레임 다루기<br>
    * 데이터전처리<br>
    * 데이터분포확인<br>
    * 데이터정제<br>
    * 데이터프레임 시각화(그래프)<br>
    
OpenAPI 연동을 통한 데이터 수집

웹페이지 스크랩핑을 통한 데이터 수집

가설검증

사이킷런(기계학습)활용<br>
    * Knn 알고리즘(최근접 이웃)


```python

```
