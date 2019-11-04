---
layout: post
title:  "20. Naver News Gathering(1)"
---

# 네이버 뉴스 기사 수집

## 용어정리
### 1) Web Scrapping(웹 스크렙핑)

컴퓨터 소프트웨어 기술로 웹 사이트들에서 원하는 정보를 추출하는 것

국내에서는 흔히 크롤링이라는 용어로 많이 알려져 있다

> 하나의 페이지에서 데이터 수집

### 2) 웹 크롤러

인터넷에 있는 웹 사이트를 방문해서 자료를 수집하는 일을 하는 프로그램.

엄청난 분량의 웹문서를 사람이 일일히 구별해서 모으는 일은 불가능에 가깝기 때문에,

웹 문서 검색에서는 이를 자동으로 수행해 준다.

> 링크를 따라다니면서 복수의 페이지에서 데이터를 수집

--------------------------------------------

## #01. 필요한 모듈 참조

>> pip install -update requests
>> pip install -update bs4


```python
import requests                           #-> 웹페이지 요청 모듈
from bs4 import BeautifulSoup             #-> 웹페이지 소스코드 분석 모듈
```

## #02. 수집 준비

1) 접속을 수행하기 위한 session 객체 생성
-- 웹페이지로부터 데이터를 수집할 경우 항상 가장 처음에 위치해아하는 코드입니다.


```python
# 접속 세션 만들기
user_agent = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/77.0.3865.120 Safari/537.36"

session = requests.Session()
session.headers.update({'User-agent':user_agent, 'referer':None})
```

2) 접근할 페이지주소(네이버 뉴스 기사)


```python
content_url = "https://news.naver.com/main/read.nhn?mode=LSD&mid=shm&sid1=101&oid=277&aid=0004565025"
```

## #03. 데이터 가져오기


```python
r = session.get(content_url)

#-> 결과확인
if r.status_code != 200:
    print("%d 에러가 발생했습니다." % r.status_code)
    # 즉시 종료 --> jupyter가 재시작됨
    quit()
```


```python
# 가져온 HTML 코드 확인
# -> 웹 페이지의 인코딩 형식을 확인하여 설정해야 한다.
r.encoding = "euc-kr"
print(r.text)
```

    <!DOCTYPE HTML> 
    <html lang="ko"> 
    <head>
    <meta charset="euc-kr">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="referrer" contents="always">
    <meta name="viewport" content="width=1106" />
    <title>11개월 연속 줄어든 수출…10월 감소폭 3년9개월來 최대 : 네이버 뉴스</title>
    
    
    	
    	
    		
    	
    
    
    	
    	
    	
    		
    		
    		
    	
    
    <meta property="me2:post_tag"		content="아시아경제 : 네이버뉴스"/>
    <meta property="me2:category1"		content="아시아경제"/>
    <meta property="me2:category2"		content="경제"/>
    <meta property="me2:image"			content="https://imgnews.pstatic.net/image/277/2019/11/02/0004565025_001_20191102080925359.jpg"/>
    
    <meta property="og:title"			content="11개월 연속 줄어든 수출…10월 감소폭 3년9개월來 최대"/>
    <meta property="og:type"			content="article"/>
    <meta property="og:url"				content="https://news.naver.com/main/read.nhn?mode=LSD&mid=sec&oid=277&aid=0004565025&sid1=001"/>
    <meta property="og:image"			content="https://imgnews.pstatic.net/image/277/2019/11/02/0004565025_001_20191102080925359.jpg"/>
    <meta property="og:description"		content="[세종=아시아경제 주상돈 기자] 지난달 수출이 또 줄어들며 지난해 12월부터 시작된 감소세가 11개월째 이어졌다. 감소율은 14.7%로 앞선 3년9개월 만의 최대폭을 기록했다. 2일 산업통상자원부에 따르면 10월 수"/>
    <meta property="og:article:author"	content="아시아경제 | 네이버"/>
    
    <meta name="twitter:card"			content="summary_large_image">
    <meta name="twitter:title"			content="11개월 연속 줄어든 수출…10월 감소폭 3년9개월來 최대">
    <meta name="twitter:site"			content="네이버 뉴스">
    <meta name="twitter:creator"		content="아시아경제">
    <meta name="twitter:image"			content="https://imgnews.pstatic.net/image/277/2019/11/02/0004565025_001_20191102080925359.jpg">
    <meta name="twitter:description"	content="[세종=아시아경제 주상돈 기자] 지난달 수출이 또 줄어들며 지난해 12월부터 시작된 감소세가 11개월째 이어졌다. 감소율은 14.7%로 앞선 3년9개월 만의 최대폭을 기록했다. 2일 산업통상자원부에 따르면 10월 수">
    
    
    
    	
    	
    		<meta name="napp-site-analysis" content="gdid=88000385_000000000000000004565025,service=news,collection=news">
    	
    
    <link rel="shortcut icon" type="image/x-icon" href="https://ssl.pstatic.net/static.news/image/news/2014/favicon/favicon.ico" />
    
    
    
    	
    	
    	
    
    
    	
    	
    		<link rel="stylesheet" type="text/css" href="https://ssl.pstatic.net/static.news/pnews/resources/20191030_165315/css/common.css"/>
    		<link rel="stylesheet" type="text/css" href="https://ssl.pstatic.net/static.news/pnews/resources/20191030_165315/css/news.css"/>
    		
    		
    	
    	
    
    
    
    
    
    
    <script type="text/javascript" src="https://ssl.pstatic.net/static.news/pnews/resources/20191030_165315/js/news.jindo.js" charset="euc-kr"></script>
    
    
    
    
    <script type="text/javascript" src="https://ssl.pstatic.net/static.news/pnews/resources/20191030_165315/js/news.jquery.js" charset="utf-8"></script>
    
    
    
    
    
    	
    	
    	
    	
    	
    	
    	
    		
    		
    	
    	
    	
    	
    	
    	
    	
    	
    	
    	
    	
    	
    	
    	
    	
    	
    	
    		
    	
    	
    
    
    
    
    	
    		
    		
    			
    		
    	
    
    
    
    <script type="text/javascript">
    document.domain='naver.com';
    var _MAIN_NEWS_MENU_ID='shm';
    var _MAIN_NEWS_SECTION_ID='103';
    var ccsrv='cc.naver.com';
    var g_ssc='news.art';
    window.nsc = g_ssc; 
    var gnb_service='news';
    var gnb_logout=encodeURIComponent(location.href);
    var gnb_template='gnb_utf8';
    var gnb_brightness = 1;
    var gnb_one_naver = 1;
    var gnb_searchbox='on';
    var gnb_shortnick='on';
    
    var gnb_timestamp = "Sat Nov 02 09:59:12 KST 2019";
    </script>
    
    
    
    
    <script type="text/javascript" src="https://ssl.pstatic.net/static.news/pnews/resources/20191030_165315/js/news.service.js" charset="euc-kr"></script>
    
    <script type="text/javascript" src="https://ssl.pstatic.net/static.news/pnews/resources/20191030_165315/js/nil.news.js" charset="utf-8"></script>
    
    
    
    
    
    <meta http-equiv="X-UA-Compatible" content="IE=9; IE=8; IE=7" />
    </head>
    <body class="chrome">
    <div id="wrap">
    	
    	<div id="da_base"></div>
    	<div id="da_stake"></div>
    	
    
    
    <div id="header" class="header">
    	
    	<div id="u_skip">
    		<a href="#lnb" tabindex="1"><span>메인 메뉴로 바로가기</span></a>
    		<a href="#main_content" tabindex="2"><span>본문으로 바로가기</span></a>
    	</div>
    	
    
    	<div class="snb_area">
    		<div class="snb_inner">
    			<div class="gnb_wrap">
       <!-- GNB 마크업 -->
       <div id="gnb"></div>
       <!-- //GNB 마크업 -->
    </div>
    			
    
    
    <div id="snb_wrap">
        <h1>
            <a href="https://www.naver.com/" class="h_logo nclicks(STA.naver)"><span class="blind">NAVER</span></a>
            <a href="/" class="h_news nclicks(STA.news)"><span class="blind">뉴스</span></a>
        </h1>
        <ul class="snb_related_service">
            <li><span class="snb_bdr"></span><a href="https://entertain.naver.com/home" class="nclicks(STA.enter)"><img src="https://imgnews.pstatic.net/image/news/2017/10/snb_h_entertain.png" width="52" height="19" alt="TV연예"></a></li>
    <li><span class="snb_bdr"></span><a href="https://sports.news.naver.com" class="nclicks(STA.sports)"><img src="https://imgnews.pstatic.net/image/news/2017/10/snb_h_sports.png" width="48" height="19" alt="스포츠"></a></li>
    <li><span class="snb_bdr"></span><a href="https://newsstand.naver.com" class="nclicks(STA.newsstand)"><img src="https://imgnews.pstatic.net/image/news/2017/10/snb_h_newsstand.png" width="77" height="19" alt="뉴스스탠드"></a></li>
    <li><span class="snb_bdr"></span><a href="https://weather.naver.com" class="nclicks(STA.weather)"><img src="https://imgnews.pstatic.net/image/news/2017/10/snb_h_weather.png" width="31" height="19" alt="날씨"></a></li>
    
    
            
        </ul>
    </div>
    		</div>
    	</div>
    	<div class="lnb_area">
    		<div class="lnb_inner">
    			
    
    
    
    
    
    
    <div id="lnb" class="lnb_menu">
    	<ul>
    		<li><a href="/main/home.nhn" class="nclicks(LNB.home)"><span class="tx">뉴스홈</span> </a></li>
    		<li><a href="/main/list.nhn?mode=LSD&mid=sec&sid1=001" class="nclicks(LNB.flash)"><span class="tx">속보</span></a></li>
    		<li><a href="/main/main.nhn?mode=LSD&mid=shm&sid1=100" class="nclicks(LNB.pol)"><span class="tx">정치</span> </a></li>
    		<li class="on"><a href="/main/main.nhn?mode=LSD&mid=shm&sid1=101" class="nclicks(LNB.eco)"><span class="tx">경제</span> <span class="blind">선택됨</span></a></li>
    		<li><a href="/main/main.nhn?mode=LSD&mid=shm&sid1=102" class="nclicks(LNB.soc)"><span class="tx">사회</span> </a></li>
    		<li><a href="/main/main.nhn?mode=LSD&mid=shm&sid1=103" class="nclicks(LNB.lif)"><span class="tx">생활/문화</span> </a></li>
    		<li><a href="/main/main.nhn?mode=LSD&mid=shm&sid1=104" class="nclicks(LNB.wor)"><span class="tx">세계</span> </a></li>
    		<li><a href="/main/main.nhn?mode=LSD&mid=shm&sid1=105" class="nclicks(LNB.sci)"><span class="tx">IT/과학</span> </a></li>
    		<li><a href="/main/opinion/home.nhn" class="nclicks(LNB.opi)"><span class="tx">오피니언</span> </a></li>
    		<li><a href="/main/photo/index.nhn?mid=pho" class="nclicks(LNB.pho)"><span class="tx">포토</span> </a></li>
    		<li><a href="/main/tv/index.nhn?mid=tvh" class="nclicks(LNB.tv)"><span class="tx">TV</span> </a></li>
    		<li><a href="/main/ranking/popularDay.nhn?mid=etc&sid1=111" class="nclicks(LNB.ranking)"><span class="tx">랭킹뉴스</span> </a></li>
    	</ul>
    	<form name="lnb_searchForm" id="lnb.searchForm" method="get" action="https://search.naver.com/search.naver" target="_blank" accept-charset="UTF-8">
    		<fieldset>
    			<legend>뉴스 검색</legend>
    			<input type="text" title="뉴스 검색" name="query" accesskey="s" class="text_index" style="ime-mode:active;"/>
    			<input type="hidden" name="where" value="news">
    			<input type="hidden" name="ie" value="utf8">
    			<input type="hidden" name="sm" value="nws_hty">
    			<button type="submit" class="btn_search_lnb nclicks(LNB.search)"><span class="tx"><span class="blind">검색</span></span></button>
    		</fieldset>
    	</form>
    </div>
    		</div>
    	</div>
    
    	
    
    
    
        <div class="lnb">
            
            
            
            
            <span class="lnb_date"><strong>11</strong>.<strong>02</strong><span class="day">(토)</span></span>
    
            
    
            
     <div class="lnb_today">
    	
    	<h3>헤드라인 뉴스</h3>
    	<div id="lnb.mainnews">
    		<ul>
    		
    			<li>
    			
    			<a href="https://news.naver.com/main/read.nhn?mode=LSD&mid=shm&sid1=102&oid=422&aid=0000399373" class="nclicks(nct.maintxt,,1)" title = "독도 수중수색 재개&hellip;가족들 사고해역으로">독도 수중수색 재개&hellip;가족들 사고해역으로</a>
    			</li>
    		
    			<li>
    			
    			<a href="https://news.naver.com/main/read.nhn?mode=LSD&mid=shm&sid1=100&oid=011&aid=0003644782" class="nclicks(nct.maintxt,,2)" title = "비건의 위상 강화가 북미 비핵화 협상에 미칠 영향">비건의 위상 강화가 북미 비핵화 협상에 미칠 영향</a>
    			</li>
    		
    			<li>
    			
    			<a href="https://news.naver.com/main/read.nhn?mode=LSD&mid=shm&sid1=104&oid=001&aid=0011185181" class="nclicks(nct.maintxt,,3)" title = "美-中 무역대표단 전화접촉&hellip;&quot;진전&quot; vs &quot;원칙적 공감대&quot;(종합)">美-中 무역대표단 전화접촉&hellip;&quot;진전&quot; vs &quot;원칙적 공감대&quot;(…</a>
    			</li>
    		
    			<li>
    			
    			<a href="https://news.naver.com/main/read.nhn?mode=LSD&mid=shm&sid1=104&oid=001&aid=0011185147" class="nclicks(nct.maintxt,,4)" title = "폼페이오, 北비핵화 &quot;진전 너무 더뎌&hellip;몇달내 좋은 결과 희망&quot;(종합)">폼페이오, 北비핵화 &quot;진전 너무 더뎌&hellip;몇달내 좋은 결과 …</a>
    			</li>
    		
    			<li>
    			
    			<a href="https://news.naver.com/main/read.nhn?mode=LSD&mid=shm&sid1=101&oid=629&aid=0000002855" class="nclicks(nct.maintxt,,5)" title = "국토부 &#39;분양가 상한제&#39; 적용지역, 집값 요동치는 &#39;비강남권&#39;도 사정권">국토부 &#39;분양가 상한제&#39; 적용지역, 집값 요동치는 &#39;비강…</a>
    			</li>
    		
    			<li>
    			
    			<a href="https://news.naver.com/main/read.nhn?mode=LSD&mid=shm&sid1=102&oid=214&aid=0000990722" class="nclicks(nct.maintxt,,6)" title = "성추행 해놓고 &#39;면책특권&#39; 거짓말&hellip;처벌 어떻게?">성추행 해놓고 &#39;면책특권&#39; 거짓말&hellip;처벌 어떻게?</a>
    			</li>
    		
    			<li>
    			
    			<a href="https://news.naver.com/main/read.nhn?mode=LSD&mid=shm&sid1=104&oid=025&aid=0002949741" class="nclicks(nct.maintxt,,7)" title = "&quot;냉동 컨테이너 사망 39명, 중국인 아닌 전원 베트남인 추정&quot;">&quot;냉동 컨테이너 사망 39명, 중국인 아닌 전원 베트남인 …</a>
    			</li>
    		
    		</ul>
    	</div>
    	
     </div>
             <ul class="lnb_side" tabindex="0">
    <li>
    <a href="https://news.naver.com/main/factcheck/main.nhn" class="nclicks(nct.right1)"
    title="팩트체크"
    >팩트체크
    </a>
    </li>
    <li>
    <a href="https://media.naver.com/channel/settings.nhn  " class="nclicks(nct.right2)"
    title="언론사 구독 "
    target="_blank">언론사 구독
    </a>
    </li>
    <li>
    <a href="https://news.naver.com/main/officeList.nhn" class="nclicks(nct.right3)"
    title="언론사 뉴스"
    >언론사 뉴스
    </a>
    </li>
    <li class="end">
    <a href="https://newslibrary.naver.com/search/searchByDate.nhn" class="nclicks(nct.right4)"
    title="라이브러리"
    target="_blank">라이브러리
    </a>
    </li>
    </ul>
    
    
        </div>
    
    </div>
    	<hr>
    	<hr>
    	
    	<table cellpadding="0" cellspacing="0" class="container" role="presentation">
    	   <colgroup>
    		   <col class="col_content">
    		   <col class="col_aside">
            </colgroup>
    		<tr>
    			<td class="content">
    				<div id="main_content" class="content">
    					<script type="text/javascript">
        if (nil) {
            nil.init('naver_news', '277');
            
            nil.add({
                'uri': 'http://news.naver.com/main/read.nhn?oid=277&aid=0004565025',
                'dimension_1': '%EA%B2%BD%EC%A0%9C'
                , 'dimension_3': '55533'
                , 'dimension_4': 'photo'
                
            });
            //cv 측정
            nil.send('cv', 'post_view');
    
            if (window.attachEvent) {
                window.attachEvent("onunload", function () {
                    nil.send('leave');
                });
            } else if (window.addEventListener) {
                window.addEventListener("unload", function () {
                    nil.send('leave');
                }, false);
            } else {
                var fnOnUnload = window.onunload;
                window.onunload = function () {
                    nil.send('leave');
                    fnOnUnload();
                };
            }
        }
    </script>
    
    <script type="text/javascript">
        if (typeof window.ReadingObserver !== 'undefined') {
            ReadingObserver.start('articleBody', {
                sContentBottomId: 'spiLayer',
                oid: '277',
                aid: '0004565025',
                sid: '101',
                articleType: '1',
                hitRefererType: 'UNKNOWN',
                gdid: '88000385_000000000000000004565025'
            });
        }
    </script>
    
    
    
    
    <!-- test -->
    
    
    
    
    <!-- 기사 헤더 -->
    
    
    
    
    
    
    
    
    <div class="article_header">
    	<div class="press_logo">
    		
    		
    			
    			<a href="https://www.asiae.co.kr/" target="_blank" class="nclicks(atp_press)"><img src='https://mimgnews.pstatic.net/image/upload/office_logo/277/2017/12/27/logo_277_38_20171227165227.png' height='35' alt='아시아경제' title='아시아경제' class='' ></a>
    		
    	</div>
    	
    <div class="head_channel" style="display: none;">
        <button type="button" class="head_channel_button nclicks(atp_pick)">
            <i class="head_channel_pick">PICK</i>
            <i class="head_channel_info">안내</i>
        </button>
        <p class="head_channel_layer" style="display: none;">
            <span class="head_channel_layer_text">해당 언론사가 주요기사로<br>직접 선정한 기사입니다.</span>
            <a href="https://news.naver.com/main/static/channelPromotion.html" target="_blank" class="head_channel_layer_link">언론사 편집판 바로가기</a>
            <button type="button" class="head_channel_layer_close">닫기</button>
        </p>
    </div>
    <script type="text/javascript">
        jindo.$Fn(function () {
            var params = getLocationQueryParams();
            var url = "/main/ajax/channel/isPickedArticle.nhn?oid=" + params.oid + "&aid=" + params.aid;
            var oAjax = jindo.$Ajax(url, {
                method: "get",
                onload: function (res) {
                    var isPicked;
                    try {
                        isPicked = res.json();
                    } catch (e) {
                        return;
                    }
    
                    if (!isPicked) {
                        return;
                    }
    
                    initChannelPickBanner();
                }
            });
    
            oAjax.request();
    
            function initChannelPickBanner() {
                var welHeadTop = jindo.$ElementList(".article_header").getFirst();
                var welLogo = jindo.$Element(welHeadTop.query(".head_channel"));
                var welLayer = jindo.$Element(welLogo.query(".head_channel_layer"));
                var welChannelPickBannerBtn = jindo.$Element(welLogo.query(".head_channel_button"));
                var layerAutoCloseManager = LayerAutoCloseManager.get_instance();
    
                var layerForAutoCloseMananger = {
                    close: function () {
                        welLayer.hide();
                    },
                    isAutoCloseExceptionEl: function (el) {
                        // toggle button일 경우 예외
                        return (welChannelPickBannerBtn.$value() === el) || welChannelPickBannerBtn.isParentOf(el);
                    }
                };
    
                jindo.$Fn(function (evt) {
                    welLayer.toggle();
    
                    // open 이라면 적용
                    if (welLayer.visible()) {
                        layerAutoCloseManager.setCurrentVisibleLayer(layerForAutoCloseMananger);
                    }
                }).attach(welChannelPickBannerBtn, "click");
    
                jindo.$Fn(function (evt) {
                    var wel = jindo.$Element(evt.currentElement);
                    evt.stop();
                    window.open(wel.attr("href"), "", "width=460, height=496");
                }).attach(jindo.$Element(welLayer.query(".head_channel_layer_link")), "click");
    
                welLogo.show();
            }
    
            function getLocationQueryParams() {
                var params = {};
                var kv = [];
                var queryString = location.search.substr(1);
                var paramStrList;
                if (queryString) {
                    paramStrList = queryString.split("&");
                    for (var i = 0, len = paramStrList.length; i < len; i++) {
                        kv = paramStrList[i].split("=");
                        params[kv[0]] = kv[1];
                    }
                }
    
                return params;
            }
        }).attach(window, "load");
    </script>
    	<div class="article_info">
    		<h3 id="articleTitle">11개월 연속 줄어든 수출…10월 감소폭 3년9개월來 최대</h3>
    		<div class="sponsor">
    			<!-- 기사 헤더 > 정보 -->
    
    
    
    
    기사입력 <span class="t11">2019.11.02. 오전 8:08</span>
    
    
    
    	
    	
    
    
    <!-- // 기사 헤더 > 정보 -->
    				
    					<a href="https://view.asiae.co.kr/article/2019110116401413932" target="_blank" class="btn_artialoriginal nclicks(are.ori,'277', 'nilGParam', '277_049d58f13b193cb1')">기사원문</a>
    				
    				<a href="/main/scrap/folderList.nhn?scrapItem.officeId=277&scrapItem.articleId=0004565025" class="btn_scrap nclicks(atp_scrap)" title="스크랩" target="_blank">스크랩</a>
    				<!-- 영문뉴스 듣기 -->
    
    	<div class="tts_svc">
    		<!-- [D] 국문기사 경우 : tts 아이콘 클릭했을때 .tts_voice 에 on 클래스를 추가해주세요. / on 일때 대체텍스트 '듣는중..'으로 변경 -->
    		<!-- [D] 영문기사 경우 : 버튼 클릭시 .tts_popup 팝업레이어 display:block 처리 -->
    		<button type="button" class="tts_voice nclicks(tts_play)" title="텍스트 음성 변환 서비스">
    			<span class="tts_voice_ico"></span>
    			<span class="tts_voice_txt">본문듣기</span>
    		</button>
    		<i class="tts_bar"></i>
            <button type="button" class="tts_setting nclicks(tts_set)" title="텍스트 음성 변환 설정">
                <span class="tts_setting_txt">설정</span>
            </button>
    		<div class="tts_popup " style="display: none;">
    	        <div class="tts_spd_select _tts_gender_select">
    	            <span class="blind">성별 선택하기</span>
    	            <!-- [D] 선택 : <span class="spd_btn--on">선택된 속도</span> 추가 -->
    	            <a href="#" id="gender_sel_f" class="_gender_btn nclicks(tts_female)" data-value="f"><span class="spd_btn"></span>여성</a>
    	            <a href="#" id="gender_sel_m" class="_gender_btn nclicks(tts_male)" data-value="m"><span class="spd_btn spd_btn--on">선택된 성별</span>남성</a>
    	        </div>
    	        <i class="tts_spd_bar"></i>
    	        <div class="tts_spd_select _tts_spd_select">
    		      <span class="blind">속도 선택하기</span>
                  <!-- [D] 선택 : <span class="spd_btn--on">선택된 속도</span> 추가 -->
                  <a href="#" id="speed_sel3" class="_spdbar_btn nclicks(tts_speed)" data-value="3"><span class="spd_btn"></span>느림</a>
                  <a href="#" id="speed_sel2" class="_spdbar_btn nclicks(tts_speed)" data-value="2"><span class="spd_btn spd_btn--on">선택된 속도</span>보통</a>
                  <a href="#" id="speed_sel0" class="_spdbar_btn nclicks(tts_speed)" data-value="0"><span class="spd_btn"></span>빠름</a>
                </div>
                <div class="tts_save">
                  <p class="tts_save__text">설정을 저장하시겠습니까?</p>
                  <a href="#" class="tts_save__btn _spd_save_btn nclicks(tts_save)">확인</a>
                  <a href="#" class="tts_save__btn _spd_cancel_btn nclicks(tts_cancel)">취소</a>
                </div>
            </div>
    	</div>
    	<div id="tts_player_div" style="display:none;"></div>
    
    	<script type="text/javascript">
    	var ttsPlayer = new nhn.NewsTTSPlayer({
    		sOfficeId	:'277',
    		sArticleId	:'0004565025',
    		sNationText : 'ko'
    	});
    	</script>
    
    				<div class="article_btns">
    					
    					<div class="article_btns_left">
    						<div class="_reactionModule u_likeit" data-sid="NEWS" data-cid="ne_277_0004565025" style="visibility: hidden" >
    							<a class="u_likeit_button _face nclicks(RTL.face)" data-label="news" href="#" aria-haspopup="true" aria-pressed="false">
    								<span class="u_likeit_icons _icons">
    									<span class="u_likeit_icon __reaction__like"><span class="u_likeit_blind">좋아요</span></span>
    								</span>
    								<span class="u_likeit_blind">좋아요 평가하기</span>
    								<span class="u_likeit_text _count">공감</span>
    							</a>
    							<ul class="u_likeit_layer _faceLayer" role="menu">
    								<li class="u_likeit_list good" role="menuitem">
    									<a class="u_likeit_list_button _button" data-type="like"  data-log="RTL.like|RTL.unlike" href="#" role="button" aria-selected="false">
    										<span class="u_likeit_list_name _label">좋아요</span>
    										<span class="u_likeit_list_count _count">0</span>
    									</a>
    								</li>
    								<li class="u_likeit_list warm" role="menuitem">
    									<a class="u_likeit_list_button _button" data-type="warm" data-log="RTL.warm|RTL.unwarm" href="#" role="button" aria-selected="false">
    										<span class="u_likeit_list_name _label">훈훈해요</span>
    										<span class="u_likeit_list_count _count">0</span>
    									</a>
    								</li>
    								<li class="u_likeit_list sad" role="menuitem">
    									<a class="u_likeit_list_button _button" data-type="sad" data-log="RTL.sad|RTL.unsad" href="#" role="button" aria-selected="false">
    										<span class="u_likeit_list_name _label">슬퍼요</span>
    										<span class="u_likeit_list_count _count">0</span>
    									</a>
    								</li>
    								<li class="u_likeit_list angry" role="menuitem">
    									<a class="u_likeit_list_button _button" data-type="angry" data-log="RTL.angry|RTL.unangry" href="#" role="button" aria-selected="false">
    										<span class="u_likeit_list_name _label">화나요</span>
    										<span class="u_likeit_list_count _count">0</span>
    									</a>
    								</li>
    								<li class="u_likeit_list want" role="menuitem">
    									<a class="u_likeit_list_button _button" data-type="want" data-log="RTL.want|RTL.unwant" href="#" role="button" aria-selected="false">
    										<span class="u_likeit_list_name _label">후속기사 원해요</span>
    										<span class="u_likeit_list_count _count">0</span>
    									</a>
    								</li>
    							</ul>
    						</div>
    						<a href="#" class="pi_btn_count nclicks(atp_reply)" id="articleTitleCommentCount">
    							<span class="blind pi_btn_count_blind">댓글</span><span class="lo_txt"></span>
    						</a>
    					</div>
    					
    					<div class="article_btns_right">
    						
    						
    							<div class="media_end_head_autosummary _auto_summary_wrapper">
    								<a href="javascript:;" class="media_end_head_autosummary_button _toggle_btn nclicks(sum_summary)">요약봇<span class="media_end_head_autosummary_icon_beta"><span class="blind">beta</span></span></a>
    								<div class="media_end_head_autosummary_layer _auto_summary_contents">
    									<div class="media_end_head_autosummary_layer_head">
    										<strong class="media_end_head_autosummary_layer_head_tit">요약봇<span class="media_end_head_autosummary_icon_beta"><span class="blind">beta</span></span><a href="https://help.naver.com/support/alias/news/news_20.naver?" class="media_end_head_autosummary_help nclicks(sum_help)" target="_blank">도움말</a></strong>
    										<span class="media_end_head_autosummary_layer_head_txt">자동 추출 기술로 요약된 내용입니다. 요약 기술의 특성상 본문의 주요 내용이 제외될 수 있어, 전체 맥락을 이해하기 위해서는<br>기사 본문 전체보기를 권장합니다.</span>
    									</div>
    									<div class="media_end_head_autosummary_layer_body">
    										<div class="_contents_body"></div>
    										<div class="_autosummary_feedback" style="display:none;">
    											<div class="media_end_head_autosummary_feedback _done_message">
    												<strong>자동 요약 결과가 어땠나요?</strong>
    												<span class="media_end_head_autosummary_feedback_completion">소중한 의견이 반영되었습니다.</span>
    											</div>
    											<div class="media_end_head_autosummary_feedback _feedback_ui">
    												<strong>자동 요약 결과가 어땠나요?</strong>
    												<div class="media_end_head_autosummary_feedback_btn">
    													<div class="_reactionModule u_likeit" data-sid="NEWS_SUMMARY" data-cid="277_0004565025">
    														<ul class="u_likeit_layer _faceLayer" role="menu">
    															<li class="u_likeit_list like" role="menuitem">
    																<a class="u_likeit_list_button _button nclicks(sum_satis)" href="javascript:;" data-type="like" role="button" aria-selected="false">
    																	<span class="u_likeit_list_name _label">만족</span>
    																</a>
    															</li>
    															<li class="u_likeit_list normal" role="menuitem">
    																<a class="u_likeit_list_button _button nclicks(sum_average)" href="javascript:;" data-type="normal" role="button" aria-selected="false">
    																	<span class="u_likeit_list_name _label">보통</span>
    																</a>
    															</li>
    															<li class="u_likeit_list toobad" role="menuitem">
    																<a class="u_likeit_list_button _button nclicks(sum_dissatis)" href="javascript:;" data-type="toobad" role="button" aria-selected="false">
    																	<span class="u_likeit_list_name _label">불만족</span>
    																</a>
    															</li>
    														</ul>
    													</div>
    												</div>
    											</div>
    										</div>
    									</div>
    									<span class="media_end_head_autosummary_blur"></span>
    									<a href="javascript:;" class="media_end_head_autosummary_layer_close _close_button nclicks(sum_close)"><span class="blind">닫기</span></a>
    								</div>
    							</div>
    						
    						
    						
    							<div class="media_end_head_fontsize _font_setting_menu_wrapper">
    								<a href="javascript:;" class="media_end_head_fontsize_set _toggle_btn nclicks(fnt_set)"><span class="blind">글자 크기 변경하기</span></a>
    								<div class="media_end_head_fontsize_setlayer">
    									<div class="media_end_head_fontsize_setlayer_section _font_size_option">
    										<strong class="media_end_head_fontsize_setlayer_section_tit">크기</strong>
    										<ul class="media_end_head_fontsize_setlayer_select">
    											<li class="media_end_head_fontsize_option1 _opt" data-value="size1">
    												<a href="javascript:;" class="media_end_head_fontsize_option_text nclicks(fnt_size)">가<em class="blind">1단계</em></a>
    											</li>
    											<li class="media_end_head_fontsize_option2 _opt" data-value="size2">
    												<a href="javascript:;" class="media_end_head_fontsize_option_text nclicks(fnt_size)">가<em class="blind">2단계</em></a>
    											</li>
    											<li class="media_end_head_fontsize_option3 _opt" data-value="size3">
    												<a href="javascript:;" class="media_end_head_fontsize_option_text nclicks(fnt_size)">가<em class="blind">3단계</em></a>
    											</li>
    											<li class="media_end_head_fontsize_option4 _opt" data-value="size4">
    												<a href="javascript:;" class="media_end_head_fontsize_option_text nclicks(fnt_size)">가<em class="blind">4단계</em></a>
    											</li>
    											<li class="media_end_head_fontsize_option5 _opt" data-value="size5">
    												<a href="javascript:;" class="media_end_head_fontsize_option_text nclicks(fnt_size)">가<em class="blind">5단계</em></a>
    											</li>
    										</ul>
    									</div>
    									<div class="media_end_head_fontsize_setlayer_section _font_family_option" style="display:none;">
    										<strong class="media_end_head_fontsize_setlayer_section_tit">글꼴</strong>
    										<ul class="media_end_head_fontsize_setlayer_select">
    											<li class="media_end_head_fontstyle_option _opt" data-value="font1"><a href="javascript:;" class="media_end_head_fontstyle_option_text nclicks(fnt_style)">굴림</a></li>
    											<li class="media_end_head_fontstyle_option _opt" data-value="font2"><a href="javascript:;" class="media_end_head_fontstyle_option_text nclicks(fnt_style)">돋움</a></li>
    											<li class="media_end_head_fontstyle_option _opt" data-value="font4"><a href="javascript:;" class="media_end_head_fontstyle_option_text nclicks(fnt_style)">맑은고딕</a></li>
    											<li class="media_end_head_fontstyle_option _opt" data-value="font5" data-nanum-font="true"><a href="javascript:;" class="media_end_head_fontstyle_option_text nclicks(fnt_style)">나눔고딕</a></li>
    										</ul>
    									</div>
    									<a href="javascript:;" class="media_end_head_fontsize_close _close_btn nclicks(fnt_close)"><span class="blind">닫기</span></a>
    									<div class="media_end_head_fontsize_linklayer _font_family_install_guide">
    										<p class="media_end_head_fontsize_linklayer_txt"><strong>나눔고딕</strong> 폰트가 설치되어있지 않습니다.<br><em>나눔 폰트</em>를 설치하러 가시겠습니까?</p>
    										<div class="media_end_head_fontsize_linklayer_btns">
    											<a href="http://hangeul.naver.com/2017/nanum" class="media_end_head_fontsize_linklayer_btn _yes_btn" target="_blank">예</a>
    											<a href="javascript:;" class="media_end_head_fontsize_linklayer_btn _no_btn">아니오</a>
    										</div>
    										<a href="javascript:;" class="media_end_head_fontsize_linklayer_close _close_btn"><span class="blind">닫기</span></a>
    									</div>
    								</div>
    							</div>
    						
    							<a href="/main/tool/print.nhn?oid=277&aid=0004565025" class="media_end_head_print nclicks(atp_print)" target="_blank"><span class="bline">인쇄하기</span></a>
    							<div class="sns_share">
    								<a href="#" title="보내기" class="naver-splugin nclicks(atp_share)" data-style="unity"
    								   data-url="http://news.naver.com/main/read.nhn?mode=LSD&mid=sec&sid1=001&oid=277&aid=0004565025"
    								   data-title="11개월 연속 줄어든 수출…10월 감소폭 3년9개월來 최대"
    								   data-likeServiceId="NEWS"
    								   data-likeContentsId="ne_277_0004565025"
    								   data-mail-url="http://news.naver.com/main/read.nhn?mode=LSD&mid=sec&sid1=001&oid=277&aid=0004565025&amp;lfrom=mail"
    								   data-blog-url="http://news.naver.com/main/read.nhn?mode=LSD&mid=sec&sid1=001&oid=277&aid=0004565025&amp;lfrom=blog"
    								   data-blog-source-type="3"
    								   data-blog-blog-id="naver"
    								   data-cafe-url="http://news.naver.com/main/read.nhn?mode=LSD&mid=sec&sid1=001&oid=277&aid=0004565025&amp;lfrom=cafe"
    								   data-cafe-source-type="3"
    								   data-memo-url="http://news.naver.com/main/read.nhn?mode=LSD&mid=sec&sid1=001&oid=277&aid=0004565025&amp;lfrom=memo"
    								   data-calendar-url="http://news.naver.com/main/read.nhn?mode=LSD&mid=sec&sid1=001&oid=277&aid=0004565025&amp;lfrom=calendar"
    								   data-band-url="http://news.naver.com/main/read.nhn?mode=LSD&mid=sec&sid1=001&oid=277&aid=0004565025&amp;lfrom=band"
    								   data-facebook-url="http://news.naver.com/main/read.nhn?mode=LSD&mid=sec&sid1=001&oid=277&aid=0004565025&amp;lfrom=facebook"
    								   data-twitter-url="http://news.naver.com/main/read.nhn?mode=LSD&mid=sec&sid1=001&oid=277&aid=0004565025&amp;lfrom=twitter"
    								   data-me-display="off">
    								<span class="naver-splugin-c sns_share_ico"></span>
    								<span class="blind">보내기</span>
    								</a>
    							</div>
    					</div>
    			</div>
    		</div>
    	</div>
    </div>
    <!-- // 기사 헤더 --><div class="article_body size3 font1 _font_setting_target" id="articleBody">
    	
    	<div id="articleBodyContents" class="_article_body_contents">
    	<!-- 본문 내용 -->
    	<!-- TV플레이어 -->
    
    <!-- // TV플레이어 -->
    <script type="text/javascript">
    // flash 오류를 우회하기 위한 함수 추가
    function _flash_removeCallback() {}
    </script>
    	
    	<span class="end_photo_org"><img src="https://imgnews.pstatic.net/image/277/2019/11/02/0004565025_001_20191102080925359.jpg?type=w647" alt="" /><em class="img_desc">(자료사진) [이미지출처=연합뉴스]</em></span><br><br>[세종=아시아경제 주상돈 기자] 지난달 수출이 또 줄어들며 지난해 12월부터 시작된 감소세가 11개월째 이어졌다. 감소율은 14.7%로 앞선 3년9개월 만의 최대폭을 기록했다.<br><br>2일 산업통상자원부에 따르면 10월 수출액(통관 기준)은 467억8400만달러로 전년 동기보다 14.7% 감소했다.<br><br>32.1% 줄어든 반도체가 수출 감소세를 주도했다. 산업부는 D램과 낸드플래시 등 메모리 반도체 가격 하락에 따른 것으로 봤다. 또 석유화학(-22.6%)과 석유제품(-26.2%), 디스플레이(-22.5%), 철강(-11.8%), 일반기계(12.1%), 자동차(-2.3) 등도 수출이 줄었다. 반면 선박(25.7%), 컴퓨터(7.7%) 등은 늘었다.<br><br>국가별로는 우리의 주력 수출국인 중국(-16.9%)과 미국(-8.4%)이 모두 줄었다. 일본(-13.8%)과 유럽연합(EU·-21.2%), 아세안(-8.3%), 인도(-12.0%), 중남미(-13.2%) 등도 감소했다.<br><br>산업부는 일본의 대한(對韓) 수출규제에 따른 영향은 제한적인 것으로 봤다. 박태성 산업부 무역투자실장은 "불화수소 등 3개 수출규제 품목이 7∼10월 전체 대일 수입에서 차지하는 비중이 1.4%로 낮고, 현재까지 관련산업의 실제 생산 차질로 연결된 사례는 없는 상황"이라며 "9월 기준 우리의 대일본 수출 감소(-6.0%)보다 일본의 대한국 수출 감소폭(-15.9%)이 더 크게 나타나 우리보다 일본이 더 큰 영향을 받고 있다"고 설명했다.<br><br>그는 ▲반도체 가격 회복  ▲미ㆍ중 협상의 스몰딜 성사 ▲수주 선박의 인도 본격화 등에 따라 내년 1분기에는 수출이 플러스로 전환할 것이라고 전망했다. 박 실장은 " 박 실장은 "수출은 10월을 저점으로 점진적으로 감소폭이 개선되고 있는 등 수출 감소 터널의 끝을 향해 나아가고 있다"며 "내년 1분기 수출은 플러스 전환이 될 것"이라고 말했다.<br><br>주상돈 기자 don@asiae.co.kr<br><br><a href="https://www.asiae.co.kr/fortune/index.htm?utm_source=navernews&utm_medium=naver_view&utm_campaign=fortune"><b>▶ 신강재강(身强財强) 해야 부자사주라고? 나는?</b></a><br><a href="https://www.asiae.co.kr/event/2019/quiz/"><b>▶ 초간단 퀴즈 풀고, 아이패드 받자! </b></a> <a href="https://cm.asiae.co.kr/list/science"><b>▶ 재미와 지식이 가득한 '과학을읽다'</b></a><br><br>&lt;ⓒ경제를 보는 눈, 세계를 보는 창 아시아경제 무단전재 배포금지&gt;
    	<!-- // 본문 내용 -->
    	</div>
    	<!-- [D] .guide_categorization_title 내 링크가 클릭되면 .guide_categorization_ct display:block; 해주세요 -->
    
    
    	
    
    
    
    	
    	
    		
    	
    
    
    <div class="guide_categorization">
    	<a href="#" class="guide_categorization_link _categorization_title">이 기사는 언론사에서 <em class="guide_categorization_item">경제</em> 섹션으로 분류했습니다.</a>
    	<div class="guide_categorization_ct" id="guideCategorizationDiv" style="display:none;">
    		<em class="guide_categorization_ct_title"><i class="guide_categorization_icon"></i>기사 섹션 분류 안내</em>
    		<p class="guide_categorization_ct_p">기사의 섹션 정보는 해당 언론사의 분류를 따르고 있습니다. 언론사는 개별 기사를 2개 이상 섹션으로 중복 분류할 수 있습니다.</p>
    		<a href="#" class="guide_categorization_ct_close"><span>닫기</span></a>
    	</div>
    </div>
    
    	
    
    <!-- 관련기사 -->
    
    <!-- // 관련기사 -->
    
    	<!-- 소셜플러그인 -->
    
    	
    
    
    
    
    
    	
    	
    	
    
    
    
    
    
    	
    	
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    	
    
    
    
    
    
    
    
    	
    	
    
    	
    
    	<div class="end_btn" id="spiLayer">
    	
    	<!-- 좋아요  u_likeit_module -->
    	<div class="_reactionModule u_likeit" data-sid="NEWS" data-cid="ne_277_0004565025" style="visibility: hidden">
        <ul class="u_likeit_layer _faceLayer" role="menu">
            <li class="u_likeit_list good" role="menuitem">
                <a class="u_likeit_list_button _button nclicks(abt_presslink)" data-type="like"  data-log="RTC.like|RTC.unlike" href="#" role="button" aria-selected="false">
                    <span class="u_likeit_list_name _label">좋아요</span>
                    <span class="u_likeit_list_count _count">0</span>
                </a>
            </li>
            <li class="u_likeit_list warm" role="menuitem">
                <a class="u_likeit_list_button _button" data-type="warm"  data-log="RTC.warm|RTC.unwarm" href="#" role="button" aria-selected="false">
                    <span class="u_likeit_list_name _label">훈훈해요</span>
                    <span class="u_likeit_list_count _count">0</span>
                </a>
            </li>
            <li class="u_likeit_list sad" role="menuitem">
                <a class="u_likeit_list_button _button" data-type="sad" data-log="RTC.sad|RTC.unsad" href="#" role="button" aria-selected="false">
                    <span class="u_likeit_list_name _label">슬퍼요</span>
                    <span class="u_likeit_list_count _count">0</span>
                </a>
            </li>
            <li class="u_likeit_list angry" role="menuitem">
                <a class="u_likeit_list_button _button" data-type="angry" data-log="RTC.angry|RTC.unangry" href="#" role="button" aria-selected="false">
                    <span class="u_likeit_list_name _label">화나요</span>
                    <span class="u_likeit_list_count _count">0</span>
                </a>
            </li>
            <li class="u_likeit_list want" role="menuitem">
                <a class="u_likeit_list_button _button" data-type="want" data-log="RTC.want|RTC.unwant" href="#" role="button" aria-selected="false">
                    <span class="u_likeit_list_name _label">후속기사 원해요</span>
                    <span class="u_likeit_list_count _count">0</span>
                </a>
            </li>
        </ul>
    </div>
    	<!-- //좋아요 -->
    	
    
    	
        <!-- 이 기사 추천 -->
        <div class="tomain as_addinfo">
            <div class="u_likeit_list_module _reactionModule" id="toMainContainer" data-sid="NEWS_MAIN" data-cid="ne_277_0004565025">
                <a href="#" class="u_likeit_list_btn _button" data-type="like" data-log="RTC.recommend|RTC.unrecommend" data-isHiddenZeroCount=true>
                    <span class="u_ico"></span>
                    <em class="u_txt _label">이 기사를 추천합니다</em>
                    <em class="u_cnt _count"></em>
                </a>
            </div>
            <div class="to_infobutton" id="to_infobutton">
                <button class="to_infobutton_b nclicks(RTC.tomaininfo)" type="button" onClick="javaScript:doDisplayTomainInfo()"><span class="blind">안내</span></button>
            </div>
    		<div class="tomain_info" id="tomain_info_new" style="display: none;">
    		</div>
        </div>
        <!-- //이 기사 추천 -->
    	
    
    	<!-- [D] 공유 아이콘 -->
    	<div class="sns_share nclicks(abt_share)">
    		<a href="#" id="spiButton" title="보내기" class="naver-splugin"
    			data-style="unity"
    			data-url="http://news.naver.com/main/read.nhn?mode=LSD&mid=sec&sid1=001&oid=277&aid=0004565025"
    			data-title="11개월 연속 줄어든 수출…10월 감소폭 3년9개월來 최대"
    		    data-likeServiceId="NEWS"
    		    data-likeContentsId="ne_277_0004565025"
    			data-mail-url="http://news.naver.com/main/read.nhn?mode=LSD&mid=sec&sid1=001&oid=277&aid=0004565025&amp;lfrom=mail"
    			data-blog-url="http://news.naver.com/main/read.nhn?mode=LSD&mid=sec&sid1=001&oid=277&aid=0004565025&amp;lfrom=blog"
    			data-blog-source-type="3"
    			data-blog-blog-id="naver"
    			data-cafe-url="http://news.naver.com/main/read.nhn?mode=LSD&mid=sec&sid1=001&oid=277&aid=0004565025&amp;lfrom=cafe"
    			data-cafe-source-type="3"
    			data-memo-url="http://news.naver.com/main/read.nhn?mode=LSD&mid=sec&sid1=001&oid=277&aid=0004565025&amp;lfrom=memo"
    			data-calendar-url="http://news.naver.com/main/read.nhn?mode=LSD&mid=sec&sid1=001&oid=277&aid=0004565025&amp;lfrom=calendar"
    			data-band-url="http://news.naver.com/main/read.nhn?mode=LSD&mid=sec&sid1=001&oid=277&aid=0004565025&amp;lfrom=band"
    			data-facebook-url="http://news.naver.com/main/read.nhn?mode=LSD&mid=sec&sid1=001&oid=277&aid=0004565025&amp;lfrom=facebook"
    			data-twitter-url="http://news.naver.com/main/read.nhn?mode=LSD&mid=sec&sid1=001&oid=277&aid=0004565025&amp;lfrom=twitter"
    			data-me-display="off">
    			<span class="naver-splugin-c sns_share_ico"></span>
    			<span class="blind">보내기</span>
    		</a>
    	</div>
    	
    	<div class="tomain_info" id="tomain_info" style="display: none;">
    	</div>
    
    	<script id="TOMAIN_DISPLAYED_BY_USER_RECOMMEND_TPL" type="text/template">
    		<p class="tomain_info_phrase">
    			<span class="tomain_info_body">
    				<span class="tomain_info_text">이 기사는 </span><strong class="tomain_info_point">사용자 추천</strong><span class="tomain_info_text">으로 모바일 메인 뉴스판에 노출된 이력이 있습니다.</span>
    			</span>
    		</p>
    	</script>
    	<script id="TOMAIN_DISPLAYED_BY_NEWS_EDIT_TPL" type="text/template">
    		<p class="tomain_info_phrase">
    			<span class="tomain_info_body">
    				<span class="tomain_info_text">이 기사는 </span><strong class="tomain_info_point">모바일 메인 뉴스판</strong><span class="tomain_info_text">에 노출된 이력이 있습니다.</span>
    			</span>
    		</p>
    	</script>
    	<script id="TOMAIN_NOT_DISPLAYED_YET_TPL" type="text/template">
    		<p class="tomain_info_layer">
    			<strong class="tomain_info_head">모두에게 보여주고 싶은 기사라면<i>?</i><span class="tomain_info_betaicon">beta</span></strong>
    			<span class="tomain_info_body">
    				<strong class="tomain_info_point">이 기사를 추천합니다 </strong><span class="tomain_info_text">버튼을 눌러주세요. 집계 기간 동안 추천을 많이 받은 기사는 네이버 자동 기사배열 영역에 추천 요소로 활용됩니다.</span>
    			</span>
    			<a href="#" class="tomain_info_close">레이어 닫기</a>
    		</p>
    	</script>
    	
    
    	<script type="text/javascript">
     		(function(){
    			var currentDate = new Date(), yyyy = currentDate.getFullYear(), mm = currentDate.getMonth() + 1, dd = currentDate.getDate();
    			var currentDateParam = "" + yyyy + (mm < 10 ? '0' + mm : mm) + (dd < 10 ? '0' + dd : dd);
    			var id = "naver-splugin-sdk";
    			var s = document.createElement("script"); s.id = id; s.type = "text/javascript", s.charset = "utf-8", s.async = false;
    			s.src = ("https://ssl.pstatic.net/spi/js/release/ko_KR/splugin.js?" + currentDateParam);
    			var d = document.getElementsByTagName('head')[0]; d.appendChild(s, d);
    		})();
     		(function(oData) {
    		    var t = new Date(), yyyy = t.getFullYear(), mm = t.getMonth() + 1, dd = t.getDate();
    		    var currentDate = "" + yyyy + (mm < 10 ? '0' + mm : mm) + (dd < 10 ? '0' + dd : dd);
    		    var s = document.createElement("script");
    		    s.type = "text/javascript";
    		    s.charset = "utf-8";
    		    s.src = "https://news.like.naver.com/js/reaction/dist/reaction.min.js?"+ currentDate; // (new Date()).toDateString().replace(/\s/g,"");
    		    (document.head || document.getElementsByTagName("head")[0]).appendChild(s);
    		})();
    		window.onload = function() {
    		    if(jindo.$Element("spiLayer").query("._reactionModule") !== null) {
    				var toMainInfoLayerManager = {
    
    					oCookieStorage : null,
    					sCookieKey : null,
    					sTemplateType : null,
    					oTemplateType2TemplateMapping : null,
    
    					welTomainInfoLayer : null,
    
    					init : function () {
    						this.setCache();
    						this.setEvent();
    
    						if (this.sTemplateType != 'N') {
    							this.renderLayer();
    						}
    					},
    
    					setCache : function () {
    						this.oCookieStorage = jindo.$Cookie(true);
    						this.sCookieKey = 'pcTomainDontShow';
    						this.sTemplateType = 'N';
    						this.oTemplateType2TemplateMapping = {
    							'R' : 'TOMAIN_DISPLAYED_BY_USER_RECOMMEND_TPL',
    							'E' : 'TOMAIN_DISPLAYED_BY_NEWS_EDIT_TPL',
    							'N' : 'TOMAIN_NOT_DISPLAYED_YET_TPL'
    						};
    						this.welTomainInfoLayer = jindo.$Element('tomain_info');
    					},
    
    					setEvent : function () {
    						this.welTomainInfoLayer.delegate('click', '.tomain_info_close', jindo.$Fn(this.onCloseClick, this).bind());
    					},
    
    					renderLayer : function () {
    						var sTemplate = this.oTemplateType2TemplateMapping[this.sTemplateType];
    						this.welTomainInfoLayer.html(jindo.$Template(sTemplate).process({}));
    						this.welTomainInfoLayer.show();
    					},
    
    					onCloseClick : function (e) {
    						e.stopDefault();
    						this.welTomainInfoLayer.hide();
    						this.oCookieStorage.set(this.sCookieKey, 'Y', 365);
    					}
    
    				};
    
    				var toMainManager = {
    
    					welContainer : null,
    					welCount : null,
    					welButton : null,
    
    					init : function () {
    						this.welContainer = jindo.$Element('toMainContainer');
    						this.welCount = jindo.$Element(this.welContainer.query('._count'));
    						this.welButton = jindo.$Element(this.welContainer.query('a'));
    					},
    
    					// 추천 수가 0인 경우, 디자인이 달라서 is_first 클래스 추가
    					addIsFirstClassIfZeroCount : function () {
    						if (this.welCount.text() == '0') {
    							this.welButton.removeClass('off').addClass('is_first');
    						}
    					},
    
    					removeIsFirstClass : function () {
    						this.welButton.removeClass('is_first');
    					},
    
    					onRecommend : function () {
    						this.removeIsFirstClass();
    					},
    
    					onCancel : function () {
    						this.addIsFirstClassIfZeroCount();
    					},
    
    					onRecommendReady : function (element) {
    						this.addIsFirstClassIfZeroCount();
    					}
    				};
    
    				toMainInfoLayerManager.init();
    				toMainManager.init();
    
    				reaction.init({
    					type: "multi",
    					domain : "https://news.like.naver.com",
    					dependentLibrary : "jquery",
    					cssId: "news",
    					isMobile: false,
    					isHiddenLabel : false,
    					isHiddenCount : false,
    					isHiddenZeroCount : false,
    					isUsedLabelAsZeroCount : false,
    					isDebugMode : false,
    					isHiddenLayerAfterSelection : true,
    					callback : {
    						clicked : function(param) {
    							// displayId 가 'NEWS_MAIN' 이면 '메인으로추천', 'NEWS'면 '좋아요'
    							if (param && param.content && param.content.displayId && param.content.displayId == 'NEWS_MAIN') {
    								if(param.content.isReacted) {
    									toMainManager.onRecommend();
    									return;
    								}
    								toMainManager.onCancel();
    							}
    						},
    						updated : function(param) {
    							if (param) {
    								jindo.$A(param.contents).filter(function (content) {
    									if (content.serviceId == 'NEWS_MAIN') {
    										return true;
    									}
    									return false;
    								}).forEach(function (content) {
    									toMainManager.onRecommendReady();
    								});
    							}
                                var autoSummaryFeedbackData = jindo.$A(param.contents)
                                        .filter(function (contentsData) {
                                            return contentsData.serviceId === 'NEWS_SUMMARY';
                                        })
                                        .$value()[0] || {};
    
                                // export
    							if(autoSummaryFeedbackData.reactions){
    								window.autoSummary = new AutoSummary()
    									.init({
    										apiUrl: 'https://tts.news.naver.com/article/277/0004565025/summary',
    										feedbackDataList: autoSummaryFeedbackData.reactions
    									});
    							}
    						},
                            click: function (param) {
                                var triggeredWrapper = jindo.$Element(param.target)
                                    .parent(function (wel) {
                                        return wel.hasClass('_reactionModule');
                                    })[0];
                                var isAutoSummaryFeedback = (triggeredWrapper) ?
                                    triggeredWrapper.attr('data-sid') === 'NEWS_SUMMARY' :
                                    false;
    
                                if (isAutoSummaryFeedback) {
                                    return window.autoSummary.confirmApplyFeedback();
                                }
                            }
    					}
    				});
    			}
    
    		    // for social plugin
    			window.__splugin = SocialPlugIn_Core({
    				// nEvent Key
    				"evKey"       : "news",
    				// 서비스명
    				"serviceName" : "뉴스",
    				"sourceName" : "아시아경제",
    				// 버튼 클릭후 호출되는 콜백함수
    				"onClick"     : function(button) {},
    				// 공유하기 레이어 노출 후 호출되는 콜백함수
    				"onShow"      : function() {},
    				// 공유하기 레이어 닫기 후 호출되는 콜백함수
    				"onHide"      : function() {}
    			});
    		}
    		
    		function onSubscribe(elTarget) {
    			return htParameter;
    		}
    
    		// 이기추 레이어 표시
    		function doDisplayTomainInfo() {
    			var welTomainInfoLayer = jindo.$Element('tomain_info_new');
    			if (welTomainInfoLayer.css("display") == "none") {
    				welTomainInfoLayer.delegate('click', '.tomain_info_close', jindo.$Fn(onCloseClick, this).bind());
    				welTomainInfoLayer.html(jindo.$Template('TOMAIN_NOT_DISPLAYED_YET_TPL').process({}));
    				welTomainInfoLayer.show();
    			} else {
    				welTomainInfoLayer.hide();
    			}
    		}
    
    		// 이기추 레이어 닫기
    		function onCloseClick(e) {
    			e.stopDefault();
    			var welTomainInfoLayer = jindo.$Element('tomain_info_new');
    			welTomainInfoLayer.hide();
    		}
    	</script>
    </div>
    
    
    
    <!-- // 소셜플러그인 -->
    
    
    <script type="text/javascript">
    /* (function() {
    	init_socialplugin();
    })(); */
    </script>
    	
    <script type="text/javascript">
        jindo.$Fn(function() {
            jindo.$Fn(function(){
                var oid = '277';
                var aid = '0004565025';
                new jindo.$Ajax('/main/ajax/series/list.nhn?oid=' + oid + '&aid=' + aid, {
                    type : 'xhr',
                    method : 'get',
                    timeout : 10,
                    async : true,
                    onload : function(res) {
                        var oJson = res.json();
                        if (oJson.message != null && oJson.message.result != null) {
                            var result = oJson.message.result;
                            var contents = '<div class="serialization_news"><h3 class="serialization_news_title"><span class="serialization_news_ico">연재</span>'
                                + '<a href="'+result.linkUrl+'" class="serialization_news_more nclicks(ser.more)" id="seriesTitle" >'
                                + result.title + '</a><span class="blind">더보기</span></h3>'
                                + '<ul class="serialization_news_list">';
    
                            jindo.$A(result.seriesItemList).forEach(function(value) {
                                if (value) {
                                    if (aid == value.articleId) {
                                        contents += '<li><div class="serialization_news_item"><span class="serialization_news_time">'+ value.articleDate +'</span><a href="'+value.url+'" class="serialization_news_link is_selected nclicks(ser.art)">' + value.title + '</a></div></li>';
                                    } else {
                                        contents += '<li><div class="serialization_news_item"><span class="serialization_news_time">'+ value.articleDate +'</span><a href="'+value.url+'" class="serialization_news_link nclicks(ser.art)">' + value.title + '</a></div></li>';
                                    }
                                }
                            });
    
                            contents += '</ul></div>';
    
                            jindo.$Element('spiLayer').afterHTML(contents);
    
                            var elLinkNews = jindo.$$('.link_news');
                            if (elLinkNews.length > 0) {
                                jindo.$Element('link_news_more').first().text(result.title);
                                jindo.$Element('link_news_more').visible(true, 'block');
                                jindo.$Element('link_news_more').attr('href', result.linkUrl);
                            }
                        }
                    }
                }).request();
            }).delay(0.8);
        }).attach(window, "load");
    </script>
    	<!-- 언론사 관련기사 -->
        <div class="link_news">
            
            <h3>아시아경제 관련뉴스<span>해당 언론사에서 선정하며 <em>언론사 페이지(아웃링크)</em>로 이동해 볼 수 있습니다.</span></h3>
            <ul>
                
                    <li><a href="https://www.asiae.co.kr/article/2019102815013662414" class="nclicks(are.link,'277', 'nilGParam', '277_fd77e9de63471aa2')" target="_blank">학점을 위한 '성관계' 보도 나오자 잇따라…'발칵'</a></li>
                
                    <li><a href="https://www.asiae.co.kr/article/2019102914430073167" class="nclicks(are.link,'277', 'nilGParam', '277_88d2ef9e43754062')" target="_blank">"16세때 피임수술…" 성매매 시킨 친할머니에</a></li>
                
                    <li><a href="https://www.asiae.co.kr/article/2019103107095407927" class="nclicks(are.link,'277', 'nilGParam', '277_aee7923bd4677265')" target="_blank">조국 사건에 갑자기 뜬 '톱스타' 대체 무슨 일?</a></li>
                
                    <li><a href="https://www.asiae.co.kr/article/2019102921230502784" class="nclicks(are.link,'277', 'nilGParam', '277_2077a9f698246bca')" target="_blank">"물도 안돼"…'2만원 한식'으로만 버틴 日 출장기</a></li>
                
                    <li><a href="https://www.asiae.co.kr/article/2019110111271844056" class="nclicks(are.link,'277', 'nilGParam', '277_2ca02d94c507c9ac')" target="_blank">"술 한잔에도 얼굴 빨개지는 사람, 이 병에 취약"</a></li>
                
            </ul>
            <a href="#" class="link_news_more nclicks(ser.sum)" id="link_news_more" style="display:none"><em></em> 기사 모아보기</a>
            
        </div>
    <!-- // 언론사 관련기사 -->
    </div>
    
    
    <script type="text/javascript">
        new FontSettingMenu();
    </script><!-- 언론중재법 -->
    
    	
    	
    	
    
    <!-- // 언론중재법 --><!-- 기능 버튼 영역 -->
    <div class="article_footer">
    	<ul>
    		<li>
    			<a href="https://www.asiae.co.kr/ " target="_blank" class="nclicks(abt_presslink)">
    			아시아경제 기사제공
    			</a>
    		</li>
    				
    		
    			
    				<li title="신문에 게재된 기사만 보실 수 있습니다.">
    					<a href="/main/list.nhn?mode=LPOD&mid=sec&sid1=001&sid2=141&oid=277&listType=paper" class="go nclicks(abt_presspaper)">
    						<i class="picon">신문</i>
    						아시아경제  신문게재기사만
    					</a>
    				</li>
    			
    			
    		
    	</ul>
    </div>
    
    <ul class="content_menu content_menu_bottom">
    	<li class="first"><a href="/main/tool/print.nhn?oid=277&aid=0004565025" class="print nclicks(abt_print)" alt="인쇄" title="인쇄" target="_blank">인쇄</a></li>
    	<li class="scrap"><a href="/main/scrap/folderList.nhn?scrapItem.officeId=277&scrapItem.articleId=0004565025" class="scrap nclicks(abt_scrap)" alt="스크랩" title="스크랩" target="_blank">스크랩</a></li>
    </ul>
    <!-- // 기능 버튼 영역 -->
    
    
    <!-- SNU 팩트체크 활성화 -->
    
    <!-- // SNU 팩트체크 활성화 -->
    
    <script type="text/javascript">
    	function doDisplay(){
    		var element = document.getElementById('articleFactcheckInfo');
    		if (element.classList.contains('is_hidden')) {
    			element.classList.remove('is_hidden');
    		} else {
    			element.classList.add('is_hidden');
    		}
    	}
    </script>
    
    <!-- (신)관련기사 -->
    
    
    <!-- //(신)관련기사 -->
    
    <!-- 스포츠 관련기사 -->
    
    
    <!-- //스포츠 관련기사 -->
    <!-- 본문 하단 광고 -->
    <div class="end_ad"><iframe id="da_727145" src="https://veta.naver.com/fxshow?su=SU10083&sid1=101&sid2=263&oid=277" width="727" height="0" marginheight="0" marginwidth="0" border="0" frameborder="0" scrolling="no" align="center" title="기사엔드하단광고" data-veta-preview="p_news_end"style="background-color: rgba(255,0,0,0.2)"></iframe></div>
    <!-- // 본문 하단 광고 -->
    
    
    
    
    
    
        <div id="cbox_module"></div>
        
    
    
    
    
    
    
    
    
    
        
            <script type="text/javascript">
                
                try {
                    var isLogForComment = false;
                    if (jindo.$Cookie().get('NID_SES') != null && jindo.$Cookie().get('NID_SES') != ''){
                        isLogForComment = true;
                    }
                    var locationSearch =location.search;
    
                    
                    var commentOptions = JSON.parse(JSON.stringify({"sLanguage":"ko","nPageSize":5.0,"sSort":"favorite","sTemplateId":"view_economy","aFormation":["count","graph","write","notice","list","view"],"sDomain":"https://ssl.pstatic.net/static.cbox","htErrorHandler":{"5010":"댓글/답글은 60초 내에 한 개만 등록하실 수 있습니다.","3006":"고객님께서는 운영원칙에서 제한하고 있는 글을 작성하셨기 때문에 무기한 글쓰기를 포함한 일부? 활동이 제한되었습니다.","3005":"고객님의 IP는 운영원칙에서 제한하고 있는 글을 작성하셨기 때문에 글쓰기를 포함한 일부? 활동이 제한되었습니다.","3004":"고객님께서는 운영원칙에서 제한하고 있는 글을 다수 작성하셨기 때문에 글쓰기를 포함한 일부? 활동이 일정 기간 제한되었습니다.","5003":"정상적으로 반영되지 않았습니다. 화면 새로고침 후 다시 시도해 주세요.","3003":"고객님께서는 운영원칙에서 제한하고 있는 글을 작성하셨기 때문에 글쓰기를 포함한 일부 활동이 일정 기간 제한되었습니다. 동일 내용 댓글의 반복작성이 확인된 경우 제한기간은 1일이며, 반복이 계속되면 기간이 연장될 수 있습니다.","5026":"공감/비공감은 최근 24시간내 50회까지 가능합니다.","4004":"해당되는 댓글이 없습니다.","5027":"공감/비공감은 10초 내에 한 번만 클릭하실 수 있습니다.","5006":"자신의 글에 공감 할 수 없습니다.","5029":"기사당 허용된 댓글 수 3개를 초과하였습니다. 기사에 작성한 댓글을 삭제 후 다시 작성하실 수 있습니다.","5008":"자신의 글에 비공감 할 수 없습니다."},"sCountry":"KR","sDateFormat":"Y.m.d. H:i:s","sCommentNo":"","bManager":false,"sHelp":"down","bSortCookie":true,"sAuthType":"both","htMessage":{"template":{"duplicate_caution_link_title":"운영규정 자세히 알아보기","write_long_placeholder":"저작권 등 다른 사람의 권리를 침해하거나 명예를 훼손하는 게시물은 이용약관 및 관련 법률에 의해 제재를 받을 수 있습니다. 건전한 토론문화와 양질의 댓글 문화를 위해, 타인에게 불쾌감을 주는 욕설 또는 특정 계층/민족, 종교 등을 비하하는 단어들은 표시가 제한됩니다.","view_all":"댓글 더보기","sort_favorite":"순공감순","duplicate_caution_link_address_pc":"https://news.naver.com/main/principle.nhn","help_contents":["작성자가 삭제한 댓글(작성자 삭제), 운영자가 삭제한 댓글(규정 미준수) 그리고 삭제되지 않은 현재 남은 댓글의 수와 이력을 투명하게 제공합니다.","순공감순은 공감수에서 비공감수를 뺀 수치가 많은 댓글입니다. 비정상적인 방법으로 공감수가 증가하는 경우 제외될 수 있습니다.<br/>정치기사의 댓글은 최신순만 제공됩니다."],"duplicate_caution_title":"동일 내용 댓글의 반복 등록이<br>확인되었습니다.","write_placeholder":"댓글을 입력해주세요","duplicate_caution_link_address_mobile":"https://m.news.naver.com/ombudsman/index.nhn?mode=rule&open=comment","help_titles":["댓글이력공개안내","댓글노출정책"],"user":{"header":{"help":{"title":"뉴스댓글 도움말","content":"댓글목록을 공개한 사용자의 댓글모음이 제공됩니다. 나의 댓글 모음에서 다른 사람에게 공개 또는 비공개 설정을 할 수 있습니다. 제공되는 목록에 삭제댓글/답글은 포함하지 않습니다."}}},"duplicate_caution_cont":"반복 등록이 계속될 경우 운영규정에 따라 <br>서비스 이용이 정지될 수 있습니다.","social_login_message":"계정을 선택하시면 <span class=\"u_cbox_msg_point\">로그인&middot;계정인증</span>을 통해<br> 댓글을 남기실 수 있습니다.<br>뉴스서비스에서는 소셜 계정 사용이 불가하며<br>댓글모음만 확인하실 수 있습니다."},"alert":{"min_length":"내용을 최소 {0}자 이상 입력해주세요.","login_require":"입력창 상단의 서비스별 아이콘을 선택하여 로그인해 주세요.","max_length":"{0}자까지 입력할 수 있습니다."},"stats":{"fold":"접기","view":"통계보기","user_env_title":"어디에서 댓글을 썼을까요?","title":"누가 댓글을 썼을까요?"}},"sApiDomain":"https://apis.naver.com/commentBox/cbox5","bIncludeAllComments":true,"sTicket":"news","sCssId":"news_w","sPageType":"more","sObjectId":"news277,0004565025","sCountType":"comment","bShowReply":"","bUseAgo":false,"bMobile":false,"nReplyPageSize":20.0,"bByCountry":false,"sLikeItId":"ne_277_0004565025"}), function (key, value) {
                        if (value && (typeof value === 'string') && value.indexOf("function") === 0) {
                            var jsFunc = new Function('return ' + value)();
                            return jsFunc;
                        }
    
                        return value;
                    });
    
                    
                    var sNoticeMessage = "";
                    
                    try {
                        var oNewsOptions = JSON.parse(JSON.stringify({"message":{"default":{"block":"언론사가 정치섹션으로 분류한 기사의 댓글은 '댓글 보기' 페이지로 이동해 확인가능하며, 언론사 홈페이지에 작성된 댓글은 '언론사 댓글로 이동'을 클릭해 볼 수 있습니다. "},"pc":{"default":{"block":"언론사가 정치섹션으로 분류한 기사의 댓글은 '댓글 보기' 페이지로 이동해 확인가능하며,<br>언론사 홈페이지에 작성된 댓글은 '언론사 댓글로 이동'을 클릭해 볼 수 있습니다. "},"custom":{"block":"아시아경제 댓글 정책에 따라 아시아경제에서 제공하는 경제섹션 기사의<br> 본문 하단에는 댓글 서비스를 제공하지 않습니다.","sort":"<em>%s</em> 댓글 정책에 따라 %s기사 본문 하단에서는<br> %s을 먼저 보여주고 아래 정렬 옵션이 추가 제공됩니다.","off":"<em>아시아경제</em>의 댓글 정책에 따라 <em>아시아경제</em>에서 제공하는<br> 경제섹션 기사에는 댓글 서비스를 제공하지 않습니다.","notice":{"layerTitle":"댓글 정책 언론사별 선택제","layerBody":"섹션별로 기사의 댓글 제공여부와 정렬방식을 <br>언론사가 직접 결정합니다. 기사 섹션 정보가<br>정치를 포함해 중복 분류된 경우 정치섹션 정책이 적용됩니다.","title":"이 기사의 댓글 정책은 <em>아시아경제</em>가 결정합니다."}}},"custom":{"block":"아시아경제 댓글 정책에 따라 아시아경제에서 제공하는 경제섹션 기사의 본문 하단에는 댓글 서비스를 제공하지 않습니다.","sort":"<em>%s</em> 댓글 정책에 따라 %s기사 본문 하단에서는 %s을 먼저 보여주고 아래 정렬 옵션이 추가 제공됩니다.","off":"<em>아시아경제</em>의 댓글 정책에 따라 <em>아시아경제</em>에서 제공하는 경제섹션 기사에는 댓글 서비스를 제공하지 않습니다.","notice":{"layerTitle":"댓글 정책 언론사별 선택제","layerBody":"섹션별로 기사의 댓글 제공여부와 정렬방식을 <br>언론사가 직접 결정합니다. 기사 섹션 정보가<br>정치를 포함해 중복 분류된 경우 정치섹션 정책이 적용됩니다.","title":"이 기사의 댓글 정책은 <em>아시아경제</em>가 결정합니다."}},"defaultSort":"순공감순"},"url":{"press":{"pc":"https://view.asiae.co.kr/article/2019110116401413932","mobile":"https://view.asiae.co.kr/article/2019110116401413932"}}}));
                        sNoticeMessage = oNewsOptions.message.pc.custom.notice;
                    } catch (e) {
                        //TODO : nelo전송
                    }
                    
    
                    
                    var serviceOptions = {
                        "bLogin" : isLogForComment,
                        "sCssId" : 'news',
                        "nPageSize" : 10,
                        "sCharset": 'euc-kr',
                        "bIncludeAllComments" : CommentUtils.parseParameter(locationSearch, "includeAllCount", true),
                        "sCommentNo" : CommentUtils.parseParameter(locationSearch, "commentNo", ''),
                        "bShowReply" : CommentUtils.parseParameter(locationSearch, "showReply", ''),
                        "vViewAllHandler" :CommentUtils.processViewAllCommentsWithOption,
                        "htEventHandler" : {
                            "loadList" : CommentUtils.resetCount,
                            "loadCreate" : CommentUtils.resetCount,
                            "afterList" :  CommentUtils.coord({"checkHighLight" : null, "loadOptionNotice" : sNoticeMessage}),
                            "afterRemove" : CommentUtils.resetCount,
                        },
                        "vCommentLinkHandler" : CommentUtils.processCommentLanding,
                        "fCommentItemHandler" : CommentUtils.itemConverter
                    }
                } catch(e) {
                    //TODO : nelo전송
                }
    
                
                try {
                    commentOptions = CommentUtils.copyOptions(commentOptions, serviceOptions);
                    jindo.$Fn(function() {
                        (function (htOption) {
                            window.__htCboxOption = htOption;
                            var retryCount = 1;
                            var onErrorRetry = function () {
                                if (retryCount == 3) {
                                    JEagleEyeClient.sendError("cbox.core.js retry 3 fail");
                                    return;
                                }
    
                                createScript(htOption);
                                retryCount += 1;
                            };
    
                            var createScript = function (htOption) {
                                var s = document.createElement('script');
                                s.type = 'text/javascript';
                                s.charset = 'utf-8';
                                s.onerror = onErrorRetry;
                                s.src = htOption.sDomain + '/js/cbox.core.js?v=' + Math.floor(new Date().getTime() / 1200000);
                                (document.head || document.getElementsByTagName("head")[0]).appendChild(s);
                            };
    
                            createScript(htOption);
                        })(commentOptions);
                    }).attach(window, "load");
                } catch(e) {
                    //TODO : nelo전송
                }
            </script>
        
        
    
    
    
    <!-- Dic Tooltip -->
    <script type="text/javascript">
    jindo.$Fn(function(){
        jindo.LazyLoading.load(
            "https://ssl.pstatic.net/dicimg/tip/tip_pc.js?" + jindo.$Date().format("Ymd"),
            function(){
                if(typeof tip === "undefined"){
                    loadVod();
                    return;
                }
    
                tip.init('#articleBodyContents', {
                    prCode : "news",
                    lang: {
                        "en": {
                            minWordLength: 2,
                            target:"ko",
                            nsc:"dic.tt.nek"
                        }
                    },
                    layerTarget : 0,
                    mousePointer: true,
                    eventBeforePlaySound : function(oEvent) {
                        if (typeof ttsPlayer != "undefined") {
                            ttsPlayer.pause();
                        }
    
                    },
                    eventAfterPlaySound: function(oEvent) {
                        if (typeof ttsPlayer != "undefined") {
                            ttsPlayer.resume();
                        }
                    }
                });
    
                loadVod();
    
                // 동영상 iframe 로딩
                function loadVod(){
                    news.read.VodIframeLazyLoader.init();
                }
            }
        );
    }).attach(window, "load");
    </script>
    <!-- 이전/다음 기사목록 보기 -->
    
    
    
    
    
    
    
    	
    
    <div class="article_list">
    
    <h4>
    
    	
    		
    			
    			
    			
    			
    				
    					
    					
    						
    							
    							
    								
    									
    									
    									
    										경제 속보 <span class="fs11"><a href="/main/list.nhn?mode=LSD&mid=sec&sid1=101" class="c6 nclicks(abt_seclist)">
    									
    								
    							
    						
    					
    				
    			
    		
    	
    	
    	
    	
    
    
    기사목록 전체보기</a></span></h4>
    
    
    
    
    	
    		
    			
    			
    				
    					<ul class="type04">
    									
    					
    					
    					
    						
    						<li class="list1">
    						
    							<a class="nclicks(abt_secart)" href="/main/read.nhn?mode=LSD&mid=sec&sid1=101&oid=018&aid=0004506945">
    							(표)환율 주간 동향</a><i class="icon_photo">포토</i>
    						</li>
    					
    						
    						<li class="list2">
    						
    							<a class="nclicks(abt_secart)" href="/main/read.nhn?mode=LSD&mid=sec&sid1=101&oid=011&aid=0003644775">
    							증시부진에 쏠림 심화...'대어' 롯데리츠 상장 첫날 시총 1조 돌파</a><i class="icon_photo">포토</i>
    						</li>
    					
    					
    					<li class="list3">
    						
    					
    						<a class="nclicks(abt_secart)" href="/main/read.nhn?mode=LSD&mid=sec&sid1=101&oid=277&aid=0004565025">
    							<strong>11개월 연속 줄어든 수출…10월 감소폭 3년9개월來 최대</strong></a><i class="icon_photo">포토</i>
    					</li>
    					
    					
    						
    							
    						<li class="list4">
    							<a class="nclicks(abt_secart)" href="/main/read.nhn?mode=LSD&mid=sec&sid1=101&oid=055&aid=0000769427">
    							코리아세일페스타, 유통업 '초저가' 공세…백화점 반쪽 참여</a> <strong class="r_ico r_vod_txt">동영상기사</strong>
    						</li>
    					
    						
    							
    						<li class="list5">
    							<a class="nclicks(abt_secart)" href="/main/read.nhn?mode=LSD&mid=sec&sid1=101&oid=015&aid=0004234720">
    							뉴욕증시, 고용지표 호조에 '급등'…S&P·나스닥 '사상 최고치'</a> <i class="icon_photo">포토</i>
    						</li>
    									
    					</ul>
    				
    			
    		
    	
    
    
    </div>
    
    
    <!-- // 이전/다음 기사목록 보기 -->
    <script type="text/javascript">
    	jindo.$Fn(function(){
    		var _guideBaseElement = jindo.$Element(jindo.$$.getSingle(".guide_categorization"));
    		var _guideCategorizationDiv = jindo.$Element("guideCategorizationDiv");
    
    		if (_guideBaseElement && _guideCategorizationDiv) {
    			jindo.$Fn(function(e) {
    				e.stopDefault();
    				_guideCategorizationDiv.toggle();
    			}, this).attach(_guideBaseElement.query("a._categorization_title"),'click');
    
    			jindo.$Fn(function(e) {
    				e.stopDefault();
    				_guideCategorizationDiv.toggle();
    			}, this).attach(_guideBaseElement.query(".guide_categorization_ct a.guide_categorization_ct_close"), 'click');
    		}
    	}).attach(window, "load");
    </script>
    <script type="text/javascript">
        jindo.$Fn(function() {
            jindo.$Fn(function(){
                handOff.Article.init(
                    jindo.$$.getSingle('._article_body_contents'),
                    {
                        category: 'news_article',
                        contentId: '277_0004565025',
                        apiDomain: 'https://sidekick.fever.naver.com'
                    }
                );
            }).delay(0.8);
        }).attach(window, "load");
    </script>
    				</div>
    			</td>
    			<td class="aside">
    				<div class="aside">
    					
    
    
    
    
    
    
        
        
        
        
            
        
    
    
    
    
        
        
    
    
        
        
        
        
            
            
                
                
                    <div class="section section_wide"> 
     <h4><a href="/main/ranking/popularDay.nhn" class="nclicks(rig.ranking)">가장 많이 본 뉴스</a></h4> 
     <div class="category"> 
      <span class="category_ranking" id="category_ranking"> <a href="#" onclick="return false;" class="nclicks(rig.ranking)" aria-selected="false" id="right.ranking_tab_100">정치</a> <a href="#" onclick="return false;" class="nclicks(rig.ranking)" aria-selected="false" id="right.ranking_tab_101">경제</a> <a href="#" onclick="return false;" class="nclicks(rig.ranking)" aria-selected="false" id="right.ranking_tab_102">사회</a> <a href="#" onclick="return false;" class="nclicks(rig.ranking)" aria-selected="false" id="right.ranking_tab_103">생활/문화</a> <a href="#" onclick="return false;" class="nclicks(rig.ranking)" aria-selected="false" id="right.ranking_tab_104">세계</a> <a href="#" onclick="return false;" class="nclicks(rig.ranking)" aria-selected="false" id="right.ranking_tab_105">IT/과학</a> </span> 
     </div> 
     <div id="right.ranking_contents"></div> 
     <div id="ranking_100" style="display:none"> 
      <h5 class="blind">정치</h5> 
      <ul class="section_list_ranking"> 
       <li><span class="rank num1"><em>1</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=214&amp;aid=0000990725&amp;date=20191102&amp;type=2&amp;rankingSeq=1&amp;rankingSectionId=100" class="nclicks(rig.rankpol)" title="文 퇴임 후 &quot;양산 간다&quot;…사저 경호 예산 편성">文 퇴임 후 &quot;양산 간다&quot;…사저 경호 예산 편성</a> </li> 
       <li><span class="rank num2"><em>2</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=022&amp;aid=0003410931&amp;date=20191102&amp;type=1&amp;rankingSeq=2&amp;rankingSectionId=100" class="nclicks(rig.rankpol)" title="박찬주는 역풍, 이자스민은 이적… ‘인재 복’ 없는 한국당">박찬주는 역풍, 이자스민은 이적… ‘인재 복’ 없는 한국당</a> </li> 
       <li><span class="rank num3"><em>3</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=005&amp;aid=0001255150&amp;date=20191102&amp;type=1&amp;rankingSeq=3&amp;rankingSectionId=100" class="nclicks(rig.rankpol)" title="자유한국당 탈당 후 정의당 입당한 ‘다문화 1호’ 이자스민 전 의원">자유한국당 탈당 후 정의당 입당한 ‘다문화 1호’ 이자스민 전 의원</a> </li> 
       <li><span class="rank num4"><em>4</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=023&amp;aid=0003484118&amp;date=20191102&amp;type=0&amp;rankingSeq=4&amp;rankingSectionId=100" class="nclicks(rig.rankpol)" title="다급해진 정부 &quot;대화하자&quot;… 일본은 뒷짐지고 큰소리">다급해진 정부 &quot;대화하자&quot;… 일본은 뒷짐지고 큰소리</a> </li> 
       <li><span class="rank num5"><em>5</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=022&amp;aid=0003410932&amp;date=20191102&amp;type=1&amp;rankingSeq=5&amp;rankingSectionId=100" class="nclicks(rig.rankpol)" title="北 “초대형 방사포 성공” 靑 “위중한 위협 아니다”">北 “초대형 방사포 성공” 靑 “위중한 위협 아니다”</a> </li> 
       <li><span class="rank num6"><em>6</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=001&amp;aid=0011185067&amp;date=20191102&amp;type=1&amp;rankingSeq=6&amp;rankingSectionId=100" class="nclicks(rig.rankpol)" title="나경원 &quot;우기지 말라&quot;, 강기정 고성 항의…靑국감 막판 진통(종합)">나경원 &quot;우기지 말라&quot;, 강기정 고성 항의…靑국감 막판 진통(종합)</a> </li> 
       <li><span class="rank num7"><em>7</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=020&amp;aid=0003250929&amp;date=20191102&amp;type=1&amp;rankingSeq=7&amp;rankingSectionId=100" class="nclicks(rig.rankpol)" title="[단독]한국당, 신보라 의원 비서 남편 영입 ‘자격 논란’">[단독]한국당, 신보라 의원 비서 남편 영입 ‘자격 논란’</a> </li> 
       <li><span class="rank num8"><em>8</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=023&amp;aid=0003484063&amp;date=20191102&amp;type=0&amp;rankingSeq=8&amp;rankingSectionId=100" class="nclicks(rig.rankpol)" title="[외교 인사이드] 김연철 모르게 전달된 조의문… 南도 北도 '통일부 패싱'">[외교 인사이드] 김연철 모르게 전달된 조의문… 南도 北도 '통일부 패싱'</a> </li> 
       <li><span class="rank num9"><em>9</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=214&amp;aid=0000990696&amp;date=20191102&amp;type=2&amp;rankingSeq=9&amp;rankingSectionId=100" class="nclicks(rig.rankpol)" title="文 퇴임 후 &quot;양산 간다&quot;…사저 경호 예산 편성">文 퇴임 후 &quot;양산 간다&quot;…사저 경호 예산 편성</a> </li> 
       <li><span class="rank num10"><em>10</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=025&amp;aid=0002949729&amp;date=20191102&amp;type=1&amp;rankingSeq=10&amp;rankingSectionId=100" class="nclicks(rig.rankpol)" title="오늘부터 또 밖으로 돈다&middot;&middot;&middot;'아스팔트 우파'에 기대는 황교안">오늘부터 또 밖으로 돈다&middot;&middot;&middot;'아스팔트 우파'에 기대는 황교안</a> </li> 
      </ul> 
      <a href="/main/ranking/popularDay.nhn" class="more_link"><span class="blind">가장 많이 본 뉴스</span>더보기</a> 
     </div> 
     <div id="ranking_101" style="display:none"> 
      <h5 class="blind">경제</h5> 
      <ul class="section_list_ranking"> 
       <li><span class="rank num1"><em>1</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=056&amp;aid=0010759573&amp;date=20191102&amp;type=2&amp;rankingSeq=1&amp;rankingSectionId=101" class="nclicks(rig.rankeco)" title="‘타다 기소’ 진실게임…검찰 “협의했다” vs 국토부 “모르는 일”">‘타다 기소’ 진실게임…검찰 “협의했다” vs 국토부 “모르는 일”</a> </li> 
       <li><span class="rank num2"><em>2</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=001&amp;aid=0011185141&amp;date=20191102&amp;type=1&amp;rankingSeq=2&amp;rankingSectionId=101" class="nclicks(rig.rankeco)" title="0%대 정기예금 속속 재등장…2%대 실종">0%대 정기예금 속속 재등장…2%대 실종</a> </li> 
       <li><span class="rank num3"><em>3</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=008&amp;aid=0004303164&amp;date=20191102&amp;type=1&amp;rankingSeq=3&amp;rankingSectionId=101" class="nclicks(rig.rankeco)" title="의왕 인덕원 신축아파트에 '프리미엄 4억' 붙은 이유가">의왕 인덕원 신축아파트에 '프리미엄 4억' 붙은 이유가</a> </li> 
       <li><span class="rank num4"><em>4</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=008&amp;aid=0004303153&amp;date=20191102&amp;type=1&amp;rankingSeq=4&amp;rankingSectionId=101" class="nclicks(rig.rankeco)" title="수도권 노후경유차는 12월~3월 운행 못한다">수도권 노후경유차는 12월~3월 운행 못한다</a> </li> 
       <li><span class="rank num5"><em>5</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=016&amp;aid=0001597482&amp;date=20191102&amp;type=1&amp;rankingSeq=5&amp;rankingSectionId=101" class="nclicks(rig.rankeco)" title="“오를 곳은 올랐다” 전국 대장주 아파트 6개월 연속 상승…역대 최고치">“오를 곳은 올랐다” 전국 대장주 아파트 6개월 연속 상승…역대 최고치</a> </li> 
       <li><span class="rank num6"><em>6</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=009&amp;aid=0004456153&amp;date=20191101&amp;type=1&amp;rankingSeq=6&amp;rankingSectionId=101" class="nclicks(rig.rankeco)" title="`-14%` 망가진 수출…쌓이는 공장매물">`-14%` 망가진 수출…쌓이는 공장매물</a> </li> 
       <li><span class="rank num7"><em>7</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=008&amp;aid=0004303172&amp;date=20191102&amp;type=1&amp;rankingSeq=7&amp;rankingSectionId=101" class="nclicks(rig.rankeco)" title="&quot;이사갈때 전세금 못받을까봐 불안해요&quot;">&quot;이사갈때 전세금 못받을까봐 불안해요&quot;</a> </li> 
       <li><span class="rank num8"><em>8</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=025&amp;aid=0002949732&amp;date=20191102&amp;type=1&amp;rankingSeq=8&amp;rankingSectionId=101" class="nclicks(rig.rankeco)" title="'전기차 세계2위' 되겠다는 현대차, 배터리 직접 만들까">'전기차 세계2위' 되겠다는 현대차, 배터리 직접 만들까</a> </li> 
       <li><span class="rank num9"><em>9</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=422&amp;aid=0000399369&amp;date=20191101&amp;type=2&amp;rankingSeq=9&amp;rankingSectionId=101" class="nclicks(rig.rankeco)" title="&quot;술 마실때 얼굴 빨개지는 사람, 류머티즘 취약&quot;">&quot;술 마실때 얼굴 빨개지는 사람, 류머티즘 취약&quot;</a> </li> 
       <li><span class="rank num10"><em>10</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=025&amp;aid=0002949650&amp;date=20191101&amp;type=1&amp;rankingSeq=10&amp;rankingSectionId=101" class="nclicks(rig.rankeco)" title="직원들 'I have a dream' 떼창에…끝내 눈시울 붉힌 한샘 회장">직원들 'I have a dream' 떼창에…끝내 눈시울 붉힌 한샘 회장</a> </li> 
      </ul> 
      <a href="/main/ranking/popularDay.nhn" class="more_link"><span class="blind">가장 많이 본 뉴스</span>더보기</a> 
     </div> 
     <div id="ranking_102" style="display:none"> 
      <h5 class="blind">사회</h5> 
      <ul class="section_list_ranking"> 
       <li><span class="rank num1"><em>1</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=214&amp;aid=0000990705&amp;date=20191102&amp;type=2&amp;rankingSeq=1&amp;rankingSectionId=102" class="nclicks(rig.ranksoc)" title="성추행 해놓고 '면책특권' 거짓말…처벌 어떻게?">성추행 해놓고 '면책특권' 거짓말…처벌 어떻게?</a> </li> 
       <li><span class="rank num2"><em>2</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=056&amp;aid=0010759587&amp;date=20191102&amp;type=2&amp;rankingSeq=2&amp;rankingSectionId=102" class="nclicks(rig.ranksoc)" title="김성태 ‘1심 판결 존중’…“김 의원&middot;이 전 회장 식사” 추가 증언">김성태 ‘1심 판결 존중’…“김 의원&middot;이 전 회장 식사” 추가 증언</a> </li> 
       <li><span class="rank num3"><em>3</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=023&amp;aid=0003484088&amp;date=20191102&amp;type=1&amp;rankingSeq=3&amp;rankingSectionId=102" class="nclicks(rig.ranksoc)" title="헬기 동체와 시신 1구 발견… 배 14척&middot;항공기 4대 동원해 밤샘 수색">헬기 동체와 시신 1구 발견… 배 14척&middot;항공기 4대 동원해 밤샘 수색</a> </li> 
       <li><span class="rank num4"><em>4</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=025&amp;aid=0002949725&amp;date=20191102&amp;type=1&amp;rankingSeq=4&amp;rankingSectionId=102" class="nclicks(rig.ranksoc)" title="&quot;착해서 보호자로 헬기 탔을 것&quot; 홍게잡이 선원 여동생 눈물">&quot;착해서 보호자로 헬기 탔을 것&quot; 홍게잡이 선원 여동생 눈물</a> </li> 
       <li><span class="rank num5"><em>5</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=025&amp;aid=0002949717&amp;date=20191102&amp;type=1&amp;rankingSeq=5&amp;rankingSectionId=102" class="nclicks(rig.ranksoc)" title="출산후 세끼 미역국 먹는 당신&middot;&middot;&middot;의사들은 갑상샘 걱정한다">출산후 세끼 미역국 먹는 당신&middot;&middot;&middot;의사들은 갑상샘 걱정한다</a> </li> 
       <li><span class="rank num6"><em>6</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=056&amp;aid=0010759589&amp;date=20191102&amp;type=1&amp;rankingSeq=6&amp;rankingSectionId=102" class="nclicks(rig.ranksoc)" title="[취재후] 미국은 소지만 해도 징역 5년…우리나라는 ‘솜방망이’ 처벌 왜?">[취재후] 미국은 소지만 해도 징역 5년…우리나라는 ‘솜방망이’ 처벌 왜?</a> </li> 
       <li><span class="rank num7"><em>7</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=001&amp;aid=0011185151&amp;date=20191102&amp;type=1&amp;rankingSeq=7&amp;rankingSectionId=102" class="nclicks(rig.ranksoc)" title="英경찰 &quot;냉동컨테이너 희생자 39명, 전원 베트남인 추정&quot;">英경찰 &quot;냉동컨테이너 희생자 39명, 전원 베트남인 추정&quot;</a> </li> 
       <li><span class="rank num8"><em>8</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=437&amp;aid=0000223295&amp;date=20191101&amp;type=2&amp;rankingSeq=8&amp;rankingSectionId=102" class="nclicks(rig.ranksoc)" title="병원 도착하기도 전에 사망 판정…여러 장의 '사체검안서'">병원 도착하기도 전에 사망 판정…여러 장의 '사체검안서'</a> </li> 
       <li><span class="rank num9"><em>9</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=025&amp;aid=0002949734&amp;date=20191102&amp;type=2&amp;rankingSeq=9&amp;rankingSectionId=102" class="nclicks(rig.ranksoc)" title="&quot;190cm 범인 만나도 문제 없어&quot;…'마동석 실사판' 경찰 24명 뭉쳤다">&quot;190cm 범인 만나도 문제 없어&quot;…'마동석 실사판' 경찰 24명 뭉쳤다</a> </li> 
       <li><span class="rank num10"><em>10</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=005&amp;aid=0001255126&amp;date=20191102&amp;type=1&amp;rankingSeq=10&amp;rankingSectionId=102" class="nclicks(rig.ranksoc)" title="헬기 독도 해상 추락 14시간 만에… 수심 72m 지점서 동체 찾아">헬기 독도 해상 추락 14시간 만에… 수심 72m 지점서 동체 찾아</a> </li> 
      </ul> 
      <a href="/main/ranking/popularDay.nhn" class="more_link"><span class="blind">가장 많이 본 뉴스</span>더보기</a> 
     </div> 
     <div id="ranking_103" style="display:none"> 
      <h5 class="blind">생활/문화</h5> 
      <ul class="section_list_ranking"> 
       <li><span class="rank num1"><em>1</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=018&amp;aid=0004506813&amp;date=20191101&amp;type=1&amp;rankingSeq=1&amp;rankingSectionId=103" class="nclicks(rig.ranklif)" title="대상 오너家 임세령, 이정재와 동반 출국..&quot;재벌 패션의 1인자&quot;">대상 오너家 임세령, 이정재와 동반 출국..&quot;재벌 패션의 1인자&quot;</a> </li> 
       <li><span class="rank num2"><em>2</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=056&amp;aid=0010759608&amp;date=20191102&amp;type=1&amp;rankingSeq=2&amp;rankingSectionId=103" class="nclicks(rig.ranklif)" title="[박광식의 건강365] ‘전기 슉슉’ 대상포진, 3일 안에 항바이러스제 복용해야!">[박광식의 건강365] ‘전기 슉슉’ 대상포진, 3일 안에 항바이러스제 복용해야!</a> </li> 
       <li><span class="rank num3"><em>3</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=001&amp;aid=0011185159&amp;date=20191102&amp;type=1&amp;rankingSeq=3&amp;rankingSectionId=103" class="nclicks(rig.ranklif)" title="[D스토리] 30대 스타 부부가 20대 대학생 입양한 사연은">[D스토리] 30대 스타 부부가 20대 대학생 입양한 사연은</a> </li> 
       <li><span class="rank num4"><em>4</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=023&amp;aid=0003484169&amp;date=20191102&amp;type=1&amp;rankingSeq=4&amp;rankingSectionId=103" class="nclicks(rig.ranklif)" title="[김지수의 인터스텔라] 이영표 “축구도 삶도, 나는 이기적으로 헌신을 선택했다&quot;">[김지수의 인터스텔라] 이영표 “축구도 삶도, 나는 이기적으로 헌신을 선택했다&quot;</a> </li> 
       <li><span class="rank num5"><em>5</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=421&amp;aid=0004283365&amp;date=20191102&amp;type=1&amp;rankingSeq=5&amp;rankingSectionId=103" class="nclicks(rig.ranklif)" title="'억 소리' 요란한 벤츠 EQC, 전기차시대 '벤치 신세'될라">'억 소리' 요란한 벤츠 EQC, 전기차시대 '벤치 신세'될라</a> </li> 
       <li><span class="rank num6"><em>6</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=009&amp;aid=0004456149&amp;date=20191101&amp;type=1&amp;rankingSeq=6&amp;rankingSectionId=103" class="nclicks(rig.ranklif)" title="가전 최대 50%, 그랜저 350만원 할인…`핫한 코세페`">가전 최대 50%, 그랜저 350만원 할인…`핫한 코세페`</a> </li> 
       <li><span class="rank num7"><em>7</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=296&amp;aid=0000043156&amp;date=20191101&amp;type=1&amp;rankingSeq=7&amp;rankingSectionId=103" class="nclicks(rig.ranklif)" title="함중아, 폐암 투병 중 별세…폐암 생존율 왜 낮을까">함중아, 폐암 투병 중 별세…폐암 생존율 왜 낮을까</a> </li> 
       <li><span class="rank num8"><em>8</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=469&amp;aid=0000436458&amp;date=20191102&amp;type=1&amp;rankingSeq=8&amp;rankingSectionId=103" class="nclicks(rig.ranklif)" title="세 명이 하는 연애… “독점 아닌 사랑이 가능할까요?”">세 명이 하는 연애… “독점 아닌 사랑이 가능할까요?”</a> </li> 
       <li><span class="rank num9"><em>9</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=018&amp;aid=0004505921&amp;date=20191101&amp;type=1&amp;rankingSeq=9&amp;rankingSectionId=103" class="nclicks(rig.ranklif)" title="김건모♥장지연 결혼, 경기도에 신혼집 마련">김건모♥장지연 결혼, 경기도에 신혼집 마련</a> </li> 
       <li><span class="rank num10"><em>10</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=015&amp;aid=0004234719&amp;date=20191102&amp;type=1&amp;rankingSeq=10&amp;rankingSectionId=103" class="nclicks(rig.ranklif)" title="[너의 이름은] 남자의 로망?…'메르세데스-벤츠'는 두 여자다">[너의 이름은] 남자의 로망?…'메르세데스-벤츠'는 두 여자다</a> </li> 
      </ul> 
      <a href="/main/ranking/popularDay.nhn" class="more_link"><span class="blind">가장 많이 본 뉴스</span>더보기</a> 
     </div> 
     <div id="ranking_104" style="display:none"> 
      <h5 class="blind">세계</h5> 
      <ul class="section_list_ranking"> 
       <li><span class="rank num1"><em>1</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=011&amp;aid=0003644770&amp;date=20191102&amp;type=1&amp;rankingSeq=1&amp;rankingSectionId=104" class="nclicks(rig.rankwor)" title="‘21세기 최악의 테러리스트’ 수괴 잃은 IS, 전 세계 테러리즘 소멸로 이어질까">‘21세기 최악의 테러리스트’ 수괴 잃은 IS, 전 세계 테러리즘 소멸로 이어질까</a> </li> 
       <li><span class="rank num2"><em>2</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=056&amp;aid=0010759599&amp;date=20191102&amp;type=2&amp;rankingSeq=2&amp;rankingSectionId=104" class="nclicks(rig.rankwor)" title="[자막뉴스] 중국 “홍콩에 전면 통제권 행사…공산당 지배력 강화”">[자막뉴스] 중국 “홍콩에 전면 통제권 행사…공산당 지배력 강화”</a> </li> 
       <li><span class="rank num3"><em>3</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=005&amp;aid=0001255014&amp;date=20191101&amp;type=1&amp;rankingSeq=3&amp;rankingSectionId=104" class="nclicks(rig.rankwor)" title="‘탕’ 소리 후 피 흘리며 쓰러진 7살… 핼러윈 참극">‘탕’ 소리 후 피 흘리며 쓰러진 7살… 핼러윈 참극</a> </li> 
       <li><span class="rank num4"><em>4</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=055&amp;aid=0000769418&amp;date=20191102&amp;type=2&amp;rankingSeq=4&amp;rankingSectionId=104" class="nclicks(rig.rankwor)" title="총격 얼룩진 美 핼러윈…파티장 총성 '아수라장' 4명 사망">총격 얼룩진 美 핼러윈…파티장 총성 '아수라장' 4명 사망</a> </li> 
       <li><span class="rank num5"><em>5</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=214&amp;aid=0000990697&amp;date=20191102&amp;type=2&amp;rankingSeq=5&amp;rankingSectionId=104" class="nclicks(rig.rankwor)" title="한국인이 日 '슈리성' 방화?…혐한 SNS 확산">한국인이 日 '슈리성' 방화?…혐한 SNS 확산</a> </li> 
       <li><span class="rank num6"><em>6</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=277&amp;aid=0004564605&amp;date=20191101&amp;type=1&amp;rankingSeq=6&amp;rankingSectionId=104" class="nclicks(rig.rankwor)" title="&quot;지인 3명 살해 후 시신도 먹었다&quot;…충격 '식인 남성' 체포">&quot;지인 3명 살해 후 시신도 먹었다&quot;…충격 '식인 남성' 체포</a> </li> 
       <li><span class="rank num7"><em>7</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=025&amp;aid=0002949713&amp;date=20191102&amp;type=1&amp;rankingSeq=7&amp;rankingSectionId=104" class="nclicks(rig.rankwor)" title="[떠먹국] 미국이 쿠르드 배신? 알고보면 복잡한 속내 있다">[떠먹국] 미국이 쿠르드 배신? 알고보면 복잡한 속내 있다</a> </li> 
       <li><span class="rank num8"><em>8</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=081&amp;aid=0003040463&amp;date=20191101&amp;type=1&amp;rankingSeq=8&amp;rankingSectionId=104" class="nclicks(rig.rankwor)" title="5년 동안 남동생 치료비 보태려고 하루 330원만 쓴 24세 중국 여대생">5년 동안 남동생 치료비 보태려고 하루 330원만 쓴 24세 중국 여대생</a> </li> 
       <li><span class="rank num9"><em>9</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=214&amp;aid=0000990720&amp;date=20191102&amp;type=2&amp;rankingSeq=9&amp;rankingSectionId=104" class="nclicks(rig.rankwor)" title="美 '핼러윈 참사' 잇따라…파티장 총격 4명 사망">美 '핼러윈 참사' 잇따라…파티장 총격 4명 사망</a> </li> 
       <li><span class="rank num10"><em>10</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=055&amp;aid=0000769288&amp;date=20191101&amp;type=1&amp;rankingSeq=10&amp;rankingSectionId=104" class="nclicks(rig.rankwor)" title="[Pick] &quot;아이 낳자&quot;는 여자친구 말에 17살 소년이 저지른 끔찍한 행동">[Pick] &quot;아이 낳자&quot;는 여자친구 말에 17살 소년이 저지른 끔찍한 행동</a> </li> 
      </ul> 
      <a href="/main/ranking/popularDay.nhn" class="more_link"><span class="blind">가장 많이 본 뉴스</span>더보기</a> 
     </div> 
     <div id="ranking_105" style="display:none"> 
      <h5 class="blind">IT/과학</h5> 
      <ul class="section_list_ranking"> 
       <li><span class="rank num1"><em>1</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=001&amp;aid=0011185134&amp;date=20191102&amp;type=1&amp;rankingSeq=1&amp;rankingSectionId=105" class="nclicks(rig.ranksci)" title="5G 타고 삼성이 돌아왔다…중국 초대형 매장 열고 '총공세'">5G 타고 삼성이 돌아왔다…중국 초대형 매장 열고 '총공세'</a> </li> 
       <li><span class="rank num2"><em>2</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=015&amp;aid=0004234597&amp;date=20191101&amp;type=1&amp;rankingSeq=2&amp;rankingSectionId=105" class="nclicks(rig.ranksci)" title="&quot;판교 마지막 금싸라기 땅 잡아라&quot; 카카오 - 엔씨소프트 격돌">&quot;판교 마지막 금싸라기 땅 잡아라&quot; 카카오 - 엔씨소프트 격돌</a> </li> 
       <li><span class="rank num3"><em>3</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=009&amp;aid=0004456155&amp;date=20191101&amp;type=1&amp;rankingSeq=3&amp;rankingSectionId=105" class="nclicks(rig.ranksci)" title="[단독] 삼성전자 `갤S10 LTE` 출고가 인하…최대 30만원">[단독] 삼성전자 `갤S10 LTE` 출고가 인하…최대 30만원</a> </li> 
       <li><span class="rank num4"><em>4</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=092&amp;aid=0002173832&amp;date=20191101&amp;type=1&amp;rankingSeq=4&amp;rankingSectionId=105" class="nclicks(rig.ranksci)" title="에어팟 프로 분해해보니… “배터리 못 바꾸는 일회용 제품”">에어팟 프로 분해해보니… “배터리 못 바꾸는 일회용 제품”</a> </li> 
       <li><span class="rank num5"><em>5</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=008&amp;aid=0004303141&amp;date=20191102&amp;type=1&amp;rankingSeq=5&amp;rankingSectionId=105" class="nclicks(rig.ranksci)" title="&quot;접어야 산다&quot;…막 오른 폴더블폰 경쟁">&quot;접어야 산다&quot;…막 오른 폴더블폰 경쟁</a> </li> 
       <li><span class="rank num6"><em>6</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=092&amp;aid=0002173893&amp;date=20191102&amp;type=1&amp;rankingSeq=6&amp;rankingSectionId=105" class="nclicks(rig.ranksci)" title="블리즈컨2019 막 올랐다...디아블로4-오버워치2 깜짝 공개">블리즈컨2019 막 올랐다...디아블로4-오버워치2 깜짝 공개</a> </li> 
       <li><span class="rank num7"><em>7</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=277&amp;aid=0004565026&amp;date=20191102&amp;type=1&amp;rankingSeq=7&amp;rankingSectionId=105" class="nclicks(rig.ranksci)" title="삼성 대 애플? 이제는 삼성 대 화웨이…격차는 단 3%P">삼성 대 애플? 이제는 삼성 대 화웨이…격차는 단 3%P</a> </li> 
       <li><span class="rank num8"><em>8</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=031&amp;aid=0000514278&amp;date=20191102&amp;type=1&amp;rankingSeq=8&amp;rankingSectionId=105" class="nclicks(rig.ranksci)" title="매장 CCTV 왜 많지?…&quot;감시 아니고 마케팅용입니다&quot;">매장 CCTV 왜 많지?…&quot;감시 아니고 마케팅용입니다&quot;</a> </li> 
       <li><span class="rank num9"><em>9</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=008&amp;aid=0004303091&amp;date=20191101&amp;type=1&amp;rankingSeq=9&amp;rankingSectionId=105" class="nclicks(rig.ranksci)" title="&quot;타다 재판 간다는데…계속 몰아도 될까요?&quot;">&quot;타다 재판 간다는데…계속 몰아도 될까요?&quot;</a> </li> 
       <li><span class="rank num10"><em>10</em></span> <a href="/main/ranking/read.nhn?mid=etc&amp;sid1=111&amp;rankingType=popular_day&amp;oid=031&amp;aid=0000514281&amp;date=20191102&amp;type=1&amp;rankingSeq=10&amp;rankingSectionId=105" class="nclicks(rig.ranksci)" title="베일 벗은 디아블로4&middot;오버워치2…블리즈컨서 첫 선">베일 벗은 디아블로4&middot;오버워치2…블리즈컨서 첫 선</a> </li> 
      </ul> 
      <a href="/main/ranking/popularDay.nhn" class="more_link"><span class="blind">가장 많이 본 뉴스</span>더보기</a> 
     </div> 
    </div> 
    <div class="da" id="doubleDA"></div> 
    <script type="text/javascript">
    var ranking_selectedSectionId = '';
    var ranking_listAllSection = jindo.$A(['100', '101', '102', '103', '104', '105']);
    function ranking_select_tab(sectionId) {
    jindo.$('right.ranking_tab_' + sectionId).innerHTML = "<strong>" + ranking_select_section_name(sectionId) + "</strong>";
    jindo.$Element('right.ranking_tab_' + sectionId).addClass('is_click').attr('aria-selected', true);
    if (ranking_selectedSectionId) {
    jindo.$('right.ranking_tab_' + ranking_selectedSectionId).innerHTML = ranking_select_section_name(ranking_selectedSectionId);
    jindo.$Element('right.ranking_tab_' + ranking_selectedSectionId).removeClass('is_click').attr('aria-selected', false);
    }
    if (ranking_selectedSectionId == sectionId) {
    jindo.$('right.ranking_tab_' + sectionId).innerHTML = "<strong>" + ranking_select_section_name(sectionId) + "</strong>";
    jindo.$Element('right.ranking_tab_' + ranking_selectedSectionId).addClass('is_click').attr('aria-selected', true);
    }
    ranking_selectedSectionId = sectionId;
    }
    function ranking_select_section(sectionId) {
    if (!ranking_listAllSection.has(sectionId)) {
    sectionId = '100';
    }
    jindo.$('right.ranking_contents').innerHTML = jindo.$('ranking_' + sectionId).innerHTML;
    ranking_select_tab(sectionId);
    }
    function ranking_select_section_name(sectionId) {
    var selectSectionName = "정치";
    switch (sectionId) {
    case '100' : selectSectionName = "정치"; break;
    case '101' : selectSectionName = "경제"; break;
    case '102' : selectSectionName = "사회"; break;
    case '103' : selectSectionName = "생활/문화"; break;
    case '104' : selectSectionName = "세계"; break;
    case '105' : selectSectionName = "IT/과학"; break;
    default : selectSectionName = "정치";
    }
    return selectSectionName;
    }
    function ranking_tab_handler(event) {
    var sectionId = jindo.$Event(event).element.id.replace('right\.ranking_tab_', '');
    if (sectionId) {
    ranking_select_section(sectionId);
    }
    }
    ranking_listAllSection.forEach(function (v, i, o) {
    jindo.$Fn(ranking_tab_handler, window).attach(jindo.$Element(jindo.$('right.ranking_tab_' + v)), 'mouseover');
    });
    ranking_select_section('101');
    </script> 
    <div class="section as_finance"> 
     <div class="as_finance_tit"> 
      <ul class="as_finance_tab" role="tab_list"> 
       <li class="on" id="tab_0"><a href="#" class="tab_stock" role="tab" aria-selected="true" onclick="return false;" onkeydown="finance_tab_focus(this);"><strong>증권</strong></a></li> 
       <li id="tab_1"><a href="#" class="tab_fund" role="tab" aria-selected="false" onclick="return false;" onkeydown="finance_tab_focus(this);">펀드</a></li> 
       <li id="tab_2"><a href="#" class="tab_exchange" role="tab" aria-selected="false" onclick="return false;" onkeydown="finance_tab_focus(this);">환율</a></li> 
      </ul> 
      <h4 class="blind">증권</h4> 
     </div> 
     <div id="finance_tab_0"> 
      <div class="as_finance_content_wrap"> 
       <div class="as_finance_content"> 
        <table cellpadding="0" cellspacing="0" class="table_finance"> 
         <caption class="blind">
          코스피,코스닥 지수
         </caption> 
         <colgroup> 
          <col width="66" /> 
          <col width="76" /> 
          <col /> 
          <col /> 
         </colgroup> 
         <tbody> 
          <tr> 
           <th scope="row"><a href="https://finance.naver.com/sise/sise_index.nhn?code=KOSPI" target="_blank" class="visit nclicks(rig.finance)">코스피</a></th> 
           <td class="num">2,100.20</td> 
           <td class="num up"><i>상승</i>16.72</td> 
           <td class="num fluctuation">+0.80%</td> 
          </tr> 
          <tr> 
           <th scope="row"><a href="https://finance.naver.com/sise/sise_index.nhn?code=KOSDAQ" target="_blank" class="visit">코스닥</a></th> 
           <td class="num">662.34</td> 
           <td class="num up"><i>상승</i>3.82</td> 
           <td class="num fluctuation">+0.58%</td> 
          </tr> 
         </tbody> 
        </table> 
        <form action="https://finance.naver.com/search/search.nhn" method="get" onsubmit="return stock_search_1079042(); return false;" target="_blank"> 
         <fieldset class="finance"> 
          <legend>증권 종목검색</legend> 
          <span> <label for="stockSearchQuery_1079042" class="blind">검색어 입력</label> <input type="text" id="stockSearchQuery_1079042" class="finance_search_input" name="query" placeholder="종목검색" /> </span> 
          <button class="finance_search_btn nclicks(rig.finance)">종목검색</button> 
          <a href="https://finance.naver.com/mystock/" class="finance_my_link nclicks(rig.finance)" target="_blank">마이스톡</a> 
         </fieldset> 
        </form> 
       </div> 
      </div> 
      <div class="as_finance_more"> 
       <dl class="as_finance_search_top"> 
        <dt>
         검색상위
        </dt> 
        <dd> 
         <a href="https://finance.naver.com/item/main.nhn?code=028300" target="_blank" class="visit nclicks(rig.finance)">에이치엘</a> 
         <span>|</span> 
         <a href="https://finance.naver.com/item/main.nhn?code=074610" target="_blank" class="visit nclicks(rig.finance)">나노메딕</a> 
         <span>|</span> 
         <a href="https://finance.naver.com/item/main.nhn?code=005930" target="_blank" class="visit nclicks(rig.finance)">삼성전자</a> 
        </dd> 
       </dl> 
      </div> 
     </div> 
     <div id="finance_tab_1" style="display:none"> 
      <div class="as_finance_content_wrap"> 
       <div class="as_finance_content"> 
        <h4 class="blind">편드</h4> 
        <table cellpadding="0" cellspacing="0" class="table_finance table_fund" summary="오늘 기준 3개월 수익률 상위펀드의 상품명과 수익률을 제공합니다."> 
         <caption class="blind">
          수익률 상위펀드
         </caption> 
         <colgroup> 
          <col width="192" /> 
          <col /> 
         </colgroup> 
         <tbody> 
          <tr> 
           <th scope="row"><a href="https://finance.naver.com/fund/fundDetail.nhn?fundCd=KR5308586050" target="_blank">PAM부동산 3</a></th> 
           <td class="num fluctuation">55.27%</td> 
          </tr> 
          <tr> 
           <th scope="row"><a href="https://finance.naver.com/fund/fundDetail.nhn?fundCd=K55214CC2135" target="_blank">유진트리플리자드지수연계증권…</a></th> 
           <td class="num fluctuation">31.24%</td> 
          </tr> 
          <tr> 
           <th scope="row"><a href="https://finance.naver.com/fund/fundDetail.nhn?fundCd=KRM102772659" target="_blank">하나UBS암바토비니켈해외자…</a></th> 
           <td class="num fluctuation">24.56%</td> 
          </tr> 
         </tbody> 
        </table> 
        <form action="https://finance.naver.com/search/searchFundList.nhn" method="get" onsubmit="return fund_search_1079042(); return false;" target="_blank"> 
         <fieldset class="finance"> 
          <legend>펀드검색</legend> 
          <span> <label for="fundSearchQuery_1079042" class="blind">검색어 입력</label> <input type="text" id="fundSearchQuery_1079042" class="text02" name="query" placeholder="펀드검색" /> </span> 
          <button alt="펀드검색" class="finance_search_btn nclicks(rig.finance)">펀드검색</button> 
          <a href="https://finance.naver.com/myfund/holdList.nhn" target="_blank" class="finance_my_link">마이펀드</a> 
         </fieldset> 
        </form> 
        <div class="fund_top"> 
         <a href="https://finance.naver.com/fund/fundFinder.nhn" target="_blank" class="more_link nclicks(rig.finance)">수익률 상위펀드 더보기</a> 
        </div> 
       </div> 
      </div> 
     </div> 
     <div id="finance_tab_2" style="display:none"> 
      <div class="as_finance_content_wrap"> 
       <div class="as_finance_content"> 
        <table cellpadding="0" cellspacing="0" class="table_finance_exchange"> 
         <caption class="blind">
          환율정보
         </caption> 
         <colgroup> 
          <col width="114" /> 
          <col /> 
          <col width="64" /> 
         </colgroup> 
         <tbody> 
          <tr> 
           <th scope="row"><img src="https://imgnews.pstatic.net/image/news/2007/new_section/ico_flag_usa.gif" alt="1 USD" width="19" height="12" class="icon" /> 1 USD</th> 
           <td class="num">1,167.00</td> 
           <td class="num dn"><i>하락</i>-1.50</td> 
          </tr> 
          <tr> 
           <th scope="row"><img src="https://imgnews.pstatic.net/image/news/2007/new_section/ico_flag_europe.gif" alt="1 EUR" width="19" height="12" class="icon" /> 1 EUR</th> 
           <td class="num">1,301.03</td> 
           <td class="num dn"><i>하락</i>-3.48</td> 
          </tr> 
          <tr> 
           <th scope="row"><img src="https://imgnews.pstatic.net/image/news/2007/new_section/ico_flag_japan.gif" alt="100 JPY" width="19" height="12" class="icon" /> 100 JPY</th> 
           <td class="num">1,080.26</td> 
           <td class="num up"><i>상승</i>1.36</td> 
          </tr> 
          <tr> 
           <th scope="row"><img src="https://imgnews.pstatic.net/image/news/2007/new_section/ico_flag_china.gif" alt="1 CNY" width="19" height="12" class="icon" /> 1 CNY</th> 
           <td class="num">165.73</td> 
           <td class="num dn"><i>하락</i>-0.02</td> 
          </tr> 
         </tbody> 
        </table> 
       </div> 
      </div> 
      <div class="as_finance_more"> 
       <dl class="as_finance_time"> 
        <dt>
         기준
        </dt> 
        <dd>
         2019.11.01 20:07
        </dd> 
       </dl> 
       <a href="https://finance.naver.com/marketindex/exchangeMain.nhn" target="_blank" class="more_link2 nclicks(rig.finance)">환율정보 더보기</a> 
      </div> 
     </div> 
     <script type="text/javascript">
    function stock_search_1079042() {
    var obj = jindo.$('stockSearchQuery_1079042');
    var query = obj.value.replace(/[ ]/g, "");
    obj.value = query;
    if (query == '') {
    alert("검색어를 입력해주세요.");
    return false;
    }
    }
    function fund_search_1079042() {
    var obj = jindo.$('fundSearchQuery_1079042');
    var query = obj.value.replace(/[ ]/g, "");
    obj.value = query;
    if (query == '') {
    alert("검색어를 입력해주세요.");
    return false;
    }
    }
    function finance_tab() {
    jindo.$('tab_0').onmouseover = function () {
    var pst = 0;
    for(var i=0 ; i<3; i++) {
    var liObj = jindo.$('tab_'+i);
    var AObjInliObj = liObj.querySelector('a');
    if (i == pst) {
    liObj.className = "on";
    AObjInliObj.innerHTML = "<strong>"+liObj.innerText+"</strong>";
    AObjInliObj.setAttribute('aria-selected', true);
    jindo.$('finance_tab_'+i).style.display = '';
    } else {
    liObj.className = "";
    if ( liObj.textContent != null) {
    AObjInliObj.textContent = AObjInliObj.textContent.replace("<strong>", "").replace("</strong>", "");
    }
    AObjInliObj.setAttribute('aria-selected', false);
    jindo.$('finance_tab_'+i).style.display = 'none';
    }
    }
    }
    jindo.$('tab_1').onmouseover = function () {
    var pst = 1;
    for(var i=0 ; i<3; i++) {
    var liObj = jindo.$('tab_'+i);
    var AObjInliObj = liObj.querySelector('a');
    if (i == pst) {
    liObj.className = "on";
    AObjInliObj.innerHTML = "<strong>"+liObj.innerText+"</strong>";
    AObjInliObj.setAttribute('aria-selected', true);
    jindo.$('finance_tab_'+i).style.display = '';
    } else {
    liObj.className = "";
    if ( liObj.textContent != null) {
    AObjInliObj.textContent = AObjInliObj.textContent.replace("<strong>", "").replace("</strong>", "");
    }
    AObjInliObj.setAttribute('aria-selected', false);
    jindo.$('finance_tab_'+i).style.display = 'none';
    }
    }
    }
    jindo.$('tab_2').onmouseover = function () {
    var pst = 2;
    for(var i=0 ; i<3; i++) {
    var liObj = jindo.$('tab_'+i);
    var AObjInliObj = liObj.querySelector('a');
    if (i == pst) {
    liObj.className = "on";
    AObjInliObj.innerHTML = "<strong>"+liObj.innerText+"</strong>";
    AObjInliObj.setAttribute('aria-selected', true);
    jindo.$('finance_tab_'+i).style.display = '';
    } else {
    liObj.className = "";
    if ( liObj.textContent != null) {
    AObjInliObj.textContent = AObjInliObj.textContent.replace("<strong>", "").replace("</strong>", "");
    }
    AObjInliObj.setAttribute('aria-selected', false);
    jindo.$('finance_tab_'+i).style.display = 'none';
    }
    }
    }
    }
    function finance_tab_focus(el) {
    if(event.keyCode == '13') {
    jindo.$('tab_0').className = '';
    jindo.$('tab_0').querySelector('a').setAttribute('aria-selected', false);
    jindo.$('finance_tab_'+0).style.display = 'none';
    jindo.$('tab_1').className = '';
    jindo.$('tab_1').querySelector('a').setAttribute('aria-selected', false);
    jindo.$('finance_tab_'+1).style.display = 'none';
    jindo.$('tab_2').className = '';
    jindo.$('tab_2').querySelector('a').setAttribute('aria-selected', false);
    jindo.$('finance_tab_'+2).style.display = 'none';
    var liObj = jindo.$(el.parentElement);
    liObj.className = 'on';
    liObj.querySelector('a').setAttribute('aria-selected', true);
    jindo.$('finance_'+liObj.id).style.display = '';
    }
    }
    function setOnOff(id) {
    var imageOn = "https://ssl.pstatic.net/static.news/image/news/admin/btn_on.gif";
    var imageOff = "https://ssl.pstatic.net/static.news/image/news/admin/btn_off.gif";
    var imageObj = jindo.$("onOffBtn_"+id);
    var imageObjSrc = imageObj.src;
    var enableValue = "";
    if (imageObjSrc.indexOf('on') > 0) {
    imageValue = imageOff;
    enableValue = "off";
    } else if (imageObjSrc.indexOf('off') > 0) {
    imageValue = imageOn;
    enableValue = "on";
    }
    Copyright.setOnOff(id, enableValue, processOnOff);
    imageObj.src = imageValue;
    }
    finance_tab();
    </script> 
    </div> 
    <div class="section" style="margin-bottom:20px; white-space:nowrap;" id="right_dailyList"> 
     <h4>분야별 주요뉴스</h4> 
     <div class="classfy sd" style="display:block"> 
      <ul class="list_txt"> 
       <li> <a href="https://news.naver.com/main/read.nhn?mode=LSD&amp;mid=shm&amp;sid1=100&amp;oid=022&amp;aid=0003410932" class="nclicks(rig.secteco)" title="北 “초대형 방사포 성공” 靑 “위중한 위협 아니다”">北 “초대형 방사포 성공” 靑 “위중한 위협 아니다”</a> </li> 
       <li> <a href="https://news.naver.com/main/read.nhn?mode=LSD&amp;mid=shm&amp;sid1=100&amp;oid=022&amp;aid=0003410931" class="nclicks(rig.secteco)" title="박찬주는 역풍, 이자스민은 이적… ‘인재 복’ 없는 한국당">박찬주는 역풍, 이자스민은 이적… ‘인재 복’ 없는 한국당</a> </li> 
       <li> <a href="https://news.naver.com/main/read.nhn?mode=LSD&amp;mid=shm&amp;sid1=100&amp;oid=057&amp;aid=0001392937" class="nclicks(rig.secteco)" title="문 대통령, 퇴임후 양산 가나…사저 경호예산 22억 신청">문 대통령, 퇴임후 양산 가나…사저 경호예산 22억 신청</a> </li> 
       <li> <a href="https://news.naver.com/main/read.nhn?mode=LSD&amp;mid=shm&amp;sid1=104&amp;oid=215&amp;aid=0000820818" class="nclicks(rig.secteco)" title="아베, 日방문 한국 국회의원들 대놓고 홀대...日회장 &quot;한국 탓&quot;">아베, 日방문 한국 국회의원들 대놓고 홀대...日회장 &quot;한국 탓&quot;</a> </li> 
       <li> <a href="https://news.naver.com/main/read.nhn?mode=LSD&amp;mid=shm&amp;sid1=104&amp;oid=001&amp;aid=0011185110" class="nclicks(rig.secteco)" title="美민주, 이달중 탄핵조사 공개로 전환…탄핵사유 추가도 검토">美민주, 이달중 탄핵조사 공개로 전환…탄핵사유 추가도 검토</a> </li> 
      </ul> 
      <ul class="list_txt"> 
       <ul class="list_txt"> 
        <li> <a href="https://news.naver.com/main/read.nhn?mode=LSD&amp;mid=shm&amp;sid1=101&amp;oid=277&amp;aid=0004565025" class="nclicks(rig.secteco)" title="11개월 연속 줄어든 수출…10월 감소폭 3년9개월來 최대">11개월 연속 줄어든 수출…10월 감소폭 3년9개월來 최대</a> </li> 
        <li> <a href="https://news.naver.com/main/read.nhn?mode=LSD&amp;mid=shm&amp;sid1=101&amp;oid=008&amp;aid=0004302827" class="nclicks(rig.secteco)" title="[단독]삼성전자 50주년에…이재용, 비공개 日 출장">[단독]삼성전자 50주년에…이재용, 비공개 日 출장</a> </li> 
        <li> <a href="https://news.naver.com/main/read.nhn?mode=LSD&amp;mid=shm&amp;sid1=101&amp;oid=629&amp;aid=0000002855" class="nclicks(rig.secteco)" title="국토부 '분양가 상한제' 적용지역, 집값 요동치는 '비강남권'도 사정권">국토부 '분양가 상한제' 적용지역, 집값 요동치는 '비강남권'도 사정권</a> </li> 
        <li> <a href="https://news.naver.com/main/read.nhn?mode=LSD&amp;mid=shm&amp;sid1=105&amp;oid=031&amp;aid=0000514281" class="nclicks(rig.secteco)" title="베일 벗은 디아블로4&middot;오버워치2…블리즈컨서 첫 선">베일 벗은 디아블로4&middot;오버워치2…블리즈컨서 첫 선</a> </li> 
        <li> <a href="https://news.naver.com/main/read.nhn?mode=LSD&amp;mid=shm&amp;sid1=105&amp;oid=008&amp;aid=0004302992" class="nclicks(rig.secteco)" title="네이버 '실시간 검색어' 정치색&middot;광고 사라질까">네이버 '실시간 검색어' 정치색&middot;광고 사라질까</a> </li> 
       </ul> 
       <ul class="list_txt"> 
        <ul class="list_txt"> 
         <li> <a href="https://news.naver.com/main/read.nhn?mode=LSD&amp;mid=shm&amp;sid1=102&amp;oid=422&amp;aid=0000399373" class="nclicks(rig.secteco)" title="독도 수중수색 재개…가족들 사고해역으로">독도 수중수색 재개…가족들 사고해역으로</a> </li> 
         <li> <a href="https://news.naver.com/main/read.nhn?mode=LSD&amp;mid=shm&amp;sid1=102&amp;oid=056&amp;aid=0010759573" class="nclicks(rig.secteco)" title="‘타다 기소’ 진실게임…검찰 “협의했다” vs 국토부 “모르는 일”">‘타다 기소’ 진실게임…검찰 “협의했다” vs 국토부 “모르는 일”</a> </li> 
         <li> <a href="https://news.naver.com/main/read.nhn?mode=LSD&amp;mid=shm&amp;sid1=102&amp;oid=008&amp;aid=0004303153" class="nclicks(rig.secteco)" title="수도권 노후경유차는 12월~3월 운행 못한다">수도권 노후경유차는 12월~3월 운행 못한다</a> </li> 
         <li> <a href="https://news.naver.com/main/read.nhn?mode=LSD&amp;mid=shm&amp;sid1=103&amp;oid=018&amp;aid=0004506635" class="nclicks(rig.secteco)" title="완성차 내수 1개월 만에 역성장…기아차만 ‘질주’(종합)">완성차 내수 1개월 만에 역성장…기아차만 ‘질주’(종합)</a> </li> 
         <li> <a href="https://news.naver.com/main/read.nhn?mode=LSD&amp;mid=shm&amp;sid1=103&amp;oid=018&amp;aid=0004506315" class="nclicks(rig.secteco)" title="가수 함중아, 폐암 투병 끝 별세.. 향년 67세">가수 함중아, 폐암 투병 끝 별세.. 향년 67세</a> </li> 
        </ul> 
       </ul>
      </ul>
     </div> 
    </div> 
    <div class="section"> 
     <div class="banner"> 
      <a href="https://media.naver.com/channel/setting.nhn?back=main" class="nclicks(rig.banner)" target="_blank"> <img src="https://imgnews.pstatic.net/image/upload/item/2018/11/27/174933298_PC_%25BF%25EC%25C3%25F8%25B9%25E8%25B3%25CA_%25B1%25B8%25B5%25B6%25C8%25B0%25BC%25BA%25C8%25AD.png" width="300" alt="네이버 메인에서 바로 보는 언론사 편집뉴스 지금 바로 구독해보세요!" /> </a> 
     </div> 
    </div> 
    <div class="section"> 
     <div class="banner"> 
      <a href="https://news.naver.com/main/ombudsman/guidecenter.nhn?mid=omb" class="nclicks(rig.banner)" target="_blank"> <img src="https://imgnews.pstatic.net/image/upload/item/2018/08/29/183229335_%25BD%25C5%25B0%25ED%25B9%25E8%25B3%25CA.png" width="300" alt="뉴스 기사와 댓글로 인한 문제 발생 시 24시간 센터로 접수해주세요" /> </a> 
     </div> 
    </div> 
    <div class="section hottopic" id="newstopic_container"> 
     <h4>뉴스토픽</h4> 
     <div class="category" role="tablist" id="newstopic_tab"> 
      <a href="#" onclick="return false;" class="is_click" role="tab" aria-selected="true" data-tab="news">뉴스</a> 
      <a href="#" onclick="return false;" role="tab" aria-selected="false" data-tab="entertain">연예/스포츠</a> 
     </div> 
     <ol class="newstopic_list" id="newstopic_news"> 
      <li><a href="https://search.naver.com/search.naver?where=nexearch&amp;query=%EC%98%A4%EB%8A%98+%EB%82%A0%EC%94%A8&amp;ie=utf8&amp;sm=nws_htk.nws" class="nclicks(rig.newstopic)" target="_blank" title="오늘 날씨"><span class="rank num1"><em>1</em></span> <strong class="title">오늘 날씨</strong></a></li> 
      <li><a href="https://search.naver.com/search.naver?where=nexearch&amp;query=%EB%AF%B8%EC%A4%91+%EB%AC%B4%EC%97%AD%ED%98%91%EC%83%81&amp;ie=utf8&amp;sm=nws_htk.nws" class="nclicks(rig.newstopic)" target="_blank" title="미중 무역협상"><span class="rank num2"><em>2</em></span> <strong class="title">미중 무역협상</strong></a></li> 
      <li><a href="https://search.naver.com/search.naver?where=nexearch&amp;query=%EC%98%A4%EB%8A%98%EC%9D%98+%EC%9A%B4%EC%84%B8&amp;ie=utf8&amp;sm=nws_htk.nws" class="nclicks(rig.newstopic)" target="_blank" title="오늘의 운세"><span class="rank num3"><em>3</em></span> <strong class="title">오늘의 운세</strong></a></li> 
      <li><a href="https://search.naver.com/search.naver?where=nexearch&amp;query=%EB%89%B4%EC%9A%95+%EC%A6%9D%EC%8B%9C&amp;ie=utf8&amp;sm=nws_htk.nws" class="nclicks(rig.newstopic)" target="_blank" title="뉴욕 증시"><span class="rank num4"><em>4</em></span> <strong class="title">뉴욕 증시</strong></a></li> 
      <li><a href="https://search.naver.com/search.naver?where=nexearch&amp;query=%EA%B0%80%EC%9D%84+%EB%82%98%EB%93%A4%EC%9D%B4&amp;ie=utf8&amp;sm=nws_htk.nws" class="nclicks(rig.newstopic)" target="_blank" title="가을 나들이"><span class="rank num5"><em>5</em></span> <strong class="title">가을 나들이</strong></a></li> 
      <li><a href="https://search.naver.com/search.naver?where=nexearch&amp;query=%EB%AF%B8%EC%84%B8%EB%A8%BC%EC%A7%80+%EB%86%8D%EB%8F%84&amp;ie=utf8&amp;sm=nws_htk.nws" class="nclicks(rig.newstopic)" target="_blank" title="미세먼지 농도"><span class="rank num6"><em>6</em></span> <strong class="title">미세먼지 농도</strong> <span class="newstopic_ico_new"><i>NEW</i></span></a></li> 
      <li><a href="https://search.naver.com/search.naver?where=nexearch&amp;query=%EB%B6%84%EC%96%91%EA%B0%80+%EC%83%81%ED%95%9C%EC%A0%9C&amp;ie=utf8&amp;sm=nws_htk.nws" class="nclicks(rig.newstopic)" target="_blank" title="분양가 상한제"><span class="rank num7"><em>7</em></span> <strong class="title">분양가 상한제</strong></a></li> 
      <li><a href="https://search.naver.com/search.naver?where=nexearch&amp;query=%ED%99%94%EC%84%B1+8%EC%B0%A8+%EC%82%AC%EA%B1%B4&amp;ie=utf8&amp;sm=nws_htk.nws" class="nclicks(rig.newstopic)" target="_blank" title="화성 8차 사건"><span class="rank num8"><em>8</em></span> <strong class="title">화성 8차 사건</strong></a></li> 
      <li><a href="https://search.naver.com/search.naver?where=nexearch&amp;query=%EC%A0%95%EC%8B%9C+%ED%99%95%EB%8C%80&amp;ie=utf8&amp;sm=nws_htk.nws" class="nclicks(rig.newstopic)" target="_blank" title="정시 확대"><span class="rank num9"><em>9</em></span> <strong class="title">정시 확대</strong></a></li> 
      <li><a href="https://search.naver.com/search.naver?where=nexearch&amp;query=%EC%A1%B0%EA%B5%AD+%EC%82%AC%ED%83%9C&amp;ie=utf8&amp;sm=nws_htk.nws" class="nclicks(rig.newstopic)" target="_blank" title="조국 사태"><span class="rank num10"><em>10</em></span> <strong class="title">조국 사태</strong></a></li> 
     </ol> 
     <ol class="newstopic_list" id="newstopic_entertain" style="display: none;"> 
      <li><a href="https://search.naver.com/search.naver?where=nexearch&amp;query=%EB%82%98%EC%9D%98+%EB%82%98%EB%9D%BC+%EC%96%91%EC%84%B8%EC%A2%85&amp;ie=utf8&amp;sm=nws_htk.ent" class="nclicks(rig.entopic)" target="_blank" title="나의 나라 양세종"><span class="rank num1"><em>1</em></span> <strong class="title">나의 나라 양세종</strong></a></li> 
      <li><a href="https://search.naver.com/search.naver?where=nexearch&amp;query=%EC%B2%9C%EB%A6%AC%EB%A7%88%EB%A7%88%ED%8A%B8+%EA%B9%80%EB%B3%91%EC%B2%A0&amp;ie=utf8&amp;sm=nws_htk.ent" class="nclicks(rig.entopic)" target="_blank" title="천리마마트 김병철"><span class="rank num2"><em>2</em></span> <strong class="title">천리마마트 김병철</strong></a></li> 
      <li><a href="https://search.naver.com/search.naver?where=nexearch&amp;query=%EB%A7%88%EB%A6%AC%ED%85%94V2+%EA%B9%80%EC%9E%A5%ED%9B%88&amp;ie=utf8&amp;sm=nws_htk.ent" class="nclicks(rig.entopic)" target="_blank" title="마리텔V2 김장훈"><span class="rank num3"><em>3</em></span> <strong class="title">마리텔V2 김장훈</strong> <span class="newstopic_ico_new"><i>NEW</i></span></a></li> 
      <li><a href="https://search.naver.com/search.naver?where=nexearch&amp;query=%EB%86%80%EB%A9%B4+%EB%AD%90%ED%95%98%EB%8B%88+%EC%9C%A0%EC%9E%AC%EC%84%9D&amp;ie=utf8&amp;sm=nws_htk.ent" class="nclicks(rig.entopic)" target="_blank" title="놀면 뭐하니 유재석"><span class="rank num4"><em>4</em></span> <strong class="title">놀면 뭐하니 유재석</strong></a></li> 
      <li><a href="https://search.naver.com/search.naver?where=nexearch&amp;query=%EB%AA%A8%EB%8D%98%ED%8C%A8%EB%B0%80%EB%A6%AC+%EC%84%B1%ED%98%84%EC%95%84&amp;ie=utf8&amp;sm=nws_htk.ent" class="nclicks(rig.entopic)" target="_blank" title="모던패밀리 성현아"><span class="rank num5"><em>5</em></span> <strong class="title">모던패밀리 성현아</strong></a></li> 
      <li><a href="https://search.naver.com/search.naver?where=nexearch&amp;query=%EB%82%98+%ED%98%BC%EC%9E%90+%EC%82%B0%EB%8B%A4+%EA%B8%B0%EC%95%8884&amp;ie=utf8&amp;sm=nws_htk.ent" class="nclicks(rig.entopic)" target="_blank" title="나 혼자 산다 기안84"><span class="rank num6"><em>6</em></span> <strong class="title">나 혼자 산다 기안84</strong></a></li> 
      <li><a href="https://search.naver.com/search.naver?where=nexearch&amp;query=%EC%8D%B8%EB%B0%94%EB%94%942+%EC%86%A1%EC%9E%AC%EC%97%BD&amp;ie=utf8&amp;sm=nws_htk.ent" class="nclicks(rig.entopic)" target="_blank" title="썸바디2 송재엽"><span class="rank num7"><em>7</em></span> <strong class="title">썸바디2 송재엽</strong> <span class="newstopic_ico_new"><i>NEW</i></span></a></li> 
      <li><a href="https://search.naver.com/search.naver?where=nexearch&amp;query=%EA%B9%80%EC%8A%B9%ED%98%84+%EC%97%AC%EC%9E%90%EC%B9%9C%EA%B5%AC&amp;ie=utf8&amp;sm=nws_htk.ent" class="nclicks(rig.entopic)" target="_blank" title="김승현 여자친구"><span class="rank num8"><em>8</em></span> <strong class="title">김승현 여자친구</strong></a></li> 
      <li><a href="https://search.naver.com/search.naver?where=nexearch&amp;query=%EA%B0%99%EC%9D%B4+%ED%8E%80%EB%94%A9+%EC%9C%A0%EC%A4%80%EC%83%81&amp;ie=utf8&amp;sm=nws_htk.ent" class="nclicks(rig.entopic)" target="_blank" title="같이 펀딩 유준상"><span class="rank num9"><em>9</em></span> <strong class="title">같이 펀딩 유준상</strong> <span class="newstopic_ico_new"><i>NEW</i></span></a></li> 
      <li><a href="https://search.naver.com/search.naver?where=nexearch&amp;query=%EC%8D%B8%EB%B0%94%EC%9D%B4%EB%B2%8C+1%2B1&amp;ie=utf8&amp;sm=nws_htk.ent" class="nclicks(rig.entopic)" target="_blank" title="썸바이벌 1+1"><span class="rank num10"><em>10</em></span> <strong class="title">썸바이벌 1+1</strong></a></li> 
     </ol> 
     <p> <span class="newstopic_error_text">추출이 일시적으로 늦어져 최신 정보를 제공할 수 없습니다.</span> <a class="newstopic_help" href="#" title="새창" target="_blank" onclick="news.external.OPS.helpHotTopicKeyword(); return false;"><span class="newstopic_time">2019.11.02. 05:30 ~ 08:30 기준</span></a> </p> 
    </div> 
    <script type="text/javascript">
    var newsTopicInfo = {
    welContainer : null,
    welTabContainer : null,
    welTabList : null,
    welTopicList : null,
    initialize : function() {
    this.setCache();
    this.setEvent();
    },
    setCache : function() {
    this.welContainer = jindo.$Element('newstopic_container');
    this.welTabContainer = jindo.$Element('newstopic_tab');
    this.welTabList = jindo.$ElementList(this.welTabContainer.queryAll('a'));
    this.welTopicList = jindo.$ElementList(this.welContainer.queryAll('ol'));
    },
    setEvent : function() {
    this.welTabContainer.delegate('mouseover', 'a', jindo.$Fn(this.onTabMouseOver, this).bind());
    this.welTabContainer.delegate('click', 'a', jindo.$Fn(this.onTabClick, this).bind());
    },
    onTabClick : function(e){
    e.stopDefault();
    },
    onTabMouseOver : function(e) {
    this.welTabList.removeClass('is_click').attr('aria-selected', false);
    var tabName = jindo.$Element(e.element).addClass('is_click').attr('aria-selected', true).attr('data-tab');
    this.welTopicList.hide();
    jindo.$Element('newstopic_' + tabName).show();
    }
    };
    newsTopicInfo.initialize();
    </script>
                
                
    
                
                <div class="da" id="rightDoubleDA" style="display: none"></div>
                <script type="text/javascript">
                    try{
                        jindo.$("doubleDA").innerHTML = '<div id="daEtc_300250" name="daEtc_300250" style="width: 300px; height: 250px;"><iframe id="etc300250" name="etc300250" src="https://veta.naver.com/fxshow?su=SU10306&sid1=101&calp=shome" width="300" height="250" marginheight="0" marginwidth="0" border="0" frameborder="0" scrolling="no" align="center" title="우측_기타영역_더블플레이광고" data-veta-preview="news_home_02"></iframe></div>';
                    }catch(e){}
                </script>
            
            
            <div class="rightBottomDouble" style="margin-top:36px;"><div id="doubleE300250" name="doubleE300250" data-dom-type="doubleplay_bottom" title="더블플레이하단광고"></div></div>
        
    
    
    
    
        <div class="da" style="display: none"></div>
    
        <script type="text/javascript">
            try {
                jindo.$("doubleDA").innerHTML = '<div id="daArticle_300250" name="daArticle_300250" style="width: 300px; height: 250px;"><iframe id="art300250" name="art300250" src="https://veta.naver.com/fxshow?su=SU10306&sid1=101&sid2=263&oid=277" width="300" height="250" marginheight="0" marginwidth="0" border="0" frameborder="0" scrolling="no" align="center" title="우측_기사엔드_더블플레이광고" data-veta-preview="news_home_02"></iframe></div>';
            }catch(e){}
        </script>
    
    				</div>
    			</td>
    		</tr>
    	</table>
    	
    	
    
    <div id="lyr_dimmed" class="lyr_dimmed lyr_sc_alert" style="margin-top:-268px">
    	<h5 class="blind">욕설 댓글 리마인드 팝업</h5>
    	<div class="lyr_dimmed_topdeco"></div>
    	<div class="lyr_dimmed_content">
    		<img>
    		<div class="lyr_sc_btmtext">
    			<p class="blind">상처 없는 댓글 세상 만들기에 많은 참여 부탁드립니다.</p>
    		</div>
    		<a href="#" class="btn_dimmed_confirm" onclick="commentLayer.hideCommentLayer(event);return false;"><span class="blind">확인</span></a>
    	</div>
    	<div class="lyr_dimmed_btmdeco"></div>
    </div>	
    
    <script type="text/javascript">
    var commentLayer = {
    	init : function () {
    		this._oFoggy = new jindo.Foggy();
    		this._welLayer = jindo.$Element("lyr_dimmed");
    		
    		var oImg = this._welLayer.query("img");
    		var nIndex = Math.floor(Math.random() * 5);
    		var aImageInfo = [{width:419,height:248,alt:"도산 안창호. 남의 결점을 지적하더라도 결코 듣기 싫은 말로 하지말고 사랑으로써 할 것이외다"}, 
    		                  {width:470,height:208,alt:"모로코 속담. 말이 입힌 상처는 칼이 입힌 상처보다 깊다"}, 
    		                  {width:453,height:208,alt:"댓글에 상처받는 이는 바로 우리의 이웃입니다"}, 
    		                  {width:481,height:208,alt:"댓글 안에 당신의 성숙함도 함께 담아주세요"}, 
    		                  {width:406,height:208,alt:"당신의 댓글, 소리내어 읽어보셨나요?"}];
    		var welImg = jindo.$Element(oImg);
    		welImg.attr('src', 'https://ssl.pstatic.net/static.news/image/news/2015/02/lyr_sc_text' + (nIndex+1) + '.gif');
    		welImg.attr('width', aImageInfo[nIndex].width);
    		welImg.attr('height', aImageInfo[nIndex].height);
    		welImg.attr('alt', aImageInfo[nIndex].alt);
    		return this;
    	},
    	showCommentLayer : function (sNclkHead) {
    		this._sNclkHead = sNclkHead;
    		this._welLayer.show();
    		this._oFoggy.show();
    	},
    	hideCommentLayer : function (event) {
    		this._welLayer.hide();
    		this._oFoggy.hide();
    		var tempNsc = nsc;
    		nsc = "news.reply";
            nclk(event, this._sNclkHead + '.camp','','');
    		nsc = tempNsc;
    	}
    }.init();
    </script>
    	<hr>
    <div class="index">
    	
    	
    
    <div class="index_inner">
    
    	<div class="floating_btn" >
    		<div class="floating_inner">
    			<a href="javascript:history.back();" class="floating_btn_back"><span class="blind">이젠 페이지</span></a>
    			<a href="#" onclick="window.scrollTo(0,0);oWebAccessibilityUtil.moveFocus(document.getElementById('da_base'));return false;" class="floating_btn_top"><span class="blind">맨위로</span></a>
    		</div>
    	</div>
    	<div id="index.press_category" class="index_tab">
    		<a id="index.press.btn" href="#" class="spr stit nclicks(fot.press)">언론사 목록<span class="_stit_tab_arrow stit_arrow"><span class="blind">열기</span></span><span class="loading" style="display:none;">로딩 중</span></a>
    		<div id="index.press.area" class="index_content is_hidden"></div>
    		<a id="index.category.btn" href="#" class="spr stit2 nclicks(fot.section)">분야별 목록<span class="_stit_tab_arrow stit_arrow"><span class="blind">열기</span></span><span class="loading" style="display:none;">로딩 중</span></a>
    		<div id="index.category.area" class="index_content02 is_hidden"></div>
    	</div>
    	<div class="index_myscrap">
    		<a href="/main/scrap/index.nhn" class="spr nclicks(fot.scrap)">마이스크랩</a>
    	</div>
    </div>
    
    
    </div>
    <hr>
    <div id="footer">
    	
    <ul>
    <li class="first"><a href="http://www.naver.com/rules/service.html" class="nclicks(fot.agreement)">이용약관</a></li>
    <li><a href="/main/ombudsman/index.nhn" class="nclicks(fot.guide)">서비스 안내</a></li>
    <li><a href="/main/ombudsman/edit.nhn?mid=omb" class="nclicks(fot.editor)">기사배열 원칙 책임자 : 유봉석</a></li>
    <li>청소년 보호 책임자 : 정연아</li>
    <li><strong><a href="http://www.naver.com/rules/privacy.html" class="nclicks(fot.privacy)">개인정보처리방침</a></strong></li>
    <li><a href="http://www.naver.com/rules/disclaimer.html" class="nclicks(fot.disclaimer)">책임의 한계와 법적고지</a></li>
    <li><a href="#" title="새창" onclick="news.external.OPS.helpNews(); return false;" class="nclicks(fot.help)">뉴스 고객센터</a></li>
    </ul>
    	<p class="copyright">본 콘텐츠의 저작권은 제공처 또는 네이버에 있으며 이를 무단 이용하는 경우 저작권법 등에 따라 법적책임을 질 수 있습니다.</p>
    
    	<address class="address_cp nclicks(fot.presscr)">Copyright ⓒ <a href=https://www.asiae.co.kr/ target=blank>아시아경제신문</a> All Rights Reserved.</address>
    
    
    	<address class="address_nhn">
    	<a href="https://www.navercorp.com/" target="_blank" class="logo nclicks(fot.naver)"><span class="blind">NAVER</span></a>
    	<em>Copyright &copy;</em>
    	<a href="https://www.navercorp.com/" target="_blank" class="nclicks(fot.navercorp)">NAVER Corp.</a>
    	<span>All Rights Reserved.</span>
    </address>
    	<!-- -->
    
    
    </div>
    <script type="text/javascript">
    
    
    
    new news.lnb.NewsSearchController('lnb.searchForm');
    
    
    
    //var lnb_weatherRolling = new news.lnb.LineRolling('lnb.weather',{size:26,moveSize:3,moveInterval:30});
    var lnb_mainnewsRolling = new news.lnb.LineRolling('lnb.mainnews',{size:17,moveSize:2,moveInterval:30,isRandomStart:true});
    var lnb_Rolling = new news.lnb.SynchronizedRolling({interval:3000});
    //lnb_Rolling.push(lnb_weatherRolling);
    lnb_Rolling.push(lnb_mainnewsRolling);
    lnb_Rolling.start();
    
    
    var index_tab = new news.index.TabController('index.press_category');
    index_tab.add(new news.index.Tab('index.press.btn','stit','index.press.area','/main/ajax/bottomIndex/press.nhn'));
    index_tab.add(new news.index.Tab('index.category.btn','stit2','index.category.area','/main/ajax/bottomIndex/category.nhn'));
    jindo.$Fn(index_tab.toggle, index_tab).attach(index_tab.tabs.keys(), 'click');
    
    
    (function() {
    	news.right.RightSideFloatingManager.init();
    })();
    
    
    
        (function() {
            news.right.TopDownFloatingManager.init();
        })();
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    		news.read.Toolbar.init({
    			oid : '277',
    			aid : '0004565025',
    			isLogin : false
    		});
        
        news.read.TopFloatingManager.init();
    
    
    
    
    
    ;(function(){
        var eventType = "onpageshow" in window ? "pageshow" : "load";
        jindo.$Fn(function(){
    
    	lcs_do_gdid("88000385_000000000000000004565025");
    	
    
        }).attach(window, eventType);
    })();
    
    
    
    
    
    
    
    
    news.startup();
    
    
    jindo.$Fn(function(){
        var welSkip = jindo.$Element("u_skip");
        if (welSkip === null) {
            return;
        }
        welSkip.delegate("click", "a", function(weEvent){
            weEvent.stopDefault();
            var elTarget = jindo.$(weEvent.element.href.split("#")[1]);
            oWebAccessibilityUtil.moveFocus(elTarget);
        });
    }).attach(window, "load");
    
    
    document.documentElement.setAttribute('data-useragent',navigator.userAgent);
    </script>
    </div>
    </body>
    </html>
    

## #04. 데이터추출


```python
# 웹 페이지의 소스코드 HTML 분석 객체로 생성
soup = BeautifulSoup(r.text, 'html.parser')

# CSS 선택자를 활용하여 가져오기를 원하는 부분 지정
# -> ""#id"값 형식으로 지정
selector = soup.select('#articleBodyContents')

if not selector:  #가져온 내용이 없다면?
    print("뉴스기사 크롤링 실패")
    quit()

print(selector)
```

    [<div class="_article_body_contents" id="articleBodyContents">
    <!-- 본문 내용 -->
    <!-- TV플레이어 -->
    <!-- // TV플레이어 -->
    <script type="text/javascript">
    // flash 오류를 우회하기 위한 함수 추가
    function _flash_removeCallback() {}
    </script>
    <span class="end_photo_org"><img alt="" src="https://imgnews.pstatic.net/image/277/2019/11/02/0004565025_001_20191102080925359.jpg?type=w647"><em class="img_desc">(자료사진) [이미지출처=연합뉴스]</em></img></span><br/><br/>[세종=아시아경제 주상돈 기자] 지난달 수출이 또 줄어들며 지난해 12월부터 시작된 감소세가 11개월째 이어졌다. 감소율은 14.7%로 앞선 3년9개월 만의 최대폭을 기록했다.<br/><br/>2일 산업통상자원부에 따르면 10월 수출액(통관 기준)은 467억8400만달러로 전년 동기보다 14.7% 감소했다.<br/><br/>32.1% 줄어든 반도체가 수출 감소세를 주도했다. 산업부는 D램과 낸드플래시 등 메모리 반도체 가격 하락에 따른 것으로 봤다. 또 석유화학(-22.6%)과 석유제품(-26.2%), 디스플레이(-22.5%), 철강(-11.8%), 일반기계(12.1%), 자동차(-2.3) 등도 수출이 줄었다. 반면 선박(25.7%), 컴퓨터(7.7%) 등은 늘었다.<br/><br/>국가별로는 우리의 주력 수출국인 중국(-16.9%)과 미국(-8.4%)이 모두 줄었다. 일본(-13.8%)과 유럽연합(EU·-21.2%), 아세안(-8.3%), 인도(-12.0%), 중남미(-13.2%) 등도 감소했다.<br/><br/>산업부는 일본의 대한(對韓) 수출규제에 따른 영향은 제한적인 것으로 봤다. 박태성 산업부 무역투자실장은 "불화수소 등 3개 수출규제 품목이 7∼10월 전체 대일 수입에서 차지하는 비중이 1.4%로 낮고, 현재까지 관련산업의 실제 생산 차질로 연결된 사례는 없는 상황"이라며 "9월 기준 우리의 대일본 수출 감소(-6.0%)보다 일본의 대한국 수출 감소폭(-15.9%)이 더 크게 나타나 우리보다 일본이 더 큰 영향을 받고 있다"고 설명했다.<br/><br/>그는 ▲반도체 가격 회복  ▲미ㆍ중 협상의 스몰딜 성사 ▲수주 선박의 인도 본격화 등에 따라 내년 1분기에는 수출이 플러스로 전환할 것이라고 전망했다. 박 실장은 " 박 실장은 "수출은 10월을 저점으로 점진적으로 감소폭이 개선되고 있는 등 수출 감소 터널의 끝을 향해 나아가고 있다"며 "내년 1분기 수출은 플러스 전환이 될 것"이라고 말했다.<br/><br/>주상돈 기자 don@asiae.co.kr<br/><br/><a href="https://www.asiae.co.kr/fortune/index.htm?utm_source=navernews&amp;utm_medium=naver_view&amp;utm_campaign=fortune"><b>▶ 신강재강(身强財强) 해야 부자사주라고? 나는?</b></a><br/><a href="https://www.asiae.co.kr/event/2019/quiz/"><b>▶ 초간단 퀴즈 풀고, 아이패드 받자! </b></a> <a href="https://cm.asiae.co.kr/list/science"><b>▶ 재미와 지식이 가득한 '과학을읽다'</b></a><br/><br/>&lt;ⓒ경제를 보는 눈, 세계를 보는 창 아시아경제 무단전재 배포금지&gt;
    	<!-- // 본문 내용 -->
    </div>]
    


```python
# html의 id속성을 통해 가져온 원소는 그 페이지 내에서 고유한 영역을 의미하므로,
# select()함수의 결과가 list라 하더라도 실제 원소는 단 하나만 존재한다.
# 그렇기 때문에 리스트에 대한 0번째 요소에 직접 접근해도 무관하다.
item = selector[0]
item
```




    <div class="_article_body_contents" id="articleBodyContents">
    <!-- 본문 내용 -->
    <!-- TV플레이어 -->
    <!-- // TV플레이어 -->
    <script type="text/javascript">
    // flash 오류를 우회하기 위한 함수 추가
    function _flash_removeCallback() {}
    </script>
    <span class="end_photo_org"><img alt="" src="https://imgnews.pstatic.net/image/277/2019/11/02/0004565025_001_20191102080925359.jpg?type=w647"><em class="img_desc">(자료사진) [이미지출처=연합뉴스]</em></img></span><br/><br/>[세종=아시아경제 주상돈 기자] 지난달 수출이 또 줄어들며 지난해 12월부터 시작된 감소세가 11개월째 이어졌다. 감소율은 14.7%로 앞선 3년9개월 만의 최대폭을 기록했다.<br/><br/>2일 산업통상자원부에 따르면 10월 수출액(통관 기준)은 467억8400만달러로 전년 동기보다 14.7% 감소했다.<br/><br/>32.1% 줄어든 반도체가 수출 감소세를 주도했다. 산업부는 D램과 낸드플래시 등 메모리 반도체 가격 하락에 따른 것으로 봤다. 또 석유화학(-22.6%)과 석유제품(-26.2%), 디스플레이(-22.5%), 철강(-11.8%), 일반기계(12.1%), 자동차(-2.3) 등도 수출이 줄었다. 반면 선박(25.7%), 컴퓨터(7.7%) 등은 늘었다.<br/><br/>국가별로는 우리의 주력 수출국인 중국(-16.9%)과 미국(-8.4%)이 모두 줄었다. 일본(-13.8%)과 유럽연합(EU·-21.2%), 아세안(-8.3%), 인도(-12.0%), 중남미(-13.2%) 등도 감소했다.<br/><br/>산업부는 일본의 대한(對韓) 수출규제에 따른 영향은 제한적인 것으로 봤다. 박태성 산업부 무역투자실장은 "불화수소 등 3개 수출규제 품목이 7∼10월 전체 대일 수입에서 차지하는 비중이 1.4%로 낮고, 현재까지 관련산업의 실제 생산 차질로 연결된 사례는 없는 상황"이라며 "9월 기준 우리의 대일본 수출 감소(-6.0%)보다 일본의 대한국 수출 감소폭(-15.9%)이 더 크게 나타나 우리보다 일본이 더 큰 영향을 받고 있다"고 설명했다.<br/><br/>그는 ▲반도체 가격 회복  ▲미ㆍ중 협상의 스몰딜 성사 ▲수주 선박의 인도 본격화 등에 따라 내년 1분기에는 수출이 플러스로 전환할 것이라고 전망했다. 박 실장은 " 박 실장은 "수출은 10월을 저점으로 점진적으로 감소폭이 개선되고 있는 등 수출 감소 터널의 끝을 향해 나아가고 있다"며 "내년 1분기 수출은 플러스 전환이 될 것"이라고 말했다.<br/><br/>주상돈 기자 don@asiae.co.kr<br/><br/><a href="https://www.asiae.co.kr/fortune/index.htm?utm_source=navernews&amp;utm_medium=naver_view&amp;utm_campaign=fortune"><b>▶ 신강재강(身强財强) 해야 부자사주라고? 나는?</b></a><br/><a href="https://www.asiae.co.kr/event/2019/quiz/"><b>▶ 초간단 퀴즈 풀고, 아이패드 받자! </b></a> <a href="https://cm.asiae.co.kr/list/science"><b>▶ 재미와 지식이 가득한 '과학을읽다'</b></a><br/><br/>&lt;ⓒ경제를 보는 눈, 세계를 보는 창 아시아경제 무단전재 배포금지&gt;
    	<!-- // 본문 내용 -->
    </div>




```python
for target in item.find_all('script'):
    target.extract()

item
```




    <div class="_article_body_contents" id="articleBodyContents">
    <!-- 본문 내용 -->
    <!-- TV플레이어 -->
    <!-- // TV플레이어 -->
    
    <span class="end_photo_org"><img alt="" src="https://imgnews.pstatic.net/image/277/2019/11/02/0004565025_001_20191102080925359.jpg?type=w647"><em class="img_desc">(자료사진) [이미지출처=연합뉴스]</em></img></span><br/><br/>[세종=아시아경제 주상돈 기자] 지난달 수출이 또 줄어들며 지난해 12월부터 시작된 감소세가 11개월째 이어졌다. 감소율은 14.7%로 앞선 3년9개월 만의 최대폭을 기록했다.<br/><br/>2일 산업통상자원부에 따르면 10월 수출액(통관 기준)은 467억8400만달러로 전년 동기보다 14.7% 감소했다.<br/><br/>32.1% 줄어든 반도체가 수출 감소세를 주도했다. 산업부는 D램과 낸드플래시 등 메모리 반도체 가격 하락에 따른 것으로 봤다. 또 석유화학(-22.6%)과 석유제품(-26.2%), 디스플레이(-22.5%), 철강(-11.8%), 일반기계(12.1%), 자동차(-2.3) 등도 수출이 줄었다. 반면 선박(25.7%), 컴퓨터(7.7%) 등은 늘었다.<br/><br/>국가별로는 우리의 주력 수출국인 중국(-16.9%)과 미국(-8.4%)이 모두 줄었다. 일본(-13.8%)과 유럽연합(EU·-21.2%), 아세안(-8.3%), 인도(-12.0%), 중남미(-13.2%) 등도 감소했다.<br/><br/>산업부는 일본의 대한(對韓) 수출규제에 따른 영향은 제한적인 것으로 봤다. 박태성 산업부 무역투자실장은 "불화수소 등 3개 수출규제 품목이 7∼10월 전체 대일 수입에서 차지하는 비중이 1.4%로 낮고, 현재까지 관련산업의 실제 생산 차질로 연결된 사례는 없는 상황"이라며 "9월 기준 우리의 대일본 수출 감소(-6.0%)보다 일본의 대한국 수출 감소폭(-15.9%)이 더 크게 나타나 우리보다 일본이 더 큰 영향을 받고 있다"고 설명했다.<br/><br/>그는 ▲반도체 가격 회복  ▲미ㆍ중 협상의 스몰딜 성사 ▲수주 선박의 인도 본격화 등에 따라 내년 1분기에는 수출이 플러스로 전환할 것이라고 전망했다. 박 실장은 " 박 실장은 "수출은 10월을 저점으로 점진적으로 감소폭이 개선되고 있는 등 수출 감소 터널의 끝을 향해 나아가고 있다"며 "내년 1분기 수출은 플러스 전환이 될 것"이라고 말했다.<br/><br/>주상돈 기자 don@asiae.co.kr<br/><br/><a href="https://www.asiae.co.kr/fortune/index.htm?utm_source=navernews&amp;utm_medium=naver_view&amp;utm_campaign=fortune"><b>▶ 신강재강(身强財强) 해야 부자사주라고? 나는?</b></a><br/><a href="https://www.asiae.co.kr/event/2019/quiz/"><b>▶ 초간단 퀴즈 풀고, 아이패드 받자! </b></a> <a href="https://cm.asiae.co.kr/list/science"><b>▶ 재미와 지식이 가득한 '과학을읽다'</b></a><br/><br/>&lt;ⓒ경제를 보는 눈, 세계를 보는 창 아시아경제 무단전재 배포금지&gt;
    	<!-- // 본문 내용 -->
    </div>




```python
for target in item.find_all('a'):
    target.extract()

item
```




    <div class="_article_body_contents" id="articleBodyContents">
    <!-- 본문 내용 -->
    <!-- TV플레이어 -->
    <!-- // TV플레이어 -->
    
    <span class="end_photo_org"><img alt="" src="https://imgnews.pstatic.net/image/277/2019/11/02/0004565025_001_20191102080925359.jpg?type=w647"><em class="img_desc">(자료사진) [이미지출처=연합뉴스]</em></img></span><br/><br/>[세종=아시아경제 주상돈 기자] 지난달 수출이 또 줄어들며 지난해 12월부터 시작된 감소세가 11개월째 이어졌다. 감소율은 14.7%로 앞선 3년9개월 만의 최대폭을 기록했다.<br/><br/>2일 산업통상자원부에 따르면 10월 수출액(통관 기준)은 467억8400만달러로 전년 동기보다 14.7% 감소했다.<br/><br/>32.1% 줄어든 반도체가 수출 감소세를 주도했다. 산업부는 D램과 낸드플래시 등 메모리 반도체 가격 하락에 따른 것으로 봤다. 또 석유화학(-22.6%)과 석유제품(-26.2%), 디스플레이(-22.5%), 철강(-11.8%), 일반기계(12.1%), 자동차(-2.3) 등도 수출이 줄었다. 반면 선박(25.7%), 컴퓨터(7.7%) 등은 늘었다.<br/><br/>국가별로는 우리의 주력 수출국인 중국(-16.9%)과 미국(-8.4%)이 모두 줄었다. 일본(-13.8%)과 유럽연합(EU·-21.2%), 아세안(-8.3%), 인도(-12.0%), 중남미(-13.2%) 등도 감소했다.<br/><br/>산업부는 일본의 대한(對韓) 수출규제에 따른 영향은 제한적인 것으로 봤다. 박태성 산업부 무역투자실장은 "불화수소 등 3개 수출규제 품목이 7∼10월 전체 대일 수입에서 차지하는 비중이 1.4%로 낮고, 현재까지 관련산업의 실제 생산 차질로 연결된 사례는 없는 상황"이라며 "9월 기준 우리의 대일본 수출 감소(-6.0%)보다 일본의 대한국 수출 감소폭(-15.9%)이 더 크게 나타나 우리보다 일본이 더 큰 영향을 받고 있다"고 설명했다.<br/><br/>그는 ▲반도체 가격 회복  ▲미ㆍ중 협상의 스몰딜 성사 ▲수주 선박의 인도 본격화 등에 따라 내년 1분기에는 수출이 플러스로 전환할 것이라고 전망했다. 박 실장은 " 박 실장은 "수출은 10월을 저점으로 점진적으로 감소폭이 개선되고 있는 등 수출 감소 터널의 끝을 향해 나아가고 있다"며 "내년 1분기 수출은 플러스 전환이 될 것"이라고 말했다.<br/><br/>주상돈 기자 don@asiae.co.kr<br/><br/><br/> <br/><br/>&lt;ⓒ경제를 보는 눈, 세계를 보는 창 아시아경제 무단전재 배포금지&gt;
    	<!-- // 본문 내용 -->
    </div>




```python
for target in item.find_all('span'):
    target.extract()

item
```




    <div class="_article_body_contents" id="articleBodyContents">
    <!-- 본문 내용 -->
    <!-- TV플레이어 -->
    <!-- // TV플레이어 -->
    
    <br/><br/>[세종=아시아경제 주상돈 기자] 지난달 수출이 또 줄어들며 지난해 12월부터 시작된 감소세가 11개월째 이어졌다. 감소율은 14.7%로 앞선 3년9개월 만의 최대폭을 기록했다.<br/><br/>2일 산업통상자원부에 따르면 10월 수출액(통관 기준)은 467억8400만달러로 전년 동기보다 14.7% 감소했다.<br/><br/>32.1% 줄어든 반도체가 수출 감소세를 주도했다. 산업부는 D램과 낸드플래시 등 메모리 반도체 가격 하락에 따른 것으로 봤다. 또 석유화학(-22.6%)과 석유제품(-26.2%), 디스플레이(-22.5%), 철강(-11.8%), 일반기계(12.1%), 자동차(-2.3) 등도 수출이 줄었다. 반면 선박(25.7%), 컴퓨터(7.7%) 등은 늘었다.<br/><br/>국가별로는 우리의 주력 수출국인 중국(-16.9%)과 미국(-8.4%)이 모두 줄었다. 일본(-13.8%)과 유럽연합(EU·-21.2%), 아세안(-8.3%), 인도(-12.0%), 중남미(-13.2%) 등도 감소했다.<br/><br/>산업부는 일본의 대한(對韓) 수출규제에 따른 영향은 제한적인 것으로 봤다. 박태성 산업부 무역투자실장은 "불화수소 등 3개 수출규제 품목이 7∼10월 전체 대일 수입에서 차지하는 비중이 1.4%로 낮고, 현재까지 관련산업의 실제 생산 차질로 연결된 사례는 없는 상황"이라며 "9월 기준 우리의 대일본 수출 감소(-6.0%)보다 일본의 대한국 수출 감소폭(-15.9%)이 더 크게 나타나 우리보다 일본이 더 큰 영향을 받고 있다"고 설명했다.<br/><br/>그는 ▲반도체 가격 회복  ▲미ㆍ중 협상의 스몰딜 성사 ▲수주 선박의 인도 본격화 등에 따라 내년 1분기에는 수출이 플러스로 전환할 것이라고 전망했다. 박 실장은 " 박 실장은 "수출은 10월을 저점으로 점진적으로 감소폭이 개선되고 있는 등 수출 감소 터널의 끝을 향해 나아가고 있다"며 "내년 1분기 수출은 플러스 전환이 될 것"이라고 말했다.<br/><br/>주상돈 기자 don@asiae.co.kr<br/><br/><br/> <br/><br/>&lt;ⓒ경제를 보는 눈, 세계를 보는 창 아시아경제 무단전재 배포금지&gt;
    	<!-- // 본문 내용 -->
    </div>




```python
for target in item.find_all('div'):
    target.extract()

item
```




    <div class="_article_body_contents" id="articleBodyContents">
    <!-- 본문 내용 -->
    <!-- TV플레이어 -->
    <!-- // TV플레이어 -->
    
    <br/><br/>[세종=아시아경제 주상돈 기자] 지난달 수출이 또 줄어들며 지난해 12월부터 시작된 감소세가 11개월째 이어졌다. 감소율은 14.7%로 앞선 3년9개월 만의 최대폭을 기록했다.<br/><br/>2일 산업통상자원부에 따르면 10월 수출액(통관 기준)은 467억8400만달러로 전년 동기보다 14.7% 감소했다.<br/><br/>32.1% 줄어든 반도체가 수출 감소세를 주도했다. 산업부는 D램과 낸드플래시 등 메모리 반도체 가격 하락에 따른 것으로 봤다. 또 석유화학(-22.6%)과 석유제품(-26.2%), 디스플레이(-22.5%), 철강(-11.8%), 일반기계(12.1%), 자동차(-2.3) 등도 수출이 줄었다. 반면 선박(25.7%), 컴퓨터(7.7%) 등은 늘었다.<br/><br/>국가별로는 우리의 주력 수출국인 중국(-16.9%)과 미국(-8.4%)이 모두 줄었다. 일본(-13.8%)과 유럽연합(EU·-21.2%), 아세안(-8.3%), 인도(-12.0%), 중남미(-13.2%) 등도 감소했다.<br/><br/>산업부는 일본의 대한(對韓) 수출규제에 따른 영향은 제한적인 것으로 봤다. 박태성 산업부 무역투자실장은 "불화수소 등 3개 수출규제 품목이 7∼10월 전체 대일 수입에서 차지하는 비중이 1.4%로 낮고, 현재까지 관련산업의 실제 생산 차질로 연결된 사례는 없는 상황"이라며 "9월 기준 우리의 대일본 수출 감소(-6.0%)보다 일본의 대한국 수출 감소폭(-15.9%)이 더 크게 나타나 우리보다 일본이 더 큰 영향을 받고 있다"고 설명했다.<br/><br/>그는 ▲반도체 가격 회복  ▲미ㆍ중 협상의 스몰딜 성사 ▲수주 선박의 인도 본격화 등에 따라 내년 1분기에는 수출이 플러스로 전환할 것이라고 전망했다. 박 실장은 " 박 실장은 "수출은 10월을 저점으로 점진적으로 감소폭이 개선되고 있는 등 수출 감소 터널의 끝을 향해 나아가고 있다"며 "내년 1분기 수출은 플러스 전환이 될 것"이라고 말했다.<br/><br/>주상돈 기자 don@asiae.co.kr<br/><br/><br/> <br/><br/>&lt;ⓒ경제를 보는 눈, 세계를 보는 창 아시아경제 무단전재 배포금지&gt;
    	<!-- // 본문 내용 -->
    </div>




```python
for target in item.find_all('br'):
    target.replace_with("\n")

item
```




    <div class="_article_body_contents" id="articleBodyContents">
    <!-- 본문 내용 -->
    <!-- TV플레이어 -->
    <!-- // TV플레이어 -->
    
    
    
    [세종=아시아경제 주상돈 기자] 지난달 수출이 또 줄어들며 지난해 12월부터 시작된 감소세가 11개월째 이어졌다. 감소율은 14.7%로 앞선 3년9개월 만의 최대폭을 기록했다.
    
    2일 산업통상자원부에 따르면 10월 수출액(통관 기준)은 467억8400만달러로 전년 동기보다 14.7% 감소했다.
    
    32.1% 줄어든 반도체가 수출 감소세를 주도했다. 산업부는 D램과 낸드플래시 등 메모리 반도체 가격 하락에 따른 것으로 봤다. 또 석유화학(-22.6%)과 석유제품(-26.2%), 디스플레이(-22.5%), 철강(-11.8%), 일반기계(12.1%), 자동차(-2.3) 등도 수출이 줄었다. 반면 선박(25.7%), 컴퓨터(7.7%) 등은 늘었다.
    
    국가별로는 우리의 주력 수출국인 중국(-16.9%)과 미국(-8.4%)이 모두 줄었다. 일본(-13.8%)과 유럽연합(EU·-21.2%), 아세안(-8.3%), 인도(-12.0%), 중남미(-13.2%) 등도 감소했다.
    
    산업부는 일본의 대한(對韓) 수출규제에 따른 영향은 제한적인 것으로 봤다. 박태성 산업부 무역투자실장은 "불화수소 등 3개 수출규제 품목이 7∼10월 전체 대일 수입에서 차지하는 비중이 1.4%로 낮고, 현재까지 관련산업의 실제 생산 차질로 연결된 사례는 없는 상황"이라며 "9월 기준 우리의 대일본 수출 감소(-6.0%)보다 일본의 대한국 수출 감소폭(-15.9%)이 더 크게 나타나 우리보다 일본이 더 큰 영향을 받고 있다"고 설명했다.
    
    그는 ▲반도체 가격 회복  ▲미ㆍ중 협상의 스몰딜 성사 ▲수주 선박의 인도 본격화 등에 따라 내년 1분기에는 수출이 플러스로 전환할 것이라고 전망했다. 박 실장은 " 박 실장은 "수출은 10월을 저점으로 점진적으로 감소폭이 개선되고 있는 등 수출 감소 터널의 끝을 향해 나아가고 있다"며 "내년 1분기 수출은 플러스 전환이 될 것"이라고 말했다.
    
    주상돈 기자 don@asiae.co.kr
    
    
     
    
    &lt;ⓒ경제를 보는 눈, 세계를 보는 창 아시아경제 무단전재 배포금지&gt;
    	<!-- // 본문 내용 -->
    </div>




```python
news_content = item.text.strip()
news_content
```




    '[세종=아시아경제 주상돈 기자] 지난달 수출이 또 줄어들며 지난해 12월부터 시작된 감소세가 11개월째 이어졌다. 감소율은 14.7%로 앞선 3년9개월 만의 최대폭을 기록했다.\n\n2일 산업통상자원부에 따르면 10월 수출액(통관 기준)은 467억8400만달러로 전년 동기보다 14.7% 감소했다.\n\n32.1% 줄어든 반도체가 수출 감소세를 주도했다. 산업부는 D램과 낸드플래시 등 메모리 반도체 가격 하락에 따른 것으로 봤다. 또 석유화학(-22.6%)과 석유제품(-26.2%), 디스플레이(-22.5%), 철강(-11.8%), 일반기계(12.1%), 자동차(-2.3) 등도 수출이 줄었다. 반면 선박(25.7%), 컴퓨터(7.7%) 등은 늘었다.\n\n국가별로는 우리의 주력 수출국인 중국(-16.9%)과 미국(-8.4%)이 모두 줄었다. 일본(-13.8%)과 유럽연합(EU·-21.2%), 아세안(-8.3%), 인도(-12.0%), 중남미(-13.2%) 등도 감소했다.\n\n산업부는 일본의 대한(對韓) 수출규제에 따른 영향은 제한적인 것으로 봤다. 박태성 산업부 무역투자실장은 "불화수소 등 3개 수출규제 품목이 7∼10월 전체 대일 수입에서 차지하는 비중이 1.4%로 낮고, 현재까지 관련산업의 실제 생산 차질로 연결된 사례는 없는 상황"이라며 "9월 기준 우리의 대일본 수출 감소(-6.0%)보다 일본의 대한국 수출 감소폭(-15.9%)이 더 크게 나타나 우리보다 일본이 더 큰 영향을 받고 있다"고 설명했다.\n\n그는 ▲반도체 가격 회복  ▲미ㆍ중 협상의 스몰딜 성사 ▲수주 선박의 인도 본격화 등에 따라 내년 1분기에는 수출이 플러스로 전환할 것이라고 전망했다. 박 실장은 " 박 실장은 "수출은 10월을 저점으로 점진적으로 감소폭이 개선되고 있는 등 수출 감소 터널의 끝을 향해 나아가고 있다"며 "내년 1분기 수출은 플러스 전환이 될 것"이라고 말했다.\n\n주상돈 기자 don@asiae.co.kr\n\n\n \n\n<ⓒ경제를 보는 눈, 세계를 보는 창 아시아경제 무단전재 배포금지>'



## #05. 추출 결과를 텍스트로 저장


```python
with open("네이버뉴스.txt", "w", encoding="utf-8") as f:
    f.write(news_content)
```


```python

```
