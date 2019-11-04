---
layout: post
title:  "24. Naver Login"
---

# 네이버 로그인

## Chromedriver 다운로드

크롬 브라우저를 제어할 수 있는 프로그램

https://chromedriver.chromium.org/downloads에서 다운로드
    
현재 사용중인 프라우저 버전에 맞는 파일 선택해야 함

## #01. 필요한 패키지 참조

> pip install --upgrade selenuim


```python
import time                                      #(내장모듈) 브라우저가 페이지를 로딩하는 동안 sleep처리를 하는 모듈
from selenium import webdriver                   # 크롬 제어를 위한 모듈
from selenium.webdriver.support.wait import WebDriverWait
from bs4 import BeautifulSoup
```

## #02.브라우저 제어를 위한 객체 생성

chromedriver.exe의 경로를 상대/절대 경로 형식으로 지정한다.

> 아래 블록이 실행되면 별도의 크롬브라우저가 실행된다. 해당 창을 닫으면 안된다.


```python
# 객체 생성
driver = webdriver.Chrome('chromedriver.exe')
# 암묵적으로 웹 자원 로드를 위해 10초까지 기다려 준다.
driver.implicitly_wait(10)
```

## #03.네이버 로그인하기

1)네이버 로그인 페이지로 이동하기


```python
# 네이버 로그인 페이지 접속
driver.get('https://nid.naver.com/nidlogin.login')
# 접속하는 동안 프로그램 대기(3초)
time.sleep(3)
```

2) 네이버 로그인 아이디, 비밀번호 입력

크롬 브라우저로 하여금 javascript 명령을 실행하도록 한다


```python
myid = 'nice00001'
mypw = '~~~~~~~'

# -> 전체문서(document)에서 id값에 의해(ById) 요소(Element)를 가져온 후 (get) 입력값(value)을 지정
script = "document.getElementById('id').value='%s'"
driver.execute_script(script % myid)

script = "document.getElementById('pw').value='%s'"
driver.execute_script(script % mypw)
```

3) 로그인 버튼 클릭


```python
# bs4와 같은 방식으로 CSS 셀렉터가 ".bnt_global"인 요소 취득
btn = driver.find_element_by_css_selector(".btn_global")

# 취득한 버튼을 클릭시킴 --> 로그인
btn.click()
```


```python

```


```python

```


```python

```


```python

```
