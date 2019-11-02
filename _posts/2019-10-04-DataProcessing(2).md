---
layout: post
title:  "04. Data Pre-Processing(2)"
---


# 데이터 전처리(2)
- 동일한 값을 갖는 데이터들끼리 그룹으로 묶고, 그 이외의 다른 데이터들에게 집계를 수행하는 형태.
- SQL의 group by 절과 같은 기능.

---------------------------------------
## #01. 필요한 모듈 참조 및 샘플 데이터 준비


```python
# pandas에서 참조
from pandas import DataFrame

# sample.py에서 참조(http://itpaper.co.kr/demo/python/sample.zip)
from sample import city_people
city_people
```




    {'도시': ['서울', '서울', '서울', '부산', '부산', '부산', '인천', '인천'],
     '연도': ['2015', '2010', '2005', '2015', '2010', '2005', '2015', '2010'],
     '인구': [9904312,
      9631482,
      9762546,
      3448737,
      3393191,
      3512547,
      2890451,
      2632035],
     '지역': ['수도권', '수도권', '수도권', '경상권', '경상권', '경상권', '수도권', '수도권']}




```python
# pandas에서 참조
df = DataFrame(city_people)
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
      <th>도시</th>
      <th>연도</th>
      <th>인구</th>
      <th>지역</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>서울</td>
      <td>2015</td>
      <td>9904312</td>
      <td>수도권</td>
    </tr>
    <tr>
      <td>1</td>
      <td>서울</td>
      <td>2010</td>
      <td>9631482</td>
      <td>수도권</td>
    </tr>
    <tr>
      <td>2</td>
      <td>서울</td>
      <td>2005</td>
      <td>9762546</td>
      <td>수도권</td>
    </tr>
    <tr>
      <td>3</td>
      <td>부산</td>
      <td>2015</td>
      <td>3448737</td>
      <td>경상권</td>
    </tr>
    <tr>
      <td>4</td>
      <td>부산</td>
      <td>2010</td>
      <td>3393191</td>
      <td>경상권</td>
    </tr>
    <tr>
      <td>5</td>
      <td>부산</td>
      <td>2005</td>
      <td>3512547</td>
      <td>경상권</td>
    </tr>
    <tr>
      <td>6</td>
      <td>인천</td>
      <td>2015</td>
      <td>2890451</td>
      <td>수도권</td>
    </tr>
    <tr>
      <td>7</td>
      <td>인천</td>
      <td>2010</td>
      <td>2632035</td>
      <td>수도권</td>
    </tr>
  </tbody>
</table>
</div>



---------------------------------------
## #02. 그룹분석
1) 그룹으로 묶을 컬럼(하나이상)과 집계를 수행할 컬럼을 추출


```python
# 도시별 평균 인구수를 위해 두 개의 컬럼을 추출
group_df =df.filter(['도시','인구'])
group_df
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
      <th>도시</th>
      <th>인구</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>서울</td>
      <td>9904312</td>
    </tr>
    <tr>
      <td>1</td>
      <td>서울</td>
      <td>9631482</td>
    </tr>
    <tr>
      <td>2</td>
      <td>서울</td>
      <td>9762546</td>
    </tr>
    <tr>
      <td>3</td>
      <td>부산</td>
      <td>3448737</td>
    </tr>
    <tr>
      <td>4</td>
      <td>부산</td>
      <td>3393191</td>
    </tr>
    <tr>
      <td>5</td>
      <td>부산</td>
      <td>3512547</td>
    </tr>
    <tr>
      <td>6</td>
      <td>인천</td>
      <td>2890451</td>
    </tr>
    <tr>
      <td>7</td>
      <td>인천</td>
      <td>2632035</td>
    </tr>
  </tbody>
</table>
</div>



2) 특정 컬럼을 그룹으로 묶고 다른 컬럼으로 집계수행

사용 가능한 집계 함수의 종류

- 그룹별데이터의 갯수:size,count<br>
- 평균,중앙값,최소,최대 : mean,median,min,max<br>
- 합계,곱,표준편차,분산,사분위수 : sum,prod,std,var,quantile<br>
- 그룹안에서 첫번째 마지막 데이터:first,last<br>


```python
도시별_평균_인구수 =group_df.groupby(group_df['도시']).mean()
도시별_평균_인구수
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
      <th>인구</th>
    </tr>
    <tr>
      <th>도시</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>부산</td>
      <td>3.451492e+06</td>
    </tr>
    <tr>
      <td>서울</td>
      <td>9.766113e+06</td>
    </tr>
    <tr>
      <td>인천</td>
      <td>2.761243e+06</td>
    </tr>
  </tbody>
</table>
</div>




```python
도시별_갯수 =group_df.groupby(group_df['도시']).count()
도시별_갯수
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
      <th>인구</th>
    </tr>
    <tr>
      <th>도시</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>부산</td>
      <td>3</td>
    </tr>
    <tr>
      <td>서울</td>
      <td>3</td>
    </tr>
    <tr>
      <td>인천</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
도시별_평균_인구수 =group_df.groupby(group_df['도시']).sum()
도시별_평균_인구수
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
      <th>인구</th>
    </tr>
    <tr>
      <th>도시</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>부산</td>
      <td>10354475</td>
    </tr>
    <tr>
      <td>서울</td>
      <td>29298340</td>
    </tr>
    <tr>
      <td>인천</td>
      <td>5522486</td>
    </tr>
  </tbody>
</table>
</div>




```python
도시별_평균_인구수 =group_df.groupby(group_df['도시']).first()
도시별_평균_인구수
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
      <th>인구</th>
    </tr>
    <tr>
      <th>도시</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>부산</td>
      <td>3448737</td>
    </tr>
    <tr>
      <td>서울</td>
      <td>9904312</td>
    </tr>
    <tr>
      <td>인천</td>
      <td>2890451</td>
    </tr>
  </tbody>
</table>
</div>



3) 두 개 이상의 컬럼을 기준으로 집계하기


```python
# 기준이 될 컬럼 2건과 집계를 수행할 컬럼 추출
group_df2 = df.filter(['지역','연도','인구'])
group_df2
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
      <th>연도</th>
      <th>인구</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>수도권</td>
      <td>2015</td>
      <td>9904312</td>
    </tr>
    <tr>
      <td>1</td>
      <td>수도권</td>
      <td>2010</td>
      <td>9631482</td>
    </tr>
    <tr>
      <td>2</td>
      <td>수도권</td>
      <td>2005</td>
      <td>9762546</td>
    </tr>
    <tr>
      <td>3</td>
      <td>경상권</td>
      <td>2015</td>
      <td>3448737</td>
    </tr>
    <tr>
      <td>4</td>
      <td>경상권</td>
      <td>2010</td>
      <td>3393191</td>
    </tr>
    <tr>
      <td>5</td>
      <td>경상권</td>
      <td>2005</td>
      <td>3512547</td>
    </tr>
    <tr>
      <td>6</td>
      <td>수도권</td>
      <td>2015</td>
      <td>2890451</td>
    </tr>
    <tr>
      <td>7</td>
      <td>수도권</td>
      <td>2010</td>
      <td>2632035</td>
    </tr>
  </tbody>
</table>
</div>




```python
도시별_평균_인구수 =group_df2.groupby([group_df2['지역'],group_df2['연도']]).mean()
도시별_평균_인구수
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
      <th></th>
      <th>인구</th>
    </tr>
    <tr>
      <th>지역</th>
      <th>연도</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="3" valign="top">경상권</td>
      <td>2005</td>
      <td>3512547.0</td>
    </tr>
    <tr>
      <td>2010</td>
      <td>3393191.0</td>
    </tr>
    <tr>
      <td>2015</td>
      <td>3448737.0</td>
    </tr>
    <tr>
      <td rowspan="3" valign="top">수도권</td>
      <td>2005</td>
      <td>9762546.0</td>
    </tr>
    <tr>
      <td>2010</td>
      <td>6131758.5</td>
    </tr>
    <tr>
      <td>2015</td>
      <td>6397381.5</td>
    </tr>
  </tbody>
</table>
</div>




```python
도시별_연도별_최대인구 =group_df2.groupby([group_df2['지역'],group_df2['연도']]).max()
도시별_연도별_최대인구
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
      <th></th>
      <th>인구</th>
    </tr>
    <tr>
      <th>지역</th>
      <th>연도</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="3" valign="top">경상권</td>
      <td>2005</td>
      <td>3512547</td>
    </tr>
    <tr>
      <td>2010</td>
      <td>3393191</td>
    </tr>
    <tr>
      <td>2015</td>
      <td>3448737</td>
    </tr>
    <tr>
      <td rowspan="3" valign="top">수도권</td>
      <td>2005</td>
      <td>9762546</td>
    </tr>
    <tr>
      <td>2010</td>
      <td>9631482</td>
    </tr>
    <tr>
      <td>2015</td>
      <td>9904312</td>
    </tr>
  </tbody>
</table>
</div>




```python
도시별_사분위점 =group_df2.groupby([group_df2['지역'],group_df2['연도']]).quantile()
도시별_사분위점
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
      <th></th>
      <th>인구</th>
    </tr>
    <tr>
      <th>지역</th>
      <th>연도</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="3" valign="top">경상권</td>
      <td>2005</td>
      <td>3512547.0</td>
    </tr>
    <tr>
      <td>2010</td>
      <td>3393191.0</td>
    </tr>
    <tr>
      <td>2015</td>
      <td>3448737.0</td>
    </tr>
    <tr>
      <td rowspan="3" valign="top">수도권</td>
      <td>2005</td>
      <td>9762546.0</td>
    </tr>
    <tr>
      <td>2010</td>
      <td>6131758.5</td>
    </tr>
    <tr>
      <td>2015</td>
      <td>6397381.5</td>
    </tr>
  </tbody>
</table>
</div>




```python
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
      <th>도시</th>
      <th>연도</th>
      <th>인구</th>
      <th>지역</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>서울</td>
      <td>2015</td>
      <td>9904312</td>
      <td>수도권</td>
    </tr>
    <tr>
      <td>1</td>
      <td>서울</td>
      <td>2010</td>
      <td>9631482</td>
      <td>수도권</td>
    </tr>
    <tr>
      <td>2</td>
      <td>서울</td>
      <td>2005</td>
      <td>9762546</td>
      <td>수도권</td>
    </tr>
    <tr>
      <td>3</td>
      <td>부산</td>
      <td>2015</td>
      <td>3448737</td>
      <td>경상권</td>
    </tr>
    <tr>
      <td>4</td>
      <td>부산</td>
      <td>2010</td>
      <td>3393191</td>
      <td>경상권</td>
    </tr>
    <tr>
      <td>5</td>
      <td>부산</td>
      <td>2005</td>
      <td>3512547</td>
      <td>경상권</td>
    </tr>
    <tr>
      <td>6</td>
      <td>인천</td>
      <td>2015</td>
      <td>2890451</td>
      <td>수도권</td>
    </tr>
    <tr>
      <td>7</td>
      <td>인천</td>
      <td>2010</td>
      <td>2632035</td>
      <td>수도권</td>
    </tr>
  </tbody>
</table>
</div>



## 피벗테이블<br>
데이터 열 중 두 개의 열을 각각 행 인덱스, 열 인덱스로 사용하여 데이터를 재배치한것


```python
# 각 도시별 연도에 따른 인구수
pv1 = df.pivot('도시', '연도', '인구')
pv1
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
      <th>연도</th>
      <th>2005</th>
      <th>2010</th>
      <th>2015</th>
    </tr>
    <tr>
      <th>도시</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>부산</td>
      <td>3512547.0</td>
      <td>3393191.0</td>
      <td>3448737.0</td>
    </tr>
    <tr>
      <td>서울</td>
      <td>9762546.0</td>
      <td>9631482.0</td>
      <td>9904312.0</td>
    </tr>
    <tr>
      <td>인천</td>
      <td>NaN</td>
      <td>2632035.0</td>
      <td>2890451.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
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
      <th>도시</th>
      <th>연도</th>
      <th>인구</th>
      <th>지역</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>서울</td>
      <td>2015</td>
      <td>9904312</td>
      <td>수도권</td>
    </tr>
    <tr>
      <td>1</td>
      <td>서울</td>
      <td>2010</td>
      <td>9631482</td>
      <td>수도권</td>
    </tr>
    <tr>
      <td>2</td>
      <td>서울</td>
      <td>2005</td>
      <td>9762546</td>
      <td>수도권</td>
    </tr>
    <tr>
      <td>3</td>
      <td>부산</td>
      <td>2015</td>
      <td>3448737</td>
      <td>경상권</td>
    </tr>
    <tr>
      <td>4</td>
      <td>부산</td>
      <td>2010</td>
      <td>3393191</td>
      <td>경상권</td>
    </tr>
    <tr>
      <td>5</td>
      <td>부산</td>
      <td>2005</td>
      <td>3512547</td>
      <td>경상권</td>
    </tr>
    <tr>
      <td>6</td>
      <td>인천</td>
      <td>2015</td>
      <td>2890451</td>
      <td>수도권</td>
    </tr>
    <tr>
      <td>7</td>
      <td>인천</td>
      <td>2010</td>
      <td>2632035</td>
      <td>수도권</td>
    </tr>
  </tbody>
</table>
</div>




```python
도시별_평균_인구수 =group_df2.groupby([group_df2['지역'],group_df2['연도']]).mean()
도시별_평균_인구수
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
      <th></th>
      <th>인구</th>
    </tr>
    <tr>
      <th>지역</th>
      <th>연도</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="3" valign="top">경상권</td>
      <td>2005</td>
      <td>3512547.0</td>
    </tr>
    <tr>
      <td>2010</td>
      <td>3393191.0</td>
    </tr>
    <tr>
      <td>2015</td>
      <td>3448737.0</td>
    </tr>
    <tr>
      <td rowspan="3" valign="top">수도권</td>
      <td>2005</td>
      <td>9762546.0</td>
    </tr>
    <tr>
      <td>2010</td>
      <td>6131758.5</td>
    </tr>
    <tr>
      <td>2015</td>
      <td>6397381.5</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 지역과 연도에 대한 조합은 두 쌍이 나타나므로 에러
pv1 = df.pivot('지역','연도','인구')
pv1
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-62-fe4e375241b8> in <module>
          1 # 지역과 연도에 대한 조합은 두 쌍이 나타나므로 에러
    ----> 2 pv1 = df.pivot('지역','연도','인구')
          3 pv1
    

    c:\users\administrator\appdata\local\programs\python\python37\lib\site-packages\pandas\core\frame.py in pivot(self, index, columns, values)
       5917         from pandas.core.reshape.pivot import pivot
       5918 
    -> 5919         return pivot(self, index=index, columns=columns, values=values)
       5920 
       5921     _shared_docs[
    

    c:\users\administrator\appdata\local\programs\python\python37\lib\site-packages\pandas\core\reshape\pivot.py in pivot(data, index, columns, values)
        428         else:
        429             indexed = data._constructor_sliced(data[values].values, index=index)
    --> 430     return indexed.unstack(columns)
        431 
        432 
    

    c:\users\administrator\appdata\local\programs\python\python37\lib\site-packages\pandas\core\series.py in unstack(self, level, fill_value)
       3743         from pandas.core.reshape.reshape import unstack
       3744 
    -> 3745         return unstack(self, level, fill_value)
       3746 
       3747     # ----------------------------------------------------------------------
    

    c:\users\administrator\appdata\local\programs\python\python37\lib\site-packages\pandas\core\reshape\reshape.py in unstack(obj, level, fill_value)
        421             level=level,
        422             fill_value=fill_value,
    --> 423             constructor=obj._constructor_expanddim,
        424         )
        425         return unstacker.get_result()
    

    c:\users\administrator\appdata\local\programs\python\python37\lib\site-packages\pandas\core\reshape\reshape.py in __init__(self, values, index, level, value_columns, fill_value, constructor)
        140 
        141         self._make_sorted_values_labels()
    --> 142         self._make_selectors()
        143 
        144     def _make_sorted_values_labels(self):
    

    c:\users\administrator\appdata\local\programs\python\python37\lib\site-packages\pandas\core\reshape\reshape.py in _make_selectors(self)
        178 
        179         if mask.sum() < len(self.index):
    --> 180             raise ValueError("Index contains duplicate entries, " "cannot reshape")
        181 
        182         self.group_index = comp_index
    

    ValueError: Index contains duplicate entries, cannot reshape


## 그룹분석 결과를 피벗테이블로 조합하기<br>
각 지역의 연도별 평균 인구수를 피벗테이블로 생성


```python
# 집계 대상을 추출
filter_df = df.filter(['지역','연도','인구'])
filter_df
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
      <th>연도</th>
      <th>인구</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>수도권</td>
      <td>2015</td>
      <td>9904312</td>
    </tr>
    <tr>
      <td>1</td>
      <td>수도권</td>
      <td>2010</td>
      <td>9631482</td>
    </tr>
    <tr>
      <td>2</td>
      <td>수도권</td>
      <td>2005</td>
      <td>9762546</td>
    </tr>
    <tr>
      <td>3</td>
      <td>경상권</td>
      <td>2015</td>
      <td>3448737</td>
    </tr>
    <tr>
      <td>4</td>
      <td>경상권</td>
      <td>2010</td>
      <td>3393191</td>
    </tr>
    <tr>
      <td>5</td>
      <td>경상권</td>
      <td>2005</td>
      <td>3512547</td>
    </tr>
    <tr>
      <td>6</td>
      <td>수도권</td>
      <td>2015</td>
      <td>2890451</td>
    </tr>
    <tr>
      <td>7</td>
      <td>수도권</td>
      <td>2010</td>
      <td>2632035</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 그룹분석
# as_index=False -> 기준열이 인덱스로 지정되는 것을 방지(인덱스로는 처리 불가하므로(데이터여야함))
group_df = filter_df.groupby([filter_df['지역'],filter_df['연도']],as_index=False).mean()
group_df
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
      <th>연도</th>
      <th>인구</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>경상권</td>
      <td>2005</td>
      <td>3512547.0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>경상권</td>
      <td>2010</td>
      <td>3393191.0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>경상권</td>
      <td>2015</td>
      <td>3448737.0</td>
    </tr>
    <tr>
      <td>3</td>
      <td>수도권</td>
      <td>2005</td>
      <td>9762546.0</td>
    </tr>
    <tr>
      <td>4</td>
      <td>수도권</td>
      <td>2010</td>
      <td>6131758.5</td>
    </tr>
    <tr>
      <td>5</td>
      <td>수도권</td>
      <td>2015</td>
      <td>6397381.5</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 피벗테이블 븐석
pivot_df = group_df.pivot('지역','연도','인구')
pivot_df
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
      <th>연도</th>
      <th>2005</th>
      <th>2010</th>
      <th>2015</th>
    </tr>
    <tr>
      <th>지역</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>경상권</td>
      <td>3512547.0</td>
      <td>3393191.0</td>
      <td>3448737.0</td>
    </tr>
    <tr>
      <td>수도권</td>
      <td>9762546.0</td>
      <td>6131758.5</td>
      <td>6397381.5</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
