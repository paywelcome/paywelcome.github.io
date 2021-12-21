---
title: MOBILE
permalink: mobile02.html
sidebar: mobile_sidebar
folder: mobile
toc: false
---

# 2. 상점 모바일 결제 연동

## 2.1 결제창 Open (주문정보 전달) - 접속 주소 및 일반필드

> 주문정보 전달이란, 하기의 Step을 의미합니다.

{% include image.html file="mobile_img03.png" %}

<br/>

상점 페이지에서 Mobile Web 서비스 접속 시, 지불수단 및 통신방식 별로 상이한 URL 을 사용합니다. 이에, 하기의 URL 을 참고하시기 바랍니다.

[//]: # (URL table)
<table class="tg" style="table-layout: fixed; width: 100%">
<colgroup>
<col style="width: 25%;">
<col style="width: 25%;">
<col style="width: 50%;">
</colgroup>
<tbody>
  <tr>
    <td class="tg-0lax" rowspan="2">HOST</td>
    <td class="tg-0lax">테스트</td>
    <td class="tg-0lax">tmobile.paywelcome.co.kr</td>
  </tr>
  <tr>
    <td class="tg-0lax">운영</td>
    <td class="tg-0lax">mobile.paywelcome.co.kr</td>
  </tr>
  <tr>
    <td class="tg-0lax" rowspan="4">지불수단별<br>상세 URL</td>
    <td class="tg-0lax">신용카드</td>
    <td class="tg-0lax">https://{HOST}/smart/wcard/</td>
  </tr>
  <tr>
    <td class="tg-0lax">가상계좌</td>
    <td class="tg-0lax">https://{HOST}/smart/vbank/</td>
  </tr>
  <tr>
    <td class="tg-0lax">계좌이체</td>
    <td class="tg-0lax">https://{HOST}/smart/bank/</td>
  </tr>
  <tr>
    <td class="tg-0lax">휴대폰</td>
    <td class="tg-0lax">https://{HOST}/smart/mobile/</td>
  </tr>
  <tr>
    <td class="tg-0lax" colspan="2">METHOD</td>
    <td class="tg-0lax">POST</td>
  </tr>
  <tr>
    <td class="tg-0lax" colspan="2">Content-Type</td>
    <td class="tg-0lax">application/x-www-form-urlencoded;<br>charset=EUC-KR</td>
  </tr>
  <tr>
    <td class="tg-0lax" colspan="3">ex) 신용카드 연동시 : https://mobile.paywelcome.co.kr/smart/wcard/</td>
  </tr>
</tbody>
</table>


## 2.2 결제창 Open (주문정보 전달) - 결제페이지 요청필드

>Mobile Web 서비스 접속 시, 결제페이지를 구성하기 위해서는 하기 Parameter를 필요로 합니다.
```javascript
양식 예시 : <input type="hidden" name="필드명" value="값 예시" />;
```

#### 1) 전 지불수단 공통 필드

<table class="tg" style="table-layout: fixed; width: 100%;">
<colgroup>
<col style="width: 20%;">
<col style="width: 15%;">
<col style="width: 14%;">
<col style="width: 16%;">
<col style="width: 40%; text-align: left;">
</colgroup>
<thead>
  <tr>
    <th style="text-align: center;">필드명</th>
    <th style="text-align: center;">목&nbsp;&nbsp;적</th>
    <th style="text-align: center;">크&nbsp;&nbsp;기</th>
    <th style="text-align: center;">필수여부</th>
    <th style="text-align: center;">부가설명 및 주의사항</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>P_MID</td>
    <td>상점아이디</td>
    <td>char(10)</td>
    <td>필수</td>
    <td>계약된 당사발급 아이디</td>
  </tr>
  <tr>
    <td>P_OID</td>
    <td>주문번호</td>
    <td>Char(40)</td>
    <td>필수대상 외 선택</td>
    <td>한글을 제외한, 숫자/영문/특수기호의 형태<br>필수대상 : 가상계좌</td>
  </tr>
  <tr>
    <td>P_AMT</td>
    <td>거래금액</td>
    <td>Char(8)</td>
    <td>필수</td>
    <td>단위 표시 기호(콤마) 를 반드시 제거 요망</td>
  </tr>
  <tr>
    <td>P_UNAME</td>
    <td>고객성명</td>
    <td>Char(30)</td>
    <td>필수</td>
    <td></td>
  </tr>
  <tr>
    <td>P_MNAME</td>
    <td>가맹점 이름</td>
    <td>Char(30)</td>
    <td>선택</td>
    <td></td>
  </tr>
  <tr>
    <td>P_NOTI</td>
    <td>기타주문정보</td>
    <td>Char(800)</td>
    <td>선택</td>
    <td>이 값은 가맹점에서 이용하는 추가 정보 필드로 전달한 값이 그대로 반환됩니다. 결제처리 시, 꼭 필요한 내용만 사용하세요.<br> 800byte를 초과하는 P_NOTI의 값은 차후 문제가 생길 여지가 있으니 반드시 800byte를 초과하지 않도록 설정해야 합니다.</td>
  </tr>
  <tr>
    <td>P_GOODS</td>
    <td>결제상품명</td>
    <td>Char(80)</td>
    <td>필수</td>
    <td></td>
  </tr>
  <tr>
    <td>P_MOBILE</td>
    <td>구매자  휴대폰번호</td>
    <td>Char(20)</td>
    <td>선택</td>
    <td>'-' 를 포함한 번호를 적어주세요.구현 예시 : 000-0000-0000</td>
  </tr>
  <tr>
    <td>P_EMAIL</td>
    <td>구매자 E-mail</td>
    <td>Char(60)</td>
    <td>선택</td>
    <td>구현 예시 : abc@abc.com</td>
  </tr>
  <tr>
    <td>P_NEXT_URL</td>
    <td>인증결과수신</td>
    <td>Char(250)</td>
    <td>예외대상 외 필수</td>
    <td>사용자의 인증이 완료될 때, 이 Url 로 인증결과를 전달합니다.<br> Method : post or get (issue : 1-24보기) <br> Scheme : https (issue : 1-22보기)<br>Parameters : 0.<br>인증결과수신 (only 2 Transaction)참고 <br> 예외대상 : Kpay <br>한글도메인 사용불가 <br>https  권장</td>
  </tr>
  <tr>
    <td>P_NOTI_URL</td>
    <td>승인결과통보Url</td>
    <td>Char(250)</td>
    <td>적용대상 필수</td>
    <td>가맹점과 인증/승인과정을 거치지 않고 승인결과를 통보하는 용도로 사용합니다.<br> 단, 가상계좌의 경우, 입금완료시각이 비동기식 이므로, 입금완료 통보를 위해 사용됩니다.<br> Method : post<br> 적용대상 : 가상계좌의 NOTI Url 은 네트워크 사정에 따라 중복전송 될 수 있으니, 중복수신여부 체크루틴을 반드시 구현하시기 바랍니다.<br> * 한글도메인 사용불가</td>
  </tr>
  <tr>
    <td>P_TAX</td>
    <td>부가세</td>
    <td>Char(8)</td>
    <td>선택</td>
    <td>영수증에 표기할 부가세 금액<>br</td>
  </tr>
  <tr>
    <td>P_TAXFREE</td>
    <td>비과세</td>
    <td>Char(8)</td>
    <td>선택</td>
    <td>과세 되지 않는 금액 대상 : &#39;부가세업체정함&#39; 설정업체에 한함</td>
  </tr>
  <tr>
    <td rowspan="6">P_OFFER_PERIOD</td>
    <td rowspan="6">제공기간</td>
    <td rowspan="6"></td>
    <td rowspan="6">선택</td>
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
    <td>P_TIMESTAMP</td>
    <td>타임스템프</td>
    <td>Char(20)</td>
    <td>필수</td>
    <td>TimeInMillis(Long형)</td>
  </tr>
  <tr>
    <td>P_SIGNATURE</td>
    <td>SIGNATRUE</td>
    <td>Char(64)</td>
    <td>필수</td>
    <td>위변조 방지 SHA256 Hash 값(mkey+P_AMT+P_OID+P_TIMESTAMP)하단의 &#39;P_SIGNATURE 필드 처리&#39</td>
  </tr>
</tbody>
</table>

#### 2) 신용카드 전용 필드

<details style="cursor:pointer;">
<summary><strong>[&nbsp;펼치기&nbsp;]</strong></summary>
<div markdown="1">


<table class="tg" style="table-layout: fixed; width: 100%;">
<colgroup>
    <col style="width: 20%;">
    <col style="width: 15%;">
    <col style="width: 14%;">
    <col style="width: 16%;">
    <col style="width: 40%; text-align: left;">
</colgroup>
<thead>
  <tr style="text-align: center">
    <th style="text-align: center;">필드명</th>
    <th style="text-align: center;">목&nbsp;&nbsp;적</th>
    <th style="text-align: center;">크&nbsp;&nbsp;기</th>
    <th style="text-align: center;">필수여부</th>
    <th style="text-align: center;">부가설명 및 주의사항</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="2">P_CARD_OPTION</td>
    <td>신용카드 우선선택 옵션</td>
    <td></td>
    <td>선택</td>
    <td>설정 시, 해당 카드코드에 해당하는 카드가 선택된 채로 Display 됩니다.<br> 간편결제는 불가능(타 카드 선택 가능) <br> 적용 예시 : selcode=14</td>
  </tr>
  <tr>
    <td>선택적 표시 옵션</td>
    <td></td>
    <td>선택</td>
    <td>설정 시, 안심결제(visa3d), ISP(isp), 간편결제(easypay), 일반카드결제(normal) 중 선택적 표시 됩니다. <br> onlycard=visa3d 적용 예시 : selcode=14:onlycard=visa3d</td>
  </tr>
  <tr>
    <td>P_ONLY_CARDCODE</td>
    <td>신용카드 노출제한 옵션</td>
    <td></td>
    <td>선택</td>
    <td>선택된 카드 리스트만 출력되며, 나머지 카드 리스트는 출력되지 않습니다.<br>적용 예시 : 롯데, 외환, BC 카드만 사용할 경우, <br> 롯데카드코드 : 03, <br>외환카드코드 : 01,<br>  BC카드코드 : 11 이므로, 03:01:11 로 설정</td>
  </tr>
  <tr>
    <td>P_ONLY_EASYPAYCODE</td>
    <td>간편결제노출제한 옵션</td>
    <td></td>
    <td>선택</td>
    <td>선택된 간편결제 리스트만 출력되며, 나머지 간편결제 리스트는 출력되지 않습니다.<br> 적용 예시 : 카카오페이, 엘페이, 페이코만 사용할 경우, <br> 카카오페이 : KAKAOPAY <br> 엘페이 : LPAY<br> 페이코 : PAYCO 이므로<br> KAKAOPAY:LPAY:PAYCO 로 설정(간편결제 코드 대문자 입력 필)</td>
  </tr>
  <tr>
    <td>P_QUOTABASE</td>
    <td>신용카드 할부기간 지정</td>
    <td></td>
    <td>선택</td>
    <td>선50,000원 이상 결제 시, 할부기간 지정 (36개월 MAX)<br> 적용 예시 :  01:02:03:04.. 01은 일시불, 02는 2개월, 99 는 일시불 제거 등등</td>
  </tr>
</tbody>
</table>

</div>
</details>

#### 3) 휴대폰 전용 필드

<details style="cursor:pointer;">
<summary><strong>[&nbsp;펼치기&nbsp;]</strong></summary>
<div markdown="1">

<table class="tg" style="table-layout: fixed; width: 100%;">
<colgroup>
<col style="width: 25%;">
<col style="width: 15%;">
<col style="width: 10%;">
<col style="width: 20%;">
<col style="width: 35%; text-align: left;">
</colgroup>
<thead>
  <tr style="text-align: center">
    <th style="text-align: center;">필드명</th>
    <th style="text-align: center;">목&nbsp;&nbsp;적</th>
    <th style="text-align: center;">크&nbsp;&nbsp;기</th>
    <th style="text-align: center;">필수여부</th>
    <th style="text-align: center;">부가설명 및 주의사항</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>P_HPP_METHOD</td>
    <td>실물여부</td>
    <td></td>
    <td>휴대폰결제 필수</td>
    <td>컨텐츠 일 경우 : 1<br>실물일 경우 : 2<br> 빌링컨텐츠 일 경우 : 4<br> 빌링실물 일 경우 : 5<br> 컨텐츠/실물/빌링컨텐츠/빌링실물 여부는 계약담당자에게 확인요청</td>
  </tr>
</tbody>
</table>

</div>
</details>

#### 4) 가상계좌 전용 필드

<details style="cursor:pointer;">
<summary><strong>[&nbsp;펼치기&nbsp;]</strong></summary>
<div markdown="1">

<table class="tg" style="table-layout: fixed; width: 100%;">
<colgroup>
<col style="width: 25%;">
<col style="width: 15%;">
<col style="width: 10%;">
<col style="width: 20%;">
<col style="width: 35%; text-align: left;">
</colgroup>
<thead>
  <tr style="text-align: center">
    <th style="text-align: center;">필드명</th>
    <th style="text-align: center;">목&nbsp;&nbsp;적</th>
    <th style="text-align: center;">크&nbsp;&nbsp;기</th>
    <th style="text-align: center;">필수여부</th>
    <th style="text-align: center;">부가설명 및 주의사항</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>P_VBANK_DT</td>
    <td>가상계좌 입금기한 날짜</td>
    <td></td>
    <td>선택</td>
    <td>설정을 하지 않으면,요청일 + 10일로 자동설정 됩니다.<br>적용 예시 : 20151225</td>
  </tr>
  <tr>
    <td>P_VBANK_TM</td>
    <td>가상계좌 입금기한 시간</td>
    <td></td>
    <td>선택</td>
    <td>시분까지 설정 가능합니다.(4자리)<br>적용 예시 :  2030</td>
  </tr>
</tbody>
</table>

>P_VBANK_DT=20180518, P_VBANK_TM=0000 으로 설정하시는 경우  2018.05.18 23 시  59 분  59 초까지로 설정됩니다.
><br>ex) P_VBANK_DT=20180518, P_VBANK_TM=0000 : 2018.05.18 23시 59분 59초까지
><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;P_VBANK_DT=20180517, P_VBANK_TM=2359 : 2018.05.17 23시 59분 00초까지
><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;P_VBANK_DT=20180518, P_VBANK_TM=0001 : 2018.05.18 00시 01분 00초까지
><br>
><br>
>**단 ,  결제요청일자와  P_VBANK_DT 가 같은 경우  V_VBANK_TM=0000  설정 불가능하며  P_VBANK_TM=2359 으로 설정하셔야 정상 승인 가능합니다.**

</div>
</details>

#### 5) 기타 옵션 필드

<details style="cursor:pointer;">
<summary><strong>[&nbsp;펼치기&nbsp;]</strong></summary>
<div markdown="1">

<table class="tg" style="table-layout: fixed; width: 100%;">
<colgroup>
<col style="width: 25%;">
<col style="width: 15%;">
<col style="width: 10%;">
<col style="width: 20%;">
<col style="width: 35%; text-align: left;">
</colgroup>
<thead>
  <tr style="text-align: center">
    <th style="text-align: center;">필드명</th>
    <th style="text-align: center;">목&nbsp;&nbsp;적</th>
    <th style="text-align: center;">크&nbsp;&nbsp;기</th>
    <th style="text-align: center;">필수여부</th>
    <th style="text-align: center;">부가설명 및 주의사항</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>P_CHARSET</td>
    <td>캐릭터셋 설정</td>
    <td></td>
    <td>선택</td>
    <td>인증, 승인결과 CHARSET 정의 default는 euc-kr이며, 인증·승인 결과를 utf-8로 받기를 원하시면 해당 옵션 설정 값을 utf8로 하시면 됩니다.<br> Ex. utf8동기방식에서 P_CHARSET=utf8 옵션 사용 시,<br>ISP 결제 진행 과정에서 인증결과 중 P_RMESG1 필드 값이 urlencode 되어 내려갈 수 있습니다.<br>인증결과 값에 대해 필요 시, 해당 값에 대해 urldecode 처리하여 사용할 수 있도록 처리 바랍니다.</td>
  </tr>
</tbody>
</table>

</div>
</details>

#### 6) 복합 필드 (P_RESERVED)

<details style="cursor:pointer;">
<summary><strong>[&nbsp;펼치기&nbsp;]</strong></summary>
<div markdown="1">

<table class="tg" style="table-layout: fixed; width: 100%;">
<colgroup>
<col style="width: 15%;">
<col style="width: 15%;">
<col style="width: 30%;">
<col style="width: 40%; text-align: left;">
</colgroup>
<thead>
  <tr>
    <th style="text-align: center;">필드명</th>
    <th style="text-align: center;">목&nbsp;&nbsp;적</th>
    <th style="text-align: center;">Variable</th>
    <th style="text-align: center;">Value 및 부가설명</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="17">P_RESERVED</td>
    <td>신용카드필수옵션</td>
    <td>twotrs_isp=Y&block_isp=Y&twotrs_isp_noti=N</td>
    <td>신용카드 거래 시, 반드시 입력되어야 하는 값 입니다.</td>
  </tr>
  <tr>
    <td>가상계좌 현금영수증 사용여부</td>
    <td>vbank_receipt=Y</td>
    <td>Default : 미표시<br> Y : 표시<br> N : 미표시</td>
  </tr>
  <tr>
    <td>계좌이체필수옵션</td>
    <td>Twotrs_bank=Y&apprun_check=Y</td>
    <td>계좌이체 거래 시, 반드시 입력되어야 하는 값입니다.</td>
  </tr>
  <tr>
    <td>계좌이체현금영수증 사용여부</td>
    <td>bank_receipt=Y</td>
    <td>Default : 미표시<br> Y : 표시<br> N : 미표시</td>
  </tr>
  <tr>
    <td>카드포인트 사용여부</td>
    <td>cp_yn=Y</td>
    <td>신용카드에 한하며, 신용카드 포인트를 사용가능하게 하는 옵션입니다.<br> 이 옵션을 사용하면, 신용카드 사의 포인트를 사용할 수 있습니다.</td>
  </tr>
  <tr>
    <td>앱 호출 시, Intent 형식 으로 호출여부</td>
    <td>apprun_check=Y</td>
    <td>카드사 창에서 호출되는 백신앱 및 앱카드를 제외한,<br> Mobile Web 서비스에서 직접 호출하는 앱(ISP등)의 호출방식을 Intent 방식으로 작동시키며,<br> 설치유무 체크를 Mobile Web 서비스에서 직접 컨트롤 하는 기능을 수행합니다.<br> (Chrome, safari, ff) 해당 기능은 Android 단말기에서만 정상 동작하며,<br> app_scheme 옵션과 같이 사용할 수 없습니다.</td>
  </tr>
  <tr>
    <td>30만원 이상 결제 시</td>
    <td>ismart_use_sign=Y</td>
    <td>Android : 이 옵션 필요 없음 (해당 없음) <br> IOS 웹 형태 : ismart_use_sign=Y<br>IOS 앱형태 : ismart_use_sign=Y&mall_app_name=가맹점스키마</td>
  </tr>
  <tr>
    <td>에스크로사용여부</td>
    <td>useescrow=Y</td>
    <td>설정 시 "에스크로 약관동의" 와 "구매자 본인확인" 페이지가 포함된 에스크로 결제창을 호출 합니다.<br>(에스크로 사용 설정된 가맹점만 사용 가능합니다.)</td>
  </tr>
  <tr>
    <td>1000원 미만 결제 허용</td>
    <td>below1000=Y</td>
    <td>신용카드 거래 시, 1000원 미만 결제를 허용하는 옵션 입니다.옵션을 사용하지 않으면, 자동 미사용 됩니다.</td>
  </tr>
  <tr>
    <td>신용카드 결제창 직접 호출</td>
    <td>d_card=00(코드)d_quota=00(할부개월)</td>
    <td>신용카드 결제창(안심클릭 / ISP)을 직접 호출하는 옵션 입니다. 설정 방법 : d_card=00(카드코드)d_quota=00(할부개월) Ex. d_card=04&amp;d_quota=03</td>
  </tr>
  <tr>
    <td>가맹점 App scheme 설정</td>
    <td>app_scheme=스키마 값</td>
    <td>가맹점 APP및 타사 앱을 통해 결제 진행 시 아래 지불수단을 사용할 경우 설정(IOS 지원)[ISP 2trs](#%EC%9D%B8%EC%A6%9D%EA%B2%B0%EA%B3%BC2trs)Ex. app_scheme=스키마명:// (스키마명 뒤에 "://"는 꼭 입력해 주셔야 합니다.)</td>
  </tr>
  <tr>
    <td>신용카드 상점무이자</td>
    <td>merc_noint=Ynoint_quota=00-00(카드-개월)</td>
    <td>무이자 이벤트 진행 시, 상점 부담 무이자 옵션 입니다.(대표 무이자 및 분담 무이자 아님) <br>설정 방법 : merc_noint = Ynoint_quota=00-00:00(카드-개월:개월) [카드-월:월]^ 카드는 OO두자리, 할부개월 01→1 카드 추가 시, 구분자는 ^ 입니다. 잘못된 예 11-02:04:06Ex. merc_noint=Y&amp; noint_quota=11-2:3^06-3:6:9:12※ 상점부담 무이자 계약 가맹점만 사용 가능합니다. (영업담당자 문의)</td>
  </tr>
  <tr>
    <td>표시될 통신사 리스트</td>
    <td>hpp_corp=통신사</td>
    <td>휴대폰 통신사(SKT, KTF, LGT, MVNO)를 지정할 수 있는 옵션 입니다.<br> Ex. SKT만 사용- hpp_corp=SKTSKT, KTF, LGT 사용 - hpp_corp=SKT:KTF:LGTMVNO중 일부만 설정 시 MVNO 제외 후 CJH(헬로모바일):KCT(티플러스):SKL(SK7mobile) 중 일부만 선택</td>
  </tr>
  <tr>
    <td>휴대폰 통신사 기본 선택</td>
    <td>hpp_default_corp=통신사</td>
    <td>통신사 리스트에서 입력 통신사가 기본 선택되어 짐SKT, KTF, LGT, MVNO 중 하나만 설정 가능MVNO 중 선택 시 CJH, KCT, SKL로 설정 가능미입력 시나 공백으로 입력 시 선택된 통신사 없음Ex. hpp_default_corp=SKT</td>
  </tr>
  <tr>
    <td>휴대폰 번호 수정 불가 여부</td>
    <td>hpp_nofix=Y</td>
    <td>휴대폰 번호를 수정 불가능하게 처리할 경우 설정(Y : 수정 불가, N : 수정가능(default))</td>
  </tr>
  <tr>
    <td>휴대폰 결제 인증 옵션</td>
    <td>hpp_authtype=ARS</td>
    <td>휴대폰 결제 인증 시 ARS로 인증하도록 처리 할 경우 설정(해당 옵션은 모빌리언스만 가능)</td>
  </tr>
  <tr>
    <td>휴대폰 빌키 발급</td>
    <td>hpp_bill=Y</td>
    <td>휴대폰 빌키 발급 시 사용상품유형 P_HPP_METHOD=4 또는 P_HPP_METHOD =5 로 설정 필요(휴대폰 빌링 사용은 별도 사용 설정 필요)</td>
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