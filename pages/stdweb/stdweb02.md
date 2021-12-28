---
title: PC(웹표준)
permalink: stdweb02.html
sidebar: stdweb_sidebar
folder: stdweb
toc: false
keywords: 결제 취소, 결제취소, 연동, PC, 요청, 승인, 인증, signkey, signKey, mid, 데이터, 신용카드, 공통, 계좌이체, 핸드폰, 스마트폰, 가상계좌, 응답, 옵션
---

<div style="display: inline-block; width: 100%;">
  <a style="float:left;" href="/stdweb01.html">◀이전페이지</a>
  <a style="float:right;" href="/stdweb03.html">다음페이지▶</a>
</div>

# 2. 결제 연동

## 2.1 샘플코드 구조
샘플소스는 가맹점의 환경에 맞도록 수정하여 사용할 수 있습니다. Web Standard서비스는 표준 웹 통신만을 사용합니다.<br>
결제요청시에는 페이지이동(Form POST Action), API통신시에는 httpClient 통신을 이용합니다.<br>
`POST Action Content-Type : application/x-www-form-urlencoded; charset=UTF-8` <br>
`HTTPS API Request(httpClient 통신) = httpClient` 등의 http Background 통신이 가능한 유틸을 통해서 웹페이지를 요청후 그 결과를 수신<br>

본 샘플소스에는 통신에 대한 별도의 로그(Log) 기능이 존재하지 않습니다.<br>
가맹점에서 환경에 맞게 로그를 개발하시기 바랍니다.

#### 주요 연동 파일 설명 

|         파일명          | 설명                                 |
| :------------------: | ---------------------------------- |
| WelStdPayRequest.xxx | 결제요청 샘플페이지                         |
|      popup.xxx       | 결제창을 팝업으로 표시할 때 사용 (권장하지 않음)       |
|      close.xxx       | 결제창(팝업,오버레이)을 닫을 때 사용 ( **수정금지** ) |
| WelStdPayReturn.xxx  | 결제 인증결과 수신 / 승인요청 API 연동 샘플페이지     |

<div class="tabs-head">
  <span data-tab="tab-1" class="tabs-nav active">Java</span>
  <span data-tab="tab-2" class="tabs-nav">ASP.net</span>
  <span data-tab="tab-3" class="tabs-nav">ASP</span>
  <span data-tab="tab-4" class="tabs-nav">PHP</span>
</div>

<div class="tabs-content">
  <div id="tab-1" class="b-tab active">
      <h2>Java</h2>
  - WelStdweb_JAVA.zip의 압축을 풀어 설치합니다. 이때 설치 절대 경로를 확인합니다.<br/>
  - WelStdweb 결제 연동 프로그램은 다음과 같이 파일과 디렉터리가 생성됩니다.<br/>
  - WenContent 이하 소스를 웹 Root 아래 넣고 이를 참고해 결제 모듈을 연동합니다.
    <pre>
    WelStdweb
    │   
    └───WelpayStdSample
    │
    └───WEB-INF
            └───lib
                 └───WelpaySample
    </pre>
    <code>
    - Welpay0_Sample_v1.4.jar : 해당 라이브러리는 샘플페이지 구동을 위한 라이브러리로 참고만 부탁드리며, 실제 반영시엔 가맹점 환경에 맞게 직접 생성 부탁드립니다.<br/>
    - 샘플 라이브러리만을 이용하여 연동시, 가맹점 환경에 따른 오작동은 당사 확인이 어려울수 있습니다.<br/>
    - WelpayStdSample : HTML, JSP Sample 이 위치하는 폴더 입니다.
    </code>

</div>
  <div id="tab-2" class="b-tab">
      <h2>ASP.net</h2>
  - WelStdweb_ASP.zip의 압축을 풀어 설치합니다. 이때 설치 절대 경로를 확인합니다.<br/>
  - WelStdweb 결제 연동 프로그램은 다음과 같이 파일과 디렉터리가 생성됩니다.
    <pre>
    WelStdweb
    │   
    └───css
    │
    └───bin     
         └───bin 
              ├── Welpaycrypto.dll
              └── WelpayNet.dll
    </pre>
    <code>Welpaycrypto.dll, WelpayNet.dll</code> : 암복호화에 사용하는 dll 파일
  </div>
  <div id="tab-3" class="b-tab">
      <h2>ASP</h2>
  - WelStdweb_ASP_Sample_v2.x.zip의 압축을 풀어 설치합니다. 이때 설치 절대 경로를 확인합니다.<br/>
  - WelStdweb 결제 연동 프로그램은 다음과 같이 파일과 디렉터리가 생성됩니다.
    <pre>
    WelStdweb
    │   
    └───css
    │
    └───include     
              ├── aspJSON1.17 
              ├── function
              └── signature
    </pre>
    <code>function</code> 기본 제공 함수<br/>
    <code>signature</code> 위변조 방지체크 기능의 signature 생성
  </div>
  <div id="tab-4" class="b-tab">
    <h2>PHP</h2>
    <pre>
    WelStdweb
    │   
    └───WelStdPaySample
    │
    └───WEB-INF
    └──lib  
    ├── CreateIdModule
    ├── HttpClient
    ├── WelpayStdMakeSignature
    └── WelStdPayUtil
    </pre>
    <code>libs</code> : Welpay 암복호화 및 결제에서 사용하는 library 파일<br/>
    <code>WelStdPaySample</code> : HTML, PHP Sample이 위치하는 폴더입니다.
 </div>
</div>
<script src="js/tabs.js"/>

## 2.2 승인 테스트
1. 웹 브라우저에서 http://127.0.0.1/WelStdPaySample/WelStdPayRequest.xxx페이지를 호출합니다.<br>
<img src="../images/stdweb/img04.png"><br>
- Ie11의 경우 localhost로 진행할 경우 팝업창의 문제가 발생 할 수 있음
2. 승인 테스트를 위해 필수 값 및 기본 옵션 값을 매뉴얼을 참조 후 확인 후 결제 요청 버튼을 누릅니다.
3. 설치 과정 없이 지불 방법을 선택 후 필요한 정보를 기입하고 "확인"을 눌러 진행합니다. (해당 사이트 팝업을 사용으로 하지 않을 시 초기화면으로 로딩 될 수 있습니다. )
4. 지불 과정중 필요에 따라 추가적인 모듈을 다운로드 하는 경우도 있습니다. 정상적으로 지불결과 메시지가 나타나는지 확인하십시오.<br>
5. 계좌이체(뱅크페이)테스트 서버에서 테스트의 경우 지정된 테스트 정보로만 테스트 가능.
- 웹결제 > 간편결제(X), **일반결제 (O)**
- 테스트주민등록번호:  <a href="mailto:mainpg_support@welcomepayments.co.kr">메일로 문의하기(support@welcomepayments.co.kr)</a>

- **취소/조회 테스트를 위해 거래번호(TID)를 기록해 두십시오.**


## 2.3 결제 요청 페이지 작성(PayRequest)
### 2.3.1 결제 요청 데이터

- 내부 처리용 데이터 별도 저장
- form 데이터 처리가 필요한 경우 페이지 표시전에 별도로 DB 또는 세션 등에 저장해 두시기 바랍니다.
- mid, signKey는 계약 완료 가맹점에 한해 별도 제공 됨


#### mid, signkey 값 설정
- 웹 표준 결제 이용시 패스워드 기능을 하는 코드로 MID 번호별로 부여됩니다. 
- mid와 signkey값은 계약가맹점에 한해 별도 전달 예정입니다.

```java
String mid = "xxxxxxxxxx"; // 가맹점 ID(가맹점 수정후 고정)
// 가맹점에 제공된 웹 표준 사인키(가맹점 수정후 고정)
String signKey = "xxxxx";
```

mid, signKey는 <a href="mailto:mainpg_support@welcomepayments.co.kr">메일로 문의하기(support@welcomepayments.co.kr)</a>

### signkey 발급 방법
- 관리자 페이지(https://wbiz.paywelcome.co.kr)의 상점정보 > 계약정보 > 부가정보의 웹결제 signkey생성 조회 버튼 클릭 후<br>
  팝업창에서 생성 버튼 클릭 후 해당 값 소스에 반영하시기 바랍니다.

### 표준결제 스크립트 Import
- 실서버( 실반영시 반드시 수정)

  `<script language="javascript" type="text/javascript" src="HTTPS://stdpay.paywelcome.co.kr/stdjs/WelStdPay.js" charset="UTF-8"></script>`
- 테스트 서버 연동(샘플로 제공 되는 테스트 MID만 사용가능하며 운영 MID 사용 불가)

   `<script language="javascript" type="text/javascript" src="HTTPS://tstdpay.paywelcome.co.kr/stdjs/WelStdPay.js" charset="UTF-8"></script>`

- head Tag안에 설정
- 페이지 인코딩에 관계없이 고정 charset="UTF-8"(실 테스트 용 구분 후 사용)

``` javascript
<head>
….
<script language="javascript" type="text/javascript" src="HTTPS://stdpay.paywelcome.co.kr/stdjs/WelStdPay.js" charset="UTF-8"></script>
….
</head>….

```

### Iframe, Popup 사이즈
- iframe의 경우 ( 사용 권장)
  `width:820px; height=600px;`
- popup 의 경우 ( 팝업 사용을 권장하지 않으며, 브라우저별 이슈 발생 시 대응불가 )
  `width=820px;height=600px`

### Popup 허용 여부 체크 기능
- 팝업 허용 설정이 안되어 있을 경우, 가맹점의 요청페이지가 허용시 리프레시됨으로, 로딩 완료 후 가 팝업을 띄워주는 기능
- `<body ... onload="INIStdPay.allowpopup();">` 추가

### WelStdpay.pay 함수호출
- INIStdpay.pay 함수 호출은 submit 이 아닌 단순 action 형태로 진행
  `<button onclick="INIStdPay.pay('SendPayForm_id')" style="padding:10px">결제요청</button>`

### Form에 결제 요청 데이터 생성
- Form Tag에 ID설정(결제요청 스크립트 실행시 사용됨)
- 필드 대소문자 구분 (일부 가맹점에서 필요에 의해 사용자가 변경하는 경우를 제외하고 모두 type="hidden"을 사용)
- 아래 요청데이터 / Sample Source를 참조

```javascript
<form id=" SendPayForm_id" name="SendPayForm_name" method="POST">
  <input type="hidden" name="mid" value="xxxxxxxxxx"/>
  <input type="hidden" name="price" value="1004"/>
   ……….. 
</form>
```
<img class="emoji" title=":warning:" alt=":warning:" src="https://github.githubassets.com/images/icons/emoji/unicode/26a0.png"> <code class="language-plaintext highlighter-rouge">
Web Standard 서비스는 Form Post로 결제 요청되며, <form> 태그에 action 속성 설정 / submit 등의 모든 동작은 Import 된 스크립트에 의해서 자동 처리됩니다.</code>

결제 인증 기본 요청데이터 필드는 아래와 같습니다.<br>


#### [1-1] 기본 요청데이터 필드

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table style = "table-layout: auto; width: 100%; table-layout: fixed;" >
<thead>
<tr>
<th class="center-align" style="width: 15%">필드</th>
<th class="center-align" style="width: 15%">필드명</th>
<th class="center-align" style="width: 20%">타입</th>
<th class="center-align" style="width: 10%">필수</th>
<th class="center-align" style="width: 40%">비고</th>
</tr>
</thead>
<tbody>
<tr>
<td class="center-align">version</td>
<td class="center-align">버전</td>
<td class="center-align">String(20)</td>
<td class="center-align">○</td>
<td>전문 버전<br><code class="language-plaintext highlighter-rouge">"1.0"</code></td>
</tr>
<tr>
<td class="center-align">mid</td>
<td class="center-align">상점아이디</td>
<td class="center-align">String(10,Fixed)</td>
<td class="center-align">○<br>위변조<br>검증</td>
<td>제공된 mid, 10자리 고정<br><code class="language-plaintext highlighter-rouge">"xxxxxxxxxx"</code></td>
</tr>
<tr>
<td class="center-align">oid</td>
<td class="center-align">주문번호</td>
<td class="center-align">String(40)</td>
<td class="center-align">○</td>
<td>주문단위 unique한 값 ( mid+&quot;_&quot;+timestamp ) <br><code class="language-plaintext highlighter-rouge">"xxx_1335233672723"</code></td>
</tr>
<tr>
<td class="center-align">goodname</td>
<td class="center-align">상품명</td>
<td class="center-align">String(80)</td>
<td class="center-align">○</td>
<td>한글/특수기호 입력가능<br>40Byte 초과 요청시 37Byte + …으로 자동 변환<br><code class="language-plaintext highlighter-rouge">“키보드/마우스”</code></td>
</tr>

<tr>
<td class="center-align">price</td>
<td class="center-align">결제금액</td>
<td class="center-align">Number(8)</td>
<td class="center-align">○<br>위변조<br>검증</td>
<td>숫자만 입력, 1달러는 100으로 시작<br><code class="language-plaintext highlighter-rouge">1004</code></td>
</tr>

<tr>
<td class="center-align">tax</td>
<td class="center-align">부가세</td>
<td class="center-align">Number(8)</td>
<td class="center-align">X</td>
<td>숫자만 입력<br>대상: <code class="language-plaintext highlighter-rouge">부가세업체정함</code>설정업체에 한함
<br>주의: 전체금액의 10%이하로 설정, 가맹점에서 등록시 VAT가 총 상품가격의 10% 초과할 경우는 거절됨
<br><code class="language-plaintext highlighter-rouge">1004</code></td>
</tr>

<tr>
<td class="center-align">taxfree</td>
<td class="center-align">비과세</td>
<td class="center-align">Number(8)</td>
<td class="center-align">X</td>
<td>숫자만 입력<br>대상: &#39;부가세업체정함&#39; 설정업체에 한함과세되지 않는 금액 <br><code class="language-plaintext highlighter-rouge">1004</code></td>
</tr>
<tr>
<td class="center-align">currency</td>
<td class="center-align">통화구분</td>
<td class="center-align">String(3)</td>
<td class="center-align">○</td>
<td>USD는 카드 결제만 가능(ISP는 결제안됨)<br><code class="language-plaintext highlighter-rouge">“WON”</code>[WON:한화,USD:달러]</td>
</tr>
<tr>
<td class="center-align">buyername</td>
<td class="center-align">구매자명</td>
<td class="center-align">String(30)</td>
<td class="center-align">○</td>
<td class="left-align">한글/특수기호 입력가능* 30Byte 초과 요청시 27Byte + …으로 자동 변환<br><code class="language-plaintext highlighter-rouge">"홍길동"</code></td>
</tr>
<tr>
<td class="center-align">buyertel</td>
<td class="center-align">구매자Mobile번호</td>
<td class="center-align">String(20)</td>
<td class="center-align">○</td>
<td>숫자와 "-"만 허용 <br><code class="language-plaintext highlighter-rouge">010-2000-1234</code></td>
</tr>
<tr>
<td class="center-align">buyeremail</td>
<td class="center-align">구매자Email</td>
<td class="center-align">String(60)</td>
<td class="center-align">X</td>
<td>이메일 형식에 맞도록 <br><code class="language-plaintext highlighter-rouge">buyer@example.com</code></td>
</tr>
<tr>
<td class="center-align">parentemail</td>
<td class="center-align">보호자Email</td>
<td class="center-align">String(60)</td>
<td></td>
<td>14세 미만 필수 <code class="language-plaintext highlighter-rouge">parent@example.com</code></td>
</tr>
<tr>
<td class="center-align">timestamp</td>
<td class="center-align">타임스탬프</td>
<td class="center-align">Number(20)</td>
<td class="center-align">○<br>위변조<br>검증</td>
<td>TimeInMillis(Long형) → 제공라이브러로 생성가능(샘플소스참조)<br><code class="language-plaintext highlighter-rouge">1335233672723</code></td>
</tr>
<tr>
<td class="center-align">signature</td>
<td class="center-align">signature</td>
<td class="center-align">String(64,Fixed)</td>
<td class="center-align">○</td>
<td>위변조 방지 SHA256 Hash 값
<a href="/prepare01.html#인증-요청-시-signature-생성">
<strong>[참조-signature 생성 대상 target 필드]</strong></a><br><code class="language-plaintext highlighter-rouge">"8ca9e064777ea2fc0d4b79a5c891f3bdf30edd45c129dcfc226ba5e7e85cd5f3"</code><br/>
<p style="color: red;"><strong>signature생성에 대한 자세한 사항은 <a href="/prepare01.html#3-signature-생성">연동 준비하기 - 1.2 Signature</a>를 참고 바랍니다.</strong></p>
</td>
</tr>
<tr>
<td class="center-align">returnUrl</td>
<td class="center-align">리턴Url(인증결과수신Url)</td>
<td class="center-align">String(N/A)</td>
<td class="center-align">○</td>
<td>결제창을 통해 인증완료된 결과를 수신받고 승인요청을 해서 결과를 표시할 페이지 URL
<a href="/stdweb02.html#24-리턴-페이지-인증수신승인-api-작성-payreturn">
<strong>[참조-리턴 페이지 인증수신/승인api 작성 payreturn]</strong></a><br><code class="language-plaintext highlighter-rouge">"HTTPS://www.exsample.com/INIpayStandardSample/INIpayResult.jsp"</code></td>
</tr>
<tr>
<td class="center-align">mKey</td>
<td class="center-align">signkey에 대한<br>hash값</td>
<td class="center-align">String(N/A)</td>
<td class="center-align">○</td>
<td>signkey에 대한 검증값<br><code class="language-plaintext highlighter-rouge">"3a9503069192f207491d4b19bd743fc249a761ed94246c8c42fed06c3cd15a33"</code></td>
</tr>
<tr>
<td class="center-align">gopaymethod</td>
<td class="center-align">요청결제수단표시</td>
<td class="center-align">String(N/A)</td>
<td class="center-align">X</td>
<td>결제 수단 중 선택적 표시<br>옵션생략시 전체 결제 수단 표시<br>
<a href="/code02.html#23-gopaymethod-옵션">
<strong>[참조-gopaymethod 옵션]</strong></a></td>
</tr>
<tr>
<td class="center-align">offerPeriod</td>
<td class="center-align">제공기간</td>
<td class="center-align">String(N/A)</td>
<td class="center-align">X</td>
<td>가맹점에서 판매상품에 대한 제공기한 설정<br><code class="language-plaintext highlighter-rouge">"20130101-20130331"</code><br>[Y2:년단위결제, M2:월단위결제, yyyyMMdd-yyyyMMdd : 시작일-종료일]</td>
</tr>
<tr>
<td class="center-align">languageView</td>
<td class="center-align">초기 표시 언어</td>
<td class="center-align">String(2)</td>
<td class="center-align">X</td>
<td>결제창 표시 언어, PC는 결제창내 언어변경 버튼 존재<br><code class="language-plaintext highlighter-rouge">"ko"</code> / [ko:한국어, en:영어]</td>
</tr>
<tr>
<td class="center-align">charset</td>
<td class="center-align">결과 인코딩</td>
<td class="center-align">String(5)</td>
<td class="center-align">X</td>
<td>결과 수신 charset <br><code class="language-plaintext highlighter-rouge">"UTF-8"</code>/ [UTF-8, EUC-KR]</td>
</tr>
<tr>
<td class="center-align">payViewType</td>
<td class="center-align">결제창 표시방법</td>
<td class="center-align">String(N/A)</td>
<td class="center-align">X</td>
<td>Default:overlay</td>
</tr>
<tr>
<td class="center-align">closeUrl</td>
<td class="center-align">결제창 닫기처리Url</td>
<td class="center-align">String(N/A)</td>
<td class="center-align">○</td>
<td>close.jsp 샘플사용(소스 수정 불필요)<br><code class="language-plaintext highlighter-rouge">"HTTPS://www.exsample.com/inipaysmart/close.jsp"</code></td>
</tr>
<tr>
<td class="center-align">popupUrl</td>
<td class="center-align">팝업처리Url</td>
<td class="center-align">String(N/A)</td>
<td class="center-align">○</td>
<td>popup.jsp 샘플사용(소스 수정 불필요 : 비권장)<br><code class="language-plaintext highlighter-rouge">"HTTPS://www.exsample.com/inipaysmart/popup.jsp"</code></td>
</tr>
<tr>
<td class="center-align">merchantData</td>
<td class="center-align">가맹점데이터</td>
<td class="center-align">String(2000)</td>
<td class="center-align">X</td>
<td>인증 성공시 가맹점으로 리턴 <br> <code class="language-plaintext highlighter-rouge">"a=A&b=B"</code></td>
</tr>
<tr>
<td class="center-align">acceptmethod</td>
<td class="center-align">acceptmethod</td>
<td class="center-align">String(N/A)</td>
<td class="center-align">X</td>
<td>결제수단별 추가 옵션값<br><code class="language-plaintext highlighter-rouge">CARDPOINT:va_receipt:vbank(20150425):SKIN(ORIGINAL):FONT(ORIGINAL): poptargetself</code></td>
</tr>
</tbody>
</table>

</div>
</details>

#### [1-2] acceptmethod 공통 추가 옵션

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table>
  <thead>
    <tr>
      <th class="center-align" style="width: 15%">필드</th>
      <th class="center-align" style="width: 15%">필드명</th>
      <th class="center-align" style="width: 15%">타입</th>
      <th class="center-align" style="width: 10%">필수</th>
      <th class="left-align" style="width: 45%">비고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align" rowspan="3">acceptmethod
<br><br>
</td>
      <td class="center-align">배경색상</td>
      <td class="center-align">String</td>
      <td class="center-align">X</td>
      <td class="left-align">결제창의 배경 색상을 변경 / 색상표 값으로 설정 가능(미 설정 시 기본값 : #c1272c)<br><code class="language-plaintext highlighter-rouge">SKIN(BLUE)</code></td>
    </tr>
    <tr>
      <td class="center-align">인증 결과 처리 방식</td>
      <td class="center-align">String</td>
      <td class="center-align">X</td>
      <td class="left-align">인증완료 후 returnUrl 호출 시 타켓을 self로 변경 결제창 내에서 페이지 전환 옵션<br>(미 설정 시 기본값 : top)<br><code class="language-plaintext highlighter-rouge">poptargetself</code></td>
    </tr>
    <tr>  
      <td class="center-align">에스크로 결제여부</td>
      <td class="center-align">String</td>
      <td class="center-align">X</td>
      <td class="left-align">설정 시 ”에스크로 약관동의”와”구매자 본인확인”페이지가 포함된 에스크로결제창을 호출합니다. (미설정시 일반거래,에스크로 사용 설정된 가맹점만 사용가능합니다.)<br><code class="language-plaintext highlighter-rouge">useescrow</code></td>
    </tr>
  </tbody>
</table>

</div>
</details>

#### [1-3] 신용카드 추가 요청필드 (선택)

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table>
  <thead>
    <tr>
      <th style="text-align: center; width: 15%">필드</th>
      <th style="text-align: center; width: 20%">하위필드</th>
      <th style="text-align: center; width: 15%">필드명</th>
      <th style="text-align: center; width: 10%">타입</th>
      <th style="text-align: left; width: 40%">비고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">quotabase</td>
      <td> </td>
      <td class="center-align">할부 개월</td>
      <td class="center-align">String</td>
      <td style="text-align: left"> 일시불은 기본적으로 표시, 생략시 일시불만<br>현대카드 1만원,그 외 5만원 이상시에만 동작<br>“2:3:4”, “2:0”<br>* 개월수를 <code class="language-plaintext highlighter-rouge">:</code> 로 구분된 값</td>
    </tr>
    <tr>
      <td class="center-align">nointerest</td>
      <td> </td>
      <td class="center-align">가맹점 부담 무이자 할부설정</td>
      <td class="center-align">String</td>
      <td class="left-align">5만원 이상시에만 동작 / 카드사 무이자와 무관<br>
      <a href="/code02.html#24-카드사-승인코드"><strong>[참조-카드사 승인코드]</strong></a><br>
      “11-2:3:5:6,34-2:6”, “04-2:6”<br>* 카드사코드-할부개월:할부개월…<br>여러카드는 공백없이,로 구분</td>
    </tr>
    <tr>
      <td style="text-align: center; vertical-align: middle" rowspan="7">acceptmethod</td>
      <td class="center-align">below1000</td>
      <td class="center-align">1000원이하 결제</td>
      <td class="center-align">String</td>
      <td class="left-align">기본적으로 1000원이하 결제 불가능<br><code class="language-plaintext highlighter-rouge">"below1000"</code></td>
    </tr>
    <tr>
      <td class="center-align">ini_onlycardcode</td>
      <td class="center-align">결제 카드사 선택</td>
      <td class="center-align">String</td>
      <td style="text-align: left"> 생략 시 결제 가능한 모든 카드사 표시
      <br><a href="/code02.html#24-카드사-승인코드"><strong>[참조-카드사 승인코드]</strong></a><br>
      카드사코드를 “:”로 구분된 값
      </td>
    </tr>
    <tr>
      <td class="center-align">onlyeasypaycode</td>
      <td class="center-align">결제 간편결제 선택</td>
      <td class="center-align">String</td>
      <td class="left-align">생략 시 결제 가능한 모든 간편결제 표시
      <br><a href="/code02.html#24-카드사-승인코드"><strong>[참조-카드사 승인코드]</strong></a><br>
      <code class="language-plaintext highlighter-rouge">“kakaopay:lpay:payco”</code><br>간편결제코드를 “:”로 구분된 값</td>
    </tr>
    <tr>
      <td class="center-align">CARDPOINT</td>
      <td class="center-align">카드포인트<br>사용유무</td>
      <td class="center-align">String</td>
      <td class="left-align">포인트를 사용하는 카드를 선택시 신용카드 메인 화면에 카드포인트를 사용할지에 대한 선택창이 표시된다.
      <br><code class="language-plaintext highlighter-rouge">“cardpoint”</code></td>
    </tr>
    <tr>
      <td class="center-align">SLIMQUOTA</td>
      <td class="center-align">부분무이자설정</td>
      <td class="center-align">String</td>
      <td class="left-align">슬림할부를 지정한다.<br>SLIMQUOTA(코드-개월:개월) 로 사용한다.<br><code class="language-plaintext highlighter-rouge">^</code>구분자로 카드코드를 구분한다.
      <br><code class="language-plaintext highlighter-rouge">“SLIMQUOTA (11-2:3^34-2:3)”</code></td>
    </tr>
    <tr>
      <td class="center-align">PAYPOPUP</td>
      <td class="center-align">안심클릭 뷰옵션</td>
      <td class="center-align">String</td>
      <td class="left-align">안심클릭을 Popup 형태로 서비스를 제공한다. Edge의 경우 자동 설정됩니다.
      <br><code class="language-plaintext highlighter-rouge">“PAYPOPUP”</code></td>
    </tr>
    <tr>
      <td class="center-align">hidebar</td>
      <td class="center-align">프로그래스바<br>뷰옵션</td>
      <td class="center-align">String</td>
      <td class="left-align">결제 진행시 노출되는 프로그래스 바를 안보이도록 설정한다.
      <br><code class="language-plaintext highlighter-rouge">"hidebar"</code></td>
    </tr>
  </tbody>
</table>

</div>
</details>

#### [1-4] 휴대폰결제 추가 요청필드 (선택)

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table>
  <thead>
    <tr>
      <th style="text-align: center; width: 15%">필드</th>
      <th style="text-align: center; width: 15%">하위필드</th>
      <th style="text-align: center; width: 15%">필드명</th>
      <th style="text-align: center; width: 10%">타입</th>
      <th style="text-align: center; width: 45%">비고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align" rowspan="6">acceptmethod
<br><br><br><br><br>
</td>
      <td class="center-align">HPP</td>
      <td class="center-align">휴대폰 결제<br>상품 유형</td>
      <td class="center-align">String</td>
      <td class="left-align">휴대폰 결제 상품 유형<br>컨텐츠/실물/빌링컨텐츠/빌링실물여부는 계약담당자에게 확인<br>
      <code class="language-plaintext highlighter-rouge">"HPP(1)"[1:컨텐츠,2:실물,4:빌링컨텐츠,5:빌링실물]</code></td>
    </tr>
    <tr>
      <td class="center-align">hppablecorp</td>
      <td class="center-align">표시될 통신사<br>리스트</td>
      <td class="center-align">String</td>
      <td class="left-align">SKT : S텔레콤, KTF : KT, LGT : LG U+, MVX : 알뜰폰<br>MVX중일부만 설정 시 MVX 제외 후 CJH(헬로모바일),KCT(티플러스),SKL(SK7mobile) 중 일부만 선택
      <br><code class="language-plaintext highlighter-rouge">“hppablecorp(SKT:KTF:LGT:MVX)”</code></td>
    </tr>
    <tr>
      <td class="center-align">hppdefaultcorp</td>
      <td class="center-align">휴대폰통신사<br>기본선택</td>
      <td class="center-align">String</td>
      <td class="left-align">통신사 리스트에서 입력 통신사가 기본 선택 되어짐<br>SKT, KTF, LGT, MVX 중 하나만 설정 가능<br>MVX 중 선택 시 CJH, KCT, SKL로 설정가능<br>미입력시나 공백으로 입력시 선택된 통신사 없음
      <br><code class="language-plaintext highlighter-rouge">“hppdefaultcorp(SKT)”</code></td>
    </tr>
    <tr>
      <td class="center-align">hppnofix</td>
      <td class="center-align">휴대폰 번호<br>수정불가여부</td>
      <td class="center-align">String</td>
      <td class="left-align">휴대폰 번호 수정불가여부<br>N : 수정가능, Y : 수정불가능
      <br><code class="language-plaintext highlighter-rouge">hppnofix(N)</code></td>
    </tr>
    <tr>
      <td class="center-align">hppauthtype</td>
      <td class="center-align">휴대폰 결제<br>인증방법 선택</td>
      <td class="center-align">String</td>
      <td class="left-align">휴대폰 결제시 문자/ARS 인증 선택(옵션없을시 SMS)<br>ARS:ARS인증, SMS:문자인증(해당 옵션은 모빌리언스만 가능)
      <br><code class="language-plaintext highlighter-rouge">hppauthtype(ARS)</code></td>
    </tr>
    <tr>
      <td class="center-align">billauth</td>
      <td class="center-align">휴대폰<br>빌키 발급</td>
      <td class="center-align">String</td>
      <td class="left-align">휴대폰 빌키 발급시 사용상품유형 HPP(4) 또는 HPP(5)로 설정 필요 휴대폰 빌링 사용은 별도 사용 설정 필요
      <br><code class="language-plaintext highlighter-rouge">billauth(HPP)</code></td>
    </tr>
  </tbody>
</table>

</div>
</details>

#### [1-5] 계좌이체 추가 요청필드 (선택)

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table>
<colgroup>
<col style="text-align: center; width: 15%">
<col style="text-align: center; width: 15%">
<col style="text-align: center; width: 15%">
<col style="text-align: center; width: 10%">
<col style="text-align: center; width: 45%">
</colgroup>
  <thead>
    <tr>
      <th class="center-align">필드</th>
      <th class="center-align">하위필드</th>
      <th class="center-align">필드명</th>
      <th class="center-align">타입</th>
      <th class="center-align">비고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">acceptmethod</td>
      <td class="center-align">no_receipt</td>
      <td class="center-align">현금영수증 미발행</td>
      <td class="center-align">String</td>
      <td class="left-align">현금영수증 발행 차단 옵션<br>계좌이체 시 사용하는 현금영수증 미발행 여부 확인 필드 – 옵션을 사용시 현금 영수증 UI 출력하지 않음 <br><code class="language-plaintext highlighter-rouge">“no_receipt”</code></td>
    </tr>
  </tbody>
</table>

</div>
</details>

#### [1-6] 가상계좌 추가 요청필드 (선택)

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table>
<colgroup>
<col style="text-align: center; width: 15%">
<col style="text-align: center; width: 15%">
<col style="text-align: center; width: 15%">
<col style="text-align: center; width: 10%">
<col style="text-align: center; width: 45%">
</colgroup>
  <thead>
    <tr>
      <th class="center-align">필드</th>
      <th class="center-align">하위필드</th>
      <th class="center-align">필드명</th>
      <th class="center-align">타입</th>
      <th class="center-align">비고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">INIregno</td>
      <td></td>
      <td class="center-align">주민번호 설정 기능</td>
      <td class="center-align">String</td>
      <td>13자리:주민번호,10자리:사업자번호,미입력시:화면에서 입력가능<br><code class="language-plaintext highlighter-rouge">“201504161111111”</code></td>
    </tr>
    <tr>
      <td class="center-align" rowspan="3">acceptmethod</td>
      <td class="center-align">vbank</td>
      <td class="center-align">입금기한 및<br>입금시간</td>
      <td class="center-align">String</td>
      <td>입금기한 및 입금 시간 설정 옵션<br>vbank(20211216) 또는 vbank(202112261900) 시분까지 지정(초 설정 불가)<br><code class="language-plaintext highlighter-rouge">"vbank(20150416)"</code></td>
    </tr>
    <tr>
      <td class="center-align">va_receipt</td>
      <td class="center-align">현금영수증 발급<br>UI 옵션</td>
      <td class="center-align">String</td>
      <td>현금영수증 발급 UI 표시 옵션<br> (CASHRECEIPT 옵션이 기준정보에 있는 경우)<br>–주민번호만 표시<br><code class="language-plaintext highlighter-rouge">“va_receipt”</code></td>
    </tr>
    <tr>
      <td class="center-align">va_ckprice</td>
      <td  class="center-align">주민번호 채번 시<br>금액 확인</td>
      <td class="center-align">String</td>
      <td>주민번호 채번시 금액 체크 기능<br><code class="language-plaintext highlighter-rouge">“va_ckprice”</code></td>
    </tr>
  </tbody>
</table>

</div>
</details>

## 2.4 리턴 페이지 (인증수신/승인 API) 작성 (PayReturn)
- 작성시Sample Source를 참고하여 작성하시기 바랍니다.

### 2.4.1. 인증결과 수신
- 결제창을통해인증이완료되면인증결과를가맹점으로전달합니다.
  인증 결과 데이터 필드는 아래와 같습니다.

#### [2-1] 인증결과 데이터

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table>
<colgroup>
<col style="text-align: center; width: 15%">
<col style="text-align: center; width: 15%">
<col style="text-align: center; width: 15%">
<col style="text-align: center; width: 55%">
</colgroup>
  <thead>
    <tr>
      <th class="center-align">필드</th>
      <th class="center-align">필드명</th>
      <th class="center-align">타입</th>
      <th class="center-align">비고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">resultCode</td>
      <td class="center-align">결과코드</td>
      <td class="center-align">String(10)</td>
      <td>[<code class="language-plaintext highlighter-rouge">0000</code> : 정상, 기타 : 실패]</td>
    </tr>
    <tr>
      <td class="center-align">resultMsg</td>
      <td class="center-align">결과메세지</td>
      <td class="center-align">String(100)</td>
      <td>성공시 : <code class="language-plaintext highlighter-rouge">OK</code>, 실패시 : 기타 오류 메시지</td>
    </tr>
    <tr>
      <td class="center-align">mid</td>
      <td class="center-align">가맹점 ID</td>
      <td class="center-align">String(10)</td>
      <td> </td>
    </tr>
    <tr>
      <td class="center-align">orderNumber</td>
      <td class="center-align">가맹점 주문번호</td>
      <td class="center-align">String(40)</td>
      <td> </td>
    </tr>
    <tr>
      <td class="center-align">authToken</td>
      <td class="center-align">승인요청</td>
      <td class="center-align">String</td>
      <td>승인요청검증토큰</td>
      <td class="center-align"> </td>
    </tr>
    <tr>
      <td class="center-align">authUrl</td>
      <td class="center-align">승인요청 Url</td>
      <td class="center-align">String</td>
      <td>해당 URL로 HTTPS API Request(httpClient 통신) 승인 요청(POST)</td>
      <td class="center-align"> </td>
    </tr>
    <tr>
      <td class="center-align">netCancelUrl</td>
      <td class="center-align">망취소요청 Url</td>
      <td class="center-align">String</td>
      <td>승인요청 후 인증결과 수신 실패 / DB저장 실패 시 해당 URL로 HTTPS API Request(httpClient 통신) 승인 요청(POST)</td>
      <td class="center-align"> </td>
    </tr>
    <tr>
      <td class="center-align">charset</td>
      <td class="center-align">인증결과 인코딩</td>
      <td class="center-align">String(5)</td>
      <td>가맹점에서 결제요청시 전달한 charset값 생략시 UTF-8</td>
    </tr>
    <tr>
      <td class="center-align">merchantData</td>
      <td class="center-align">가맹점 데이터</td>
      <td class="center-align">String(2000)</td>
      <td>가맹점 관리데이터</td>
    </tr>
  </tbody>
</table>

</div>
</details>

### 2.4.2 승인API 요청

- 인증결과가 성공일때 authUrl로 HTTPS API Request(httpClient 통신)를 통해 페이지 요청
- HTTPS API Request(httpClient 통신)
- httpClient 등의 http Background 통신이 가능한 유틸을 통해서 웹페이지를 요청후 그 결과를 수신
- 가맹점 환경에 따른 charset, format을 지정하여 요청
- 승인요청은 인증결과 리턴후 5분이내 이루어져야만 합니다.
- 결제 승인 요청데이터는 필드는 아래와 같습니다.

#### [2-2] 승인요청 데이터

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table>
  <thead>
    <tr>
      <th style="text-align: center; width: 15%">필드</th>
      <th style="text-align: center; width: 15%">필드명</th>
      <th style="text-align: center; width: 15%">타입</th>
      <th style="text-align: center; width: 10%">필수</th>
      <th style="text-align: left; width: 45%">비고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">mid</td>
      <td class="center-align">가맹점 id</td>
      <td class="center-align">String(10,fixed)</td>
      <td class="center-align">○</td>
      <td>가맹점 아이디</td>
    </tr>
    <tr>
      <td class="center-align">authToken</td>
      <td class="center-align">인증 결과코드</td>
      <td class="center-align">String</td>
      <td class="center-align">○<br>위변조<br>검증</td>
      <td>인증 결과에 대한 위변조 검증값</td>
      <td></td>
    </tr>
    <tr>
      <td class="center-align">price</td>
      <td class="center-align">인증가격</td>
      <td class="center-align">Number(64)</td>
      <td class="center-align">○<br>위변조<br>검증</td>
      <td>인증 가격 결과에 대한 위변조 확인용</td>
    </tr>
    <tr>
      <td class="center-align">timestamp</td>
      <td class="center-align">타임스템프</td>
      <td class="center-align">Number(20)</td>
      <td class="center-align">○<br>위변조<br>검증</td>
      <td>TimeInMillis(Long형)→제공라이브러리로 생성가능</td>
    </tr>
    <tr>
      <td class="center-align">signature</td>
      <td class="center-align">signature</td>
      <td class="center-align">String(64)</td>
      <td class="center-align">○</td>
      <td>위변조 방지 SHA256 Hash 값, 결제요청 동일한 방법으로 signature와 생성<br>
      <a href="/prepare01.html#승인-요청-시-signature-생성"><strong>[참조-승인요청 signature 생성 대상target필드]</strong></a><br/>
      <p style="color: red;"><strong>signature생성에 대한 자세한 사항은 <a href="/prepare01.html#3-signature-생성">연동 준비하기 - 3 Signature</a>를 참고 바랍니다.</strong></p></td>
    </tr>
    <tr>
      <td class="center-align">charset</td>
      <td class="center-align">리턴 인코딩</td>
      <td class="center-align">String(5)</td>
      <td></td>
      <td>결과 수신 charset</td>
    </tr>
    <tr>
      <td class="center-align">format</td>
      <td class="center-align">리턴 형식</td>
      <td class="center-align">String(5)</td>
      <td></td>
      <td>결과 수신 형태XML : <result>내의 XML 결과 리턴<br>JSON : root 없이 json 결과 리턴<br>NVP : name=value&amp;name=value으로 결과 리턴</result><br>
      <a href="/stdweb02.html#2-13-리턴-형식별-승인결과-예시"><strong>[참조-리턴 형식별 승인결과 예시]</strong></a></td>
    </tr>
  </tbody>
</table>

</div>
</details>

### 2.4.3. 승인API 결과(결제완료)

- 승인 요청후 결제결과(responseBody)를 받아 요청타입(format)에 따라서 파싱 후에 내부처리(DB저장 등) 하시기 바랍니다.
- 수신시 전송 필드을 명확히하여 처리하시기 바랍니다. (필드 대/소문자 구분)
- 승인에 실패하였을 경우 실패시 전달되는 데이터만 전송됩니다.
- 결제 수단에 따라 공통필드외 추가적으로 다른 데이터가 전송됩니다.
- 승인 결과 데이터 필드는 아래와 같습니다.

#### [2-4] 승인결과 데이터(공통)

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table>
  <thead>
    <tr>
      <th class="center-align" style="width: 15%">필드</th>
      <th class="center-align" style="width: 25%">필드명</th>
      <th class="center-align" style="width: 15%">타입</th>
      <th class="center-align" style="width: 45%">비고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">tid</td>
      <td class="center-align">거래번호</td>
      <td class="center-align">String(40)</td>
      <td>거래 번호</td>
    </tr>
    <tr>
      <td class="center-align">resultCode</td>
      <td class="center-align">결과코드</td>
      <td class="center-align">String(10)</td>
      <td>[0000 : 정상, 기타 : 실패]승인결과코드 참조</td>
    </tr>
    <tr>
      <td class="center-align">resultMsg</td>
      <td class="center-align">결과메세지</td>
      <td class="center-align">String(100)</td>
      <td>결과 메세지</td>
    </tr>
    <tr>
      <td class="center-align">EventCode</td>
      <td class="center-align">이벤트코드</td>
      <td class="center-align">String(3)</td>
      <td>카드 할부 및 행사 적용 코드<a href="code02.html#29-카드-이벤트-적용-코드"><strong>[참조-카드 이벤트 적용 코드]</strong></a></td>
    </tr>
    <tr>
      <td class="center-align">TotPrice</td>
      <td class="center-align">거래금액</td>
      <td class="center-align">String(20)</td>
      <td>결제결과 금액</td>
    </tr>
    <tr>
      <td class="center-align">MOID</td>
      <td class="center-align">주문번호</td>
      <td class="center-align">String(12)</td>
      <td>상점주문번호, 결제 요청시 "oid"필드에 설정된값</td>
    </tr>
    <tr>
      <td class="center-align">payMethod</td>
      <td class="center-align">지불수단</td>
      <td class="center-align">String(10)</td>
      <td>결제 방법</td>
    </tr>
    <tr>
      <td class="center-align">applNum</td>
      <td class="center-align">승인번호</td>
      <td class="center-align">String(16)</td>
      <td>결제수단에 따리 미전송</td>
    </tr>
    <tr>
      <td class="center-align">applDate</td>
      <td class="center-align">승인일자</td>
      <td class="center-align">String(8)</td>
      <td>YYYYMMDD</td>
    </tr>
    <tr>
      <td class="center-align">applTime</td>
      <td class="center-align">승인시간</td>
      <td class="center-align">String(6)</td>
      <td>hh24miss</td>
    </tr>
    <tr>
      <td class="center-align">buyerEmail</td>
      <td class="center-align">구매자Email</td>
      <td class="center-align">String(60)</td>
      <td>“buyer@example.com”</td>
    </tr>
    <tr>
      <td class="center-align">buyerTel</td>
      <td class="center-align">구매자Mobile번호</td>
      <td class="center-align">String(20)</td>
      <td>“010-2000-1234”</td>
    </tr>
    <tr>
      <td class="center-align">buyerName</td>
      <td class="center-align">구매자명</td>
      <td class="center-align">String(30)</td>
      <td>“홍길동”</td>
    </tr>
  </tbody>
</table>

</div>
</details>

- 결제수단에 따라 승인 결과가 추가로 수신됩니다. 데이터는 다음과 같습니다.

#### [2-5] 승인결과 데이터(신용카드)

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table>
<colgroup>
<col style="text-align: center; width: 20%">
<col style="text-align: center; width: 20%">
<col style="text-align: center; width: 15%">
<col style="text-align: center; width: 45%">
</colgroup>
  <thead>
    <tr>
      <th class="center-align">필드</th>
      <th class="center-align">필드명</th>
      <th class="center-align">타입</th>
      <th class="center-align">비고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">CARD_Num</td>
      <td class="center-align">신용카드번호</td>
      <td class="center-align">String(16)</td>
      <td>신용카드번호</td>
    </tr>
    <tr>
      <td class="center-align">CARD_Interest</td>
      <td class="center-align">할부여부</td>
      <td class="center-align">String(1)</td>
      <td>카드 할부여부<br>("1"이면 무이자할부)</td>
    </tr>
    <tr>
      <td class="center-align">CARD_Quota</td>
      <td class="center-align">카드 할부기간</td>
      <td class="center-align">String(2)</td>
      <td>카드 할부기간</td>
    </tr>
    <tr>
      <td class="center-align">CARD_Code</td>
      <td class="center-align">카드사 코드<br></td>
      <td class="center-align">String(2)</td>
      <td>카드사 코드 <a href="/code02.html#24-카드사-승인코드"><strong>[참조-카드사 승인코드]</strong></a></td>
    </tr>
    <tr>
      <td class="center-align">CARD_PRTC_CODE</td>
      <td class="center-align">부분취소 가능여부</td>
      <td class="center-align">String(1)</td>
      <td>부분취소 가능여부 (1:가능, 0:불가능)</td>
    </tr>
    <tr>
      <td class="center-align">CARD_BankCode</td>
      <td class="center-align">카드발급사</td>
      <td class="center-align">String(2)</td>
      <td>카드발급사(은행) 코드 <a href="/code02.html#26-카드-발급사은행-코드"><strong>[참조-카드 발급사(은행) 코드]</strong></a><br>카드사 직발행 카드가 아닌 계열카드인 경우, 2자리 신용카드사 코드와 더불어 자세한 카드 정보를 나타냅니다.<br>(직발행 카드인 경우 "00"으로 반환됩니다.)<br>CARD_Code가 "11", CARD_BankCode가 "23"인 경우 – 제일은행에서 발급한 BC카드</td>
    </tr>
    <tr>
      <td class="center-align">CARD_SrcCode</td>
      <td class="center-align">간편(앱)결제 구분</td>
      <td class="center-align">String(1)</td>
      <td>C : PAYCO<br> B : 삼성페이<br>D : 삼성페이(체크)<br> G : SSGPAY<br>O : KAKAOPAY<br>L : LPAY<br>K : 국민앱카드<br>A : KPAY</td>
    </tr>
    <tr>
      <td class="center-align">CARD_Point</td>
      <td class="center-align">카드포인트 사용여부</td>
      <td class="center-align">String(1)</td>
      <td>"": 카드 포인트 사용안함<br> "1": 카드 포인트 사용</td>
    </tr>
    <tr>
      <td class="center-align">currency</td>
      <td class="center-align">통화코드</td>
      <td class="center-align">String(3)</td>
      <td>달러결제 정보, 통화코드</td>
    </tr>
    <tr>
      <td class="center-align">OrgPrice</td>
      <td class="center-align">달러 환전금액</td>
      <td class="center-align">String(20)</td>
      <td>해외카드 + 달러(USD) 결제 일 경우 환전금액<br>(국내카드로 달러 결제 시 환전금액으로 표기X)</td>
    </tr>
  </tbody>
</table>

</div>
</details>

#### [2-6] 승인결과 데이터(무통장)

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

  <table>
  <colgroup>
      <col style="text-align: center; width: 20%">
      <col style="text-align: center; width: 20%">
      <col style="text-align: center; width: 15%">
      <col style="text-align: center; width: 45%">
  </colgroup>
      <thead>
        <tr>
          <th class="center-align">필드</th>
          <th class="center-align">필드명</th>
          <th class="center-align">타입</th>
          <th class="left-align">비고</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td style="text-align: center">VACT_Num</td>
          <td style="text-align: center">입금계좌번호</td>
          <td style="text-align: center">String(20)</td>
          <td style="text-align: left">무통장입금 가상계좌번호</td>
        </tr>
        <tr>
          <td style="text-align: center">VACT_BankCode</td>
          <td style="text-align: center">입금은행코드</td>
          <td style="text-align: center">String(2)</td>
          <td style="text-align: left"><a href="/code02.html#27-은행증권사-코드"><strong>[참조-은행(증권사)코드]</strong></a></td>
        </tr>
        <tr>
          <td style="text-align: center">VACT_Name</td>
          <td style="text-align: center">예금주명</td>
          <td style="text-align: center">String(20)</td>
          <td style="text-align: left">예금주명</td>
        </tr>
        <tr>
          <td style="text-align: center">VACT_InputName</td>
          <td style="text-align: center">송금자명</td>
          <td style="text-align: center">String(20)</td>
          <td style="text-align: left">입금 시 고객명</td>
        </tr>
        <tr>
          <td style="text-align: center">VACT_Date</td>
          <td style="text-align: center">송금 일자</td>
          <td style="text-align: center">String(8)</td>
          <td style="text-align: left">송금 일자</td>
        </tr>
        <tr>
          <td style="text-align: center">VACT_Time</td>
          <td style="text-align: center">송금 시각</td>
          <td style="text-align: center">String(8)</td>
          <td style="text-align: left">송금 시각</td>
        </tr>
        <tr>
          <td style="text-align: center">vactBankName</td>
          <td style="text-align: center">입금은행명</td>
          <td style="text-align: center">String(20)</td>
          <td style="text-align: left">무통장 입금 은행명</td>
        </tr>
      </tbody>
    </table>

</div>
</details>

#### [2-7] 승인결과데이터(계좌이체)

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

 <table>
      <colgroup>
      <col style="text-align: center; width: 20%">
       <col style="text-align: center; width: 20%">
       <col style="text-align: center; width: 20%">
       <col style="text-align: center; width: 40%">
       </colgroup>
       <thead>
        <tr>
          <th class="center-align">필드</th>
          <th class="center-align">필드명</th>
          <th class="center-align">타입</th>
          <th class="center-align">비고</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td style="text-align: center">ACCT_BankCode</td>
          <td style="text-align: center">은행코드</td>
          <td style="text-align: center">String(2)</td>
          <td style="text-align: left">은행코드 <a href="/code02.html#27-은행증권사-코드"><strong>[참조-은행(증권사)코드]</strong></a></td>
        </tr>
        <tr>
          <td style="text-align: center">CSHR_ResultCode</td>
          <td style="text-align: center">현금영수증발행정상여부</td>
          <td style="text-align: center">String(10)</td>
          <td style="text-align: left">220000(정상처리)</td>
        </tr>
        <tr>
          <td style="text-align: center">CSHR_Type</td>
          <td style="text-align: center">현금영수증구분</td>
          <td style="text-align: center">String(1)</td>
          <td style="text-align: left">0 = 소득공제 / 1 = 지출증빙</td>
        </tr>
      </tbody>
    </table>

</div>
</details>

#### [2-8] 승인결과데이터(휴대폰결제)

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">
    <table>
        <colgroup>
       <col style="text-align: center; width: 20%">
       <col style="text-align: center; width: 20%">
       <col style="text-align: center; width: 20%">
       <col style="text-align: center; width: 40%">
       </colgroup>
      <thead>
        <tr>
          <th class="center-align">필드</th>
          <th class="center-align">필드명</th>
          <th class="center-align">타입</th>
          <th class="left-align">비고</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td class="center-align">HPP_Num</td>
          <td class="center-align">휴대폰번호</td>
          <td class="center-align">String(14)</td>
          <td class="left-align">휴대폰번호</td>
        </tr>
        <tr>
          <td class="center-align">payDevice</td>
          <td class="center-align">결제장치</td>
          <td class="center-align">String(6)</td>
          <td class="left-align">PC</td>
        </tr>
        <tr>
          <td class="center-align">HPP_BillKey</td>
          <td class="center-align">휴대폰 빌키</td>
          <td class="center-align">String(40)</td>
          <td class="left-align">휴대폰 빌링 사용시 빌키 발급</td>
        </tr>
      </tbody>
    </table>
</div>
</details>

- 가맹점 설정에 따라 승인결과 형식(return content type)을 다양하게 수신하실 수 있습니다.
- 승인결과 형식은 다음과 같습니다.

#### [2-13] 리턴 형식별 승인결과 예시

#### XML / ContentType=text/xml 


```xml

<?xml version="1.0" encoding="UTF-8"?>
<result>
  <applDate>20141211</applDate>
  <applNum>12858596</applNum>
  <applPrice>50000</applPrice>
  <applTime>135636</applTime>
  <buyerEmail>test@kggroup.co.kr</buyerEmail>
  <buyerName>홍길동</buyerName>
  <buyerTel>010-1111-1111</buyerTel>
  <cardBankCode>81</cardBankCode>
  <cardCode>17</cardCode>
  <cardNoInterest>0</cardNoInterest>
  <cardNum>532092000175</cardNum>
  <cardQuota>0</cardQuota>
  <clEvent/>
  <currency>WON</currency>
  <custEmail>test@kggroup.co.kr</custEmail>
  <expire/>
  <goodName>PRODUCT</goodName>
  <gwCode>A</gwCode>
  <memberNum/>
  <mid> xxxxx </mid>
  <oid> xxxxx_1418273735611</oid>
  <parentEmail/>
  <payDevice>PC</payDevice>
  <payMethod>Card</payMethod>
  <point>0</point>
  <price>50000</price>
  <prtcCode>0</prtcCode>
  <purchaseCode/>
  <resultCode>0000</resultCode>
  <resultMsg>정상처리되었습니다.</resultMsg>
  <terminalNum>0196282000</terminalNum>
  <tid>StdpayCARDINIWelTest20141211135635953969</tid>
</result>

```


#### JSON / ContentType=application/json 

```json
{
"applDate":"20130219",
"applTime": "165006",
"payMethod": "VBank",
  "price": "1004",
  "resultCode": "0000",
  "resultMsg": "정상처리되었습니다.",
  "tid": "StdpayVBNKINIWelTest20130219165005394245",
…
…
}

```

#### NVP /  ContentType=text/plain

```text
applDate=20130219&applTime=164631&buyerEmail=ehbang@welcomepg.co.kr&buyerName=홍길동&buyerTel=01020001234&currency=WON&custEmail=sample@welcomepg.co.kr&goodName=PRODUCT&mid=xxxxx&oid=xxxxx_1361259979159&parentEmail=&payDevice=Mobile&payMethod=VBank&price=1004&resultCode=0000&resultMsg=정상처리되었습니다.&tid=StdpayVBNKINIWelTest20130219164630729304&vactBankCode=11&vactBankName=농협중앙회&vactDate=20130228&vactInputName=홍길동&vactName=웰컴페이먼츠&vactNum=01443364911441&vactTime=235900
```

## 2.5 에스크로 결제
- 웹 표준 결제는 에스크로 결제 및 구매 확인만 지원 합니다. 
- 배송 등록, 결제 취소, 거절 확인는 PAYAPI 모듈로 진행 되므로 (배포본)PAYAPI 연동메뉴얼과 함께 참고하여 개발 진행 부탁드립니다.
- 가맹점에서 거래에 따라 일반 결제와 에스크로 결제의 구분 결제를 희망하시면 에스크로로 신규 또는 전환계약이 필요합니다. (단, 일부 호스팅 가맹점은 신 에스크로 설정에, 제한이 있을 수 있음)
- 에스크로 계약에 문의가 있거나 자세한 사항은 계약 담당자에게 문의하여 주시기 바랍니다.

### 2.5.1 에스크로 결제 요청 연동
- 표준결제 스크립트 Import 
- 실서버( 실 반영시 반드시 수정)
```javascript 
<script language="javascript" type="text/javascript" src="https://stdpay.paywelcome.co.kr/stdjs/ INIStdPay_escrow_conf.js" charset="UTF-8"></script>
```
- 테스트서버연동( 샘플로 제공 되는 테스트 MID만 사용가능하며 운영 MID 사용 불가 )
```javascript
<script language="javascript" type="text/javascript" src="https://tstdpay.paywelcome.co.kr/stdjs/ INIStdPay_escrow_conf.js" charset="UTF-8"></script>
```
- 3.1 참조하여 결제페이지 작성
- 신용카드, 실시간계좌이체, 무통장입금(가상계좌)

<br>
<img class="emoji" title=":warning:" alt=":warning:" src="https://github.githubassets.com/images/icons/emoji/unicode/26a0.png">
`에스크로 서비스를 이용하시려면 결제요청페이지안에 accepmethod 의 value 를 useescrow 로 추가하셔야 합니다.<br>값을 추가하지 않을 경우 일반결제로 진행됩니다.`<br>
```javascript
<input type="hidden" name="acceptmethod" value="SKIN(ORIGINAL):HPP(1): useescrow ">
```

### 2.5.2 에스크로 구매확인 연동

- 에스크로 구매확인은 고객이 결제를 완료하고, 배송등록(가맹점관리자나 PAYAPI를 통해 등록 필요)이 이뤄진 상태에서 설정 가능하며, 구매자가 구매확정 또는 구매거절을 선택합니다.
- 매매보호서비스에서 소비자의 구매확정은 반드시 필요한 기능 입니다.

#### [3-1] 구매확인 요청 파라미터

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table>
  <thead>
    <tr>
      <th style="text-align: center; width: 20%">필드</th>
      <th style="text-align: center; width: 15%">필드명</th>
      <th style="text-align: center; width: 15%">타입</th>
      <th style="text-align: center; width: 10%">필수</th>
      <th style="width: 40%">비고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">version</td>
      <td class="center-align">버전</td>
      <td class="center-align">String(20)</td>
      <td class="center-align">○</td>
      <td>전문 버전<br><code class="language-plaintext highlighter-rouge">"1.0"</code></td>
    </tr>
    <tr>
      <td class="center-align">mid</td>
      <td class="center-align">상점아이디</td>
      <td class="center-align">String(10,Fixed)</td>
      <td class="center-align">○<br>위변조<br>검증</td>
      <td>제공된 mid, 10자리 고정<br><code class="language-plaintext highlighter-rouge">"xxxxx"</code></td>
    </tr>
    <tr>
      <td class="center-align">tid</td>
      <td class="center-align">거래번호</td>
      <td class="center-align">String(40)</td>
      <td class="center-align">○</td>
      <td>승인 성공시 응답 받은 거래번호<br><code class="language-plaintext highlighter-rouge">"xxx_1335233672723"</code></td>
    </tr>
    <tr>
      <td class="center-align">currency</td>
      <td class="center-align">통화</td>
      <td class="center-align">String(3)</td>
      <td class="center-align">○</td>
      <td>USD는 카드 결제만 가능(ISP는 결제안됨)<br><code class="language-plaintext highlighter-rouge">“WON”</code>[WON:한화,USD:달러]</td>
    </tr>
    <tr>
      <td class="center-align">timestamp</td>
      <td class="center-align">시간변환</td>
      <td class="center-align">Number(20)</td>
      <td class="center-align">○<br>위변조<br>검증</td>
      <td>TimeInMillis(Long형)<br>제공라이브러로생성가능(샘플소스참조)<br><code class="language-plaintext highlighter-rouge">"1335233672723"</code></td>
    </tr>
    <tr>
      <td class="center-align">mkey</td>
      <td class="center-align">암호화키</td>
      <td class="center-align">String(N/A)</td>
      <td class="center-align">○</td>
      <td>signkey에 대한 검증값<br><code class="language-plaintext highlighter-rouge">"3a9503069192f207491d4b19bd743fc249a761ed94246c8c42fed06c3cd15a33"</code></td>
    </tr>
    <tr>
      <td class="center-align">charset</td>
      <td class="center-align">인코딩</td>
      <td class="center-align">String(N/A)</td>
      <td class="center-align">X</td>
      <td>결과 수신 charset<br><code class="language-plaintext highlighter-rouge">"UTF-8"/ [UTF-8, EUC-KR]</code></td>
    </tr>
    <tr>
      <td class="center-align">payViewType</td>
      <td class="center-align">결체창표시방법</td>
      <td class="center-align">String(N/A)</td>
      <td class="center-align">X</td>
      <td>결제 호출 방식을 결정</td>
    </tr>
    <tr>
      <td class="center-align">returnUrl</td>
      <td class="center-align">응답URL</td>
      <td class="center-align">String(N/A)</td>
      <td class="center-align">○</td>
      <td>구매확인 또는 거절 후 결과 전문을 받기 위한 URL</td>
    </tr>
    <tr>
      <td class="center-align">closeUrl</td>
      <td class="center-align">결제창닫기URL</td>
      <td class="center-align">String(N/A)</td>
      <td class="center-align">X</td>
      <td>결제 창을 닫기위한 URL</td>
    </tr>
    <tr>
      <td class="center-align">popupUrl</td>
      <td class="center-align">팝업처리URL</td>
      <td class="center-align">String(N/A)</td>
      <td class="center-align">X</td>
      <td>결체창 팝업 진행시 사용 하는 URL<br>(비권장)</td>
    </tr>
  </tbody>
</table>

</div>
</details>

#### [3-2] 구매확인요청파라미터

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table>
  <thead>
    <tr>
      <th class="center-align" style="width: 40%">필드</th>
      <th class="center-align" style="width: 60%">필드명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">ResultCode</td>
      <td style="text-align: left">처리결과코드</td>
    </tr>
    <tr>
      <td class="center-align">ResultMsg</td>
      <td style="text-align: left">처리결과내용, 상세코드표시</td>
    </tr>
    <tr>
      <td class="center-align">CNF_Date</td>
      <td style="text-align: left">구매확정일경우, 처리일자 형식은YYYYMMDD</td>
    </tr>
    <tr>
      <td class="center-align">CNF_Time</td>
      <td style="text-align: left">구매확정일경우, 처리시각 형식은hhmmss</td>
    </tr>
    <tr>
      <td class="center-align">DNY_Date</td>
      <td style="text-align: left">구매거절일경우, 처리일자 형식은YYYYMMDD</td>
    </tr>
    <tr>
      <td class="center-align">DNY_Time</td>
      <td style="text-align: left">구매거절일경우, 처리시각 형식은hhmmss</td>
    </tr>
  </tbody>
</table>

</div>
</details>

### 2.5.3 에스크로 상태변경 노티 수신

- 에스크로 주요 시점 (예 >구매자가 구매결정을 완료 등)에 가맹점 측으로 해당 내역을 통보해주는 기능입니다. 상점 측에서는 정상수신 여부를 응답(NOTI CONFIRM)하여야합니다.
- 해당 기능을 이용하려면 계약 담당자를 통해,수신 받을 상점 측 URL을 등록하셔야 합니다.
- 지불 수단 별,승인요청 시점의 주문번호를 기준으로 응답하며,배송등록 시점에 사용되는 주문번호와 동일하게 설정을 권장합니다.
- 거래금액은 에스크로 상태에 따라 거래취소 시에는 취소금액,그 외는 승인금액입니다.
- 원거래TID는 부분취소거래만 설정됩니다.

##### [노티발송 웰컴페이먼츠 > 가맹점]

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table>
      <colgroup>
       <col style="text-align: center; width: 20%">
       <col style="text-align: center; width: 20%">
       <col style="text-align: center; width: 20%">
       <col style="text-align: center; width: 40%">
       </colgroup>
      <thead>
        <tr>
          <th class="center-align">필드</th>
          <th class="center-align">필드명</th>
          <th class="center-align">크기</th>
          <th class="left-align">비고</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td class="center-align">id_merchant</td>
          <td class="center-align">상점아이디</td>
          <td class="center-align">String(10)</td>
          <td class="left-align">P_MID로전달한값</td>
        </tr>
        <tr>
          <td class="center-align">no_oid</td>
          <td class="center-align">주문번호</td>
          <td class="center-align">String(40)</td>
          <td class="left-align">가맹점주문번호</td>
        </tr>
        <tr>
          <td class="center-align">no_tid</td>
          <td class="center-align">거래번호</td>
          <td class="center-align">String(40)</td>
          <td class="left-align">승인시전달된TID</td>
        </tr>
        <tr>
          <td class="center-align">cl_status</td>
          <td class="center-align">에스크로상태</td>
          <td class="center-align">String(2)</td>
          <td class="left-align">배송등록(2), 구매확인(3), 자동구매확인(31), 강제구매확인(32), 구매거절(4), 거래취소(8), 거절확인(10)</td>
        </tr>
        <tr>
          <td class="center-align">dt_req</td>
          <td class="center-align">요청일자</td>
          <td class="center-align">String(14)</td>
          <td class="left-align">YYYYMMDDhhmmss</td>
        </tr>
        <tr>
          <td class="center-align">cl_paymethod</td>
          <td class="center-align">결제수단</td>
          <td class="center-align">String(2)</td>
          <td class="left-align">신용카드(0), ISP(1), 계좌이체(16), 가상계좌(17)</td>
        </tr>
        <tr>
          <td class="center-align">msg_deny</td>
          <td class="center-align">구매거절사유</td>
          <td class="center-align">String(256)</td>
          <td class="left-align"> </td>
        </tr>
        <tr>
          <td class="center-align">price</td>
          <td class="center-align">거래금액</td>
          <td class="center-align">String(12)</td>
          <td class="left-align"> </td>
        </tr>
        <tr>
          <td class="center-align">tid_org</td>
          <td class="center-align">원거래거래번호</td>
          <td class="center-align">String(40)</td>
          <td class="left-align">부분취소시원거래거래번호</td>
        </tr>
      </tbody>
</table>

</div>
</details>

##### [노티응답 가맹점  &gt; 웰컴페이먼츠 ]

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

|   필드    | 필드명  |     크기     | 비고                   |
| :------: | :---: | :--------: | -------------------- |
| cd_rslt  | 결과코드  |  String(4)   | 0000:정상처리, 9999:처리실패 |
| msg_rslt | 결과메세지 | String(1000) | 처리실패시 상세 오류 메세지      |

</div>
</details>

## 2.6 가상계좌 입금통보 (노티 수신) 사용 방법 
> 상점 입금통보 수신 페이지는 고객이 가상계좌이체 서비스를 사용하여 가상계좌를 발급받은 후 무통장 입금을 하였을 때,<br> 은행으로부터 통보된 입금결과를 상점으로 전송해 주기 위해 상점 측에 필요한 페이지입니다.<br>고객이 보는 결제 화면과는 무관하며, HTTP/HTTPS 모두 지원합니다.

### 2.6.1 노티를 받을 때 전달되는 파라미터

#### [3-1] 이체결과 파라미터

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

 <table>
      <thead>
        <tr>
          <th style="text-align: center">필드</th>
          <th style="text-align: center">필드명</th>
          <th style="text-align: center">크기</th>
          <th style="text-align: center">비고</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td style="text-align: center">no_tid</td>
          <td style="text-align: center">거래번호</td>
          <td style="text-align: center">String(40)</td>
          <td class="left-align"></td>
        </tr>
        <tr>
          <td style="text-align: center">no_oid</td>
          <td style="text-align: center">상점 주문번호</td>
          <td style="text-align: center">String(40)</td>
        </tr>
        <tr>
          <td style="text-align: center">cd_bank</td>
          <td style="text-align: center">계좌를 발급한 은행 코드</td>
          <td style="text-align: center">String(8)</td>
          <td class="left-align"></td>
        </tr>
        <tr>
          <td style="text-align: center">cd_deal</td>
          <td style="text-align: center">거래 취급 기관 코드</td>
          <td style="text-align: center">String(8)</td>
          <td class="left-align">실제 입금 은행</td>
        </tr>
        <tr>
          <td style="text-align: center">dt_trans</td>
          <td style="text-align: center">금융기관발생 거래일자</td>
          <td style="text-align: center">String(8)</td>
          <td class="left-align"></td>
        </tr>
        <tr>
          <td style="text-align: center">tm_trans</td>
          <td style="text-align: center">금융기관발생 거래 시각</td>
          <td style="text-align: center">String(6)</td>
          <td class="left-align"></td>
        </tr>
        <tr>
          <td style="text-align: center">no_vacct</td>
          <td style="text-align: center">계좌번호</td>
          <td style="text-align: center">String(20)</td>
          <td class="left-align"></td>
        </tr>
        <tr>
          <td style="text-align: center">amt_input</td>
          <td style="text-align: center">입금금액</td>
          <td style="text-align: center">NUMBER(13)</td>
          <td class="left-align"></td>
        </tr>
        <tr>
          <td style="text-align: center">flg_close</td>
          <td style="text-align: center">마감구분</td>
          <td style="text-align: center">String(1)</td>
          <td class="left-align">0:당일마감전, 1:당일마감후</td>
        </tr>
        <tr>
          <td style="text-align: center">cl_close</td>
          <td style="text-align: center">마감구분코드</td>
          <td style="text-align: center">String(1)</td>
          <td class="left-align">0:당일마감전, 1:당일마감후</td>
        </tr>
        <tr>
          <td style="text-align: center">type_msg</td>
          <td style="text-align: center">거래구분</td>
          <td style="text-align: center">String(4)</td>
          <td class="left-align">0200:정상, 0400:취소</td>
        </tr>
        <tr>
          <td style="text-align: center">nm_inputbank</td>
          <td style="text-align: center">입금은행명</td>
          <td style="text-align: center">String(10)</td>
          <td class="left-align"></td>
        </tr>
        <tr>
          <td style="text-align: center">nm_input</td>
          <td style="text-align: center">입금자명</td>
          <td style="text-align: center">String(20)</td>
          <td class="left-align"></td>
        </tr>
        <tr>
          <td style="text-align: center">dt_inputstd</td>
          <td style="text-align: center">입금기준일자</td>
          <td style="text-align: center">NUMBER(8)</td>
          <td class="left-align"></td>
        </tr>
        <tr>
          <td style="text-align: center">dt_calculstd</td>
          <td style="text-align: center">정산기준일자</td>
          <td style="text-align: center">NUMBER(8)</td>
          <td class="left-align"></td>
        </tr>
        <tr>
          <td style="text-align: center">dt_transbase</td>
          <td style="text-align: center">거래기준일자</td>
          <td style="text-align: center">NUMBER(8)</td>
          <td class="left-align"></td>
        </tr>
        <tr>
          <td style="text-align: center">cl_trans</td>
          <td style="text-align: center">거래구분코드</td>
          <td style="text-align: center">String(4)</td>
          <td class="left-align">EX ) 1100</td>
        </tr>
        <tr>
          <td style="text-align: center">cl_kor</td>
          <td style="text-align: center">한글구분코드</td>
          <td style="text-align: center">NUMBER(1)</td>
          <td class="left-align"></td>
        </tr>
        <tr>
          <td style="text-align: center">dt_cshr</td>
          <td style="text-align: center">현금영수증 발급일자</td>
          <td style="text-align: center">NUMBER(8)</td>
          <td class="left-align"></td>
        </tr>
        <tr>
          <td style="text-align: center">tm_cshr</td>
          <td style="text-align: center">현금영수증 발급시간</td>
          <td style="text-align: center">NUMBER(6)</td>
          <td class="left-align"></td>
        </tr>
        <tr>
          <td style="text-align: center">no_cshr_appl</td>
          <td style="text-align: center">현금영수증 발급번호</td>
          <td style="text-align: center">NUMBER(9)</td>
          <td class="left-align"></td>
        </tr>
        <tr>
          <td style="text-align: center">no_cshr_tid</td>
          <td style="text-align: center">현금영수증 발급TID</td>
          <td style="text-align: center">String(40)</td>
          <td class="left-align"></td>
        </tr>
      </tbody>
    </table>


</div>
</details>

### 2.6.2 주의사항 

- 리턴메세지를 반드시 적용해주셔야 합니다.
- 상점 데이터베이스 등록 성공 유무에 따라서, 성공시에는 "OK" 문자열만 응답되어야 합니다.
  `ASP : response.write "OK";`
  `JSP : out.print("OK");`
  `PHP : echo "OK";`
- 로그를 반드시 작성해주시기 바랍니다.
  로그는 문제 발생시 웰컴페이먼츠와 데이터를 확인할 수 있는 근거 데이터이므로
  반드시 적용해주시기 바랍니다.

### 2.6.3 입금정보 수신 실패 사유 확인

- 채번된 가상계좌로 정상 입금되었는지 확인
  `상점관리자 > 거래내역 > 가상계좌 > 입금결과 조회`
- 입금결과조회내역에서정상조회되며, 입금TID가생성된경우
  가상계좌 > 입금통보 재전송 메뉴에서 가상계좌 번호 조회

1. 상점으로부터 성공 응답받기 실패
  가맹점 노티수신페이지에서 입금통보 노티 수신 후 “OK”를 응답해야하나,
  OK가 아닌 다른 응답을 한 경우 입니다.

가맹점 노티수신페이지에서 OK응답을 하지 않거니 HTTP 500 에러 또는 404 에러 등으로
인해 정상 응답하지 못한 경우 등 10회까지 노티가 재전송 됩니다. (`OK 응답을 하지 않아도 가상계좌 거래건이 취소되지는 않습니다.`)
노티수신페이지에서 정상응답하지 못한 사유는 가맹점 내부적으로 확인이 필요합니다.


##### 가맹점 노티 수신페이지 세팅
- PC 가상계좌상점관리자 > 거래내역 > 가상계좌 > 입금통보방식선택 > "URL 수신사용"설정 및 URL 세팅
- 모바일가상계좌 > 모바일 결제요청 데이터 내 P_NOTI_URL 세팅

2. 통보전문구문오류
- 통보전문 방식이 선택되지 않은 경우 발생됩니다.
  상점관리자 > 상점정보 > 계약정보 > 결제수단정보 > 가상계좌 내 통보전문  “URL 수신사용(일반)” 으로 설정

3. 상점서버정보 없음 (IP,PORT,전문구분)
  통보전문 방식을 “수신모듈사용” 으로 설정 후 입금내역통보 IP/PORT 가 세팅되지 않은 경우 발생됩니다.
  통보전문 방식을 “URL 수신사용” 으로 설정하시고 입금통보 URL을 세팅바랍니다.

상점관리자 > 상점정보 > 계약정보 > 결제수단정보 > 가상계좌 내 통보전문  “URL 수신사용(일반)” 으로 설정 및 가맹점 노티수신 URL 세팅

### 2.6.4 가상계좌 입금통보 테스트

- 테스트 서버에서 진행한 가상계좌 입금통보 확인을 웰컴페이먼츠 홈페이지에서 조회 가능<br>
  `웰컴페이먼츠(https://www.welcomepayments.co.kr) > 고객센터 > 입금통보테스트`
  테스트 결제창에서 가상계좌 결제방식으로 결제 진행 후 해당내역 확인 가능

1. 결제창 연동 후 mid는 xxx로 가상계좌 번호를 채번
2. 채번이 완료되면 웰컴페이먼츠 홈페이지의 입금통보테스트 화면에서 채번 플랫폼 선택 후 은행코드, 계좌번호, 금액, 가상계좌 입금정보를 받을 URL을 입력합니다.
3. 채번 정보를 입력 후 입금통보 버튼을 누를시 결과 메시지가 생성됩니다.
  이때의 결과 메시지는 입금통보 테스트가 성공했는지를 보여주는 것이며 실제 거래와는 무관합니다.
4. 서버에 로그가 정상적으로 생성되었는지 확인합니다.
5. DB에 정상적으로 데이터가 들어왔는지 확인합니다.

##### 결과 메시지 예시
```json
{
    "tid":"INIpayVBNKtest00101020050201152330736424",
    "noOid":"mall_use_orer_id",
    "buyerNm":"홍길동","goodsNm":"축구공"
 }
```
성공 메시지가 나오면 상점으로 socket 송신을 완료한 상태입니다.
상점 내 수신 로그 및 DB상태를 확인하세요.


## 2.7 웹표준 결제 취소

웹표준 결제는 거래 취소 기능을 지원하지 않습니다.
따라서, 결제 취소는 별도의 PAYAPI 서비스 연동하시어 취소기능을 활용하셔야 합니다.  
자세한 문의사항은 당사 기술지원팀으로 문의 바랍니다.<br>
<a href="mailto:mainpg_support@welcomepayments.co.kr">기술지원 문의(support@welcomepayments.co.kr)</a>


<div style="display: inline-block; width: 100%; margin-top: 50px;">
  <a style="float:left;" href="/stdweb01.html">◀이전페이지</a>
  <a style="float:right;" href="/stdweb03.html">다음페이지▶</a>
</div>
