# 데이터프레임 개요

### Pandas 란?

- 데이터 분석, 처리 등을 쉽게 하도록 만들어진 python package
- 대용량 데이터를 보다 쉽고 안정적으로 처리할 수 있다

### Pandas 설치

> pip install pandas

### Pandas의 자료구조
**DataFrame**

- 열과 행으로 구성된 엑셀 표와 같은 구조
- 각 행과 열을 이루는 단위는 Series라는 객체
- Series가 모여서 DataFrame가 됨(Series는 엑셀의 세로 셀)

### Series
- index와 value로 구성된 numpy 배열의 확장 객체

-------------------------
## #01. 필요한 모듈 참고


```python
# pandas 모듈에서 Series 클래스 가져오기
from pandas import Series
```

---------------------------
## #02. Series 객체 살펴보기

### **Series 객체생성**


```python
# 기본 Series 만들기
# -> List 자료형을 가공하여 생성된 데이터 구조가 Series임
# list -> numpy array --> Series : 파이썬의 리스트를 numpy array를 가공한게 Series 임 : 참고로 파이썬의 리스트는 원래 배열이라고 생각 하면 됨
# numpy에서 사용하는 함수는 기본으로 pandas에 다 들어가 있음
items = [10,30,50,70,90]
column = Series(items)
column
```




    0    10
    1    30
    2    50
    3    70
    4    90
    dtype: int64




```python
# -> 인덱스를 활용한 개별 값 확인
print(column[0])
print(column[2])
print(column[4])
```

    10
    50
    90
    


```python
# 시리즈의 값들만 추출
column.values
```




    array([10, 30, 50, 70, 90], dtype=int64)




```python
# 타입을 확인하면 Numpy 배열임을 알 수 있다.
type(column.values)
```




    numpy.ndarray




```python
# --> 시리즈의 값들을 저장하고 있는 numpy 배열을 list로 변환
value_list = list(column.values)
value_list
```




    [10, 30, 50, 70, 90]




```python
# 시리즈의 색인(index)만 추출
column.index
```




    RangeIndex(start=0, stop=5, step=1)




```python
# 색인들의 타입 확인
type(column.index)
```




    pandas.core.indexes.range.RangeIndex




```python
# 시리즈의 색인(index)을 list로 변환
list(column.index)
```




    [0, 1, 2, 3, 4]



### **조건검색**


```python
# 특정 조건에 맞는 항목들만 추출
# -> 이름[이름에 대한 조건식]
# -> 30초과인 항목들만 추출
in1 = column[column > 30]
in1
```




    2    50
    3    70
    4    90
    dtype: int64




```python
# -> 70이하 and 10초과인 항목들만 추출
in2 = column[column > 10][column<=70]
in2
```




    1    30
    2    50
    3    70
    dtype: int64




```python
# -> 10이하 or 70이상인 항목들만 추출
in3 = column[(column <= 10)|(column>=70)]
in3
```




    0    10
    3    70
    4    90
    dtype: int64



### **인덱스를 직접 지정하기**


```python
week1 = Series([290000,310000], index=['토','일'])
week1
```




    토    290000
    일    310000
    dtype: int64




```python
week2 = Series([120000,220000], index=['일','토'])
week2
```




    일    120000
    토    220000
    dtype: int64




```python
# 시리즈 객체의 사칙연산
# --> index가 동일한 항목끼리 연산이 수행된다.
Result = week1 + week2
Result
```




    일    430000
    토    510000
    dtype: int64




```python

```
