---
title: 모바일 부록
permalink: mobile03.html
sidebar: mobile_sidebar
folder: mobile
toc: false
keywords: 계좌이체, 유의사항, 주의사항, 사항, 주의, 
---

<div style="display: inline-block; width: 100%;">
  <a style="float:left;" href="/mobile02.html">◀이전페이지</a>
</div>

# 부록

## 3.1 계좌이체 연동시 유의사항

- 맹점 안드로이드/IOS 앱에서 계좌이체를 연동하시는 경우 아래의 앱스키마 정보에 대해 가맹점앱에서 처리 가능하도록 구현되어 있어야 하며,<br>OS별 상세 처리는 아래를 참고바랍니다.

<table style="width: 100%;">
<colgroup>
  <col style="width: 30%">
  <col style="width: 70%">
</colgroup>
  <thead>
    <tr>
      <th style="text-align: center">App</th>
      <th>custom scheme</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">뱅크페이<br>(  기본 )</td>
      <td><code class="language-plaintext highlighter-rouge">kftc-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">뱅크윌렛</td>
      <td><code class="language-plaintext highlighter-rouge">bankwallet://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">케이뱅크 페이</td>
      <td><code class="language-plaintext highlighter-rouge">ukbanksmartbanknonloginpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">산업</td>
      <td><code class="language-plaintext highlighter-rouge">kdb-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">기업</td>
      <td><code class="language-plaintext highlighter-rouge">ibk-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">국민</td>
      <td><code class="language-plaintext highlighter-rouge">kb-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">KEB 하나</td>
      <td><code class="language-plaintext highlighter-rouge">keb-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">수협</td>
      <td><code class="language-plaintext highlighter-rouge">sh-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">NH 농협</td>
      <td><code class="language-plaintext highlighter-rouge">nhb-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">농축협</td>
      <td><code class="language-plaintext highlighter-rouge">nh-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">우리</td>
      <td><code class="language-plaintext highlighter-rouge">wr-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">SC</td>
      <td><code class="language-plaintext highlighter-rouge">sc-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">신한</td>
      <td><code class="language-plaintext highlighter-rouge">s-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">씨티</td>
      <td><code class="language-plaintext highlighter-rouge">ct-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">대구</td>
      <td><code class="language-plaintext highlighter-rouge">dg-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">부산</td>
      <td><code class="language-plaintext highlighter-rouge">bnk-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">광주</td>
      <td><code class="language-plaintext highlighter-rouge">kj-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">제주</td>
      <td><code class="language-plaintext highlighter-rouge">jj-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">전북</td>
      <td><code class="language-plaintext highlighter-rouge">jb-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">경남</td>
      <td><code class="language-plaintext highlighter-rouge">kn-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">우정사업본부</td>
      <td><code class="language-plaintext highlighter-rouge">kp-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">신협</td>
      <td><code class="language-plaintext highlighter-rouge">cu-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">새마을</td>
      <td><code class="language-plaintext highlighter-rouge">mg-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">K 뱅크</td>
      <td><code class="language-plaintext highlighter-rouge">kbn-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">카카오뱅크</td>
      <td><code class="language-plaintext highlighter-rouge">kkb-bankpay://</code></td>
    </tr>
  </tbody>
</table>

### 3.1.1 안드로이드 연동 시 유의사항

- 계좌이체 결제 스키마 정보는 기본적으로 intent스키마가 아닌 URL 스키마로 호출됩니다. 가맹점에서는 특정 스키마에 대해서만 허용되도록 개발되어 있는 경우라면 위 명시되어 있는 URL스키마가 호출되는 경우에도 앱이 정상적으로 호출될 수 있도록 처리해 주셔야 합니다.<br>
  각각의 처리가 어려워 intent스키마로 연동이 필요하신 경우 아래 옵션을 통해 각 스키마 정보에 대해 intent 스키마로 처리가 가능합니다.

- 안드로이드 계좌이체  intent 스키마 호출 옵션정보

<table style="width: 100%;">
<colgroup>
  <col style="width: 50%;">
  <col style="width: 50%;">
</colgroup>
  <thead>
    <tr>
      <th style="text-align: center">필드명</th>
      <th style="text-align: center">값</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">P_RESERVED</td>
      <td style="text-align: center">apprun_check=Y</td>
    </tr>
  </tbody>
</table>

### 3.1.2 IOS 연동 시 유의사항

IOS 가맹점 앱에서 계좌이체 앱 실행을 위해서는 위의 스키마정보가 info.plist 파일에 White List로 등록되어 있어야합니다.<br>
해당 스키마 설정 추가와 관련하여 상세 내용은 이전 장에서 안내된 가이드를 참고바랍니다.

### 3.1.3 계좌이체 연동 시 권장 옵션

앱 및 웹 환경의 사용자 페이지의 자연스러운 전환을 위해 모바일 계좌이체 결제 진행 시 아래 옵션추가를 권장합니다.

<table style="width: 100%;">
<colgroup>
  <col style="width: 30%;">
  <col style="width: 70%;">
</colgroup>
  <thead>
    <tr>
      <th style="text-align: center">환경</th>
      <th>필드 및 옵션</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">안드로이드 웹/앱, 아이폰 웹</td>
      <td><code class="language-plaintext highlighter-rouge">P_RESERVED=twotrs_bank=Y&amp;apprun_check=Y</code></td>
    </tr>
    <tr>
      <td style="text-align: center">아이폰 앱</td>
      <td>
<code class="language-plaintext highlighter-rouge">P_RESERVED=twotrs_bank=Y&amp;iosapp=Y&amp;app_scheme={가맹점앱스키마}://</code><br><code class="language-plaintext highlighter-rouge">P_RETURN_URL={가맹점앱스키마}://</code>
</td>
    </tr>
  </tbody>
</table>

## 3.2 기타 연동시 주의사항

### 3.2.1 Form Encode issue

- Mobile Web 서비스는 EUC-KR을 사용합니다.<red>반드시  EUC-KR  인코딩으로 전송 바랍니다.</red>

```javascript
<form method="post" accept-charset="euc-kr"> 
```

<red>한글 깨졌을 때 추가 체크 포인트</red>

(1) 소스파일 EUC-KR로 저장<br/>
(2) 페이지 인코딩 확인(JAVA 기준) : ```<%@ page language="java" contentType="text/html; charset=euc-kr" pageEncoding="euc-kr"%> ```<br/>
(3) 헤더 인코딩 확인(JAVA 기준) : ``` <meta http-equiv="Content-Type" content="text/html; charset=euc-kr">```<br/>
(4) 결제창에서 한글 깨지는 경우  submit 함수에서 submit 처리전 ```document.charset = "euc-kr"``` 추가

### 3.2.2 UrlEncode issue

- 상점 페이지에서 Mobile Web 서비스로 주문정보 전송 시, Form Data 가 Double Encoded 되어 전송되는 경우가 있습니다. 하기의 Case 를 확인하시어, Encoding 여부를 체크하십시오.

<table style="width: 100%">
<colgroup>
  <col style="width: 25%">
  <col style="width: 25%">
  <col style="width: 50%">
</colgroup>
  <thead>
    <tr>
      <th style="text-align: center">가맹점 BASE</th>
      <th style="text-align: center">Mobile Web  서비스 호출  BASE</th>
      <th style="text-align: center">Url-Encode 여부</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">Web-Browser</td>
      <td style="text-align: center">Web-Browser</td>
      <td style="text-align: center">필요 없음</td>
    </tr>
    <tr>
      <td style="text-align: center">App</td>
      <td style="text-align: center">WebView</td>
      <td style="text-align: center">:warning:<red>체크 요망</red></td>
    </tr>
    <tr>
      <td style="text-align: center">App</td>
      <td style="text-align: center">Web-Browser</td>
      <td style="text-align: center">필요 없음</td>
    </tr>
  </tbody>
</table>

- urlEncode 구현 시, 필드명은 미포함 한, input 의 value 부만 encoding 해야 합니다.
  예시 ) ```<input type="hidden" name="P_RESERVED" value="urlencode(value)" />```

### 3.2.3 iFrame issue

- Mobile Web 서비스는 Non-Iframe 에 최적화 되어 있습니다.<br>이에, iFrame 내에 구현하는 것을 권장하지 않습니다. iFrame 구현에 따른 문제에 대하여는 당사에서 책임지지 않습니다.

### 3.2.4 Parameter issue

- P_RESERVED 복합필드 외에, 일반필드에서는 Value 값에 하기의 특수기호를 불허합니다.

<table style="width: 60%;">
<colgroup>
  <col style="width: 10%;">
  <col style="width: 10%;">
  <col style="width: 10%;">
  <col style="width: 20%;">
  <col style="width: 10%;">
  <col style="width: 10%;">
  <col style="width: 30%;">
</colgroup>
<tbody>
  <tr>
    <td>:</td>
    <td>?</td>
    <td>`</td>
    <td>new line</td>
    <td>"</td>
    <td>&</td>
    <td>외 특수기호</td>
  </tr>
</tbody>
</table>

 **※ 특히, 주문번호필드(P_OID)와 기타주문정보(P_NOTI)필드에는 절대 불허합니다.**

### 3.2.5 가상계좌 채번시  P_NOTI_URL issue

- P_NOTI_URL 은 입금 통보 시 전달되는 URL로 사용되는 필드입니다.<br>
  입금 통보 외에 가상 계좌 채번 시에도 P_NOTI_URL 로 결과가 전송 되오니,<br>
  채번 시 전달되는 내용은 무시하시기 바랍니다. 자세한 내용을 샘플을 참조하여 주시기 바랍니다.

[부가설명]

```
가상계좌 채번이란, 고객이 가상계좌번호를 발급받는 단계를 의미합니다.
입금 통보 란, 고객이 가상계좌 채번 시 받은 계좌번호로 돈을 입금 한 단계를 일컫습니다.
```

### 3.2.6 모바일 거래 결제취소 issue

- Mobile Web 서비스는 거래취소기능을 지원하지 않습니다.<br>
  따라서, 결제 취소는 별도의 PayAPI 서비스 연동하여 활용하시기 바랍니다.<br>
  자세한 문의사항은 당사 기술지원팀으로 문의 바랍니다.

### 3.2.7 DNS 설정관련 issue

- 가맹점의 웹 서버의 언어가 java인 경우 반드시 DNS캐쉬 기능을 꺼주셔야 합니다.<br>
  (단말기와 웹서버에 Cache 된 DNS 정보가 상이할 경우, 결제 실패됨)
- JVM(JDK)설정 파일 networkaddress.cache.ttl 항목 설정 (java.security)
- 이중화 서비스 이용을 위해 반드시 필요한 설정입니다. (설정 후 WAS 재 시작.)
- $JAVA_HOME/jre/lib/security/java.security 설정파일에 &quot;networkaddress.cache.ttl=0&quot; 설정

### 3.2.8 인증결과 수신 및 승인결과 수신 시 issue

- Mobile Web 서비스에서 전달하는 파라미터를 Parsing 하여 사용하실 때의 주의사항입니다.
- 당사에서는 전달되는 파라미터의 순서를 변경하거나, 추가적으로 삽입할 수 있습니다.
- POST 혹은 GET 으로 넘어오는 데이터 전체를 Array 에 담아, 순서를 정한 채 사용하지 마십시오.
- 항시  Key &amp; Value  의 형태를 유지하시기 바랍니다.
```php
<?php
//인증결과 수신시 
$_data = $_POST;
$receiveData = array();
foreach($data as $value)
{
  $tmp = explode(“=”,$value);
  $receiveData[] = $tmp[1];
}
/* 순서가 바뀔 수 있으며, 일부 파라미터는 삭제될 수도 있음 */
$P_STATUS = $receiveData[0];
$P_RMESG1 = $receiveData[1];
$P_TID = $receiveData[2];
….	
?>
```

## 3.2.9 P_NEXT_URL의 Scheme issue

- 근래에 들어 보안 Page 에서 비보안 Page 로의 Submit 에 대한 제약이 강화되고 있습니다.
- Mobile Web 서비스는 Https Scheme 을 사용한 보안 페이지로, 가맹점의 P_NEXT_URL 로 인증결과를 송신할 때, P_NEXT_URL 의 Scheme 이 Http 일 경우, 하기와 같이 경고가 발생할 수 있습니다.<br>
  따라서, 되도록이면 Https Scheme 을 사용하도록 권장하며, Http 의 사용에 따른 오류에 대하여 당사는 책임지지 않습니다.
- 또한 ,  사설  SSL  인증서 사용 시, 전송이 불가할 수 있사오니, 반드시 체크 바랍니다 .
- iOS 11.3 업데이트 이후 보안정책이 강화됨에 따라 http 프로토콜을 사용하는 경우 인증결과를 받을 수 없습니다.
- 가맹점 주문정보 값 중 P_NEXT_URL (인증결과 받는 URL) 값이 http일 경우 https로 변경 필요

## 3.2.10 브라우저 환경에서의 쿠키허용 issue

- Mobile Web 서비스는 정상적으로 사용하기 위해서는 사용자의 브라우져에서 쿠키를 허용하는 상태여야 합니다.

- Android

<table style="width: 100%;">
<colgroup>
  <col style="width: 50%;">
  <col style="width: 50%;">
</colgroup>
  <thead>
    <tr>
      <th>기본</th>
      <th>권장(필수)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>설정 &gt; 개인정보 보호 및 보안 &gt; 쿠키허용 체크활성</td>
      <td>설정 &gt; 개인정보 보호 및 보안 &gt; 쿠키허용 체크활성</td>
    </tr>
  </tbody>
</table>

- IOS

<table style="width: 100%;">
<colgroup>
  <col style="width: 50%;">
  <col style="width: 50%;">
</colgroup>
  <thead>
    <tr>
      <th>기본</th>
      <th>권장(필수)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>설정 &gt; Safari &gt; 쿠키차단 &gt; 내가 방문한 웹사이트에서 허용</td>
      <td>설정 &gt; Safari &gt; 쿠키차단 &gt; 항상 허용</td>
    </tr>
  </tbody>
</table>
<p style="font-size: 80%;">브라우져 버전에 따라 메뉴 명이 다를 수 있습니다.</p>

## 3.2.11 인증결과 수신 시 Method issue

- Mobile Web 서비스는 다양한 카드사 및 인증사와의 복잡한 연계시스템을 구축하고 있습니다.<br>때문에 상황에 따라, 인증결과 송신과정에 대하여 post 혹은 get 방식을 선택적으로 운영해야 합니다.<br>
- 가맹점에서는 인증결과 수신 시, 개별 파라미터에 대하여 post 와 get 을 모두 수용할 수 있도록 처리해야 하며, 인증결과 파라미터는 가감되거나, 순서가 변경될 수 있사오니, 이점 유의 바랍니다.<br>(단, 결제 확인에 필요한 필수 파라미터는 가감되지 않음)

## 3.2.12 네이버/카카오톡 앱 환경 최적화 issue

- 네이버/카카오 앱에서는 해당 앱 특성에 따라, 당사 결제창을 띄울 때, 새 창(_blank)을 띄울 경우, 정상적으로 결제가 진행되지 않을 수 있습니다.<br>따라서 가맹점 플랫폼에서, 당사 결제창을 띄울 때, 새 창이 아닌, _self 형태로 띄워주시길 권장합니다.

## 3.2.13 안드로이드/IOS 앱 USER AGENT 수정

- 신용카드 결제 시 각 카드사 ACS페이지에서는 사용자의 USER AGENT를 검증하고 있습니다.<br>(검증방식은 카드사별 상이) 가맹점 앱에서 USER AGENT를 임의로 변경하는 경우, 카드사 인증실패가 발생할 수 있으니 이점 유의 바랍니다.

## 3.2.14 아이폰 3rd party( 제 3 공급자) 앱브라우져 결제 issue

- iOS 기본 브라우저인 Safari 외 앱 브라우저(다음, 네이버, 크롬, 페이스북 등) 에서 ISP, 계좌이체 결제 진행 시, ISP 앱에서 인증 완료 후 결제를 진행한 브라우저 앱이 아닌 Safari 브라우저로 돌아가는 이슈가 있습니다.<br>
- 해당 브라우저 앱에서 결제를 진행하는 경우, 앱 브라우저의 user-agent를 확인하여 P_RESERVED에 ```app_scheme={앱스키마}://``` 형태를 설정하시면 해당 이슈가 해결 됩니다.<br>

ex) 카카오톡 앱에서 결제 진행 시
<table style="width: 100%;">
<colgroup>
  <col style="width: 30%;">
  <col style="width: 70%;">
</colgroup>
  <tbody>
    <tr>
      <td>신용카드</td>
      <td>P_RESERVED=twotrs_isp=Y&amp;block_isp=Y &amp;app_scheme=kakaotalk:// &amp;</td>
    </tr>
  </tbody>
</table>

- 확인된 App Scheme ( 18.12.31 기준 )

<table style="width: 100%;">
<colgroup>
  <col style="width: 30%;">
  <col style="width: 70%;">
</colgroup>
  <tbody>
    <tr>
      <td>다음</td>
      <td>daumapps://open</td>
    </tr>
    <tr>
      <td>네이버</td>
      <td>naversearchapp://</td>
    </tr>
    <tr>
      <td>크롬</td>
      <td>googlechromes://</td>
    </tr>
    <tr>
      <td>페이스북</td>
      <td>fb://</td>
    </tr>
    <tr>
      <td>카카오톡</td>
      <td>kakaotalk://</td>
    </tr>
  </tbody>
</table>

## 3.2.15 결제 요청 시 주의사항

- 모바일 연동 관련 변경사항 및 안내사항에 대해 본 매뉴얼을 통해 안내하고 있습니다.<br>
- 일반 웹사이트에 유포되는 샘플코드를 사용하여 연동하시는 경우 지원종료 옵션 인입으로 결제가 정상적으로 처리되지 않을 수 있으니 당사 홈페이지 기술지원메뉴의 최신 메뉴얼을 참고하여 인입 파라미터에 대한 지원 확인 후 결제 진행하시기 바랍니다.<br>(지원파라미터는 본 메뉴얼 1-1-2. 1-1-3 의 일반필드/복합필드를 참고바랍니다. )

## 3.2.16 주문요청 시 유의사항

- 주문요청 시 method는 반드시 POST 방식으로 요청되어야 합니다.<br>GET방식을 사용하여 결제 요청 시 브라우저 정책에 따라 결제요청 데이터가 유실되거나 페이지 전환이 진행되지 않을 수 있습니다.

```javascript
<form method="post" accept-charset="euc-kr">
```

<div style="display: inline-block; width: 100%; margin-top: 50px;">
  <a style="float:left;" href="/mobile02.html">◀이전페이지</a>
</div>
