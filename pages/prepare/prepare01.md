---
title: 연동 준비
permalink: prepare01.html
sidebar: prepare_sidebar
folder: prepare
toc: false
---

## 1. 상점 연동시 주의사항

해킹시도 및 불법접속 차단 등의 보안을 위해 해외에서 접속 시에는 당사 서비스가 제한이 되며, 해외IP 차단해제를 위해서는 [ip-block@welcomepayments.co.kr](mailto:ip-block@welcomepayments.co.kr)로 아래 내용 작성해서 요청 주시기 바랍니다 .

| 업체명(MID)    | 접속 국가 | 접속 공인IP(대역) | 요청사항                 |
|:-------------:| :---------: | :-----------------: | :------------------------: |
| 계약가맹점 별도 전달 | 중국      | 111.111.111.111   | 해외아이피 차단해제 요청 |

## 2. 설치

### 2.1. 설치 가능한 운영체제
>Java, php, asp.net등 HTTPS 통신이 가능한 웹서버 환경의 모든 운영체제에서 사용이 가능합니다. <br>
다만, 개인용 PC에서는 운영을 권장하지 않습니다.

### 2.2. 소프트웨어 요구사항
> `Web Server 웹서버 (또는 웹 컨테이너)`<br>
SHA256 Hash값의 생성 httpClient(http Background) 통신이 가능한 웹서버<br><br>
>
>`DBMS`<br>
거래내역 및 처리결과를 데이터베이스에 저장하길 원하신다면, 데이터베이스 소프트웨어가 별도로 필요합니다.<br>
Web Standard서비스는 데이터베이스 연동 작업을 위한 기능이 포함되어 있지 않습니다.<br>(데이터베이스 연동을 위한 지불 결과 데이터만 제공)

### 2.3. 하드웨어 요구사항
>일반적인 서버 운영체제의 운용환경에 준하며, 특별한 하드웨어 요구사항은 없습니다.


### 2.4. 방화벽 설정
>이용 가맹점 서버 앞에 방화벽이 있는 경우 통신이 가능하도록 방화벽 설정을 해야 합니다.<br>

#### 테스트

<table>
<thead>
<tr>
<th class="center-align" style="width: 40%">연결대상</th>
<th class="center-align" style="width: 15%">프로토콜</th>
<th class="center-align" style="width: 15%">포트번호</th>
<th class="center-align" style="width: 30%">연결방향</th>
</tr>
</thead>
    <tr>
      <td class="center-align">https://tstdpay.paywelcome.co.kr</td>
      <td class="center-align" rowspan="3">HTTPS</td>
      <td class="center-align" rowspan="3">443</td>
      <td class="center-align" rowspan="3">INBOUNT, OUTBOUND</td>
    </tr>
    <tr>
      <td class="center-align">https://tmobile.paywelcome.co.kr</td>
    </tr>
    <tr>
      <td class="center-align">https://tpayapi.paywelcome.co.kr</td>
    </tr>
</table>

#### 운영

<table>
<thead>
<tr>
<th class="center-align" style="width: 40%">연결대상</th>
<th class="center-align" style="width: 15%">프로토콜</th>
<th class="center-align" style="width: 15%">포트번호</th>
<th class="center-align" style="width: 30%">연결방향</th>
</tr>
</thead>
    <tr>
      <td class="center-align">https://stdpay.paywelcome.co.kr</td>
      <td class="center-align" rowspan="3">HTTPS</td>
      <td class="center-align" rowspan="3">443</td>
      <td class="center-align" rowspan="3">INBOUNT, OUTBOUND</td>
    </tr>
    <tr>
      <td class="center-align">https://mobile.paywelcome.co.kr</td>
    </tr>
    <tr>
      <td class="center-align">https://payapi.paywelcome.co.kr</td>
    </tr>
</table>

## 3. signature 생성

## 3.1 signature 개요

{% include image.html file="pre_img01.png" %}

- 결제요청시 등 HTTPS post 요청시 가맹점의 요청이 정상적인 요청인지 여부 / 사용자의 위변조 방지를 위해 일부 데이터를 SHA256으로 Hash한 값

- signature는 form.submit 시 적용됩니다.signature생성은 Sample Source를 참고하여 작성하시기 바랍니다.

## 3.2 signature 첨부 대상
서비스 별로 Signature생성 방식이 상이하므로 아래의 표를 참고해주시기 바랍니다.<br/>

Signature생성에 필요한 mid와 signkey는 계약 가맹점에 한해 별도로 전달됩니다.

**※ Signature 필드 생성 순서 중요**

### 웹표준(PC) 서비스의 Signature 생성

#### 인증 요청 시 Signature 생성

>인증 요청시 signature필드의 구성은 다음과 같습니다.<br>
생성 순서 : <code class="language-plaintext highlighter-rouge">mkey=&oid=&price=&timestamp=</code><br/>
<img class="emoji" title=":warning:" alt=":warning:" src="https://github.githubassets.com/images/icons/emoji/unicode/26a0.png"><code class="language-plaintext highlighter-rouge">필드 순서유지(알파벳순)</code>

<table>
  <thead>
    <tr>
      <th class="center-align" style="width: 10%">순번</th>
      <th class="center-align" style="width: 15%">필드</th>
      <th class="center-align" style="width: 10%">필드명</th>
      <th class="center-align" style="width: 55%">비고</th>
      <th class="center-align" style="width: 10%">필수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">1</td>
      <td class="center-align">mKey</td>
      <td class="center-align">검증값</td>
      <td>SHA256방식으로 생성한 값 → 제공라이브러리로 생성가능
      <br><code class="language-plaintext highlighter-rouge">"346eaecb81e3a1629805b9d55fe0431dc25a06aaa2d48366b404939a3d4330a3"
      </code>
      </td>
      <td class="center-align">Yes</td>
    </tr>
    <tr>
      <td class="center-align">2</td>
      <td class="center-align">oid</td>
      <td class="center-align">주문번호</td>
      <td>xxx_1335247243103</td>
      <td class="center-align">Yes</td>
    </tr>
    <tr>
      <td class="center-align">3</td>
      <td class="center-align">price</td>
      <td class="center-align">가격</td>
      <td>가맹점 주문번호 / 결제단위 Unique <br>
      <code class="language-plaintext highlighter-rouge">"10000"</code>
      </td>
      <td style="text-align: center">Yes</td>
    </tr>
    <tr>
      <td class="center-align">4</td>
      <td class="center-align">timestamp</td>
      <td class="center-align">타임스탬프</td>
      <td>TimeInMillis(Long형) → 제공라이브러리로 생성가능(샘플소스참조)<br><code class="language-plaintext highlighter-rouge">1335233672723</code></td>
      <td class="center-align">Yes</td>
    </tr>
  </tbody>
</table>

##### Target 데이터 예시 : `mKey=346eaecb81e3a1629805b9d55f...&oid=xxx_1335247243103&price=1000&timestamp=2020110222`

<br/>

#### 승인 요청 시 Signature 생성
>승인 요청 시 signature필드의 구성은 다음과 같습니다.<br>
생성 순서 : <code class="language-plaintext highlighter-rouge">authToken=&timestamp=</code><br/>
<img class="emoji" title=":warning:" alt=":warning:" src="https://github.githubassets.com/images/icons/emoji/unicode/26a0.png"><code class="language-plaintext highlighter-rouge">필드 순서유지(알파벳순)</code>

<table>
  <thead>
    <tr>
      <th class="center-align" style="width: 10%">순번</th>
      <th class="center-align" style="width: 15%">필드</th>
      <th class="center-align" style="width: 15%">필드명</th>
      <th class="center-align" style="width: 50%">비고</th>
      <th class="center-align" style="width: 10%">필수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">1</td>
      <td class="center-align">authToken</td>
      <td class="center-align">인증 결과 수신 후<br>생성된 토큰 값</td>
      <td>인증결과 수신한 authToken<br>sgnWSY9uZ3c9lbkJItgiP4VdD5L+dM0+dmuv+R707vExQC5XjwjSCUOa/QumiTMW Y8+aLvjFu …….</td>
      <td class="center-align">Yes</td>
    </tr>
    <tr>
      <td class="center-align">2</td>
      <td class="center-align">timestamp</td>
      <td class="center-align">타임스탬프</td>
      <td>TimeInMillis(Long)밀리세컨드 타임스템프를 Long형으로 변환한 숫자<br>제공라이브러리로 생성가능<br>1335247243103</td>
      <td class="center-align">Yes</td>
    </tr>
  </tbody>
</table>

##### Target 데이터 예시 : `authToken=sgnWSY9uZ3c9lbkJItgiP4VdD5L+dM0+dmuv+R707vExQC5XjwjSCUOa/iT……&timestamp=2020110222`

#### Signature 생성방법은 아래의 [3.3 signature 생성] 참조
>Web Standard 서비스의 모든 요청<br/>
>결제(인증), 승인APIsignature 생성 대상 필드(Target) 모든 요청의 signature의 생성방법 동일하며, 요청별로 생성 대상 필드가 다름<br/>
>요청별로 명시된 signature 생성 대상(Target)필드 를 참조<br/>
>인증요청(결제요청) : oid,price,timestamp<br/>
>승인요청 : authToken, timestamp<br/>

[//]: # (          <a href="/stdweb03.html#table-1-3-signature-생성-대상target-필드">[TABLE 1-3] signature 생성 대상&#40;Target&#41; 필드 참조]</a><br/>)
[//]: # (          <a href="/stdweb03.html#table-2-3-승인요청-signature-생성-대상target-필드">[TABLE 2-3] 승인요청 signature 생성 대상&#40;Target&#41; 필드 참조]</a></td>)

### MOBILE 서비스의 Signature 생성

생성 순서 : <code class="language-plaintext highlighter-rouge">mkey=&P_AMT=&P_OID=&P_TIMESTAMP=</code><br/>
필드 순서유지(명시된순으로)

<table style="width: 100%;">
<colgroup>
  <col style="width: 10%;">
  <col style="width: 20%;">
  <col style="width: 30%;">
  <col style="width: 30%;">
  <col style="width: 10%;">
</colgroup>
  <thead>
    <tr>
      <th class="center-align">순번</th>
      <th class="center-align">필드</th>
      <th class="center-align">필드명</th>
      <th class="center-align">비고</th>
      <th class="center-align">필수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">1</td>
      <td class="center-align">mkey</td>
      <td class="center-align"></td>
      <td>sha256(signkey)<br/>(signkey값은 계약가맹점에 한해 별도 전달 예정)</td>
      <td class="center-align">필수</td>
    </tr>
    <tr>
      <td class="center-align">2</td>
      <td class="center-align">P_AMT</td>
      <td class="center-align">금액</td>
      <td>가맹점 주문번호/결제단위 Unique</td>
      <td class="center-align">필수</td>
    </tr>
    <tr>
      <td class="center-align">3</td>
      <td class="center-align">P_OID</td>
      <td class="center-align">주문번호</td>
      <td>주문단위 unique한 값</td>
      <td class="center-align">필수</td>
    </tr>
    <tr>
      <td class="center-align">4</td>
      <td class="center-align">P_TIMESTAMP</td>
      <td class="center-align">타임스탬프</td>
      <td>TimeInMillis(Long형)</td>
      <td class="center-align">필수</td>
    </tr>
  </tbody>
</table>

##### Target 데이터 예시 : `mkey=346eaecb81e3a1629805b9d55f...&P_AMT=1000&P_OID=xxx_1335247243103&P_TIMESTAMP=2020110222`

### PAYAPI 서비스의 Signature 생성

필드 순서유지(API별로 명시된 순으로)

<table style="width: 100%;">
<colgroup>
  <col style="width: 10%;">
  <col style="width: 35%;">
  <col style="width: 55%;">
</colgroup>
  <thead>
    <tr>
      <th class="center-align">순번</th>
      <th class="center-align">API명</th>
      <th>Signature 생성 필드</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">1</td>
      <td class="center-align">결제 전체 취소 API</td>
      <td>mid+mkey+timestamp</td>
    </tr>
    <tr>
      <td class="center-align">2</td>
      <td class="center-align">결제 부분 취소 API</td>
      <td>mid+mkey+timestamp</td>
    </tr>
    <tr>
      <td class="center-align">3</td>
      <td class="center-align">신용카드 빌키 발급 API</td>
      <td>mid+mkey+cardNumber+timestamp</td>
    </tr>
    <tr>
      <td class="center-align">4</td>
      <td class="center-align">신용카드 비인증 빌키 발급 API</td>
      <td>mid+mkey+cardNumber+timestamp</td>
    </tr>
    <tr>
      <td class="center-align">5</td>
      <td class="center-align">신용카드 빌링 승인 API</td>
      <td>mid+mkey+oid+price+timestamp</td>
    </tr>
    <tr>
      <td class="center-align">6</td>
      <td class="center-align">신용카드 빌키 삭제 API</td>
      <td>mid+mkey+timestamp</td>
    </tr>
    <tr>
      <td class="center-align">7</td>
      <td class="center-align">휴대폰 빌키 승인 API</td>
      <td>mid+mkey+oid+price+timestamp</td>
    </tr>
    <tr>
      <td class="center-align">8</td>
      <td class="center-align">신용카드 키인결제 API</td>
      <td>mid+mkey+oid+price+timestamp</td>
    </tr>
    <tr>
      <td class="center-align">9</td>
      <td class="center-align">신용카드 PREFIX 조회 API</td>
      <td>mid+mkey+cardNumber+timestamp</td>
    </tr>
    <tr>
      <td class="center-align">10</td>
      <td class="center-align">에스크로 배송등록 API</td>
      <td>mid+mkey+timestamp</td>
    </tr>
    <tr>
      <td class="center-align">11</td>
      <td class="center-align">에스크로 구매확정 API</td>
      <td>mid+mkey+timestamp</td>
    </tr>
    <tr>
      <td class="center-align">12</td>
      <td class="center-align">에스크로 구매거절 API</td>
      <td>mid+mkey+timestamp</td>
    </tr>
    <tr>
      <td class="center-align">13</td>
      <td class="center-align">에스크로 구매거절 확인 API</td>
      <td>mid+mkey+timestamp</td>
    </tr>
    <tr>
      <td class="center-align">14</td>
      <td class="center-align">에스크로 상태조회 API</td>
      <td>mid+mkey+timestamp</td>
    </tr>
    <tr>
      <td class="center-align">15</td>
      <td class="center-align">SMS결제용 단축 URL생성 API</td>
      <td>mid+mkey+P_OID+P_AMT+timestamp</td>
    </tr>
  </tbody>
</table>
<strong>※자세한 필드는 각 API명세서를 참고 바랍니다.</strong>

## 3.3 signature 생성 방법
- 위변조 방지를 위한 보안조치로서 필수 체크 데이터를 NVP 방식으로 연결한 데이터를SHA256으로 Hash한 값
- NVP : nameandvalue parameters
  ex) name=value&amp;name=value&amp;name=value&amp;name=value
- 필드 순서유지(알파벳순), 마지막 &amp;는 생략, 공백생략, 모든대상 필드는 Form에 설정되는 데이터와 동일한 값을 이용

## 3.4 signature 생성 샘플(결제요청)
- 언어별 제공된 라이브러리 소스를 통해서 생성가능합니다.

#### signature 생성 예
- Target 데이터(signParam)

  |   mKey=12345&amp;oid=INIWelTest_1361252896871&amp;price=1004&amp;&amp;timestamp=1361252896871  |
    
- Hash 데이터 (위 Target데이터를 SHA256 Hash한 값)

  | 2883da372a7ccf6cdad99b4b9d52ef67cb4cc52d77192e36d8cce8258bcdecdf |

#### 잘못된 Target 데이터 생성 예

#### 띄어쓰기 및 & 중복의 경우
##### 원본 

|mKey=xxxxxxxxxx&amp;oid=1231231&amp;price=10000 **&amp; &amp;** timestamp=1335247243103   |

##### 수정   

| mKey=xxxxxxxxxx&amp;oid=1231231&amp;price=10000&amp;timestamp=1335247243103 |

#### 마지막에 & 가 붙는 경우
##### 원본 

| mKey=xxxxxxxxxx&amp;oid=1231231&amp;price=10000&amp;timestamp=1335247243103 **&amp;** |

##### 수정 

| mKey=xxxxxxxxxx&amp;oid=1231231&amp;price=10000&amp;timestamp=1335247243103 |

#### 샘플소스

<ul class="nav nav-tabs">
    <li class="active"><a href="#sigSample1" data-toggle="tab">java</a></li>
    <li><a href="#sigSample2" data-toggle="tab">node.js</a></li>
    <li><a href="#sigSample3" data-toggle="tab">PHP</a></li>
    <li><a href="#sigSample4" data-toggle="tab">ASP</a></li>
</ul>
<div class="tab-content">
  <div role="tabpanel" class="tab-pane active" id="sigSample1">
  
  <script src="https://gist.github.com/paywelcome/f5385130876ede2d6664082f5c09b63e.js"></script>
  
  </div>
  <div role="tabpanel" class="tab-pane" id="sigSample2">
  
  <script src="https://gist.github.com/paywelcome/281af4c8a0aa6354404613bf6f721f94.js"></script>
  
  </div>
  <div role="tabpanel" class="tab-pane" id="sigSample3">
  
  <script src="https://gist.github.com/paywelcome/4c9d4eebe8984b070ad7ac2dc18043ad.js"></script>
  
  </div>
  <div role="tabpanel" class="tab-pane" id="sigSample4">
  
  <script src="https://gist.github.com/paywelcome/d4f365be16b76619a53e81c2e7bfc13c.js"></script>
  
  </div>
</div>


<div class="tabs-head">
  <span data-tab="tab-1" class="tabs-nav active" onclick="Tabs();">Tab 1</span>
  <span data-tab="tab-2" class="tabs-nav" onclick="Tabs();">Tab 2</span>
  <span data-tab="tab-3" class="tabs-nav" onclick="Tabs();">Tab 3</span>
</div>

<div class="tabs-content">
  <div id="tab-1" class="b-tab active">

   <script src="https://gist.github.com/paywelcome/f5385130876ede2d6664082f5c09b63e.js"></script>

  </div>
  <div id="tab-2" class="b-tab">

   <script src="https://gist.github.com/paywelcome/281af4c8a0aa6354404613bf6f721f94.js"></script>

  </div>
  <div id="tab-3" class="b-tab">

   <script src="https://gist.github.com/paywelcome/d4f365be16b76619a53e81c2e7bfc13c.js"></script>

  </div>
</div>

<style>
.tabs-head{display:flex;border-bottom:1px solid #ebeced;margin-bottom:30px;font-size:13px}
.tabs-head > *:not(:last-child){margin-right:7px}
.tabs-head > *{padding:8px 15px;border:1px solid #ebeced;border-bottom:0;border-radius:4px 4px 0 0;position:relative;color:inherit;cursor:default}
.tabs-head > *:after{content:'';display:block;width:100%;height:2px;background-color:#fafafc;position:absolute;left:0;bottom:-1px;visibility:hidden;opacity:0}
.tabs-head > .active:after{opacity:1;visibility:visible}
.tabs-content{position:relative}
.tabs-content .b-tab{display:none;width:100%}
.tabs-content .b-tab.active{display:block}
</style>
