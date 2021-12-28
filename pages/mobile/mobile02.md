---
title: MOBILE
permalink: mobile02.html
sidebar: mobile_sidebar
folder: mobile
toc: false
keywords: 승인, 요청, 응답, 카드, 모바일, 계좌이체, 핸드폰, 인증, 스마트폰, 모바일 취소, 취소, 결제취소, 결제 취소, signkey, signKey, mid, 데이터, 공통, ios, Android, ANDROID, 안드로이드
---

<div style="display: inline-block; width: 100%;">
  <a style="float:left;" href="/mobile01.html">◀이전페이지</a>
  <a style="float:right;" href="/mobile03.html">다음페이지▶</a>
</div>

# 2. 결제 연동

## 2.1 결제 요청 페이지작성 - 접속 주소 및 일반필드

> 주문정보 전달이란, 하기의 Step을 의미합니다.

{% include image.html file="mobile_img03.png" %}

<br/>

상점 페이지에서 Mobile Web 서비스 접속 시, 지불수단 및 통신방식 별로 상이한 URL 을 사용합니다. 이에, 하기의 URL 을 참고하시기 바랍니다.

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

[//]: # (URL table)
<table class="tg" style="table-layout: fixed; width: 100%">
<colgroup>
<col style="width: 25%;">
<col style="width: 25%;">
<col style="width: 50%;">
</colgroup>
<tbody>
  <tr>
    <td class="center-align" rowspan="2">HOST</td>
    <td class="center-align">테스트</td>
    <td class="center-align">tmobile.paywelcome.co.kr</td>
  </tr>
  <tr>
    <td class="center-align">운영</td>
    <td class="center-align">mobile.paywelcome.co.kr</td>
  </tr>
  <tr>
    <td class="center-align" rowspan="4">지불수단별<br>상세 URL</td>
    <td class="center-align">신용카드</td>
    <td class="center-align">https://{HOST}/smart/wcard/</td>
  </tr>
  <tr>
    <td class="center-align">가상계좌</td>
    <td class="center-align">https://{HOST}/smart/vbank/</td>
  </tr>
  <tr>
    <td class="center-align">계좌이체</td>
    <td class="center-align">https://{HOST}/smart/bank/</td>
  </tr>
  <tr>
    <td class="center-align">휴대폰</td>
    <td class="center-align">https://{HOST}/smart/mobile/</td>
  </tr>
  <tr>
    <td class="center-align" colspan="2">METHOD</td>
    <td class="center-align">POST</td>
  </tr>
  <tr>
    <td class="center-align" colspan="2">Content-Type</td>
    <td class="center-align">application/x-www-form-urlencoded;<br>charset=EUC-KR</td>
  </tr>
  <tr>
    <td class="center-align" colspan="3">ex) 신용카드 연동시 : https://mobile.paywelcome.co.kr/smart/wcard/</td>
  </tr>
</tbody>
</table>

</div>
</details>

#### 상점 연동을 위한 테스트 MID

>Test mid와 signkey값은 계약가맹점에 한해 별도 전달 예정입니다.

[//]: # (MID 연동 table)
<table class="tg" style="table-layout: fixed; width: 100%">
<tbody>
  <tr>
    <td class="center-align">Test mid</td>
    <td class="center-align" rowspan="2"><a href="mailto:mainpg_support@welcomepayments.co.kr">메일로 문의하기(support@welcomepayments.co.kr)</a></td>
  </tr>
  <tr>
    <td class="center-align">signKey</td>
  </tr>
</tbody>
</table>


`샘플로 제공 되는 테스트 MID만 사용가능하며 운영 MID 사용 불가`

<br/>

## 2.2 결제 요청 페이지작성 - 결제페이지 요청필드

>Mobile Web 서비스 접속 시, 결제페이지를 구성하기 위해서는 하기 Parameter를 필요로 합니다.
```javascript
양식 예시 : <input type="hidden" name="필드" value="값 예시" />;
```

### 2.2.1 전 지불수단 공통 필드

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table class="tg" style="table-layout: fixed; width: 100%;">
<colgroup>
<col style="width: 20%;">
<col style="width: 15%;">
<col style="width: 15%;">
<col style="width: 5%;">
<col style="width: 45%; text-align: left;">
</colgroup>
<thead>
  <tr>
    <th style="text-align: center;">필드</th>
    <th style="text-align: center;">필드명</th>
    <th style="text-align: center;">타입</th>
    <th style="text-align: center;">필수</th>
    <th style="text-align: center;">비고</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="center-align">P_MID</td>
    <td class="center-align">상점아이디</td>
    <td class="center-align">String(10)</td>
    <td class="center-align">○</td>
    <td>계약된 당사발급 아이디</td>
  </tr>
  <tr>
    <td class="center-align">P_OID</td>
    <td class="center-align">주문번호</td>
    <td class="center-align">String(40)</td>
    <td class="center-align">△</td>
    <td>한글을 제외한, 숫자/영문/특수기호의 형태<br>필수대상 : 가상계좌</td>
  </tr>
  <tr>
    <td class="center-align">P_AMT</td>
    <td class="center-align">거래금액</td>
    <td class="center-align">String(8)</td>
    <td class="center-align">○</td>
    <td>단위 표시 기호(콤마) 를 반드시 제거 요망</td>
  </tr>
  <tr>
    <td class="center-align">P_UNAME</td>
    <td class="center-align">고객성명</td>
    <td class="center-align">String(30)</td>
    <td class="center-align">○</td>
    <td></td>
  </tr>
  <tr>
    <td class="center-align">P_MNAME</td>
    <td class="center-align">가맹점 이름</td>
    <td class="center-align">String(30)</td>
    <td class="center-align">X</td>
    <td></td>
  </tr>
  <tr>
    <td class="center-align">P_NOTI</td>
    <td class="center-align">기타주문정보</td>
    <td class="center-align">String(800)</td>
    <td class="center-align">X</td>
    <td>이 값은 가맹점에서 이용하는 추가 정보 필드로 전달한 값이 그대로 반환됩니다. <code class="language-plaintext highlighter-rouge">결제처리 시, 꼭 필요한 내용만 사용하세요.</code>800byte를 초과하는 P_NOTI의 값은 차후 문제가 생길 여지가 있으니 반드시 800byte를 초과하지 않도록 설정해야 합니다.</td>
  </tr>
  <tr>
    <td class="center-align">P_GOODS</td>
    <td class="center-align">결제상품명</td>
    <td class="center-align">String(80)</td>
    <td class="center-align">○</td>
    <td></td>
  </tr>
  <tr>
    <td class="center-align">P_MOBILE</td>
    <td class="center-align">구매자 휴대폰번호</td>
    <td class="center-align">String(20)</td>
    <td class="center-align">X</td>
    <td>'-' 를 포함한 번호를 적어주세요.<br>예시 : 000-0000-0000</td>
  </tr>
  <tr>
    <td class="center-align">P_EMAIL</td>
    <td class="center-align">구매자 E-mail</td>
    <td class="center-align">String(60)</td>
    <td class="center-align">X</td>
    <td>예시 : abc@abc.com</td>
  </tr>
  <tr>
    <td class="center-align">P_NEXT_URL</td>
    <td class="center-align">인증결과수신</td>
    <td class="center-align">String(250)</td>
    <td class="center-align">△</td>
    <td>사용자의 인증이 완료될 때, 이 Url 로 인증결과를 전달합니다.<br> Method : post or get (issue : 1-24보기) <br> Scheme : https (issue : 1-22보기)<br>Parameters : 0.<br>인증결과수신 (only 2 Transaction)참고 <br> 예외대상 : Kpay <br><code class="language-plaintext highlighter-rouge">한글도메인 사용불가, https 권장</code></td>
  </tr>
  <tr>
    <td class="center-align">P_NOTI_URL</td>
    <td class="center-align">승인결과통보Url</td>
    <td class="center-align">String(250)</td>
    <td class="center-align">△</td>
    <td>가맹점과 인증/승인과정을 거치지 않고 승인결과를 통보하는 용도로 사용합니다. 단, 가상계좌의 경우, 입금완료시각이 비동기식 이므로, 입금완료 통보를 위해 사용됩니다.<br> Method : post<br> 가상계좌의 NOTI Url 은 네트워크 사정에 따라 중복전송 될 수 있으니, 중복수신여부 체크루틴을 반드시 구현하시기 바랍니다.<br><code class="language-plaintext highlighter-rouge">한글도메인 사용불가</code></td>
  </tr>
  <tr>
    <td class="center-align">P_TAX</td>
    <td class="center-align">부가세</td>
    <td class="center-align">String(8)</td>
    <td class="center-align">X</td>
    <td>영수증에 표기할 부가세 금액<br>주의 : 전체금액의 10%이하로 설정<br>대상 : '부가세업체정함' 설정업체에 한함</td>
  </tr>
  <tr>
    <td class="center-align">P_TAXFREE</td>
    <td class="center-align">비과세</td>
    <td class="center-align">String(8)</td>
    <td class="center-align">X</td>
    <td>과세 되지 않는 금액<br>대상 : '부가세업체정함' 설정업체에 한함</td>
  </tr>
  <tr>
    <td class="center-align" rowspan="6">P_OFFER_PERIOD</td>
    <td class="center-align" rowspan="6">제공기간</td>
    <td class="center-align" rowspan="6"></td>
    <td class="center-align" rowspan="6">X</td>
    <td>상품의 제공기간을 설정해야 하는 경우, 사용되는 옵션으로, Mobile Web 서비스에 디스플레이 하는 용도로만 사용됩니다.</td>
  </tr>
  <tr>
    <td>1) 상점에서 16자리 값 입력 시 (2013012920130229): 날짜 표시 Ex. 2013.01.29 ~ 2013.02.29<br></td>
  </tr>
  <tr>
    <td>2) 상점에서 24자리 값 입력 시 (201301291130201302291230): 날짜시간표시 Ex. 2013.01.29 11:30 ~ 2013.02.29 12:30</td>
  </tr>
  <tr>
    <td>3) 상점에서 M2 값 설정 시 (M2) : 월 자동결제 </td>
  </tr>
  <tr>
    <td>4) 상점에서 Y2 값 설정 시 (Y2): 연 자동결제</td>
  </tr>
  <tr>
    <td>5) 1 ~ 4번의 조건을 만족하지 않으면 ( 글자길이가 맞지 않거나 문자를 삽입하는 경우 ) &#39;별도 제공 기간 없음&#39; 으로 표기</td>
  </tr>
  <tr>
    <td class="center-align">P_TIMESTAMP</td>
    <td class="center-align">타임스템프</td>
    <td class="center-align">String(20)</td>
    <td class="center-align">○</td>
    <td>TimeInMillis(Long형)</td>
  </tr>
  <tr>
    <td class="center-align">P_SIGNATURE</td>
    <td class="center-align">SIGNATRUE</td>
    <td class="center-align">String(64)</td>
    <td class="center-align">○</td>
    <td>위변조 방지 SHA256 Hash 값(mkey+P_AMT+P_OID+P_TIMESTAMP)<a href="/prepare01.html#mobile-서비스의-signature-생성">참조 - P_SIGNATURE 필드 처리</a><br/>
    <p style="color: red;"><strong>P_SIGNATURE의 자세한 생성방식은 <a href="/prepare01.html#12-signature-개요">연동 준비하기 - 1.2 Signature</a>를 참고 바랍니다.</strong></p></td>
  </tr>
</tbody>
</table>

</div>
</details>

### 2.2.2 신용카드 전용 필드

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table class="tg" style="table-layout: fixed; width: 100%;">
<colgroup>
    <col style="width: 20%;">
    <col style="width: 15%;">
    <col style="width: 15%;">
    <col style="width: 10%;">
    <col style="width: 40%; text-align: left;">
</colgroup>
<thead>
  <tr>
    <th class="center-align">필드</th>
    <th class="center-align">필드명</th>
    <th class="center-align">타입</th>
    <th class="center-align">필수</th>
    <th class="center-align">비고</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="center-align" rowspan="2">P_CARD_OPTION</td>
    <td class="center-align">신용카드 우선선택 옵션</td>
    <td class="center-align" rowspan="2">String(10)</td>
    <td class="center-align">X</td>
    <td>설정 시, 해당 카드코드에 해당하는 카드가 선택된 채로 Display 됩니다. 간편결제는 불가능(타 카드 선택 가능) <br>예시 : selcode=14</td>
  </tr>
  <tr>
    <td class="center-align">선택적 표시 옵션</td>
    <td class="center-align">X</td>
    <td>설정 시, 안심결제(visa3d), ISP(isp), 간편결제(easypay), 일반카드결제(normal) 중 선택적 표시 됩니다. <br> onlycard=visa3d 적용예시 : selcode=14:onlycard=visa3d</td>
  </tr>
  <tr>
    <td class="center-align">P_ONLY_CARDCODE</td>
    <td class="center-align">신용카드 노출제한 옵션</td>
    <td class="center-align">String(N/A)</td>
    <td class="center-align">X</td>
    <td>선택된 카드 리스트만 출력되며, 나머지 카드 리스트는 출력되지 않습니다.<br>적용 예시 : 롯데, 외환, BC 카드만 사용할 경우, <br> 롯데카드코드 : 03, <br>외환카드코드 : 01,<br>  BC카드코드 : 11 이므로, 03:01:11 로 설정</td>
  </tr>
  <tr>
    <td class="center-align">P_ONLY_EASYPAYCODE</td>
    <td class="center-align">간편결제 노출제한 옵션</td>
    <td class="center-align">String(N/A)</td>
    <td class="center-align">X</td>
    <td>선택된 간편결제 리스트만 출력되며, 나머지 간편결제 리스트는 출력되지 않습니다.<br> 적용 예시 : 카카오페이, 엘페이, 페이코만 사용할 경우, <br> 카카오페이 : KAKAOPAY <br> 엘페이 : LPAY<br> 페이코 : PAYCO 이므로<br> KAKAOPAY:LPAY:PAYCO 로 설정(간편결제 코드 대문자 입력 필)</td>
  </tr>
  <tr>
    <td class="center-align">P_QUOTABASE</td>
    <td class="center-align">신용카드 할부기간 지정</td>
    <td class="center-align">String(N/A)</td>
    <td class="center-align">X</td>
    <td>선50,000원 이상 결제 시, 할부기간 지정(36개월 MAX)<br> 적용 예시 :  01:02:03:04.. 01은 일시불, 02는 2개월, 99 는 일시불 제거 등등</td>
  </tr>
</tbody>
</table>

</div>
</details>

### 2.2.3 휴대폰 전용 필드

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table class="tg" style="table-layout: fixed; width: 100%;">
<colgroup>
<col style="width: 20%;">
<col style="width: 10%;">
<col style="width: 15%;">
<col style="width: 10%;">
<col style="width: 45%; text-align: left;">
</colgroup>
<thead>
  <tr>
    <th class="center-align">필드</th>
    <th class="center-align">필드명</th>
    <th class="center-align">타입</th>
    <th class="center-align">필수</th>
    <th class="left-align">비고</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="center-align">P_HPP_METHOD</td>
    <td class="center-align">실물여부</td>
    <td class="center-align">String(1)</td>
    <td class="center-align">○</td>
    <td class="left-align">컨텐츠 일 경우 : 1<br>실물일 경우 : 2<br> 빌링컨텐츠 일 경우 : 4<br> 빌링실물 일 경우 : 5<br> 컨텐츠/실물/빌링컨텐츠/빌링실물 여부는 계약담당자에게 확인요청</td>
  </tr>
</tbody>
</table>

</div>
</details>

### 2.2.4 가상계좌 전용 필드

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table class="tg" style="table-layout: fixed; width: 100%;">
<colgroup>
<col style="width: 15%;">
<col style="width: 20%;">
<col style="width: 10%;">
<col style="width: 10%;">
<col style="width: 45%; text-align: left;">
</colgroup>
<thead>
  <tr class="center-align">
    <th style="text-align: center;">필드</th>
    <th style="text-align: center;">필드명</th>
    <th style="text-align: center;">타입</th>
    <th style="text-align: center;">필수</th>
    <th style="text-align: center;">비고</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="center-align">P_VBANK_DT</td>
    <td class="center-align">가상계좌 입금기한 날짜</td>
    <td class="center-align">String(8)</td>
    <td class="center-align">X</td>
    <td>설정을 하지 않으면,요청일 + 10일로 자동설정 됩니다.<br>적용 예시 : 20151225</td>
  </tr>
  <tr>
    <td class="center-align">P_VBANK_TM</td>
    <td class="center-align">가상계좌 입금기한 시간</td>
    <td class="center-align">String(4)</td>
    <td class="center-align">X</td>
    <td>시분까지 설정 가능합니다.(4자리)<br>적용 예시 : 2030</td>
  </tr>
</tbody>
</table>

- P_VBANK_DT=20180518, P_VBANK_TM=0000 으로 설정하시는 경우 2018.05.18 23시 59분 59초까지로 설정됩니다.
```
예시)
P_VBANK_DT=20180518, P_VBANK_TM=0000 : 2018.05.18 23시 59분 59초까지
P_VBANK_DT=20180517, P_VBANK_TM=2359 : 2018.05.17 23시 59분 00초까지
P_VBANK_DT=20180518, P_VBANK_TM=0001 : 2018.05.18 00시 01분 00초까지
```

- **단 ,  결제요청일자와  P_VBANK_DT 가 같은 경우  V_VBANK_TM=0000  설정 불가능하며  P_VBANK_TM=2359 으로 설정하셔야 정상 승인 가능합니다.**

</div>
</details>

### 2.2.5 기타 옵션 필드

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table class="tg" style="table-layout: fixed; width: 100%;">
<colgroup>
<col style="width: 15%;">
<col style="width: 15%;">
<col style="width: 10%;">
<col style="width: 10%;">
<col style="width: 50%; text-align: left;">
</colgroup>
<thead>
  <tr class="center-align">
    <th style="text-align: center;">필드</th>
    <th style="text-align: center;">필드명</th>
    <th style="text-align: center;">타입</th>
    <th style="text-align: center;">필수</th>
    <th style="text-align: center;">비고</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="center-align">P_CHARSET</td>
    <td class="center-align">인코딩 설정</td>
    <td class="center-align">String(6)</td>
    <td class="center-align">X</td>
    <td>인증, 승인결과 CHARSET 정의 default는 euc-kr이며, 인증·승인 결과를 utf-8로 받기를 원하시면 해당 옵션 설정 값을 utf8로 하시면 됩니다.<br> Ex. utf8동기방식에서 P_CHARSET=utf8 옵션 사용 시,<br>ISP 결제 진행 과정에서 인증결과 중 P_RMESG1 필드 값이 urlencode 되어 내려갈 수 있습니다.<br>인증결과 값에 대해 필요 시, 해당 값에 대해 urldecode 처리하여 사용할 수 있도록 처리 바랍니다.</td>
  </tr>
</tbody>
</table>

</div>
</details>

### 2.2.6 복합 필드 (P_RESERVED)

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table class="tg" style="table-layout: fixed; width: 100%;">
<colgroup>
<col style="width: 15%;">
<col style="width: 20%;">
<col style="width: 25%;">
<col style="width: 40%; text-align: left;">
</colgroup>
<thead>
  <tr>
    <th class="center-align">필드</th>
    <th class="center-align">필드명</th>
    <th class="center-align">Variable</th>
    <th class="center-align">비고</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="center-align" rowspan="17">P_RESERVED</td>
    <td class="center-align">신용카드 필수옵션</td>
    <td class="center-align">twotrs_isp=Y&block_isp=Y&twotrs_isp_noti=N</td>
    <td>신용카드 거래 시, 반드시 입력되어야 하는 값 입니다.</td>
  </tr>
  <tr>
    <td class="center-align">가상계좌 현금영수증<br>사용여부</td>
    <td class="center-align">vbank_receipt=Y</td>
    <td>Default : 미표시<br> Y : 표시<br> N : 미표시</td>
  </tr>
  <tr>
    <td class="center-align">계좌이체 필수옵션</td>
    <td class="center-align">twotrs_bank=Y&apprun_check=Y</td>
    <td>계좌이체 거래 시, 반드시 입력되어야 하는 값입니다.</td>
  </tr>
  <tr>
    <td class="center-align">계좌이체 현금영수증<br>사용여부</td>
    <td class="center-align">bank_receipt=Y</td>
    <td>Default : 미표시<br> Y : 표시<br> N : 미표시</td>
  </tr>
  <tr>
    <td class="center-align">카드포인트 사용여부</td>
    <td class="center-align">cp_yn=Y</td>
    <td>신용카드에 한하며, 신용카드 포인트를 사용가능하게 하는 옵션입니다.<br> 이 옵션을 사용하면, 신용카드 사의 포인트를 사용할 수 있습니다.</td>
  </tr>
  <tr>
    <td class="center-align">앱 호출 시, Intent 형식으로 호출여부</td>
    <td class="center-align">apprun_check=Y</td>
    <td>카드사 창에서 호출되는 백신앱 및 앱카드를 제외한,<br> Mobile Web 서비스에서 직접 호출하는 앱(ISP등)의 호출방식을 Intent 방식으로 작동시키며,<br> 설치유무 체크를 Mobile Web 서비스에서 직접 컨트롤 하는 기능을 수행합니다.<br> (Chrome, safari, ff) 해당 기능은 Android 단말기에서만 정상 동작하며,<br> app_scheme 옵션과 같이 사용할 수 없습니다.</td>
  </tr>
  <tr>
    <td class="center-align">30만원 이상 결제 시</td>
    <td class="center-align">ismart_use_sign=Y</td>
    <td>Android : 이 옵션 필요 없음 (해당 없음) <br> IOS 웹 형태 : ismart_use_sign=Y<br>IOS 앱형태 : ismart_use_sign=Y&mall_app_name=가맹점스키마</td>
  </tr>
  <tr>
    <td class="center-align">에스크로사용여부</td>
    <td class="center-align">useescrow=Y</td>
    <td>설정 시 "에스크로 약관동의" 와 "구매자 본인확인" 페이지가 포함된 에스크로 결제창을 호출 합니다.<br>(에스크로 사용 설정된 가맹점만 사용 가능합니다.)</td>
  </tr>
  <tr>
    <td class="center-align">1000원 미만 결제 허용</td>
    <td class="center-align">below1000=Y</td>
    <td>신용카드 거래 시, 1000원 미만 결제를 허용하는 옵션 입니다.옵션을 사용하지 않으면, 자동 미사용 됩니다.</td>
  </tr>
  <tr>
    <td class="center-align">신용카드 결제창<br>직접 호출</td>
    <td class="center-align">d_card=00(코드)d_quota=00(할부개월)</td>
    <td>신용카드 결제창(안심클릭 / ISP)을 직접 호출하는 옵션 입니다.<br>설정 방법 : d_card=00(카드코드)d_quota=00(할부개월)<br>Ex. d_card=04&amp;d_quota=03</td>
  </tr>
  <tr>
    <td class="center-align">가맹점 App scheme<br>설정</td>
    <td class="center-align">app_scheme=스키마 값</td>
    <td>가맹점 APP및 타사 앱을 통해 결제 진행 시 아래 지불수단을 사용할 경우 설정(IOS 지원)<br>ISP 2trs<br>Ex. app_scheme=스키마명:// (스키마명 뒤에 "://"는 꼭 입력해 주셔야 합니다.)</td>
  </tr>
  <tr>
    <td class="center-align">신용카드 상점무이자</td>
    <td class="center-align">merc_noint=Ynoint_quota=00-00(카드-개월)</td>
    <td>무이자 이벤트 진행 시, 상점 부담 무이자 옵션 입니다.<br>(대표 무이자 및 분담 무이자 아님) <br>설정 방법 : merc_noint = Ynoint_quota=00-00:00(카드-개월:개월) [카드-월:월]^ 카드는 OO두자리, 할부개월 01→1 카드 추가 시, 구분자는 ^ 입니다.<br>잘못된 예 11-02:04:06Ex. merc_noint=Y&amp; noint_quota=11-2:3^06-3:6:9:12<br>※ 상점부담 무이자 계약 가맹점만 사용 가능합니다.<br>(영업담당자 문의)</td>
  </tr>
  <tr>
    <td class="center-align">표시될 통신사 리스트</td>
    <td class="center-align">hpp_corp=통신사</td>
    <td>휴대폰 통신사(SKT, KTF, LGT, MVNO)를 지정할 수 있는 옵션 입니다.<br> Ex. SKT만 사용- hpp_corp=SKT <br> SKT, KTF, LGT 사용 - hpp_corp=SKT:KTF:LGT <br> MVNO중 일부만 설정 시 MVNO 제외 후 CJH(헬로모바일):KCT(티플러스):SKL(SK7mobile) 중 일부만 선택</td>
  </tr>
  <tr>
    <td class="center-align">휴대폰 통신사 기본 선택</td>
    <td class="center-align">hpp_default_corp=통신사</td>
    <td>통신사 리스트에서 입력 통신사가 기본 선택되어 짐 <br> SKT, KTF, LGT, MVNO 중 하나만 설정 가능 <br> MVNO 중 선택 시 CJH, KCT, SKL로 설정 가능미입력 시나 공백으로 입력 시 선택된 통신사 없음 <br> Ex. hpp_default_corp=SKT</td>
  </tr>
  <tr>
    <td class="center-align">휴대폰 번호 수정 불가 여부</td>
    <td class="center-align">hpp_nofix=Y</td>
    <td>휴대폰 번호를 수정 불가능하게 처리할 경우 설정 <br> (Y : 수정 불가, N : 수정가능(default))</td>
  </tr>
  <tr>
    <td class="center-align"> 휴대폰 결제 인증 옵션</td>
    <td class="center-align"> hpp_authtype=ARS</td>
    <td>휴대폰 결제 인증 시 ARS로 인증하도록 처리 할 경우 설정 <br> (해당 옵션은 모빌리언스만 가능)</td>
  </tr>
  <tr>
    <td class="center-align">휴대폰 빌키 발급</td>
    <td class="center-align">hpp_bill=Y</td>
    <td>휴대폰 빌키 발급 시 사용상품유형 P_HPP_METHOD=4 또는 P_HPP_METHOD =5 로 설정 필요 <br> (휴대폰 빌링 사용은 별도 사용 설정 필요)</td>
  </tr>
</tbody>
</table>
<p style="font-size: 80%">(상기 기능 외, 옵션에 대하여는 별도 문의 바랍니다)</p>

</div>
</details>
<br/>
앱 내 WebView 로 구현하는 경우, P_RESERVED 옵션이 추가됩니다.
( 2장. 앱 환경의 설치방법(안드로이드)의 2.B. ISP 연동방법 ) 를 참고하십시오. 

복합필드 설정엔 아래의 방식을 추천드립니다.
```text
 신용카드, 계좌이체 거래시, intent 방식으로 앱을 호울할 수 있도록 하기와 같이 기본적으로 구성하는 것을 권장합니다.
  ==> 신용카드 : twotrs_isp=Y&twotrs_isp&twotrs_isp_noti=N&apprun_check=Y
  ==> 계좌이체 : twotrs_isp=Y&apprun_check=Y
``` 

하기는 복합필드의  apprun_check=Y  사용 / 미사용 시 ,  로직에 대한 상세 안내입니다 .
&lt;apprun_check=Y 미 사용시 &gt; - ISP 앱이 없을 땐, 오류 페이지가 발생합니다.

{% include image.html file="mobile_img04.png" %}

_( __이어서…__ )_

{% include image.html file="mobile_img05.png" %}

&lt;apprun_check=Y 사용시 &gt; - ISP 앱이 없다면, 앱 스토어 이동 및 설치 후, 결제를 이어서 진행할 수 있습니다.

[카카오페이 /L.Pay/ 페이코 직연동]
- 간편결제 직연동을 원하신다면 해당 호출 값을 활용하시기 바랍니다.
- 간편결제 직연동 시, 웰컴페이먼츠 계약담당자와 사전 협의가 이루어져야 합니다.
- 간편결제 직연동 시, 전자금융거래 이용약관은 가맹점 페이지에서 동의 받아 주셔야 합니다.
- 이 외 정보는 상기 본 메뉴얼과 동일합
- 간편결제 직접호출

```html
<input type="hidden" name="P_RESERVED" value="d_kakaopay=Y&" />
<input type="hidden" name="P_RESERVED" value="d_payco=Y&" />
<input type="hidden" name="P_RESERVED" value="d_lpay=Y&" />
```

## 2.3 결제 페이지 구성 예제

#### 1) 2 Transaction 방식의 구성
하기 예제는 2 Transaction 구성에 한한 예제 입니다. (head,body 부 생략)
```html
<meta http-equiv="Content-Type" content="text/html;charset=euc-kr"/>
<script>
function formSubmit(){
	document.getElementById("form1").submit();
}
</script>
<form id="form1" name="form1" method="post" action="지불수단URL">
    <input type="hidden" name="P_GOODS" value="테스트상품" />
    <input type="hidden" name="P_MID" value="상점아이디" />
    <input type="hidden" name="P_AMT" value="상품가격" />
    <input type="hidden" name="P_OID" value="5124213" />
    <input type="hidden" name="P_EMAIL" value="abc@abc.com" />
    <input type="hidden" name="P_UNAME" value="구매자명" />
    <input type="hidden" name="P_NEXT_URL" value="https://가맹점 Next_Url" />
    <input type="button” onclick=”formSubmit();” />
</form>
```

#### 2) 1 Transaction 방식의 구성
하기 예제는 1 Transaction 구성에 한한 예제 입니다. (head,body 부 생략)
```html
 <meta http-equiv="Content-Type" content="text/html;charset=euc-kr"/>
<script>
function formSubmit(){
	document.getElementById("form1").submit();
}
</script>
<form id="form1" name="form1" method="post" action="지불수단URL">
    <input type="hidden" name="P_GOODS" value="테스트상품" />
    <input type="hidden" name="P_MID" value="상점아이디" />
    <input type="hidden" name="P_AMT" value="상품가격" />
    <input type="hidden" name="P_OID" value="5124213" />
    <input type="hidden" name="P_EMAIL" value="abc@abc.com" />
    <input type="hidden" name="P_UNAME" value="구매자명" />
    <input type="hidden" name="P_NOTI_URL" value="https://가맹점 Noti_Url" />
    <input type="button" onclick="formSubmit();" />
</form>
```

## 2.4 인증 결과 수신

- 2.4 장은 2 Transaction 을 위한 설명 페이지 입니다.
- 1 Transaction 방식은 [1-1. 연동 Flow장](/mobile01.html) 을 참고하세요.

{% include image.html file="mobile_img06.png" %}

2 Transaction 거래의 경우, [2-1. 결제 요청 페이지작성 - 접속 주소 및 일반필드](/mobile02.html#221-전-지불수단-공통-필드) 에 기재된, P_NEXT_URL 로 인증결과를 전달합니다. 이때 Mobile Web 서비스에서 P_NEXT_URL 로 전달하는 Parameter 는 하기와 같습니다.

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table class="tg" style="table-layout: fixed; width: 100%">
<colgroup>
<col style="width: 15%">
<col style="width: 20%">
<col style="width: 15%">
<col style="width: 50%">
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
    <td class="center-align">P_STATUS</td>
    <td class="center-align">인증상태</td>
    <td class="center-align">String(4)</td>
    <td class="left-align">성공 시 00, 그 외 실패</td>
  </tr>
  <tr>
    <td class="center-align">P_RMESG1</td>
    <td class="center-align">결과메시지</td>
    <td class="center-align">String(10)</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">P_TID</td>
    <td class="center-align">인증거래번호</td>
    <td class="center-align">String(40)</td>
    <td class="left-align">성공시에만 반환</td>
  </tr>
  <tr>
    <td class="center-align">P_REQ_URL</td>
    <td class="center-align">승인요청 Url</td>
    <td class="center-align">String(N/A)</td>
    <td class="left-align">가맹점에서 Mobile Web 서비스로 승인요청을 할 때, 사용되는 Url 입니다. 거래 건 마다 상이한 URL 이 전달됩니다.<code class="language-plaintext highlighter-rouge">따라서, 절대 고정하여 사용하지 마십시오.</code> Http Scheme 은 https 를 사용합니다.<br><code class="language-plaintext highlighter-rouge">보안을 위해 https프로토콜 사용을 통한 통신만 지원하며, https 보안 프로토콜 적용이 불가능한IP 기반의 통신은 제공하지 않습니다.</code></td>
  </tr>
  <tr>
    <td class="center-align">P_NOTI</td>
    <td class="center-align">기타주문정보</td>
    <td class="center-align">String(N/A)</td>
    <td class="left-align">최초 거래 시 주문정보에 P_NOTI 를 설정하셨다면, 그 값을 전달받을 수 있습니다. 이 값은 P_NOTI 값을 그대로 리턴합니다.</td>
  </tr>
  <tr>
    <td class="center-align">P_AMT</td>
    <td class="center-align">거래금액</td>
    <td class="center-align">String(8)</td>
    <td class="left-align">최초 거래 시 주문정보에 설정한 P_AMT 전달(주요 지불수단인 신용카드, 휴대폰, 계좌이체, 가상계좌 등 일부만 전달)</td>
  </tr>
</tbody>
</table>

</div>
</details>

또한, 당사에서 인증결과 송신 시 사용하는 Method 는 post, get 을 선택적으로 사용하오니, 두가지 방식을 모두 수용할 수 있도록 처리 바랍니다.

## 2.5 승인 요청 송신 및 승인 처리 결과 수신

### 2.5.1 승인 요청 송신

>승인요청 및 결과 수신&quot; 이란, 하기의 Step을 의미합니다.

{% include image.html file="mobile_img07.png" %}

<br>

승인요청 시에 사용되는 P_REQ_URL(승인요청 Url) 은 Front-End 단에서 Submit 을 하지 않고, Http-Socket 통신을 통해 Back-End 단으로 요청하셔야 합니다.
당사 P_REQ_URL 은 승인과정을 거친 후, 가맹점의 특정 Url 로 승인결과를 전송하지 않고, 페이지 상에, echo 를 통해 결과를 출력하기만 합니다.
따라서, 승인결과 메시지는 Http-Socket 의 Receive-Data 로 수신받으셔야 합니다. 인증요청을 받은 후, 승인 요청하는 Flow 는 하기의 방식을 참고 하십시오.

<br>

{% include image.html file="mobile_img08.png" %}

<br>

- 승인요청 시, 사용하는 통신 규격은 하기와 같습니다.

<table style="table-layout: fixed; width: 100%; text-align: center">
<colgroup>
<col style="width: 30%;">
<col style="width: 70%;">
</colgroup>
  <thead>
    <tr>
      <th class="center-align">통신수단</th>
      <th class="center-align">통신방식</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">Http-Socket</td>
      <td class="center-align">post</td>
    </tr>
  </tbody>
</table>

- 승인요청 시, 하기의 필드를 반드시 첨부하셔야 합니다.

<table style="table-layout: fixed; width: 100%; text-align: center">
<colgroup>
<col style="width: 30%;">
<col style="width: 25%;">
<col style="width: 55%;">
</colgroup>
  <thead>
    <tr>
      <th class="center-align">필드</th>
      <th class="center-align">필드명</th>
      <th class="center-align">비고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">P_TID</td>
      <td class="center-align">인증거래번호</td>
      <td style="text-align: left">인증결과 수신 시, 포함된 인증거래번호(P_TID)</td>
    </tr>
    <tr>
      <td class="center-align">P_MID</td>
      <td class="center-align">상점아이디</td>
      <td style="text-align: left">거래 시 사용된, 당사발급 아이디</td>
    </tr>
  </tbody>
</table>

- Http-Socket 을 이용한 승인요청의 샘플 코드는 하기와 같습니다.<br>
_( __하기 코드 내 함수는 직접 구현하셔야 합니다__ 하기 코드는 로직안내를 위해 작성된 예시입니다.)_

<script src="https://gist.github.com/paywelcome/14fba8e0b2fba9a4dcb464febc44d439.js"></script>

### 2.5.2 승인 결과 수신

### 승인결과 수신필드 상세 (only 2 Transaction)

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table style="table-layout: fixed; width: 100%; text-align: center">
<colgroup>
<col style="width: 10%;">
<col style="width: 25%;">
<col style="width: 20%;">
<col style="width: 15%;">
<col style="width: 30%;">
</colgroup>
  <thead>
    <tr>
      <th class="center-align">지불수단</th>
      <th class="center-align">필드</th>
      <th class="center-align">필드명</th>
      <th class="center-align">타입</th>
      <th class="center-align">비고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align" rowspan="14">공통</td>
      <td class="center-align">P_STATUS</td>
      <td class="center-align">거래상태</td>
      <td class="center-align">String(4)</td>
      <td class="left-align">성공: 00</td>
    </tr>
    <tr>
      <td class="center-align">P_TID</td>
      <td class="center-align">거래번호</td>
      <td class="center-align">String(40)</td>
      <td class="left-align"></td>
    </tr>
    <tr>
      <td class="center-align">P_TYPE</td>
      <td class="center-align">지불수단</td>
      <td class="center-align">String(10)</td>
      <td class="left-align"></td>
    </tr>
    <tr>
      <td class="center-align">P_TYPE</td>
      <td class="center-align">지불수단</td>
      <td class="center-align">String(N/A)</td>
      <td class="left-align">CARD(ISP,안심클릭,국민앱카드)<br />VBANK(가상계좌)<br />MOBILE(휴대폰)<br />BANK(계좌이체)</td>
    </tr>
    <tr>
      <td class="center-align">P_AUTH_DT</td>
      <td class="center-align">승인일자</td>
      <td class="center-align">String(14)</td>
      <td class="left-align">YYYYmmddHHmmss</td>
    </tr>
    <tr>
      <td class="center-align">P_MID</td>
      <td class="center-align">상점아이디</td>
      <td class="center-align">String(10)</td>
    </tr>
    <tr>
      <td class="center-align">P_OID</td>
      <td class="center-align">상점주문번호</td>
      <td style="center-align">String(100)</td>
      <td></td>
    </tr>
    <tr>
      <td class="center-align">P_AMT</td>
      <td class="center-align">거래금액</td>
      <td style="center-align">String(8)</td>
      <td></td>
    </tr>
    <tr>
      <td class="center-align">P_UNAME</td>
      <td class="center-align">주문자명</td>
      <td style="center-align">String(30)</td>
      <td></td>
    </tr>
    <tr>
      <td class="center-align">P_MNAME</td>
      <td class="center-align">가맹점 이름</td>
      <td class="center-align">String(N/A)</td>
      <td class="left-align">주문정보에 입력한 값 반환</td>
    </tr>
    <tr>
      <td class="center-align">P_RMESG1</td>
      <td class="center-align">메시지1</td>
       <td class="center-align">String(500)</td>
      <td class="left-align">지불 결과 메시지</td>
    </tr>
    <tr>
      <td class="center-align">P_NOTI</td>
      <td class="center-align">주문정보</td>
      <td class="center-align">String(800)</td>
      <td class="left-align">주문정보에 입력한 값 반환</td>
    </tr>
    <tr>
      <td class="center-align">P_NOTEURL</td>
      <td class="center-align">가맹점 전달 NOTI URL</td>
      <td class="center-align">String(N/A)</td>
      <td class="left-align">거래요청 시 입력한 값을 <strong>그대로 반환</strong></td>
    </tr>
    <tr>
      <td class="center-align">P_NEXT_URL</td>
      <td class="center-align">가맹점 전달 NEXT URL</td>
      <td class="center-align">String(N/A)</td>
      <td class="left-align">거래요청 시 입력한 값을 <strong>그대로 반환</strong></td>
    </tr>
     <tr>
     <td class="center-align">신용카드<br>U포인트</td>
      <td class="center-align">P_CARD_NUM</td>
      <td class="center-align">카드번호</td>
      <td class="center-align">String(16)</td>
      <td class="left-align">계약관계에 따라 틀림</td>
    </tr>
     <tr>
     <td class="center-align" rowspan="11">신용카드</td>
      <td class="center-align">P_CARD_ISSUER_CODE</td>
      <td class="center-align">발급사 코드</td>
      <td style="center-align">String(2)</td>
    </tr>
    <tr>
      <td class="center-align">P_CARD_MEMBER_NUM</td>
      <td class="center-align">가맹점번호</td>
      <td class="center-align">String(15)</td>
      <td style="text-align: left">자체 가맹점 일 경우만 해당</td>
    </tr>
    <tr>
      <td class="center-align">P_CARD_PURCHASE_CODE</td>
      <td class="center-align">매입사 코드</td>
      <td class="center-align">String(2)</td>
      <td style="text-align: left">자체 가맹점 일 경우만 해당</td>
    </tr>
    <tr>
      <td class="center-align">P_CARD_PRTC_CODE</td>
      <td class="center-align">부분취소 가능여부</td>
      <td class="center-align">String(1)</td>
      <td style="text-align: left">부분취소가능 : 1 , 부분취소불가능 : 0</td>
    </tr>
    <tr>
      <td class="center-align">P_CARD_INTEREST</td>
      <td class="center-align">무이자 할부여부</td>
      <td class="center-align">String(1)</td>
      <td style="text-align: left">0 : 일반, 1 : 무이자</td>
    </tr>
    <tr>
      <td class="center-align">P_CARD_CHECKFLAG</td>
      <td class="center-align">카드 구분</td>
      <td class="center-align">String(1)</td>
      <td style="text-align: left">0 : 신용카드,1 : 체크카드,2 : 기프트카드</td>
    </tr>
    <tr>
      <td class="center-align">P_RMESG2</td>
      <td class="center-align">메시지2</td>
      <td class="center-align">String(500)</td>
      <td class="left-align">신용카드 할부 개월 수</td>
    </tr>
    <tr>
      <td class="center-align">P_FN_CD1</td>
      <td class="center-align">카드코드</td>
      <td class="center-align">String(4)</td>
      <td style="text-align: left"></td>
    </tr>
    <tr>
      <td class="center-align">P_AUTH_NO</td>
      <td class="center-align">승인번호</td>
      <td class="center-align">String(30)</td>
      <td style="text-align: left">신용카드거래에서만 사용합니다.</td>
    </tr>
    <tr>
      <td class="center-align">P_ISP_CARDCODE</td>
      <td class="center-align">VP 카드코드</td>
      <td class="center-align">String(25)</td>
      <td style="text-align: left"> </td>
    </tr>
    <tr>
      <td class="center-align">P_FN_NM</td>
      <td class="center-align">결제카드사 한글명</td>
      <td class="center-align">String(N/A)</td>
      <td style="text-align: left">BC카드</td>
    </tr>
     <tr>
      <td class="center-align" rowspan="2">계좌이체</td>
      <td class="center-align">P_FN_CD1</td>
      <td class="center-align">은행코드</td>
      <td class="center-align">String(4)</td>
      <td style="text-align: left"></td>
    </tr>
    <tr>
      <td class="center-align">P_FN_NM</td>
      <td class="center-align">결제은행 한글명</td>
      <td class="center-align">String(N/A)</td>
      <td style="text-align: left"></td>
    </tr>
    <tr>
      <td class="center-align" rowspan="3">휴대폰</td>
      <td class="center-align">P_HPP_CORP</td>
      <td class="center-align">휴대폰통신사</td>
      <td class="center-align">String(3)</td>
      <td class="left-align"></td>
    </tr>
    <tr>
      <td class="center-align">P_HPP_NUM</td>
      <td class="center-align">결제 휴대폰 번호</td>
      <td class="center-align">String(11)</td>
      <td style="text-align: left"> </td>
    </tr>
    <tr>
      <td class="center-align">P_HPP_BILLKEY</td>
      <td class="center-align">휴대폰 빌키</td>
      <td class="center-align"></td>
      <td style="text-align: left">휴대폰 빌링 사용시 휴대폰 빌키( 승인은 PAYAPI 통해서 진행)</td>
    </tr>
     <tr>
      <td class="center-align">앱연동<br>결제구분</td>
      <td class="center-align">P_SRC_CODE</td>
      <td class="center-align">앱연동여부</td>
      <td class="center-align">String(3)</td>
      <td style="text-align: left">P : 페이핀<br />K : 국민앱카드<br />C: 페이코<br />B: 삼성페이<br />L: LPAY<br />O: 카카오페이<br />G: SSGPAY</td>
    </tr>
    <tr>
      <td class="center-align" rowspan="9">현금<br>영수증</td>
      <td class="center-align">P_CSHR_CODE</td>
      <td class="center-align">처리상태</td>
      <td class="center-align">String(6)</td>
      <td class="left-align">220000 : 정상, 그 외 : 오류</td>
    </tr>
    <tr>
      <td class="center-align">P_CSHR_MSG</td>
      <td class="center-align">처리메시지</td>
      <td class="center-align">String(N/A)</td>
      <td class="left-align"> </td>
    </tr>
    <tr>
      <td class="center-align">P_CSHR_AMT</td>
      <td class="center-align">현금영수증 총 금액</td>
      <td class="center-align">String(N/A)</td>
      <td class="left-align">총금액 = 공급가액+세금+봉사료</td>
    </tr>
    <tr>
      <td class="center-align">P_CSHR_SUP_AMT</td>
      <td class="center-align">공급가액</td>
      <td class="center-align">String(N/A)</td>
      <td class="left-align"> </td>
    </tr>
    <tr>
      <td class="center-align">P_CSHR_TAX</td>
      <td class="center-align">세금</td>
      <td class="center-align">String(N/A)</td>
      <td class="left-align"> </td>
    </tr>
    <tr>
      <td class="center-align">P_CSHR_SRVC_AMT</td>
      <td class="center-align">봉사료</td>
      <td class="center-align">String(N/A)</td>
      <td class="left-align"> </td>
    </tr>
    <tr>
      <td class="center-align">P_CSHR_TYPE</td>
      <td class="center-align">용도구분</td>
      <td class="center-align">String(1)</td>
      <td class="left-align">0:소득공제용, 1:지출증빙용</td>
    </tr>
    <tr>
      <td class="center-align">P_CSHR_DT</td>
      <td class="center-align">발행시간</td>
      <td class="center-align">String(14)</td>
      <td class="left-align">YYYYMMDDhhmmss</td>
    </tr>
    <tr>
      <td class="center-align">P_CSHR_AUTH_NO</td>
      <td class="center-align">발행번호</td>
      <td class="center-align">String(9)</td>
      <td class="left-align">가상계좌의 경우 입금 완료 시 생성되어 모바일 내 채번시에는 전달되지 않습니다.</td>
    </tr>
  </tbody>
</table>

</div>
</details>

### 가상계좌 수신 필드 및 상세안내

"가상계좌 방식" 과 "계좌이체 방식" 은 입금 통보 등의 과정을 필요로 하기 때문에, 상기에 안내한 방식과 다소 다른 점이 있습니다.
하기에는 가상계좌와 계좌이체에서 각기 사용하는 "인증완료 후, 이동페이지" 와, "입금통보 혹은 승인완료 통보" 방식에 대하여 안내합니다.

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table style="table-layout: fixed; width: 100%; text-align: center">
<colgroup>
<col style="width: 20%;">
<col style="width: 40%;">
<col style="width: 40%;">
</colgroup>
  <thead>
    <tr>
      <th>항목</th>
      <th>인증완료 후 이동 URL(Front단)</th>
      <th>입금사실 통보 URL(Back 단)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>가상계좌</td>
      <td>P_NEXT_URL(인증결과송신)</td>
      <td>P_NOTI_URL(채번정보송신, 입금완료송신)</td>
    </tr>
  </tbody>
</table>

</div>
</details>

하기에는 호출 된, P_NEXT_URL 에 전달될 파라미터 입니다.

([2.5.2 승인결과 수신필드 상세 (only 2 Transaction) 의 공통 필드](/mobile02.html#승인결과-수신필드-상세-only-2-transaction) )외 하기필드

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table style="table-layout: fixed; width: 100%; text-align: center">
<colgroup>
<col style="width: 30%;">
<col style="width: 25%;">
<col style="width: 15%;">
<col style="width: 40%;">
</colgroup>
  <thead>
    <tr>
      <th class="center-align">필드</th>
      <th class="center-align">필드명</th>
      <th class="center-align">타입</th>
      <th style="text-align: left">비고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">P_VACT_NUM</td>
      <td class="center-align">입금할 계좌 번호</td>
      <td class="center-align">String(20)</td>
      <td class="left-align"></td>
    </tr>
    <tr>
      <td class="center-align">P_VACT_DATE</td>
      <td class="center-align">입금마감일자</td>
      <td class="center-align">String(8)</td>
      <td class="left-align">yyyymmdd</td>
    </tr>
    <tr>
      <td class="center-align">P_VACT_TIME</td>
      <td class="center-align">입금마감시간</td>
      <td class="center-align">String(6)</td>
      <td class="left-align">hhmmss</td>
    </tr>
    <tr>
      <td class="center-align">P_VACT_NAME</td>
      <td class="center-align">계좌주명</td>
      <td class="center-align">String(18)</td>
      <td class="left-align"> </td>
    </tr>
    <tr>
      <td class="center-align">P_VACT_BANK_CODE</td>
      <td class="center-align">채번은행코드</td>
      <td class="center-align">String(2)</td>
      <td class="left-align"> <a href="/code02.html#26-카드-발급사은행-코드"><strong>[참조-카드 발급사(은행) 코드]</strong></a></td>
    </tr>
  </tbody>
</table>

</div>
</details>

P_NOTI_URL로 전송되는 승인결과는 하단의 노티 수신 사용법 안내에 대한 내용을 참고 바랍니다.
_가상계좌 Flow_ 는 하기와 같습니다.

{% include image.html file="mobile_img09.png" %}

가상계좌는 상기와 같이 채번 시 1회, 입금 확인 후 1회, 총 2회 노티를 통해 통보합니다.

상기에 안내한 바와 같이, 가상계좌 방식과 계좌이체 방식, 그리고 기타 방식(신용카드 등) 의 차이점이 있사오니, 이점 유의 하시기 바랍니다.



### 2.5.3 1 Transaction 방식에서 결제 완료 후 결과 수신

P_NOTI_URL 로 전송되는 파라미터 및 값은 하단의 노티 수신 사용방법 안내 내용을 참고하여 주시기 바랍니다.

-  <img class="emoji" title=":warning:" alt=":warning:" src="https://github.githubassets.com/images/icons/emoji/unicode/26a0.png"><code class="language-plaintext highlighter-rouge">P_NOTI_URL은 네트워크 사정에 따라 1회 이상 발생될 수 있사오니, 중복호출여부를 체크하는 루틴을 반드시 구현하십시오.</code>
-  NOTI 를 통한 결과 송신은 하기의 조건에 따라 수행됩니다.<br>
   24시간 이내 재전송 가능 | 24시간 이후 시퀀스 종료 | 재전송 주기 약 10분


### 2.5.4 P_NOTI_URL 수신 후, 처리방법

당사 Back 단에서 전송된 Noti 는 하기의 조건을 충족하지 않을 경우, 재전송 루틴을 수행하게 됩니다.
따라서, ([2.5.3.1 Transaction 방식에서 결제 완료 후 결과 수신](/mobile02.html#253-1-transaction-방식에서-결제-완료-후-결과-수신))장에서 안내한 바와 같이 중복체크 루틴을 반드시 구현하시고, 하기의 조건을 충족하여 주시기 바랍니다.

- Noti 수신 후, P_NOTI_URL 에 OK 만 출력 요망.

- <span style="color:red;">대문자 OK 외 html 및 공백, 개행문자 불허<span style="color:red;">

## 2.6 안드로이드 / IOS 연동

### 2.6.1 기본적인 설치방법

### 안드로이드
>안드로이드 어플리케이션 내 WebView (이하 WebView) 에서 Mobile Web 서비스를 구현하는 경우에 해당됩니다.<br>
Mobile Web 서비스를 WebView 내에 구현하는 경우, 발생할 수 있는 Encoding Issue 는 ( [3.2.2 부록-주의사항 &lt;UrlEncode issue&gt;](/mobile03.html#322-urlencode-issue) ) 를 참조하셔 주십시오.<br>
WebView 에서 Mobile Web 서비스를 띄우는 방식은 앞 장에서 설명한 ([1.기본적인 설치 방법](/mobile01.html) 의 방법과 동일합니다.<br>
이에 이번 장 에서는 ISP 앱 호출 시 주의사항, 카드사 백신 앱 스키마 호출 및 &quot;미설치 시, 앱스토어 이동 이슈&quot; 등의 내용을 주로 다룹니다.<br>

### ISO
>IOS 어플리케이션 내 WebView (이하 WebView) 에서 Mobile Web 서비스를 구현하는 경우에 해당됩니다.<br>
Mobile Web 서비스를 WebView 내에 구현하는 경우, 발생할 수 있는 Encoding Issue 는 ( [3.2.2 부록-주의사항 &lt;UrlEncode issue&gt;](/mobile03.html#322-urlencode-issue) ) 를 참조하셔 주십시오.<br>
WebView 에서 Mobile Web 서비스를 띄우는 방식은 앞 장에서 설명한 ([1.기본적인 설치 방법](/mobile01.html)) 의 방법과 동일합니다. 이에 이번 장 에서는 ISP 앱 호출 시 주의사항, 카드사 백신 앱 스키마 호출 및 &quot;미설치 시, 앱스토어 이동 이슈&quot; 등의 내용을 주로 다룹니다.

### 2.6.2 ISP 연동방법 (안드로이드)

### 앱 미설치 체크로직 직접구현 or 자동체크
- ISP 앱의 기본정보는 하기와 같습니다.

<table style="width: 100%;">
<colgroup>
  <col style="width: 30%;">
  <col style="width: 70%;">
</colgroup>
  <thead>
    <tr>
      <th class="center-align">Application Scheme</th>
      <th class="center-align">InstallUrl</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">ispmobile://</td>
      <td class="center-align">http://mobile.vpay.co.kr/jsp/MISP/andown.jsp</td>
    </tr>
  </tbody>
</table>

- 상기 Scheme 과 Install Url 정보로 구현가능한 안드로이드 코드는 하기와 같습니다.

**1)** WebViewClient 를 상속받은 클래스를 구현하시고, shouldOverrideUrlLoading() 을 호출 하십시오.

```java
private class INIP2PWebView extends WebViewClient {
    @Override     
    public boolean shouldOverrideUrlLoading(WebView view, String url) {
    ….
    }
```
**2)** 상기 shouldOverrideUrlLoading() 함수 내에, try{} catch{e} 를 통해, try 내에서는 startActivity(intent) 를 구현하시고, catch Event 발생 시, 앱 스토어로 이동할 수 있도록 조치하시면 됩니다. 하기에 안내되는 소스는 상기 방식에 대한 Full-Source 입니다.<br/>

#### [shouldOverrideUrlLoading 부]

<script src="https://gist.github.com/paywelcome/2dc5e80c26a09944b1298ae8ba915a07.js"></script>

<p style="font-size: 80%"> [ISP 앱스토어 이동처리 부] - alertIsp</p>

<script src="https://gist.github.com/paywelcome/4a26f9d2c478d4d95735bb26da35f077.js"></script>

**3)** ISP 가 단말기에 기 설치되어 있는 경우, ISP 가 정상구동 됩니다.<br/>
**4)** ISP 가 단말기에 미 설치되어 있는 경우, 설치 후, Mobile Web 서비스를 다시 띄워주시면 됩니다.<br>
   예시[shouldOverrideUrlLoading 부](/mobile02.html#shouldoverrideurlloading-부) 의 에 대하여 true 혹은 false 를 설정하는 것은 하기의 표를 참고하십시요.

<table style="width: 100%;">
<colgroup>
  <col style="width: 15%">
  <col style="width: 30%">
  <col style="width: 30%">
  <col style="width: 25s%">
</colgroup>
  <thead>
    <tr>
      <th class="center-align">apprun_check</th>
      <th class="center-align">작동방식</th>
      <th class="center-align">앱 미설치 시, 앱스토어 이동 후<br>결제페이지 잔존여부</th>
      <th class="center-align">true / false 설정</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">Y</td>
      <td class="center-align">ISP,  계좌이체앱<br>- intent  작동</td>
      <td class="center-align">상태 유지</td>
      <td class="center-align">true</td>
    </tr>
    <tr>
      <td class="center-align">N or  미설정</td>
      <td class="center-align">ISP,  계좌이체앱<br>- appScheme  작동</td>
      <td class="center-align">하기 [그림 1]  과 같이  Display  됨</td>
      <td class="center-align">false</td>
    </tr>
  </tbody>
</table>

- [shouldOverrideUrlLoading 부](/mobile02.html#shouldoverrideurlloading-부) 의 ①을 true 로 할 경우, Mobile Web 서비스를 띄운 WebView 는 사라집니다.
  따라서, app Scheme 형태로 결제 앱을 호출할 경우에는 &quot;그림 1&quot; 과 같이 오류 페이지가 Display 되기 때문에, WebView 를 remove 하는 것이 좋습니다.

{% include image.html file="mobile_img10.jpg" %}
[그림1]

- [shouldOverrideUrlLoading 부](/mobile02.html#shouldoverrideurlloading-부) 의 ①을 false 로 할 경우, Mobile Web 서비스를 띄운 WebView 는 사라지지 않기 때문에,
  apprun_check=Y 를 통해 현 결제 페이지가 유지되는 방식을 사용 하는 것이 좋습니다. 이 방법을 자동체크방식이라 합니다.
- 단, apprun_check 옵션을 통해 설치체크로직이 작동되므로, alertIsp 함수는 구현될 필요가 없습니다.
  apprun_check 로직에 대하여 상세히 확인하시려면 ( [2.2.6 결제 요청 페이지작성 - 복합필드](/mobile02.html#226-복합-필드-p_reserved) ) 를 확인하여 주십시오. 또한, Intent 호출에 대하여 예외처리를 반드시 체크하셔야 합니다.

### 인증결과 전송

- ISP 앱에서 인증과정이 완료되면, 다시 당사 모바일 결제창으로 돌아와서 하기의 이미지와 같이 &#39;확인&#39; 버튼을 클릭해야, 승인과정을 시작하게 됩니다.

- 안드로이드는 운영체제 특성 상, 현재 앱이 종료될 경우, 이 앱을 실행시킨 이전 앱이 다시 자동으로 수행됩니다.
  (LIFO 방식) 따라서, ISP 앱이 종료되면, 가맹점의 앱은 자동으로 다시 활성화될 것입니다.


### 2.6.3 ISP 연동방법 (IOS)

### 신용카드 ISP, 계좌이체 연동방법
- 신용카드 ISP 및 계좌이체 앱이 종료 된 뒤, 가맹점 앱을 다시 띄우기 위한 조치사항을 안내합니다.
- IOS 는 Android 계열과 다르게도 ISP 및 계좌이체 앱이 종료된 뒤, 가맹점 앱은 Background 에 머문 채, 바탕화면이 개제됩니다.
  (IOS의 운영체제 특성에 기반) 이 때문에, 결제 앱이 종료되면서, 가맹점 appScheme 을 호출하도록 구성해야 합니다. 하기와 같이 셋팅 시, 요구사항과 같이 가맹점 앱이 다시 기동 됩니다. ( 신용카드, 계좌이체 동기옵션 사용시에만 설정 가능)

<table style="width: 100%;">
<colgroup>
  <col style="width: 45%;">
  <col style="width: 55%;">
</colgroup>
  <thead>
    <tr>
      <th class="center-align">신용카드</th>
      <th class="center-align">계좌이체</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align"><code class="language-plaintext highlighter-rouge">P_RESERVED=app_scheme=가맹점스키마명://</code></td>
      <td class="center-align">
<code class="language-plaintext highlighter-rouge">P_RESERVED=iosapp=Y&amp;app_scheme=가맹점스키마명://</code><br> <code class="language-plaintext highlighter-rouge">P_RETURN_URL=가맹점스키마명://</code>
</td>
    </tr>
  </tbody>
</table>

- P_RESERVED 옵션에 대한 설명은 ([2.2.6 결제 요청 페이지작성 - 복합필드](/mobile02.html#226-복합-필드-p_reserved)) 를 참조 부탁 드립니다.<br>
  더불어 상기 옵션 셋팅 시, 가맹점스키마명 뒤 ://은 필수로 입력해 주셔야 ISP 앱 종료 후 가맹점 앱이 호출 됩니다.<br>
  (Ex. 가맹점 스키마명이 WelcomeMobile일 경우 app_scheme=WelcomeMobile:// 로 셋팅 해 주시면 됩니다.)

### 2.6.4 안심클릭 결제 시, 카드사 백신 앱 연동
### 안드로이드
- Mobile Web 서비스는 BC 계열을 제외한, 나머지 카드사의 결제창은 카드사 페이지에서 결제가 이루어지고 있습니다.
  이에, 카드사에서 개별적으로 사용하는 백신 앱의 경우, 가맹점 앱에서도 하기의 유의사항을 반드시 체크하셔야 합니다.

1. WebView 내에서 http와 https URL, 그리고 App Url 을 분기하여 처리해야 함.
2. shouldOverrideUrlLoading() 처리로직을 하기와 같이 구현함.

<table style="width: 100%">
<colgroup>
  <col style="width: 50%">
  <col style="width: 50%">
</colgroup>
  <thead>
    <tr>
      <th class="center-align">App Url  일 경우</th>
      <th class="center-align">Web Url 일 경우</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">activity 호출</td>
      <td class="center-align">WebView 에서 Loading</td>
    </tr>
  </tbody>
</table>

상기의 유의사항을 고려한 샘플 코드는 하기와 같습니다. (_Kitkat_ _이하 정상구동여부 확인됨_)

<details style="cursor:pointer;">
<summary><strong>[&nbsp;상세보기&nbsp;]</strong></summary>
<div markdown="1">

<script src="https://gist.github.com/paywelcome/22184803212ce6b83acd4651d8fe87c3.js"></script>

</div>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             
</details>


### IOS

- IOS 환경에서는 카드사에서 별도로 백신을 구동하지 않습니다. 따라서, 해당 부분은 체크하실 부분이 없습니다.

### 2.6.5 결제 금액이 30 만원 이상일 때의 공인인증 앱 연동 방법 

### 안드로이드

- 만약 상점에서의 판매가격이 30만원 이상일 수 있고 카드로 결제할 경우, 사용자는 공인인증서 서명과정을 거쳐야 합니다.<br>
- 안드로이드의 경우, 개별 카드사 앱에서 공인인증서 서명을 할 수 있습니다. 이에, 카드사 창 내에서 호출하는 intent 혹은 app Scheme 를 허용할 수 있도록 가맹점 앱에서 처리해줘야 합니다.<br>이는 (3.B . 안심클릭 결제 시, 카드사 백신 앱 연동)의 코드를 반영하면 해결됩니다.

### 2.6.6 앱 환경 별 체크사항

#### Android API Level 21  이상 일 때
- Android API Level 21 (Lollipop 출시 때 배포) 부터는 webview 에서 Insecurity Page 에 대한 Access 및 Mixed contents, Third party cookies 사용을 차단할 수 있게 업데이트 되었습니다.
  먼저, Insecurity Page 에 대한 Access 차단으로 P_NEXT_URL 의 Scheme 을 Http 로 하는 경우, 페이지가 호출되지 않아 인증결과가 전달되지 않을 수 있습니다.
  하기의 설정을 확인하십시오.

<table style="width: 100%">
<colgroup>
  <col style="width: 30%">
  <col style="width: 70%">
</colgroup>
  <thead>
    <tr>
      <th>상태</th>
      <th>코드</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">Insecurity  페이지 차단</td>
      <td><code class="language-plaintext highlighter-rouge">WebSettings web = paymentView.getSettings(); web.setMixedContentMode(web.MIXED_CONTENT_NEVER_ALLOW);</code></td>
    </tr>
    <tr>
      <td class="center-align">Insecurity  페이지 허용</td>
      <td><code class="language-plaintext highlighter-rouge">WebSettings web = paymentView.getSettings(); web.setMixedContentMode(web.MIXED_CONTENT_ALWAYS_ALLOW);</code></td>
    </tr>
  </tbody>
</table>

- P_NEXT_URL 의 Scheme 이 Http 일 경우, 반드시 &quot;Insecurity 페이지 허용&quot; 으로 설정되어야 합니다.
  또한, Third party cookies 사용의 차단으로 안심클릭 카드 결제 시, 보안 키보드를 불러오지 못 하는 이슈 등이 발생할 수 있으니 하기 설정을 확인하십시오.

<table style="width: 100%">
<colgroup>
  <col style="width: 40%">
  <col style="width: 60%">
</colgroup>
  <thead>
    <tr>
      <th>상태</th>
      <th>코드</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">Third party cookies  허용</td>
      <td>
<code class="language-plaintext highlighter-rouge">CookieManager cookieManager = CookieManager.getInstance();<br>cookieManager.setAcceptCookie(true);<br>cookieManager.setAcceptThirdPartyCookies(sampleWebView, true);</code><br> // false 설정 시 오류 발생</td>
    </tr>
  </tbody>
</table>

#### IOS9 버전 Application 구현 시

- IOS9 업데이트 이후, APP 내 보안정책 강화로 canOpenUrl 또는 openUrl 함수 사용 시, info.plist 파일에 LSApplicationQueriesSchemes 배열을 정의하여 호출할 App scheme list를 등록 해주셔야 합니다. (White List 등록)
  아래는 LSApplicationQueriesSchemes 등록 예시이며, 기존 앱 스키마에서 `://` 부분을 제거 후, 등록하시면 됩니다.

예시 1. XCODE info.plist
```javascript
<key> LSApplicationQueriesSchemes </key>
     <array>
<string> fbapi </string>
<string> fbauth2 </string>
<string> fbshareextension </string>
<string> fb-messenger-api </string>
<string> twitter </string>
<string> whatsapp </string>
<string> wechat </string>
<string> line </string>
<string> instagram </string>
<string> kakaotalk </string>
<string> mqq </string>
<string> vk </string>
<string> mqq </string>
     </array>
```

예시 2. XML info.plist

- 아래 MOBILETX 에서 사용 중인 Custom Scheme List를 참고하셔서 지불수단 별, 필요한 부분사용 바랍니다.

&lt;2021.09.06 Custom Scheme List&gt;

#### Custom Scheme List (지불수단 : 신용카드)

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table style="width: 100%;">
<colgroup>
  <col style="width: 40%;">
  <col style="width: 60%;">
</colgroup>
  <thead>
    <tr>
      <th>App</th>
      <th>custom scheme</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">신한 앱카드</td>
      <td><code class="language-plaintext highlighter-rouge">shinhan-sr-ansimclick://</code></td>
    </tr>
    <tr>
      <td class="center-align">신한 공인인증 앱<br>( 일반결제 )</td>
      <td><code class="language-plaintext highlighter-rouge">smshinhanansimclick://</code></td>
    </tr>
    <tr>
      <td class="center-align">현대 앱카드</td>
      <td><code class="language-plaintext highlighter-rouge">hdcardappcardansimclick://</code></td>
    </tr>
    <tr>
      <td class="center-align">현대 공인인증 앱<br>( 일반결제 )</td>
      <td><code class="language-plaintext highlighter-rouge">smhyundaiansimclick://</code></td>
    </tr>
    <tr>
      <td class="center-align">삼성 앱카드</td>
      <td><code class="language-plaintext highlighter-rouge">mpocket.online.ansimclick://</code></td>
    </tr>
    <tr>
      <td class="center-align">삼성 공인인증 앱<br>( 일반결제 )</td>
      <td><code class="language-plaintext highlighter-rouge">scardcertiapp://</code></td>
    </tr>
    <tr>
      <td class="center-align">하나 앱카드</td>
      <td><code class="language-plaintext highlighter-rouge">cloudpay://</code></td>
    </tr>
    <tr>
      <td class="center-align">하나 공인인증 앱<br>( 일반결제 )</td>
      <td><code class="language-plaintext highlighter-rouge">hanaskcardmobileportal://</code></td>
    </tr>
    <tr>
      <td class="center-align">농협 공인인증 앱<br>( 일반결제 )</td>
      <td><code class="language-plaintext highlighter-rouge">nonghyupcardansimclick://</code></td>
    </tr>
    <tr>
      <td class="center-align">국민 앱카드</td>
      <td><code class="language-plaintext highlighter-rouge">kb-acp://</code></td>
    </tr>
    <tr>
      <td class="center-align">롯데 앱카드</td>
      <td><code class="language-plaintext highlighter-rouge">lotteappcard://</code></td>
    </tr>
    <tr>
      <td class="center-align">롯데 스마트 페이</td>
      <td><code class="language-plaintext highlighter-rouge">lottesmartpay://</code></td>
    </tr>
    <tr>
      <td class="center-align">KPAY</td>
      <td><code class="language-plaintext highlighter-rouge">kpay://</code></td>
    </tr>
    <tr>
      <td class="center-align">ISP</td>
      <td><code class="language-plaintext highlighter-rouge">ispmobile://</code></td>
    </tr>
    <tr>
      <td class="center-align">PayPin</td>
      <td><code class="language-plaintext highlighter-rouge">paypin://</code></td>
    </tr>
    <tr>
      <td class="center-align">PAYCO</td>
      <td><code class="language-plaintext highlighter-rouge">payco://</code></td>
    </tr>
    <tr>
      <td class="center-align">Syrup 앱카드</td>
      <td><code class="language-plaintext highlighter-rouge">tswansimclick://</code></td>
    </tr>
    <tr>
      <td class="center-align">농협 앱카드<br>(  올원페이 )</td>
      <td><code class="language-plaintext highlighter-rouge">nhallonepayansimclick://</code></td>
    </tr>
    <tr>
      <td class="center-align">씨티 앱카드</td>
      <td><code class="language-plaintext highlighter-rouge">citimobileapp://</code></td>
    </tr>
    <tr>
      <td class="center-align">LPAY LPOINT</td>
      <td><code class="language-plaintext highlighter-rouge">lpayapp:// lmslpay://</code></td>
    </tr>
    <tr>
      <td class="center-align">카카오페이</td>
      <td><code class="language-plaintext highlighter-rouge">kakaotalk://</code></td>
    </tr>
    <tr>
      <td class="center-align">SSGPAY</td>
      <td><code class="language-plaintext highlighter-rouge">shinsegaeeasypayment://</code></td>
    </tr>
    <tr>
      <td class="center-align">우리 WON 카드</td>
      <td><code class="language-plaintext highlighter-rouge">com.wooricard.wcard://</code></td>
    </tr>
    <tr>
      <td class="center-align">Liiv(KB국민은행)</td>
      <td><code class="language-plaintext highlighter-rouge">liivbank://</code></td>
    </tr>
    <tr>
      <td class="center-align">토스뱅크 ( 하나카드 )</td>
      <td><code class="language-plaintext highlighter-rouge">supertoss://</code></td>
    </tr>
    <tr>
      <td class="center-align">KB 국민은행  Liiv Reboot</td>
      <td><code class="language-plaintext highlighter-rouge">newliiv://</code></td>
    </tr>
    <tr>
      <td class="center-align">우리  WON  뱅킹</td>
      <td><code class="language-plaintext highlighter-rouge">NewSmartPib://</code></td>
    </tr>
  </tbody>
</table>

</div>
</details>

### 2.6.7 카드사 앱 연동 방법

### IOS

- 안심클릭 결제 진행에 필요한 Application (앱카드 등의) 호출이 필요할 경우 아래 샘플코드를 참고 바랍니다.

<table style="width: 100%;">
<colgroup>
  <col style="width: 45%;">
  <col style="width: 55%;">
</colgroup>
  <thead>
    <tr>
      <th class="center-align">주 문 정 보</th>
      <th class="center-align">앱 내 소스</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align"><a href="/mobile02.html#226-복합-필드-p_reserved">[(결제 요청 페이지작성 - 복합필드)</a> 내 참조</td>
      <td class="center-align">하기 샘플 참조</td>
    </tr>
  </tbody>
</table>

<details style="cursor:pointer;">
<summary><strong>[&nbsp;상세보기&nbsp;]</strong></summary>
<div markdown="1">

<script src="https://gist.github.com/paywelcome/c3638db97912e0eda559feaedeb11d7f.js"></script>

</div>
</details>

- 해당 샘플은 참고용으로 각 가맹점 앱에 맞게 구현하시면 됩니다.
- 또한, 하기의 조건을 충족하는 경우에 결제가 가능하오니, 이점 유의 바랍니다.

    1. 고객 단말기의 OS 버전이 4.x 이상인 경우
    2. 가맹점 Application 이 Multi switching 이 지원되는 경우
    3. OS 버전이 9.x 이상일 경우 하기 &#39;[2.7.6 IOS9 버전 Application 구현 시, 주의 사항](/mobile02.html#276-ios9-버전-application-구현-시-주의-사항)&#39; 내용을 참고 바랍니다.

### 2.6.8 쿠키 설정

### IOS

Mobile Web 서비스를 IOS WebView 에서 호출하고, 안심클릭 계열 서비스를 사용하는 경우,<br>
세션만료 오류경고가 발생할 수 있습니다. 이에, 하기의 샘플과 같이 쿠키를 허용해야 합니다.

<script src="https://gist.github.com/paywelcome/098accb2576a71ce69a5c83532bdcdcc.js"></script>

## 2.7 에스크로 결제

>Mobile Web 서비스 화면에서, 에스크로 서비스를 호출하는 옵션입니다.<br>
>배송 등록, 결제 취소, 거절 확인은 PAYAPI 모듈로 진행되므로 (배포본)PAYAPI 연동메뉴얼과 함께 참고하여 개발 진행 부탁드립니다.<br>
>가맹점에서 거래에 따라 일반 결제와 에스크로 결제의 구분 결제를 희망하시면 에스크로로 신규 또는 전환계약이 필요합니다. (단, 일부 호스팅 가맹점은 신 에스크로 설정에, 제한이 있을 수 있음)<br>
>에스크로 계약에 문의가 있거나 자세한 사항은 계약 담당자에게 문의하여 주시기 바랍니다.

### 2.7.1 에스크로 사용가능 지불수단

- 신용카드
- 계좌이체
- 가상계좌

**※ 에스크로 결제 진행 시에는 당사에서 제공하는 간편결제는 사용 불가합니다.**
**(카드사 결제 창 내 제공하는 간편결제가 아닌 당사 결제페이지 내 노출되는 부분에 한함)**

#### A. 설정 방법

- 매뉴얼 결제창 [2.2.6 결제 요청 페이지작성 - 복합필드](/mobile02.html#226-복합-필드-p_reserved)섹션을 보면, P_RESERVED 파라미터 항목이 있습니다.
  참고 하시어, 동일하게 상위의 옵션을 설정하시면 됩니다.

>예) `<INPUT type=”hidden” name=”P_RESERVED” value=”useescrow=Y”/> `

### 2.7.2 에스크로 구매결정 연동

- 모바일 결제창을 통한 에스크로 구매결정 연동을 안내합니다.
  가맹점 페이지내에 구매결정 버튼을 클릭하여 에스크로 구매결정 창이 호출되도록 구현하시면 됩니다.

[구매결정 요청 URL]
<table style="width: 100%;">
<colgroup>
  <col style="width: 20%;">
  <col style="width: 20%;">
  <col style="width: 60%;">
</colgroup>
<tbody>
  <tr>
    <th rowspan="2">HOST</th>
    <td>테스트</td>
    <td>tmobile.paywelcome.co.kr</td>
  </tr>
  <tr>
    <td>운영</td>
    <td>mobile.paywelcome.co.kr</td>
  </tr>
  <tr>
    <th>에스크로</th>
    <td>구매결정</td>
    <td>https://{HOST}/smart/escrow_confirm/</td>
  </tr>
  <tr>
    <td colspan="3">ex) 에스크로 구매결정 연동 시 :<br>https://mobile.paywelcome.co.kr/smart/escrow_confirm/</td>
  </tr>
</tbody>
</table>

#### [구매결정 요청 파라미터]

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table style="width: 100%;">
<colgroup>
  <col style="width: 30%;">
  <col style="width: 15%;">
  <col style="width: 15%;">
  <col style="width: 40%;">
</colgroup>
  <thead>
    <tr>
      <th class="center-align">필드</th>
      <th class="center-align">타입</th>
      <th class="center-align">필수</th>
      <th>비고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">P_MID</td>
      <td class="center-align">String(10)</td>
      <td class="center-align">○</td>
      <td>주문요청시 사용한 P_MID</td>
    </tr>
    <tr>
      <td class="center-align">P_ESCROW_TID</td>
      <td class="center-align">String(40)</td>
      <td class="center-align">○</td>
      <td>에스크로 결제 승인 TID</td>
    </tr>
    <tr>
      <td class="center-align">P_NEXT_URL</td>
      <td class="center-align">String(800)</td>
      <td class="center-align">○</td>
      <td>결과수신 URLhttps(http)가 포함된 전체 URL이며, URL내 get 방식의 파라미터는 사용불가 합니다.</td>
    </tr>
    <tr>
      <td class="center-align">P_NEXT_URL_TAGET</td>
      <td class="center-align">String(10)</td>
      <td class="center-align">○</td>
      <td>결과 수신 URL선택 값 : socket, get, post(미입력 시 기본값:socket)<br>get,post 방식은 완료 후 가맹점 페이지로 해당 방식으로 전환되며, socket 방식은 NOTI로 해당 값을 통보하여, 사용자페이지는 닫힙니다.</td>
    </tr>
    <tr>
      <td class="center-align">P_RESERVED</td>
      <td class="center-align">String(100)</td>
      <td class="center-align">X</td>
      <td>복합파라미터정보P_RESERVED=escrow_purchase_opt=vertify(구매확인버튼만 표시) P_RESERVED=escrow_purchase_opt=deny(구매거절버튼만 표시)옵션 미지정 시 구매확인/거절 모두 표시</td>
    </tr>
  </tbody>
</table>

</div>
</details>

#### [구매결정 응답 파라미터]

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table style="width: 100%;">
<colgroup>
  <col style="width: 30%">
  <col style="width: 30%">
  <col style="width: 40%">
</colgroup>
  <thead>
    <tr>
      <th class="center-align">필드</th>
      <th class="center-align">필드명</th>
      <th class="center-align">비고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">P_ESCROW_TID</td>
      <td class="center-align">전달된 에스크로 TID</td>
      <td> </td>
    </tr>
    <tr>
      <td class="center-align">P_CL_STATUS</td>
      <td class="center-align">구매결정/구매거절여부</td>
      <td>buyComplete / denyComplete</td>
    </tr>
    <tr>
      <td class="center-align">P_STATUS</td>
      <td class="center-align">상태값</td>
      <td>구매결정, 구매거절에 대한 코드값(하단 코드표 참조)</td>
    </tr>
    <tr>
      <td class="center-align">P_RMESG1</td>
      <td class="center-align">처리결과메세지</td>
      <td>urlEncode 전달</td>
    </tr>
    <tr>
      <td class="center-align">P_PG_IP</td>
      <td class="center-align">처리된 승인서버 IP</td>
      <td> </td>
    </tr>
  </tbody>
</table>

</div>
</details>

### 2.7.3 에스크로 상태변경 노티 수신

에스크로 주요 시점(예&gt;구매자가 구매결정을 완료 등)에 가맹점 측으로 해당 내역을 통보해주는 기능입니다. 상점 측에서는 정상수신 여부를 응답(NOTI CONFIRM)하여야합니다.<br>
해당 기능을 이용하려면 계약 담당자를 통해, 수신 받을 상점 측 URL을 등록하셔야 합니다.<br>

-지불수단별, 승인요청 시점의 주문번호를 기준으로 응답하며, 배송등록 시점에 사용되는 주문번호와 동일하게 설정을 권장합니다.
-거래금액은 에스크로 상태에 따라 거래취소 시에는 취소금액, 그 외는 승인 금액입니다.
-원거래TID는 부분취소거래만 설정됩니다.

[노티발송 웰컴페이먼츠 &gt; 가맹점]

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table style="width: 100%">
<colgroup>
  <col style="width: 20%;">
  <col style="width: 20%;">
  <col style="width: 15%;">
  <col style="width: 45%;">
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
      <td class="center-align">id_merchant</td>
      <td class="center-align">상점아이디</td>
      <td class="center-align">String(10)</td>
      <td class="left-align">P_MID로 전달한 값</td>
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
      <td class="left-align">승인 시 전달된 TID</td>
    </tr>
    <tr>
      <td class="center-align">cl_status</td>
      <td class="center-align">에스크로 상태</td>
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
      <td class="center-align">원거래 거래번호</td>
      <td class="center-align">String(40)</td>
      <td class="left-align">부분취소시 원거래 거래번호</td>
    </tr>
  </tbody>
</table>

</div>
</details>

[노티응답 가맹점 > 웰컴페이먼츠]

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table style="width: 100%;">
<colgroup>
  <col style="width: 20%;">
  <col style="width: 20%;">
  <col style="width: 15%;">
  <col style="width: 45%;">
</colgroup>
  <thead>
    <tr>
      <th class="center-align">파라미터</th>
      <th class="center-align">설명</th>
      <th class="center-align">타입</th>
      <th class="center-align">비고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">cd_rslt</td>
      <td class="center-align">결과코드</td>
      <td class="center-align">String(4)</td>
      <td class="left-align">0000:정상처리, 9999:처리실패</td>
    </tr>
    <tr>
      <td class="center-align">msg_rslt</td>
      <td class="center-align">결과메세지</td>
      <td class="center-align">String(1000)</td>
      <td class="left-align">처리실패 시 상세 오류 메세지</td>
    </tr>
  </tbody>
</table>

</div>
</details>

### 2.7.4 에스크로 관련 코드

[구매결정 상태별 코드]

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table style="width: 100%;">
<colgroup>
  <col style="width: 30%;">
  <col style="width: 70%;">
</colgroup>
  <thead>
    <tr>
      <th class="center-align">P_STATUS</th>
      <th class="center-align">P_RMESGI</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">00</td>
      <td class="center-align">정상처리완료</td>
    </tr>
    <tr>
      <td class="center-align">00</td>
      <td class="center-align">기 구매거절 거래</td>
    </tr>
    <tr>
      <td class="center-align">310004</td>
      <td class="center-align">결제 기통보 거래</td>
    </tr>
    <tr>
      <td class="center-align">310006</td>
      <td class="center-align">취소 불가 지불수단</td>
    </tr>
    <tr>
      <td class="center-align">310014</td>
      <td class="center-align">기 구매확인 거래</td>
    </tr>
    <tr>
      <td class="center-align">310015</td>
      <td class="center-align">구매확인 불가 거래상태</td>
    </tr>
    <tr>
      <td class="center-align">310017</td>
      <td class="center-align">구매거절 불가 거래상태</td>
    </tr>
    <tr>
      <td class="center-align">310020</td>
      <td class="center-align">구매결정 할 수 없는 상태</td>
    </tr>
    <tr>
      <td class="center-align">310026</td>
      <td class="center-align">원거래 없음</td>
    </tr>
  </tbody>
</table>

</div>
</details>

[거래 상태별 응답]

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table style="width: 100%;">
<colgroup>
  <col style="width: 15%;">
  <col style="width: 25%;">
  <col style="width: 15%;">
  <col style="width: 30%;">
  <col style="width: 15%;">
</colgroup>
  <thead>
    <tr>
      <th class="center-align">기존상태</th>
      <th class="center-align">처리 요청 상태</th>
      <th class="center-align">P_STATUS</th>
      <th class="center-align">P_CL_STATUS</th>
      <th class="center-align">P_RMESG1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">미정</td>
      <td class="center-align">구매결정 성공</td>
      <td class="center-align">00</td>
      <td class="center-align">buyComplete</td>
      <td class="center-align">정상처리완료</td>
    </tr>
    <tr>
      <td class="center-align">미정</td>
      <td class="center-align">구매결정실패, 구매거부실패</td>
      <td class="center-align">에러코드</td>
      <td class="center-align">buyComplete, denyComplete</td>
      <td class="center-align">에러메세지, 가변적</td>
    </tr>
    <tr>
      <td class="center-align">미정</td>
      <td class="center-align">구매거부성공</td>
      <td class="center-align">00</td>
      <td class="center-align">denyComplete</td>
      <td class="center-align">정상처리완료</td>
    </tr>
    <tr>
      <td class="center-align">기 구매거부</td>
      <td class="center-align">구매결정성공</td>
      <td class="center-align">00</td>
      <td class="center-align">buyComplete</td>
      <td class="center-align">기 구매거절 거래</td>
    </tr>
    <tr>
      <td class="center-align">기 구매거부</td>
      <td class="center-align">구매결정실패, 구매거부실패</td>
      <td class="center-align">에러코드</td>
      <td class="center-align">buyComplete, denyComplete</td>
      <td class="center-align">에러메세지, 가변적</td>
    </tr>
    <tr>
      <td class="center-align">기 구매거부</td>
      <td class="center-align">구매거부성공</td>
      <td class="center-align">00</td>
      <td class="center-align">denyComplete</td>
      <td class="center-align">기 구매거절 거래</td>
    </tr>
  </tbody>
</table>

</div>
</details>

## 2.8 가상계좌 입금통보 사용방법 안내

>웰컴페이먼츠 지불서버는 지불 결과를 실시간으로 회원사 측의 가상계좌 입금통보(P_NOTI_URL)를 호출하여 지불 결과를 통보합니다.<br>
>가상계좌 입금통보(P_NOTI_URL)는 정상적으로 결제 데이터를 받을 때까지 반복 호출됩니다.<br>
>가상계좌 입금통보(P_NOTI_URL)페이지는 웰컴페이먼츠에서 백엔드(backend)로 호출을 하는 페이지로, 고객이 보는 결제 화면과는 무관합니다.<br>

[노티를 받을 때 전달되는 파라미터]

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

<table style="width: 100%;">
<colgroup>
    <col style="width: 25%;">
    <col style="width: 20%;">
    <col style="width: 15%;">
    <col style="width: 40%;">
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
    <td class="center-align">P_STATUS</td>
    <td class="center-align">거래상태</td>
    <td class="center-align">String(2)</td>
    <td>성공: 00, 실패 : 01, 가상계좌 입금 통보 시 : 02</td>
  </tr>
  <tr>
    <td class="center-align">P_TID</td>
    <td class="center-align">거래번호</td>
    <td class="center-align">String(40)</td>
    <td></td>
  </tr>
  <tr>
    <td class="center-align">P_TYPE</td>
    <td class="center-align">지불수단</td>
    <td class="center-align">String(10)</td>
    <td>ISP(신용카드  ISP), CARD(신용카드 안심클릭 및 국민앱카드), VBANK( 가상계좌 )</td>
  </tr>
  <tr>
    <td class="center-align">P_AUTH_DT</td>
    <td class="center-align">승인일자</td>
    <td class="center-align">String(14)</td>
    <td>YYYYmmddHHmmss</td>
  </tr>
  <tr>
    <td class="center-align">P_MID</td>
    <td class="center-align">상점아이디</td>
    <td class="center-align">String(10)</td>
    <td></td>
  </tr>
  <tr>
    <td class="center-align">P_OID</td>
    <td class="center-align">상점 주문번호</td>
    <td class="center-align">String(100)</td>
    <td></td>
  </tr>
  <tr>
    <td class="center-align">P_FN_CD1</td>
    <td class="center-align">금융사코드</td>
    <td class="center-align">String(4)</td>
    <td>계좌이체, 가상계좌: 은행코드(계좌이체 내 뱅크월렛 결제 건은 BW로 전달) <br> 카드:카드코드, 핸드폰결제: 핸드폰 번호 앞 3자리</td>
  </tr>
  <tr>
    <td class="center-align">P_FN_CD2</td>
    <td class="center-align">금융사코드</td>
    <td class="center-align">String(10)</td>
    <td>계좌이체: 은행영문 코드 (계좌이체 내 뱅크월렛 결제 건은 BW로 전달) <br> 카드: P_FN_CD1과 동일 <br> 핸드폰결제: P_FN_CD1과 동일</td>
  </tr>
  <tr>
    <td class="center-align">P_FN_NM</td>
    <td class="center-align">금융사명</td>
    <td class="center-align">String(50)</td>
    <td>은행명, 카드사명, 이동통신사명</td>
  </tr>
  <tr>
    <td class="center-align">P_AMT</td>
    <td class="center-align">거래금액</td>
    <td class="center-align">String(12)</td>
    <td></td>
  </tr>
  <tr>
    <td class="center-align">P_UNAME</td>
    <td class="center-align">주문자명</td>
    <td class="center-align">String(30)</td>
    <td></td>
  </tr>
  <tr>
    <td class="center-align">P_RMESG1</td>
    <td class="center-align">메시지1</td>
    <td class="center-align">String(500)</td>
    <td>가상계좌 : 채번 된 가상계좌번호, 입금기한<br>예) <code>P_VACCT_NO=01440064018781P_EXP_DT=20100325</code></td>
  </tr>
  <tr>
    <td class="center-align">P_RMESG2</td>
    <td class="center-align">메시지2</td>
    <td class="center-align">String(500)</td>
    <td>신용카드의 경우, 할부 결제 시 할부 개월 수 표시  예) 02 (02개월)</td>
  </tr>
  <tr>
    <td class="center-align">P_RMESG3</td>
    <td class="center-align">메시지3</td>
    <td class="center-align">String(500)</td>
    <td>임의필드<code>(name^value|name^value|…)</code> <br> RM3_DISC_AMT : 할인금액 char(12)<br>RM3_PRICE : 실승인금액 char(12)<br>RM3_ORG_AMT : 원금액 char(12)<br>RM3_EVENT_CODE : 이벤트 코드 char(2)<br>RM3_INTEREST : 신용카드 무이자 여부 char(1)<br>RM3_ COUPONFLAG : 쿠폰사용여부 char(1)<br>RM3_COUPONPRICE : 쿠폰사용 실 승인금액 char(12)<br>RM3_COUPONDISCOUNT : 쿠폰 할인금액 char(12)</td>
  </tr>
  <tr>
    <td class="center-align">P_NOTI</td>
    <td class="center-align">주문정보</td>
    <td class="center-align">String(4000)</td>
    <td>거래요청시 입력한 P_NOTI의 값을 **그대로 반환**합니다.</td>
  </tr>
  <tr>
    <td class="center-align">P_AUTH_NO</td>
    <td class="center-align">승인번호</td>
    <td class="center-align">String(30)</td>
    <td>신용카드거래에서만 사용합니다.<br><strong>여신 승인거래에 대해서만 전달</strong></td>
  </tr>
  <tr>
    <td class="center-align">P_CARD_ISSUER_CODE</td>
    <td class="center-align">발급사 코드</td>
    <td class="center-align">String(4)</td>
    <td class="center-align"></td>
  </tr>
  <tr>
    <td class="center-align">P_CARD_NUM</td>
    <td class="center-align">카드번호</td>
    <td class="center-align">String(16)</td>
    <td>계약관계에 따라 틀림<br><strong>여신 승인거래에 대해서만 전달</strong></td>
  </tr>
  <tr>
    <td class="center-align">P_CARD_MEMBER_NUM</td>
    <td class="center-align">가맹점번호</td>
    <td class="center-align">String(15)</td>
    <td>자체 가맹점 일 경우만 해당</td>
  </tr>
  <tr>
    <td class="center-align">P_CARD_PURCHASE_CODE</td>
    <td class="center-align">매입사코드</td>
    <td class="center-align">String(2)</td>
    <td>자체 가맹점 일 경우만 해당</td>
  </tr>
  <tr>
    <td class="center-align">P_PRTC_CODE</td>
    <td class="center-align">부분취소 가능여부</td>
    <td class="center-align">String(1)</td>
    <td>부분취소가능 : 1, 부분취소불가능 : 0</td>
  </tr>
  <tr>
    <td class="center-align">P_SRC_CODE</td>
    <td class="center-align">앱 연동 결제 구분</td>
    <td class="center-align">String(3)</td>
    <td>K : 국민앱카드</td>
  </tr>
  <tr>
    <td class="center-align">P_ISP_CARDCODE</td>
    <td class="center-align">VCARD코드</td>
    <td class="center-align">String(25)</td>
    <td>ISP 발급사코드 및 기타 정보</td>
  </tr>
  <tr>
    <td class="center-align">P_CARD_PURCHASE_NAME</td>
    <td class="center-align">매입사명</td>
    <td class="center-align">String(22)</td>
    <td></td>
  </tr>
  <tr>
    <td class="center-align">P_CARD_ISSUER_NAME</td>
    <td class="center-align">발급사명</td>
    <td class="center-align">String(22)</td>
    <td></td>
  </tr>
  <tr>
    <td class="center-align">P_MERCHANT_RESERVED</td>
    <td class="center-align">임시필드</td>
    <td class="center-align">String(5000)</td>
    <td>1) pg에서 임의로 사용하는 필드<br>형태 : <code>name^value|name^value|..</code><br>2) 현대M포인트, BC TOP포인트 등 사용 내역 표시<br>예시 : <code>dXNlcG9pbnQ9MCY=(Base64encode) usepoint=0&(Base64decode)</code></td>
  </tr>
  <tr>
    <td class="center-align">P_CSHR_AMT</td>
    <td class="center-align">현금영수증 거래 금액</td>
    <td class="center-align">String(12)</td>
    <td>계좌이체, 가상계좌 현금영수증 거래 금액<br><strong>※ 가상계좌 채번 결과에 전달</strong></td>
  </tr>
  <tr>
    <td class="center-align">P_CSHR_SUP_AMT</td>
    <td class="center-align">현금영수증 공급가액</td>
    <td class="center-align">String(12)</td>
    <td>계좌이체, 가상계좌 현금영수증 공급가액<br><strong>※ 가상계좌 채번 결과에 전달</strong></td>
  </tr>
  <tr>
    <td class="center-align">P_CSHR_TAX</td>
    <td class="center-align">현금영수증 부가가치세</td>
    <td class="center-align">String(12)</td>
    <td>계좌이체, 가상계좌 현금영수증 부가가치세<br><strong>※ 가상계좌 채번 결과에 전달</strong></td>
  </tr>
  <tr>
    <td class="center-align">P_CSHR_SRVC_AMT</td>
    <td class="center-align">현금영수증 봉사료</td>
    <td class="center-align">String(12)</td>
    <td>계좌이체, 가상계좌 현금영수증 부가가치세<br><strong>※ 가상계좌 채번 결과에 전달</strong></td>
  </tr>
  <tr>
    <td class="center-align">P_CSHR_TYPE</td>
    <td class="center-align">현금영수증 거래자 구분</td>
    <td class="center-align">String(1)</td>
    <td>0 : 소비자 소득공제용 / 1 : 사업자 지출증빙용계좌이체, 가상계좌 현금영수증 거래자 구분<br>※ 가상계좌 채번 결과에 전달</td>
  </tr>
  <tr>
    <td class="center-align">P_CSHR_DT</td>
    <td class="center-align">현금영수증 발행일자</td>
    <td class="center-align">String(14)</td>
    <td>YYYYmmddHHmmss계좌이체, 가상계좌 현금영수증 발행일자※ 가상계좌 입금 결과에 전달</td>
  </tr>
  <tr>
    <td class="center-align">P_CSHR_AUTH_NO</td>
    <td class="center-align">현금영수증 발행승인번호</td>
    <td class="center-align">String(9)</td>
    <td>계좌이체, 가상계좌 현금영수증 발행승인번호※ 가상계좌 입금 결과에 전달</td>
  </tr>
</tbody>
</table>

</div>
</details>

- 16, 18번 항목의 승인번호 및 카드번호의 경우 페이코포인트 전액, 카카오머니 거래의 경우 여신승인 대상이 아님으로 전달되지 않습니다.

#### 주의사항

- WEB 방식의 가상계좌를 이용하는 경우에도 입금통보를 위해 Receive 페이지를 구성하게 되는데,
  입금통보 외에 가상 계좌 채번 시에도 P_NOTI_URL 로 설정된 주소로 결과가 전송되니 채번 시 전달되는 내용은 무시하시기 바랍니다.
- 또한, 입금 통보 수신 시, 기 수신받은 P_TID 인지 반드시 체크하는 로직을 구성하시길 바랍니다.
- 노티는 네트워크의 사정에 따라, 중복수신 될 수 있습니다.

<div style="display: inline-block; width: 100%; margin-top: 50px;">
  <a style="float:left;" href="/mobile01.html">◀이전페이지</a>
  <a style="float:right;" href="/mobile03.html">다음페이지▶</a>
</div>
