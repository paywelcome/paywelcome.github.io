---
title: PAYAPI 신용카드 키인승인 API
permalink: payapi04.html
sidebar: payapi_sidebar
folder: payapi
toc: false
keywords: 키인, 결제, 수기결제, 수기 결제, 키인 결제, 키인결제
---

<div style="display: inline-block; width: 100%;">
  <a style="float:left;" href="/payapi03.html">◀이전페이지</a>
  <a style="float:right;" href="/payapi05.html">다음페이지▶</a>
</div>

# 4. 신용카드 키인결제  API

## 4.1 신용카드 키인결제 API

신용카드 수기 승인시 사용하는 서비스입니다.

- 해당 API를 사용하기 위해서는 계약담당자를 통해 별도 사용요청 해주시기 바랍니다.
- 키인결제 테스트 MID : <a href="mailto:mainpg_support@welcomepayments.co.kr">메일로 문의하기(support@welcomepayments.co.kr)</a>

[//]: # (신용카드 키인결제 API URL)
<table class="tg" style="width: 100%">
  <colgroup>
    <col style="width: 20%">
    <col style="width: 80%">
  </colgroup>
  <tbody>
    <tr>
      <td class="center-align">운영</td>
      <td class="center-align">https://payapi.paywelcome.co.kr/noauth/pay/card</td>
    </tr>
    <tr>
      <td class="center-align">테스트</td>
      <td class="center-align">https://tpayapi.paywelcome.co.kr/noauth/pay/card</td>
    </tr>
  </tbody>
</table>

#### 1) 신용카드 키인결제 요청 파라미터

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

[//]: # (키인결제 요청)
<table class="tg" style="table-layout: fixed; width: 100%">
<colgroup>
<col style="text-align: center; width: 5%">
<col style="text-align: center; width: 15%">
<col style="text-align: center; width: 15%">
<col style="text-align: center; width: 8%">
<col style="text-align: center; width: 6%">
<col style="text-align: center; width: 8%">
<col style="text-align: center; width: 10%">
<col style="text-align: left; width: 33%">
</colgroup>
<thead>
  <tr>
    <th class="center-align">구분</th>
    <th class="center-align">필드</th>
    <th class="center-align">필드명</th>
    <th class="center-align">크기</th>
    <th class="center-align">필수</th>
    <th class="center-align">암호화</th>
    <th class="center-align">타입</th>
    <th class="center-align">비고</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="center-align">1</td>
    <td class="center-align">mid</td>
    <td class="center-align">가맹점ID</td>
    <td class="center-align">10</td>
    <td class="center-align">○</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">2</td>
    <td class="center-align">cardNumber</td>
    <td class="center-align">카드번호</td>
    <td class="center-align">16</td>
    <td class="center-align">○</td>
    <td class="center-align">○</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">3</td>
    <td class="center-align">cardExpireYY</td>
    <td class="center-align">유효기간(년)</td>
    <td class="center-align">2</td>
    <td class="center-align">○</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">2자리</td>
  </tr>
  <tr>
    <td class="center-align">4</td>
    <td class="center-align">cardExpireMM</td>
    <td class="center-align">유효기간(월)</td>
    <td class="center-align">2</td>
    <td class="center-align">○</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">2자리</td>
  </tr>
  <tr>
    <td class="center-align">5</td>
    <td class="center-align">registNo</td>
    <td class="center-align">생년월일</td>
    <td class="center-align">20</td>
    <td class="center-align"></td>
    <td class="center-align">○</td>
    <td class="center-align">String</td>
    <td class="left-align">생년월일 6자리/사업자번호<br/>구인증(카유생) 설정 업체만<br/>필수(담당자 확인필요)</td>
  </tr>
  <tr>
    <td class="center-align">6</td>
    <td class="center-align">passwd</td>
    <td class="center-align">비밀번호</td>
    <td class="center-align">2</td>
    <td class="center-align"></td>
    <td class="center-align">○</td>
    <td class="center-align">String</td>
    <td class="left-align">앞 2자리<br/>구인증(카유생비) 설정 업체만<br/>필수(담당자 확인 필요)</td>
  </tr>
  <tr>
    <td class="center-align">7</td>
    <td class="center-align">cardQuota</td>
    <td class="center-align">할부개월수</td>
    <td class="center-align">2</td>
    <td class="center-align">○</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">00:일시불, 02:2개월 ….</td>
  </tr>
  <tr>
    <td class="center-align">8</td>
    <td class="center-align">quotaInterest</td>
    <td class="center-align">무이자여부</td>
    <td class="center-align">1</td>
    <td class="center-align">○</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">0:일반, 1:무이자</td>
  </tr>
  <tr>
    <td class="center-align">9</td>
    <td class="center-align">oid</td>
    <td class="center-align">상점주문번호</td>
    <td class="center-align">40</td>
    <td class="center-align">○</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">10</td>
    <td class="center-align">price</td>
    <td class="center-align">금액</td>
    <td class="center-align">10</td>
    <td class="center-align">○</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">11</td>
    <td class="center-align">tax</td>
    <td class="center-align">부가세</td>
    <td class="center-align">10</td>
    <td class="center-align"></td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">대상: &#39;부가세업체정함&#39; 설정업체에 한함<br/>주의: 전체금액의 10%이하로 설정가맹점에서 등록시 VAT가 총 상품가격의 10% 초과할 경우는 거절됨</td>
  </tr>
  <tr>
    <td class="center-align">12</td>
    <td class="center-align">taxfree</td>
    <td class="center-align">비과세</td>
    <td class="center-align">10</td>
    <td class="center-align"></td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">대상: &#39;부가세업체정함&#39; 설정업체에 한함<br/>과세되지 않는 금액</td>
  </tr>
  <tr>
    <td class="center-align">13</td>
    <td class="center-align">goodsName</td>
    <td class="center-align">상품명</td>
    <td class="center-align">80</td>
    <td class="center-align"></td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">14</td>
    <td class="center-align">buyerName</td>
    <td class="center-align">구매자명</td>
    <td class="center-align">30</td>
    <td class="center-align">○</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">15</td>
    <td class="center-align">buyerTel</td>
    <td class="center-align">구매자전화번호</td>
    <td class="center-align">40</td>
    <td class="center-align"></td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">16</td>
    <td class="center-align">buyerEmail</td>
    <td class="center-align">구매자이메일</td>
    <td class="center-align">40</td>
    <td class="center-align"></td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">17</td>
    <td class="center-align">timestamp</td>
    <td class="center-align">타임스탬프</td>
    <td class="center-align">14</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">예) 20190906110100</td>
  </tr>
  <tr>
    <td class="center-align">18</td>
    <td class="center-align">signature</td>
    <td class="center-align">검증값</td>
    <td class="center-align">N/A</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">Sha256<br>(mid+mkey+oid+price+timestamp)</td>
  </tr>
</tbody>
</table>

</div>
</details>

#### 2) 신용카드 키인결제 응답 파라미터

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

[//]: # (신용카드 키인결제 응답 파라미터)
<table class="tg" style="table-layout: fixed; width: 100%">
<colgroup>
<col style="width: 6%">
<col style="width: 25%">
<col style="width: 15%">
<col style="width: 6%; text-align: center">
<col style="width: 6%; text-align: center">
<col style="width: 8%; text-align: center">
<col style="width: 8%">
<col style="width: 26%">
</colgroup>
<thead>
  <tr>
    <th class="center-align">구분</th>
    <th class="center-align">필드</th>
    <th class="center-align">필드명</th>
    <th class="center-align">크기</th>
    <th class="center-align">필수</th>
    <th class="center-align">암호화</th>
    <th class="center-align">타입</th>
    <th class="left-align">비고</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="center-align">1</td>
    <td class="center-align">ResultCode</td>
    <td class="center-align">결과코드</td>
    <td class="center-align">6</td>
    <td class="center-align">○</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">00: 정상, 그 외 실패</td>
  </tr>
  <tr>
    <td class="center-align">2</td>
    <td class="center-align">ResultMsg</td>
    <td class="center-align">결과메시지</td>
    <td class="center-align">100</td>
    <td class="center-align">○</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
 </tr>
  <tr>
    <td class="center-align">3</td>
    <td class="center-align">PayDate</td>
    <td class="center-align">승인날짜</td>
    <td class="center-align">8</td>
    <td class="center-align">△</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
 </tr>
  <tr>
    <td class="center-align">4</td>
    <td class="center-align">PayTime</td>
    <td class="center-align">승인시간</td>
    <td class="center-align">6</td>
    <td class="center-align">△</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
 </tr>
  <tr>
    <td class="center-align">5</td>
    <td class="center-align">Price</td>
    <td class="center-align">금액</td>
    <td class="center-align">10</td>
    <td class="center-align">△</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
 </tr>
  <tr>
    <td class="center-align">6</td>
    <td class="center-align">tid</td>
    <td class="center-align">거래ID</td>
    <td class="center-align">40</td>
    <td class="center-align">△</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">7</td>
    <td class="center-align">ApplNum</td>
    <td class="center-align">승인번호</td>
    <td class="center-align">10</td>
    <td class="center-align">△</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
</tbody>
</table>

</div>
</details>

<div style="display: inline-block; width: 100%; margin-top: 50px;">
  <a style="float:left;" href="/payapi03.html">◀이전페이지</a>
  <a style="float:right;" href="/payapi05.html">다음페이지▶</a>
</div>