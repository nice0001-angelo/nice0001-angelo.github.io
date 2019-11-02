## Pandas 시각화

### Pandas와 pyplot의 연계
- pandas의 시리즈나 데이터프레임은 Plot이라는 시각화 함수를 내장하고 있다
- plot은 matplotlib를 내부적으로 임포트하여 사용한다

--------------------------------
## #01. 필요한 패키지 및 샘플 데이터 준비


```python
import numpy
from pandas import DataFrame
from matplotlib import pyplot
from sample import traffic
```


```python
df = DataFrame(traffic)
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
      <th>seoul</th>
      <th>busan</th>
      <th>daegu</th>
      <th>inchun</th>
      <th>month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>3166</td>
      <td>927</td>
      <td>933</td>
      <td>655</td>
      <td>1월</td>
    </tr>
    <tr>
      <td>1</td>
      <td>2728</td>
      <td>857</td>
      <td>982</td>
      <td>586</td>
      <td>2월</td>
    </tr>
    <tr>
      <td>2</td>
      <td>3098</td>
      <td>988</td>
      <td>1049</td>
      <td>629</td>
      <td>3월</td>
    </tr>
    <tr>
      <td>3</td>
      <td>3172</td>
      <td>955</td>
      <td>1032</td>
      <td>669</td>
      <td>4월</td>
    </tr>
    <tr>
      <td>4</td>
      <td>3284</td>
      <td>1014</td>
      <td>1083</td>
      <td>643</td>
      <td>5월</td>
    </tr>
    <tr>
      <td>5</td>
      <td>3247</td>
      <td>974</td>
      <td>1117</td>
      <td>627</td>
      <td>6월</td>
    </tr>
    <tr>
      <td>6</td>
      <td>3268</td>
      <td>1029</td>
      <td>1076</td>
      <td>681</td>
      <td>7월</td>
    </tr>
    <tr>
      <td>7</td>
      <td>3308</td>
      <td>1040</td>
      <td>1080</td>
      <td>657</td>
      <td>8월</td>
    </tr>
    <tr>
      <td>8</td>
      <td>3488</td>
      <td>1058</td>
      <td>1174</td>
      <td>662</td>
      <td>9월</td>
    </tr>
    <tr>
      <td>9</td>
      <td>3312</td>
      <td>971</td>
      <td>1163</td>
      <td>606</td>
      <td>10월</td>
    </tr>
    <tr>
      <td>10</td>
      <td>3375</td>
      <td>958</td>
      <td>1146</td>
      <td>641</td>
      <td>11월</td>
    </tr>
    <tr>
      <td>11</td>
      <td>3179</td>
      <td>982</td>
      <td>1135</td>
      <td>663</td>
      <td>12월</td>
    </tr>
  </tbody>
</table>
</div>



## #02. 데이터 전처리


```python
# 빈 딕셔너리 생성
new_name = {}

# '월'에 대한 컬럼만 리스트로 변환하여 반복처리
for i, v in enumerate(list(df['month'])):
    # 딕셔너리에 {인덱스:값} 형식으로 채워 넣음
    new_name[i] = v

new_name
```




    {0: '1월',
     1: '2월',
     2: '3월',
     3: '4월',
     4: '5월',
     5: '6월',
     6: '7월',
     7: '8월',
     8: '9월',
     9: '10월',
     10: '11월',
     11: '12월'}




```python
# 데이터프레임의 인덱스이름과 컬럼이름 변경
월별교통사고 = df.rename(index=new_name, columns={'seoul':'서울','busan':'부산','daegu':'대구','inchun':'인천'})

#결과확인
월별교통사고
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
      <th>서울</th>
      <th>부산</th>
      <th>대구</th>
      <th>인천</th>
      <th>month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1월</td>
      <td>3166</td>
      <td>927</td>
      <td>933</td>
      <td>655</td>
      <td>1월</td>
    </tr>
    <tr>
      <td>2월</td>
      <td>2728</td>
      <td>857</td>
      <td>982</td>
      <td>586</td>
      <td>2월</td>
    </tr>
    <tr>
      <td>3월</td>
      <td>3098</td>
      <td>988</td>
      <td>1049</td>
      <td>629</td>
      <td>3월</td>
    </tr>
    <tr>
      <td>4월</td>
      <td>3172</td>
      <td>955</td>
      <td>1032</td>
      <td>669</td>
      <td>4월</td>
    </tr>
    <tr>
      <td>5월</td>
      <td>3284</td>
      <td>1014</td>
      <td>1083</td>
      <td>643</td>
      <td>5월</td>
    </tr>
    <tr>
      <td>6월</td>
      <td>3247</td>
      <td>974</td>
      <td>1117</td>
      <td>627</td>
      <td>6월</td>
    </tr>
    <tr>
      <td>7월</td>
      <td>3268</td>
      <td>1029</td>
      <td>1076</td>
      <td>681</td>
      <td>7월</td>
    </tr>
    <tr>
      <td>8월</td>
      <td>3308</td>
      <td>1040</td>
      <td>1080</td>
      <td>657</td>
      <td>8월</td>
    </tr>
    <tr>
      <td>9월</td>
      <td>3488</td>
      <td>1058</td>
      <td>1174</td>
      <td>662</td>
      <td>9월</td>
    </tr>
    <tr>
      <td>10월</td>
      <td>3312</td>
      <td>971</td>
      <td>1163</td>
      <td>606</td>
      <td>10월</td>
    </tr>
    <tr>
      <td>11월</td>
      <td>3375</td>
      <td>958</td>
      <td>1146</td>
      <td>641</td>
      <td>11월</td>
    </tr>
    <tr>
      <td>12월</td>
      <td>3179</td>
      <td>982</td>
      <td>1135</td>
      <td>663</td>
      <td>12월</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 기존의 '월'컬럼은 삭제
월별교통사고.drop('month',axis=1,inplace=True)

# 결과확인
월별교통사고
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
      <th>서울</th>
      <th>부산</th>
      <th>대구</th>
      <th>인천</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1월</td>
      <td>3166</td>
      <td>927</td>
      <td>933</td>
      <td>655</td>
    </tr>
    <tr>
      <td>2월</td>
      <td>2728</td>
      <td>857</td>
      <td>982</td>
      <td>586</td>
    </tr>
    <tr>
      <td>3월</td>
      <td>3098</td>
      <td>988</td>
      <td>1049</td>
      <td>629</td>
    </tr>
    <tr>
      <td>4월</td>
      <td>3172</td>
      <td>955</td>
      <td>1032</td>
      <td>669</td>
    </tr>
    <tr>
      <td>5월</td>
      <td>3284</td>
      <td>1014</td>
      <td>1083</td>
      <td>643</td>
    </tr>
    <tr>
      <td>6월</td>
      <td>3247</td>
      <td>974</td>
      <td>1117</td>
      <td>627</td>
    </tr>
    <tr>
      <td>7월</td>
      <td>3268</td>
      <td>1029</td>
      <td>1076</td>
      <td>681</td>
    </tr>
    <tr>
      <td>8월</td>
      <td>3308</td>
      <td>1040</td>
      <td>1080</td>
      <td>657</td>
    </tr>
    <tr>
      <td>9월</td>
      <td>3488</td>
      <td>1058</td>
      <td>1174</td>
      <td>662</td>
    </tr>
    <tr>
      <td>10월</td>
      <td>3312</td>
      <td>971</td>
      <td>1163</td>
      <td>606</td>
    </tr>
    <tr>
      <td>11월</td>
      <td>3375</td>
      <td>958</td>
      <td>1146</td>
      <td>641</td>
    </tr>
    <tr>
      <td>12월</td>
      <td>3179</td>
      <td>982</td>
      <td>1135</td>
      <td>663</td>
    </tr>
  </tbody>
</table>
</div>



## #02)선 그래프

1)그래프 환경설정


```python
# 한글폰트, 그래픽 크기 설정
pyplot.rcParams["font.family"] = 'Malgun Gothic'
pyplot.rcParams["font.size"] = 16
pyplot.rcParams["figure.figsize"] = (20,10)
```


```python
# x좌표를 의미할 리스트나 배열 생성
xpos = numpy.arange(len(월별교통사고['서울']))
xpos
```




    array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11])




```python
# x좌표에 적용할 텍스트의 리스트 생성
xtext = list(월별교통사고.index)
xtext
```




    ['1월', '2월', '3월', '4월', '5월', '6월', '7월', '8월', '9월', '10월', '11월', '12월']



2) 특정 컬럼에 대한 선 그래프


```python
# 특정컬럼에 대해서만 시각화 하기
월별교통사고['서울'].plot(color='#ff0000')
pyplot.grid()
pyplot.legend()
pyplot.title("2017년 서울의 월별 교통사고")
pyplot.xlabel("월")
pyplot.ylabel("교통사고 수")
pyplot.xticks(xpos, xtext)
pyplot.savefig('2017년 서울의 월별 교통사고.png', dpi =300)
pyplot.show()
```


![png](output_13_0.png)


3) 전체 컬럼에 대한 시각화


```python
# 전체컬럼에 대해서만 시각화 하기
# 월별교통사고.plot(color='#660000')  //google에서 color picker 검색하면 색상값을 찾을 수 있다
# 월별교통사고.plot(color=['#660000','#006600','#000066','#660066']) // 아무 색상값도 지정하지 않으면 알아서 지정된다
월별교통사고.plot()
pyplot.grid()
pyplot.legend()
pyplot.title("2017년 서울의 월별 교통사고")
pyplot.xlabel("월")
pyplot.ylabel("교통사고 수")
pyplot.xticks(xpos, xtext)
pyplot.savefig('2017년 서울의 월별 교통사고.png', dpi =300)
pyplot.show()
```


![png](output_15_0.png)


## #03. 세로 막대 그래프

1) 특정 컬럼에 대한 시각화


```python
# 특정컬럼에 대해서만 시각화 하기
# 월별교통사고['서울'].plot.bar()
# --> rot 파라미터는 x축 텍스트의 각도, 기본값 90 // 기본값으로는 옆으로 글자가 누워있는 상태
# --> width 파라미터는 모든 막대가 공백없이 꽉 찬 상태를 1로 하여 비율적으로 지정. 기본값은 0.5
월별교통사고['서울'].plot.bar(color='#8046eb', rot=0, width=0.7)
pyplot.grid()
pyplot.legend()
pyplot.title("2017년 서울의 월별 교통사고")
pyplot.xlabel("월")
pyplot.ylabel("교통사고 수")
pyplot.xticks(xpos, xtext)
# y축의 범위 설정 // x축의 번위를 설정할 경우에는 xlim(min,max) 사용
pyplot.ylim(2500,3800)

# 그래프에 텍스트 표시하기
for i, v in enumerate(list(월별교통사고['서울'])):
    txt = "%d건" % v
    pyplot.text(i,v,txt, fontsize=14, color ='#ff0000',horizontalalignment='center',verticalalignment='bottom')
pyplot.show()
```


![png](output_17_0.png)


2) 전체 컬럼에 대한 시각화


```python
# 전체 컬럼에 대해서만 시각화 하기
# --> rot 파라미터는 x축 텍스트의 각도. 기본값 90
월별교통사고.plot.bar(rot=0, width=0.85)
pyplot.grid()
pyplot.legend()
pyplot.title("2017년 서울의 월별 교통사고")
pyplot.xlabel("월")
pyplot.ylabel("교통사고 수")
pyplot.xticks(xpos, xtext)
pyplot.ylim(0,4300)
pyplot.show()
```


![png](output_19_0.png)


## #03. 가로 막대 그래프

1)특정컬럼에 대한 시각화


```python
# 특정컬럼에 대해서만 시각화 하기
# 월별교통사고['서울'].plot.barh()
# --> rot 파라미터는 x축 텍스트의 각도, 기본값 90 // 기본값으로는 옆으로 글자가 누워있는 상태
# --> width 파라미터는 모든 막대가 공백없이 꽉 찬 상태를 1로 하여 비율적으로 지정. 기본값은 0.5
월별교통사고['서울'].plot.barh(color='#8046eb', rot=0, width=0.7)
pyplot.grid()
pyplot.legend()
pyplot.title("2017년 서울의 월별 교통사고")
pyplot.xlabel("교통사고 수") #ylabel->xlabel
pyplot.ylabel("월")          #xlabel->ylabel  
pyplot.yticks(xpos, xtext) #xticks -> yticks

# y축의 범위 설정 // x축의 범위를 설정할 경우에는 xlim(min,max) 사용
pyplot.xlim(2500,3550) #ylim -> xlim

# 그래프에 텍스트 표시하기
for i, v in enumerate(list(월별교통사고['서울'])):
    txt = "%d건" % v
    pyplot.text(v,i,txt, fontsize=14, color ='#ff0000',horizontalalignment='left',verticalalignment='center') # i,v -> v,i  center,bottom -> left,center
pyplot.show()
```


![png](output_21_0.png)


2) 전체 컬럼에 대한 시각화


```python
# 전체 컬럼에 대해서만 시각화 하기
# --> rot 파라미터는 x축 텍스트의 각도. 기본값 90
월별교통사고.plot.barh(rot=0, width=0.85)
pyplot.grid()
pyplot.legend()
pyplot.title("2017년 서울의 월별 교통사고")
pyplot.ylabel("월")
pyplot.xlabel("교통사고 수")
pyplot.yticks(xpos, xtext)
pyplot.xlim(0,4300)
pyplot.show()
```


![png](output_23_0.png)


## #04. 파이 그래프

데이터프레임의 특정 컬럼을 지정하여 전체를 기준으로 어느정도의 비율을 차지하는지를 시각화 하는 그래프

1)파이 그래프 기본형


```python
# 각 컬럼별로 합계 구하기 --> 도시별 1년간의 교통사고량
total = 월별교통사고.sum()
total
```




    서울    38625
    부산    11753
    대구    12970
    인천     7719
    dtype: int64




```python
# 구해진 총합을 사용해서 데이터프레임 생성
교통사고합계 = DataFrame(total, columns=['교통사고'])
교통사고합계
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
      <th>교통사고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>서울</td>
      <td>38625</td>
    </tr>
    <tr>
      <td>부산</td>
      <td>11753</td>
    </tr>
    <tr>
      <td>대구</td>
      <td>12970</td>
    </tr>
    <tr>
      <td>인천</td>
      <td>7719</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 데이터프레임의 특정 컬럼에 대한 파이그래프 표시 -> 반드시 특정 컬럼을 지정해야 함
교통사고합계['교통사고'].plot.pie()
pyplot.show()
```


![png](output_27_0.png)


2) 파이 그래프의 옵션 설정


```python
# 라벨
라벨 = ['Seoul','Busan','Daegu','Inchun']

# 각 항목의 색상
색상 = ['#ff6600','#ff00ff','#ffff00','#00ffff']

# 확대비율
비율 = [0.0, 0.0, 0.2, 0.0]

#파이 그래프에 각각의 옵션 적용
교통사고합계['교통사고'].plot.pie(labels=라벨, colors=색상, explode=비율, autopct='%0.2f%%', shadow=True, startangle=90)

# y축 라벨 표시 안함
pyplot.ylabel(None)

# 제목지정
pyplot.title("주요도시의 1년간 교통사고 비율")

pyplot.show()
```


![png](output_29_0.png)



```python
# 아래는 상용구처럼 흔히 쓴다
# pct는 각 섹션의 비율, values는 전체 데이터 리스트
def make_autopct(pct, values):
    total = sum(values)
    val = int(round(pct*total/100.0)) # 퍼센티지*전체값/100 해서 실제 교통사고건수를 역으로 구함
    return '{p:0.2f}%\n({v:d})'.format(p=pct,v=val)

# 파이그래프의 각 섹션 수 만큼 'make_autopic'함수가 호출되고 이 함수 안에서는 각 섹션에 출력할 텍스트를 만들어서 리턴한다
교통사고합계['교통사고'].plot.pie(labels=None, autopct=lambda pct: make_autopct(pct, 교통사고합계['교통사고']), textprops={'color':"#ffffff",'fontsize':18})
    
#교통사고합계['교통사고'].plot.pie(labels=None, textprops={'color':"#ffffff",'fontsize':18})    

pyplot.ylabel(None)

# 범주지정
# labels -> 각 섹션별 제목
# bbox_to_anchor(x,y) -> 0,0을 기준으로 범주의 위치(2차원 좌표)
pyplot.legend(labels=list(교통사고합계.index), bbox_to_anchor=(0.95,0.625))

pyplot.show()
```


![png](output_30_0.png)


## #05. 산점도 그래프

- 두 변수 간의 영향력을 보여주기 위해 가로축과 세로축에 대한 데이터 포인트를 그리는데 사용된다
- 데이터포인트들이 오밀조밀 뭉쳐 있으면 두 변수는 서로 관련성 정도가 높고 흩어져 있으면 관련성이 낮다.

예)여름철 온도와 아이스크림 판매량의 상관관계 분석

- 첫번째변수 : 날짜별 온도
- 두번째변수 : 날짜별 아이스크림 판매량

이 두 변수의 상관관계를 표현한 그래프를 산점도로 표현할 수 있다


```python
# 온도와 아이스크림 판매 수량
data = {
    '기온':[23,25,26,27,28,29,30,32,33],
    '판매량':[2100,2300,2500,2800,3300,3500,3600,3700,3900]
}

df=DataFrame(data)
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
      <th>기온</th>
      <th>판매량</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>23</td>
      <td>2100</td>
    </tr>
    <tr>
      <td>1</td>
      <td>25</td>
      <td>2300</td>
    </tr>
    <tr>
      <td>2</td>
      <td>26</td>
      <td>2500</td>
    </tr>
    <tr>
      <td>3</td>
      <td>27</td>
      <td>2800</td>
    </tr>
    <tr>
      <td>4</td>
      <td>28</td>
      <td>3300</td>
    </tr>
    <tr>
      <td>5</td>
      <td>29</td>
      <td>3500</td>
    </tr>
    <tr>
      <td>6</td>
      <td>30</td>
      <td>3600</td>
    </tr>
    <tr>
      <td>7</td>
      <td>32</td>
      <td>3700</td>
    </tr>
    <tr>
      <td>8</td>
      <td>33</td>
      <td>3900</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 산점도 그래프는 두 컬럼(변수)간의 관계를 분석하기 위해 사용된다.
# marker -> o,v,^,<,>,8,s,p,*,h,H,D,d,P,X
df.plot.scatter(x='기온',y='판매량',color='#ff6600',marker='x',label='판매수량')
pyplot.grid()
pyplot.title("기온과 아이스크림 판매량의 상관관계")
pyplot.ylabel('아이스크림 판매수량')
pyplot.xlabel('기온')
pyplot.show()
```


![png](output_33_0.png)


# KOSIS : 국가정보포털에서 필요한 데이터 받아서 처리한다.<br>
# --> 원하는거 필터걸고 엑셀로 다운로드 받아서 처리한다


```python

```
