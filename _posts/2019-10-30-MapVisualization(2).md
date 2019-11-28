---
layout: post
title:  "30. MapVisualization(2)"
---
# 지도시각화 (2)

엑셀 파일에 표시된 위,경도를 사용하여 전국 초,중고읃학교 위치 표시하기

## #01. 필요한 패키지 가져오기


```python
import folium
from pandas import DataFrame
from pandas import ExcelFile
```

## #02. 데이터 수집


```python
# 엑셀파일을원격으로 내려받아 데이터프레임으로 변환(다소 시간이 소요된다...)
xlsx = ExcelFile("http://itpaper.co.kr/demo/python/school2019.xlsx")
df = xlsx.parse(xlsx.sheet_names[0])
df
```


    ---------------------------------------------------------------------------

    ImportError                               Traceback (most recent call last)

    <ipython-input-4-6081de10cebe> in <module>
          1 # 엑셀파일을원격으로 내려받아 데이터프레임으로 변환(다소 시간이 소요된다...)
    ----> 2 xlsx = ExcelFile("http://itpaper.co.kr/demo/python/school2019.xlsx")
          3 df = xlsx.parse(xlsx.sheet_names[0])
          4 df
    

    c:\users\mchinae\appdata\local\programs\python\python37\lib\site-packages\pandas\io\excel\_base.py in __init__(self, io, engine)
        817         self._io = _stringify_path(io)
        818 
    --> 819         self._reader = self._engines[engine](self._io)
        820 
        821     def __fspath__(self):
    

    c:\users\mchinae\appdata\local\programs\python\python37\lib\site-packages\pandas\io\excel\_xlrd.py in __init__(self, filepath_or_buffer)
         18         """
         19         err_msg = "Install xlrd >= 1.0.0 for Excel support"
    ---> 20         import_optional_dependency("xlrd", extra=err_msg)
         21         super().__init__(filepath_or_buffer)
         22 
    

    c:\users\mchinae\appdata\local\programs\python\python37\lib\site-packages\pandas\compat\_optional.py in import_optional_dependency(name, extra, raise_on_missing, on_version)
         91     except ImportError:
         92         if raise_on_missing:
    ---> 93             raise ImportError(message.format(name=name, extra=extra)) from None
         94         else:
         95             return None
    

    ImportError: Missing optional dependency 'xlrd'. Install xlrd >= 1.0.0 for Excel support Use pip or conda to install xlrd.


## #03. 데이터 전처리

## 1) 사용할 필드만 추출


```python
df2 = df.filter(['학교명','학교급구분','소재지도로명주소','위도','경도'])
df
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-5-e8c9511be84a> in <module>
    ----> 1 df2 = df.filter(['학교명','학교급구분','소재지도로명주소','위도','경도'])
          2 df
    

    NameError: name 'df' is not defined


## 2) 서울시의 초등학교만 추출
1. '학교급구분' 필드 값이 **초등학교**
2. '소재지도로명주소'에 서울이라는 단어가 포함된 경우
     ```python
     # Like 연산
     컬럼이름.str.contains('검색어')
     ```


```python
df3 = df2.query(
        "학교급구분 == '초등학교' and 소재지도로명주소.str.contains('서울')")
df3
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-6-8f3b0e873d1c> in <module>
    ----> 1 df3 = df2.query(
          2         "학교급구분 == '초등학교' and 소재지도로명주소.str.contains('서울')")
          3 df3
    

    NameError: name 'df2' is not defined


# #03.데이터 시각화

## 01) 지도객체 생성


```python
# zoom_start : 배율 1~22
map_osm = folium.Map(location=[37.566651, 126.978428], zoom_start=12)
map_osm
```




<div style="width:100%;"><div style="position:relative;width:100%;height:0;padding-bottom:60%;"><iframe src="data:text/html;charset=utf-8;base64,PCFET0NUWVBFIGh0bWw+CjxoZWFkPiAgICAKICAgIDxtZXRhIGh0dHAtZXF1aXY9ImNvbnRlbnQtdHlwZSIgY29udGVudD0idGV4dC9odG1sOyBjaGFyc2V0PVVURi04IiAvPgogICAgCiAgICAgICAgPHNjcmlwdD4KICAgICAgICAgICAgTF9OT19UT1VDSCA9IGZhbHNlOwogICAgICAgICAgICBMX0RJU0FCTEVfM0QgPSBmYWxzZTsKICAgICAgICA8L3NjcmlwdD4KICAgIAogICAgPHNjcmlwdCBzcmM9Imh0dHBzOi8vY2RuLmpzZGVsaXZyLm5ldC9ucG0vbGVhZmxldEAxLjUuMS9kaXN0L2xlYWZsZXQuanMiPjwvc2NyaXB0PgogICAgPHNjcmlwdCBzcmM9Imh0dHBzOi8vY29kZS5qcXVlcnkuY29tL2pxdWVyeS0xLjEyLjQubWluLmpzIj48L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL21heGNkbi5ib290c3RyYXBjZG4uY29tL2Jvb3RzdHJhcC8zLjIuMC9qcy9ib290c3RyYXAubWluLmpzIj48L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2NkbmpzLmNsb3VkZmxhcmUuY29tL2FqYXgvbGlicy9MZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy8yLjAuMi9sZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy5qcyI+PC9zY3JpcHQ+CiAgICA8bGluayByZWw9InN0eWxlc2hlZXQiIGhyZWY9Imh0dHBzOi8vY2RuLmpzZGVsaXZyLm5ldC9ucG0vbGVhZmxldEAxLjUuMS9kaXN0L2xlYWZsZXQuY3NzIi8+CiAgICA8bGluayByZWw9InN0eWxlc2hlZXQiIGhyZWY9Imh0dHBzOi8vbWF4Y2RuLmJvb3RzdHJhcGNkbi5jb20vYm9vdHN0cmFwLzMuMi4wL2Nzcy9ib290c3RyYXAubWluLmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL21heGNkbi5ib290c3RyYXBjZG4uY29tL2Jvb3RzdHJhcC8zLjIuMC9jc3MvYm9vdHN0cmFwLXRoZW1lLm1pbi5jc3MiLz4KICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9tYXhjZG4uYm9vdHN0cmFwY2RuLmNvbS9mb250LWF3ZXNvbWUvNC42LjMvY3NzL2ZvbnQtYXdlc29tZS5taW4uY3NzIi8+CiAgICA8bGluayByZWw9InN0eWxlc2hlZXQiIGhyZWY9Imh0dHBzOi8vY2RuanMuY2xvdWRmbGFyZS5jb20vYWpheC9saWJzL0xlYWZsZXQuYXdlc29tZS1tYXJrZXJzLzIuMC4yL2xlYWZsZXQuYXdlc29tZS1tYXJrZXJzLmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL3Jhd2Nkbi5naXRoYWNrLmNvbS9weXRob24tdmlzdWFsaXphdGlvbi9mb2xpdW0vbWFzdGVyL2ZvbGl1bS90ZW1wbGF0ZXMvbGVhZmxldC5hd2Vzb21lLnJvdGF0ZS5jc3MiLz4KICAgIDxzdHlsZT5odG1sLCBib2R5IHt3aWR0aDogMTAwJTtoZWlnaHQ6IDEwMCU7bWFyZ2luOiAwO3BhZGRpbmc6IDA7fTwvc3R5bGU+CiAgICA8c3R5bGU+I21hcCB7cG9zaXRpb246YWJzb2x1dGU7dG9wOjA7Ym90dG9tOjA7cmlnaHQ6MDtsZWZ0OjA7fTwvc3R5bGU+CiAgICAKICAgICAgICAgICAgPG1ldGEgbmFtZT0idmlld3BvcnQiIGNvbnRlbnQ9IndpZHRoPWRldmljZS13aWR0aCwKICAgICAgICAgICAgICAgIGluaXRpYWwtc2NhbGU9MS4wLCBtYXhpbXVtLXNjYWxlPTEuMCwgdXNlci1zY2FsYWJsZT1ubyIgLz4KICAgICAgICAgICAgPHN0eWxlPgogICAgICAgICAgICAgICAgI21hcF85YjMwMzkzMTYwYWQ0NjJjYTlkYTBjMmYxNDA2MGNlMSB7CiAgICAgICAgICAgICAgICAgICAgcG9zaXRpb246IHJlbGF0aXZlOwogICAgICAgICAgICAgICAgICAgIHdpZHRoOiAxMDAuMCU7CiAgICAgICAgICAgICAgICAgICAgaGVpZ2h0OiAxMDAuMCU7CiAgICAgICAgICAgICAgICAgICAgbGVmdDogMC4wJTsKICAgICAgICAgICAgICAgICAgICB0b3A6IDAuMCU7CiAgICAgICAgICAgICAgICB9CiAgICAgICAgICAgIDwvc3R5bGU+CiAgICAgICAgCjwvaGVhZD4KPGJvZHk+ICAgIAogICAgCiAgICAgICAgICAgIDxkaXYgY2xhc3M9ImZvbGl1bS1tYXAiIGlkPSJtYXBfOWIzMDM5MzE2MGFkNDYyY2E5ZGEwYzJmMTQwNjBjZTEiID48L2Rpdj4KICAgICAgICAKPC9ib2R5Pgo8c2NyaXB0PiAgICAKICAgIAogICAgICAgICAgICB2YXIgbWFwXzliMzAzOTMxNjBhZDQ2MmNhOWRhMGMyZjE0MDYwY2UxID0gTC5tYXAoCiAgICAgICAgICAgICAgICAibWFwXzliMzAzOTMxNjBhZDQ2MmNhOWRhMGMyZjE0MDYwY2UxIiwKICAgICAgICAgICAgICAgIHsKICAgICAgICAgICAgICAgICAgICBjZW50ZXI6IFszNy41NjY2NTEsIDEyNi45Nzg0MjhdLAogICAgICAgICAgICAgICAgICAgIGNyczogTC5DUlMuRVBTRzM4NTcsCiAgICAgICAgICAgICAgICAgICAgem9vbTogMTIsCiAgICAgICAgICAgICAgICAgICAgem9vbUNvbnRyb2w6IHRydWUsCiAgICAgICAgICAgICAgICAgICAgcHJlZmVyQ2FudmFzOiBmYWxzZSwKICAgICAgICAgICAgICAgIH0KICAgICAgICAgICAgKTsKCiAgICAgICAgICAgIAoKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgdGlsZV9sYXllcl8yMGRhZmEyY2ZkNmM0MTg1ODk5YzgyMWRmMmNmYzAxZSA9IEwudGlsZUxheWVyKAogICAgICAgICAgICAgICAgImh0dHBzOi8ve3N9LnRpbGUub3BlbnN0cmVldG1hcC5vcmcve3p9L3t4fS97eX0ucG5nIiwKICAgICAgICAgICAgICAgIHsiYXR0cmlidXRpb24iOiAiRGF0YSBieSBcdTAwMjZjb3B5OyBcdTAwM2NhIGhyZWY9XCJodHRwOi8vb3BlbnN0cmVldG1hcC5vcmdcIlx1MDAzZU9wZW5TdHJlZXRNYXBcdTAwM2MvYVx1MDAzZSwgdW5kZXIgXHUwMDNjYSBocmVmPVwiaHR0cDovL3d3dy5vcGVuc3RyZWV0bWFwLm9yZy9jb3B5cmlnaHRcIlx1MDAzZU9EYkxcdTAwM2MvYVx1MDAzZS4iLCAiZGV0ZWN0UmV0aW5hIjogZmFsc2UsICJtYXhOYXRpdmVab29tIjogMTgsICJtYXhab29tIjogMTgsICJtaW5ab29tIjogMCwgIm5vV3JhcCI6IGZhbHNlLCAib3BhY2l0eSI6IDEsICJzdWJkb21haW5zIjogImFiYyIsICJ0bXMiOiBmYWxzZX0KICAgICAgICAgICAgKS5hZGRUbyhtYXBfOWIzMDM5MzE2MGFkNDYyY2E5ZGEwYzJmMTQwNjBjZTEpOwogICAgICAgIAo8L3NjcmlwdD4=" style="position:absolute;width:100%;height:100%;left:0;top:0;border:none !important;" allowfullscreen webkitallowfullscreen mozallowfullscreen></iframe></div></div>



# 02)데이터프레임의 행 수만큼 반복하면서 처리


```python
for i in df3.index:
    # 행 우선 접근 방식으로 값 추출하기
    name = df3.loc[i,'학교명']
    lat = df3.loc[i,'위도']
    lng = df3.loc[i,'경도']
    
    
    marker = folium.Marker([lat,lng], popup=name)
    marker.add_to(map_osm)
    
map_osm    
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-8-8fca172ccaf2> in <module>
    ----> 1 for i in df3.index:
          2     # 행 우선 접근 방식으로 값 추출하기
          3     name = df3.loc[i,'학교명']
          4     lat = df3.loc[i,'위도']
          5     lng = df3.loc[i,'경도']
    

    NameError: name 'df3' is not defined



```python

```


```python

```


```python

```
