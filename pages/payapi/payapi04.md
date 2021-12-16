---
title: PAYAPI
permalink: payapi04.html
sidebar: payapi_sidebar
folder: payapi
toc: false
---

# 4. 신용카드 키인결제  API

## 4.1 신용카드 키인결제 API

신용카드 수기 승인시 사용하는 서비스입니다.

- 해당 API를 사용하기 위해서는 계약담당자를 통해 별도 사용요청 해주시기 바랍니다.
- 키인결제 테스트 MID : <a href="mailto:mainpg_support@welcomepayments.co.kr">메일로 문의하기</a>

[//]: # (부분 취소 API URL)
<table class="tg" style="width: 100%">
  <colgroup>
    <col style="width: 20%">
    <col style="width: 80%">
  </colgroup>
  <tbody>
    <tr>
      <td class="tg-0lax">운영</td>
      <td class="tg-0lax">https://payapi.paywelcome.co.kr/noauth/pay/card</td>
    </tr>
    <tr>
      <td class="tg-0lax">테스트</td>
      <td class="tg-0lax">https://tpayapi.paywelcome.co.kr/noauth/pay/card</td>
    </tr>
  </tbody>
</table>

#### 1) 키인결제 요청 파라미터

[//]: # (키인결제 요청)
<table class="tg" style="table-layout: fixed; width: 100%">
<colgroup>
<col style="width: 8%">
<col style="width: 12%">
<col style="width: 16%">
<col style="width: 8%">
<col style="width: 8%">
<col style="width: 12%">
<col style="width: 10%">
<col style="width: 26%">
</colgroup>
<thead>
  <tr>
    <th class="tg-0lax">구분</th>
    <th class="tg-0lax">필드</th>
    <th class="tg-0lax">필드명</th>
    <th class="tg-0lax">길이</th>
    <th class="tg-0lax">필수</th>
    <th class="tg-0lax">암호화</th>
    <th class="tg-0lax">타입</th>
    <th class="tg-0lax">비고</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0lax">1</td>
    <td class="tg-0lax">mid</td>
    <td class="tg-0lax">가맹점ID</td>
    <td class="tg-0lax">10</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">2</td>
    <td class="tg-0lax">cardNumber</td>
    <td class="tg-0lax">카드번호</td>
    <td class="tg-0lax">16</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">3</td>
    <td class="tg-0lax">cardExpireYY</td>
    <td class="tg-0lax">유효기간(년)</td>
    <td class="tg-0lax">2</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">2자리</td>
  </tr>
  <tr>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax">cardExpireMM</td>
    <td class="tg-0lax">유효기간(월)</td>
    <td class="tg-0lax">2</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">2자리</td>
  </tr>
  <tr>
    <td class="tg-0lax">5</td>
    <td class="tg-0lax">registNo</td>
    <td class="tg-0lax">생년월일</td>
    <td class="tg-0lax">20</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">생년월일 6자리/ 사업자번호구인증(카유생) 설정 업체만 필수(담당자 확인필요)</td>
  </tr>
  <tr>
    <td class="tg-0lax">6</td>
    <td class="tg-0lax">passwd</td>
    <td class="tg-0lax">비밀번호</td>
    <td class="tg-0lax">2</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">앞 2자리구인증(카유생비) 설정 업체만 필수(담당자 확인 필요)</td>
  </tr>
  <tr>
    <td class="tg-0lax">7</td>
    <td class="tg-0lax">cardQuota</td>
    <td class="tg-0lax">할부개월수</td>
    <td class="tg-0lax">2</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">00:일시불, 02:2개월 ….</td>
  </tr>
  <tr>
    <td class="tg-0lax">8</td>
    <td class="tg-0lax">quotaInterest</td>
    <td class="tg-0lax">무이자여부</td>
    <td class="tg-0lax">1</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">0:일반, 1:무이자</td>
  </tr>
  <tr>
    <td class="tg-0lax">9</td>
    <td class="tg-0lax">oid</td>
    <td class="tg-0lax">상점주문번호</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">10</td>
    <td class="tg-0lax">price</td>
    <td class="tg-0lax">금액</td>
    <td class="tg-0lax">10</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">11</td>
    <td class="tg-0lax">tax</td>
    <td class="tg-0lax">부가세</td>
    <td class="tg-0lax">10</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">대상: &#39;부가세업체정함&#39; 설정업체에 한함주의: 전체금액의 10%이하로 설정가맹점에서 등록시 VAT가 총 상품가격의 10% 초과할 경우는 거절됨</td>
  </tr>
  <tr>
    <td class="tg-0lax">12</td>
    <td class="tg-0lax">taxfree</td>
    <td class="tg-0lax">비과세</td>
    <td class="tg-0lax">10</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">대상: &#39;부가세업체정함&#39; 설정업체에 한함과세되지 않는 금액</td>
  </tr>
  <tr>
    <td class="tg-0lax">13</td>
    <td class="tg-0lax">goodsName</td>
    <td class="tg-0lax">상품명</td>
    <td class="tg-0lax">80</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">14</td>
    <td class="tg-0lax">buyerName</td>
    <td class="tg-0lax">구매자명</td>
    <td class="tg-0lax">30</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">15</td>
    <td class="tg-0lax">buyerTel</td>
    <td class="tg-0lax">구매자전화번호</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">16</td>
    <td class="tg-0lax">buyerEmail</td>
    <td class="tg-0lax">구매자이메일</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">17</td>
    <td class="tg-0lax">timestamp</td>
    <td class="tg-0lax">타임스탬프</td>
    <td class="tg-0lax">14</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">예) 20190906110100</td>
  </tr>
  <tr>
    <td class="tg-0lax">18</td>
    <td class="tg-0lax">signature</td>
    <td class="tg-0lax">검증값</td>
    <td class="tg-0lax">N/A</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">Sha256<br>(mid+mkey+oid+price+timestamp)</td>
  </tr>
</tbody>
</table>

#### 2) 키인결제 응답 파라미터

[//]: # (키인결제 응답 파라미터)
<table class="tg" style="table-layout: fixed; width: 100%">
<colgroup>
<col style="width: 8%">
<col style="width: 12%">
<col style="width: 16%">
<col style="width: 8%">
<col style="width: 8%">
<col style="width: 12%">
<col style="width: 10%">
<col style="width: 26%">
</colgroup>
<thead>
  <tr>
    <th class="tg-0lax">구분</th>
    <th class="tg-0lax">필드</th>
    <th class="tg-0lax">필드명</th>
    <th class="tg-0lax">길이</th>
    <th class="tg-0lax">필수</th>
    <th class="tg-0lax">암호화</th>
    <th class="tg-0lax">타입</th>
    <th class="tg-0lax">비고</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0lax">1</td>
    <td class="tg-0lax">ResultCode</td>
    <td class="tg-0lax">결과코드</td>
    <td class="tg-0lax">6</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">00: 정상, 그 외 실패</td>
  </tr>
  <tr>
    <td class="tg-0lax">2</td>
    <td class="tg-0lax">ResultMsg</td>
    <td class="tg-0lax">결과메시지</td>
    <td class="tg-0lax">100</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">3</td>
    <td class="tg-0lax">PayDate</td>
    <td class="tg-0lax">승인날짜</td>
    <td class="tg-0lax">8</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax">PayTime</td>
    <td class="tg-0lax">승인시간</td>
    <td class="tg-0lax">6</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">5</td>
    <td class="tg-0lax">Price</td>
    <td class="tg-0lax">금액</td>
    <td class="tg-0lax">10</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">6</td>
    <td class="tg-0lax">tid</td>
    <td class="tg-0lax">거래ID</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">7</td>
    <td class="tg-0lax">ApplNum</td>
    <td class="tg-0lax">승인번호</td>
    <td class="tg-0lax">10</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
</tbody>
</table>
