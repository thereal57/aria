---
theme : "black"
transition: "slide"
highlightTheme: "monokai"
---

# WAI-ARIA
<small>Created by [연구4팀] 이혜경,배희진,윤종경,문선혜</small>

---

## WAI-ARIA란?

--

W3C에 의해 제정된 RIA의 웹 접근성 권고안


<small><strong>W</strong>eb <strong>A</strong>ccessibility <strong>I</strong>nitiative - <strong>A</strong>ccessible <strong>R</strong>ich <strong>I</strong>nternet A</strong>pplications; WAI-ARIA</small>

<!--
웹접근성이란?
장애를 가진 사람과 장애를 가지지 않은 사람 모두가 웹사이트를 이용할 수 있게 하는것
-->
--

장애인이 웹 콘텐츠 및 웹 응용 프로그램에 보다 쉽게 액세스할 수 있도록 하는 방법

--

<a href="https://www.w3.org/TR/wai-aria-1.2/" target="_blank"><img src='//img.danawa.com/img/etc/aria/w3c.jpg' alt='W3C wai aria page' /></a>

---

## WAI-ARIA 필요성

--

* 동적인 웹 애플리케이션 접근성 보장을 위한 지침이 부족
* 실시간 변경 콘텐츠를 보조기기(스크린리더기 등)가 못 읽을 수 있음 <!-- .element: class="fragment fade-up" -->
* 페이지 콘텐츠 중 일부만 변경 시, 동일한 내용을 계속 읽어야 하는 문제 발생 <!-- .element: class="fragment fade-up" -->
* 화면 확대 사용자의 경우, 가시 범위 밖의 콘텐츠 변경 내용을 알 수 없음 <!-- .element: class="fragment fade-up" -->

---

## WAI-ARIA 효과

--

ARIA를 코드에 올바르게 통합하면<br />보조 기술 장치 사용자가<br />필요한 모든 정보를 얻을 수 있음

--

ARIA는 잘못된 마크업을 수정하고 HTML 격차를 해소하여 보조 기술(AT)을 사용하는 사용자들에게 보다 쉽게 다가갈 수 있도록 속성 모음을 정의

--


역할(Role),속성(Property),상태(State)를 추가하여<br />보조기기(스크린리더)에 접근성 및 상호 운용성 향상

--

## WAI-ARIA의 3대 요소

역할(role)

상태(state)

속성(property)

--

### 역할(role)

유저 인터페이스(User Interface, 이하 UI)에 포함된<br /> 특정 컴포넌트의 역할을 정의

--

<pre><code data-trim data-noescape style="font-weight:bold">&lt;a href="/" onclick="playApp()" <mark class="fragment">role="button"</mark>&gt; 재생 &lt;/a&gt;</code></pre>

<span class="fragment">a 요소에 <mark>role="button"</mark>을 지정하면<br />스크린리더는<br />링크가 아닌 버튼으로 읽어주게 되어<br />컴포넌트의 정확한 용도를 이해하고 사용</span>

--

### 속성(Property) & 상태(State)

해당 컴포넌트의 특징이나 상황, 상태 정보를 정의

속성명으로 "aria-*"라는 접두사를 사용 <!-- .element: class="fragment fade-up" -->

--

<pre><code data-trim data-noescape style="font-weight:bold">&lt;div class="id-area"&gt;
	&lt;label for="user-email"&gt;아이디&lt;/label&gt;
	&lt;input type="email" id="user-email" <mark class="fragment">aria-required="true"</mark> &gt;
&lt;/div&gt; </code></pre>

<span class="fragment">입력 값이 필수 항목일 경우<br /> <mark>aria-required="true"</mark>를 지정하면<br />스크린리더가 필수항목 임을 알 수 있도록 제공</span>

---

## WAI-ARIA EXAMPLE

---

### tab UI

탭 목록, 탭, 탭 패널 (role="tablist / tab / tabpanel")

<a href="http://markup.danawa.com/aria/?loc=01_tab" target="_blank"><img src="//img.danawa.com/img/etc/aria/tab.jpg" alt="tab UI" /></a>

--

#### As-is

<pre><code data-trim data-noescape style="max-height:300px;font-weight:bold">&lt;ul&gt;
	&lt;li id="tab1" tabindex="0"&gt;첫번째&lt;/li&gt;
	&lt;li id="tab2" tabindex="0"&gt;두번째&lt;/li&gt;
&lt;/ul&gt;
&lt;div id="panel1"&gt;
	첫번째 탭 내용입니다.
&lt;/div&gt;
&lt;div id="panel2"&gt;
	두번째 탭 내용입니다.
&lt;/div&gt;</code></pre>

<p class="fragment" style="font-size:0.7em">스크린리더기 출력내용</p>
<pre class="fragment" style="max-height:200px;overflow-y:auto;">목록 항목 수 2개
<mark>클릭 가능</mark>
첫번째
<mark>클릭 가능</mark>
두번째
첫번째 탭 내용입니다.</pre>

--

#### To-be

<pre><code data-trim data-noescape style="max-height:300px;font-weight:bold">&lt;ul <span class="fragment">role="tablist"</span>&gt;
	&lt;li id="tab1" tabindex="0" <span class="fragment">role="tab" aria-controls="<mark>panel1</mark>" aria-selected="true"</span>&gt;첫번째&lt;/li&gt;
	&lt;li id="tab2" tabindex="0" <span class="fragment">role="tab" aria-controls="<mark>panel2</mark>" aria-selected="false"</span>&gt;두번째&lt;/li&gt;
&lt;/ul&gt;
&lt;div id="<mark>panel1</mark>" <span class="fragment">role="tabpanel" aria-labelledby="tab1"</span>&gt;
	첫번째 탭 내용입니다.
&lt;/div&gt;
&lt;div id="<mark>panel2</mark>" <span class="fragment">role="tabpanel" aria-labelledby="tab2"</span>&gt;
	두번째 탭 내용입니다.
&lt;/div&gt;</code></pre>

<p class="fragment" style="font-size:0.7em">스크린리더기 출력내용</p>
<pre class="fragment" style="max-height:200px;overflow-y:auto;"><mark>탭 선택됨</mark>
첫번째
<mark>탭</mark>
두번째
첫번째 탭 내용입니다.</pre>

---

### layer popup

대화상자 (role="dialog")

<a href="//markup.danawa.com/aria/?loc=02_layerpopup" target="_blank"><img src="//img.danawa.com/img/etc/aria/layerpopup.jpg" alt="layer popup" /></a>

--

#### As-is

<pre><code data-trim data-noescape style="max-height:300px;font-weight:bold">&lt;div&gt;&lt;a href="#"&gt;링크1&lt;/a&gt;&lt;/div&gt;
&lt;div&gt;&lt;a href="#"&gt;링크2&lt;/a&gt;&lt;/div&gt;
&lt;div&gt;&lt;a href="#"&gt;링크3&lt;/a&gt;&lt;/div&gt;
&lt;div&gt;
	&lt;a href="#" id="layer_open_before"&gt;팝업창열기&lt;/a&gt;
&lt;/div&gt;
&lt;div class="layer_area_before" id="layer_before"&gt;
	&lt;h1 id="dialogTitle_before" tabindex="0"&gt;레이어팝업&lt;/h1&gt;
		&lt;ol&gt;
			&lt;li&gt;팝업창에 포커스이동&lt;/li&gt;
			&lt;li&gt;탭키 사용시 순환적 이동&lt;/li&gt;
			&lt;li&gt;ESC키/닫기버튼 사용시 팝업종료&lt;/li&gt;
			&lt;li&gt;팝업종료시 포커스 이동&lt;/li&gt;
		&lt;/ol&gt;
	&lt;div&gt;
	&lt;input type="button" value="닫기" id="layer_close_before"&gt;
	&lt;/div&gt;
&lt;/div&gt;
&lt;div&gt;&lt;a href="#"&gt;링크4&lt;/a&gt;&lt;/div&gt;
&lt;div&gt;&lt;a href="#"&gt;링크5&lt;/a&gt;&lt;/div&gt;</code></pre>

<p class="fragment" style="font-size:0.7em">스크린리더기 출력내용</p>
<pre class="fragment" style="max-height:200px;overflow-y:auto;">목록 항목 수 2개
링크1
방문함 링크
링크2
방문함 링크
링크3
방문함 링크
팝업창열기
방문함 링크

<small> /***** 팝업창 열림 *****/ </small>
레이어팝업
헤딩 레벨 1
닫기
버튼

<small> /***** 팝업이 열린상태에서 다음링크로 이동 *****/ </small>
링크4
방문함 링크
링크5
방문함 링크</pre>

--

#### To-be

<pre><code data-trim data-noescape style="max-height:300px;font-weight:bold">&lt;div&gt;&lt;a href="#"&gt;링크1&lt;/a&gt;&lt;/div&gt;
&lt;div&gt;&lt;a href="#"&gt;링크2&lt;/a&gt;&lt;/div&gt;
&lt;div&gt;&lt;a href="#"&gt;링크3&lt;/a&gt;&lt;/div&gt;
&lt;div&gt;
	&lt;a href="#" id="layer_open"&gt;팝업창열기&lt;/a&gt;
    &lt;/div&gt;
    &lt;div class="layer_area" id="layer" 
	<span class="fragment">role="dialog" aria-hidden="true" aria-labelledby="<mark>dialogTitle</mark>"</span>&gt;
        &lt;h1 id="<mark>dialogTitle</mark>" tabindex="0"&gt;레이업 팝업&lt;/h1&gt;
	&lt;ol&gt;
		&lt;li&gt;팝업창에 포커스이동&lt;/li&gt;
		&lt;li&gt;탭키 사용시 순환적 이동&lt;/li&gt;
		&lt;li&gt;팝업종료시 포커스 이동&lt;/li&gt;
	&lt;/ol&gt;
	&lt;input type="button" value="닫기" id="layer_close"&gt;
    &lt;/div&gt;
&lt;div&gt;&lt;a href="#"&gt;링크4&lt;/a&gt;&lt;/div&gt;
&lt;div&gt;&lt;a href="#"&gt;링크5&lt;/a&gt;&lt;/div&gt;</code></pre>

<p class="fragment" style="font-size:0.7em">스크린리더기 출력내용</p>
<pre class="fragment" style="max-height:200px;overflow-y:auto;">링크1
링크
링크2
링크
링크3
링크
팝업창열기
링크

<small>/*****  팝업창 열림 *****/ </small>
<mark>레이업 팝업  대화상자</mark>

<small>/*****  팝업내용 읽기 *****/ </small>
레이업 팝업
헤딩  레벨 1
레이업 팝업
헤딩  레벨 1
레이업 팝업
목록  항목 수 3개
팝업창에 포커스이동
탭키 사용시 순환적 이동
팝업종료시 포커스 이동
목록 끝
버튼
닫기

<small>/*****  탭키로 닫기버튼 이동 *****/ </small>
닫기
버튼

<small>/*****  탭키로 다음 이동시 다시 레이어팝업 안에있는 컨텐츠로 이동 *****/ </small>
레이업 팝업
헤딩  레벨 1

<small>/*****  탭키로 닫기버튼 이동 후 엔터 *****/ </small>
닫기
버튼

<small>/*****  기존 링크로 돌아옴 *****/ </small>
링크
팝업창열기
링크4
링크
링크5
링크</pre>

--

### keyboard interface

<pre><code data-trim data-noescape style="max-height:300px;font-weight:bold">$('#layer_close').keydown(function(e){
	var keyCode = e.keyCode || e.which;
	if (e.shiftKey && keyCode == 9 ) { //shift+tab 키
		$(this).prev().focus();//이전 링크로 커서이동
	}else if(keyCode == 9){//탭키
		e.preventDefault();//탭키의 기본기능 삭제
		$('#layer h1').focus();//첫번째 링크로 이동
	}
});</code></pre>

키보드 초점을 대화상자 내부 첫 번째 콘트롤(레이업 팝업 헤딩  레벨 1)으로 이동

대화상자를 표시하는 동안 초점은 대화상자 안에서 벗어나지 않게 처리

---

### ID/PASSWORD

추가적인 설명문 제공<br />
(aria-describedby=" ID reference list ")

<a href="//markup.danawa.com/aria/?loc=03_idpasswd" target="_blank"><img src="//img.danawa.com/img/etc/aria/idpasswd.jpg" alt="id / password" /></a>

--

#### As-is

<pre><code data-trim data-noescape style="max-height:300px;font-weight:bold">&lt;div&gt;
	&lt;div class="id"&gt;
		&lt;label for="fname"&gt;ID&lt;/label&gt;
		&lt;input type="text" id="fname"&gt;
		&lt;div id="idcommt"&gt;5~20자의 영문 소문자, 숫자와 특수기호(_), (-)만 사용 가능합니다.&lt;/div&gt;
	&lt;/div&gt;
	&lt;div class="pw"&gt;
		&lt;label for="pwpw"&gt;PW&lt;/label&gt;
		&lt;input type="password" id="pwpw"&gt;
		&lt;div id="pwcommt"&gt;6~16자 영문 대 소문자, 숫자, 특수문자를 사용하여 입력해 주세요.&lt;/div&gt;
	&lt;/div&gt;
&lt;/div&gt;</code></pre>

<p class="fragment" style="font-size:0.7em">스크린리더기 출력내용</p>
<pre class="fragment" style="max-height:200px;overflow-y:auto;">ID  편집창
빈줄
PW  편집창  보호됨
빈줄</pre>

--

#### To-be

<pre><code data-trim data-noescape style="max-height:300px;font-weight:bold">&lt;div class="id"&gt;
	&lt;label for="fname2"&gt;ID&lt;/label&gt;
	&lt;input type="text" id="fname2" <span class="fragment">aria-describedby="<mark>idcommt2<mark></span>"&gt;
	&lt;div id="<mark>idcommt2</mark>"&gt;5~20자의 영문 소문자, 숫자와 특수기호(_), (-)만 사용 가능합니다.&lt;/div&gt;
&lt;/div&gt;
&lt;div class="pw"&gt;
	&lt;label for="pwpw2"&gt;PW&lt;/label&gt;
	&lt;input type="password" id="pwpw2" <span class="fragment">aria-describedby="<mark>pwcommt2</mark></span>"&gt;
	&lt;div id="<mark>pwcommt2</mark>"&gt;6~16자 영문 대 소문자, 숫자, 특수문자를 사용하여 입력해 주세요.&lt;/div&gt;
&lt;/div&gt;</code></pre>

<p class="fragment" style="font-size:0.7em">스크린리더기 출력내용</p>
<pre class="fragment" style="max-height:200px;overflow-y:auto;"><small>/*****  ID관련 메세지 안내 *****/ </small>
ID  편집창  <mark>5~20자의 영문 소문자, 숫자와 특수기호(_), (-)만 사용 가능합니다.</mark>
빈줄
<small>/*****  PW관련 메세지 안내 *****/ </small>
PW  편집창  보호됨  <mark>6~16자 영문 대 소문자, 숫자, 특수문자를 사용하여 입력해 주세요.</mark>
빈줄</pre>

---

### 이미지형 게시판

의미 없음(role="none presentation")

<a href="//markup.danawa.com/aria/?loc=04_board" target="_blank"><img src="//img.danawa.com/img/etc/aria/board.jpg" alt="board" /></a>

--

#### As-is

<pre><code data-trim data-noescape style="max-height:300px;font-weight:bold">&lt;ul class="news_list"&gt;
    &lt;li class="news_row"&gt;
        &lt;div class="thumb"&gt;
            &lt;a href=""&gt;
                &lt;img src="http://img.danawa.com/images/attachFiles/4/710/3709001_7.png?1535000163342" 
				alt="첫번째 뉴스 이미지" /&gt;
            &lt;/a&gt;
        &lt;/div&gt;
        &lt;div class="info"&gt;
            &lt;a href=""&gt;
                &lt;div&gt;
                    &lt;strong&gt;첫번째 뉴스 제목&lt;/strong&gt;
                &lt;/div&gt;
                &lt;div class="desc font_dotum"&gt;첫번째 뉴스 설명글입니다.&lt;/div&gt;
            &lt;/a&gt;
        &lt;/div&gt;
    &lt;/li&gt;
&lt;/ul&gt;</code></pre>

<p class="fragment" style="font-size:0.7em">스크린리더기 출력내용</p>
<pre class="fragment" style="max-height:200px;overflow-y:auto;"><small>/***** 링크내의 불필요한 중복(이미지)정보 안내 *****/ </small>
<mark>방문함  링크</mark>
<mark>그래픽</mark>
<mark>첫번째 뉴스 이미지</mark>
방문함  링크
첫번째 뉴스 제목
방문함  링크
첫번째 뉴스 설명글입니다</pre>

--

#### To-be

<pre><code data-trim data-noescape style="max-height:300px;font-weight:bold">&lt;ul class="news_list"&gt;
    &lt;li class="news_row"&gt;
        &lt;div class="thumb"&gt;
            &lt;a href="" <span class="fragment"><mark>aria-hidden="true" tabindex="-1"</mark></span>&gt;
                &lt;img src="http://img.danawa.com/images/attachFiles/4/710/3709001_7.png?1535000163342" 
				alt="첫번째 뉴스 이미지" 
				<span class="fragment"><mark>role="presentation"</mark></span>
                /&gt;
            &lt;/a&gt;
        &lt;/div&gt;
        &lt;div class="info"&gt;
            &lt;a href=""&gt;
                &lt;div&gt;
                    &lt;strong&gt;첫번째 뉴스 제목&lt;/strong&gt;
                &lt;/div&gt;
                &lt;div class="desc font_dotum"&gt;첫번째 뉴스 설명글입니다.&lt;/div&gt;
            &lt;/a&gt;
        &lt;/div&gt;
    &lt;/li&gt;
&lt;/ul&gt;</code></pre>

<p class="fragment" style="font-size:0.7em">스크린리더기 출력내용</p>
<pre class="fragment" style="max-height:200px;overflow-y:auto;"><mark>/***** 링크내의 불필요한 중복(이미지)정보 안내안함 *****/ </mark>
방문함  링크
첫번째 뉴스 제목
방문함  링크
첫번째 뉴스 설명글입니다.</pre>

---

### 페이지 내비게이션
(role="navigation")

<a href="//markup.danawa.com/aria/?loc=04_board" target="_blank"><img src="http://timg.danawa.com/img/etc/aria/pagination.jpg" alt="pagination" /></a>

--

#### As-is

<pre><code data-trim data-noescape style="max-height:300px;font-weight:bold">&lt;ul class="pagination"&gt;
    &lt;li class="active"&gt;&lt;a href="#"&gt;&lt;span&gt;현재 페이지&lt;/span&gt;&lt;span&gt;1&lt;/span&gt;&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href="#"&gt;&lt;span&gt;2&lt;/span&gt;&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href="#"&gt;&lt;span&gt;3&lt;/span&gt;&lt;/a&gt;&lt;/li&gt;
&lt;/ul&gt;</code></pre>

<p class="fragment" style="font-size:0.7em">스크린리더기 출력내용</p>
<pre class="fragment" style="max-height:200px;overflow-y:auto;">목록  항목 수 3개
링크
1
링크
2
링크
3</pre>

--

#### To-be


<pre><code data-trim data-noescape style="max-height:300px;font-weight:bold">&lt;div <span class="fragment"><mark>role="navigation" aria-label="페이지 탐색 내비게이션"</mark></span>&gt;
&lt;ul class="pagination"&gt;
    &lt;li class="active"&gt;&lt;a href="#"&gt;&lt;span&gt;현재 페이지&lt;/span&gt;&lt;span&gt;1&lt;/span&gt;&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href="#"&gt;&lt;span&gt;2&lt;/span&gt;&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href="#"&gt;&lt;span&gt;3&lt;/span&gt;&lt;/a&gt;&lt;/li&gt;
&lt;/ul&gt;</code></pre>

<p class="fragment" style="font-size:0.7em">스크린리더기 출력내용</p>
<pre class="fragment" style="max-height:200px;overflow-y:auto;"><small>/*****  페이지 내비게이션 안내 *****/ </small>
<mark>페이지 탐색 내비게이션 navigation 랜드마크 </mark>
목록  항목 수 3개
링크
1
링크
2
링크
3</pre>

--
<img src="//img.danawa.com/img/etc/aria/pagination02.jpg" alt="landmark" />
<p>콘텐츠가 많은 페이지에서 쉽게 이동할수 있게 스크린리더기에서 편의 제공</p>

---

## 사용 환경

브라우저: Chrome

스크린리더: NVDA 2018.3.2

---

## 참고문서
<a href="https://www.w3.org/TR/html52/"  target="_blank">HTML 5.2</a><br />
<a href="https://www.w3.org/TR/wai-aria/" target="_blank">WAI-ARIA 1.1</a><br />
<a href="https://www.w3.org/TR/using-aria/" target="_blank">Using ARIA</a><br />
<a href="https://www.w3.org/TR/html-aria/" target="_blank">ARIA in HTML</a><br />
<a href="https://www.w3.org/TR/wai-aria-practices/" target="_blank">WAI-ARIA Authoring Practices 1.1</a><br />
<a href="https://www.w3.org/TR/wai-aria-practices/examples/landmarks/" target="_blank">ARIA Landmarks Example</a>

---


## 감사합니다.