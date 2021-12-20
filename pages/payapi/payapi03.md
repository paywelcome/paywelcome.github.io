---
title: PAYAPI
permalink: payapi03.html
sidebar: payapi_sidebar
folder: payapi
toc: false
---

# 3. 빌링결제 API

## 3.1 신용카드 빌키 발급 API
신용카드 빌링 결제에 필요한 빌키 발급 시 사용하는 서비스입니다.

- 해당 API를 사용하기 위해서는 계약담당자를 통해 별도 사용요청 해주시기 바랍니다.
- 빌링용 테스트 MID : <a href="mailto:mainpg_support@welcomepayments.co.kr">메일로 문의하기</a>

[//]: # (신용카드 빌키 발급 API)
<table class="tg" style="width: 100%">
  <colgroup>
    <col style="width: 20%">
    <col style="width: 80%">
  </colgroup>
  <tbody>
    <tr>
      <td class="tg-0lax">운영</td>
      <td class="tg-0lax">https://payapi.paywelcome.co.kr/billing/billkey/card</td>
    </tr>
    <tr>
      <td class="tg-0lax">테스트</td>
      <td class="tg-0lax">https://tpayapi.paywelcome.co.kr/billing/billkey/card</td>
    </tr>
  </tbody>
</table>

#### 1) 신용카드 빌키 발급 요청 파라미터

[//]: # (신용카드 빌키 발급 API 요청)
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
    <td class="tg-0lax">goodsName</td>
    <td class="tg-0lax">상품명</td>
    <td class="tg-0lax">80</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">3</td>
    <td class="tg-0lax">price</td>
    <td class="tg-0lax">금액</td>
    <td class="tg-0lax">10</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax">buyerName</td>
    <td class="tg-0lax">구매자명</td>
    <td class="tg-0lax">30</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">5</td>
    <td class="tg-0lax">buyerTel</td>
    <td class="tg-0lax">구매자전화번호</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">6</td>
    <td class="tg-0lax">buyerEmail</td>
    <td class="tg-0lax">구매자이메일</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">7</td>
    <td class="tg-0lax">cardNumber</td>
    <td class="tg-0lax">카드번호</td>
    <td class="tg-0lax">16</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">8</td>
    <td class="tg-0lax">cardExpireYY</td>
    <td class="tg-0lax">유효기간(년)</td>
    <td class="tg-0lax">2</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">2자리</td>
  </tr>
  <tr>
    <td class="tg-0lax">9</td>
    <td class="tg-0lax">cardExpireMM</td>
    <td class="tg-0lax">유효기간(월)</td>
    <td class="tg-0lax">2</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">2자리</td>
  </tr>
  <tr>
    <td class="tg-0lax">10</td>
    <td class="tg-0lax">registNo</td>
    <td class="tg-0lax">생년월일</td>
    <td class="tg-0lax">20</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">생년월일 6자리/ 사업자번호</td>
  </tr>
  <tr>
    <td class="tg-0lax">11</td>
    <td class="tg-0lax">passwd</td>
    <td class="tg-0lax">비밀번호</td>
    <td class="tg-0lax">2</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">앞 2자리</td>
  </tr>
  <tr>
    <td class="tg-0lax">12</td>
    <td class="tg-0lax">payPeriodCode</td>
    <td class="tg-0lax">결제주기코드</td>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"><a href="/payapi09.html#91-결제-주기-코드">*별첨 결제주기코드표 참고</a><br/>실제 빌키 승인 요청시에는 사용되지 않고 가맹점관리자에서 조회시에 참고용으로 입력하는 코드임</td>
  </tr>
  <tr>
    <td class="tg-0lax">13</td>
    <td class="tg-0lax">etc</td>
    <td class="tg-0lax">비고</td>
    <td class="tg-0lax">100</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">14</td>
    <td class="tg-0lax">timestamp</td>
    <td class="tg-0lax">타임스탬프</td>
    <td class="tg-0lax">14</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">예) 20190906110100</td>
  </tr>
  <tr>
    <td class="tg-0lax">15</td>
    <td class="tg-0lax">signature</td>
    <td class="tg-0lax">검증값</td>
    <td class="tg-0lax">N/A</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">SHA256<br>(mid+mkey+cardNumber+timestamp)</td>
  </tr>
</tbody>
</table>

#### 2) 신용카드 빌키 발급 응답 파라미터

[//]: # (신용카드 빌키 발급 응답)
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
    <td class="tg-0lax">CardResultCode</td>
    <td class="tg-0lax">카드사 코드</td>
    <td class="tg-0lax">2</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"><a href="/code01.html">* 별첨 카드사(매입사) 코드 참고</a></td>
  </tr>
  <tr>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax">CardKind</td>
    <td class="tg-0lax">카드종류</td>
    <td class="tg-0lax">1</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">0: 개인, 1:법인, 9:기타</td>
  </tr>
  <tr>
    <td class="tg-0lax">5</td>
    <td class="tg-0lax">Billkey</td>
    <td class="tg-0lax">빌키</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">6</td>
    <td class="tg-0lax">Price</td>
    <td class="tg-0lax">금액</td>
    <td class="tg-0lax">10</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">0</td>
  </tr>
  <tr>
    <td class="tg-0lax">7</td>
    <td class="tg-0lax">PayDate</td>
    <td class="tg-0lax">빌키발급날짜</td>
    <td class="tg-0lax">8</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">8</td>
    <td class="tg-0lax">PayTime</td>
    <td class="tg-0lax">빌키발급시간</td>
    <td class="tg-0lax">6</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">9</td>
    <td class="tg-0lax">tid</td>
    <td class="tg-0lax">거래번호</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
</tbody>
</table>

## 3.2 신용카드 비인증 빌키 발급 API  
빌링 결제에 필요한 빌키 발급 시 사용하는 서비스입니다.

발급 받은 빌키로 승인은 3.3 빌링 승인 API로 진행해 주시기 바랍니다.

- 해당 API를 사용하기 위해서는 계약담당자를 통해 별도 사용요청 해주시기 바랍니다.
- 빌링용 테스트 MID : <a href="mailto:mainpg_support@welcomepayments.co.kr">메일로 문의하기</a>

[//]: # (신용카드 빌키 발급 API)
<table class="tg" style="width: 100%">
  <colgroup>
    <col style="width: 20%">
    <col style="width: 80%">
  </colgroup>
  <tbody>
    <tr>
      <td class="tg-0lax">운영</td>
      <td class="tg-0lax">https://payapi.paywelcome.co.kr/noauth/billkey/card</td>
    </tr>
    <tr>
      <td class="tg-0lax">테스트</td>
      <td class="tg-0lax">https://tpayapi.paywelcome.co.kr/noauth/billkey/card</td>
    </tr>
  </tbody>
</table>

#### 1) 신용카드 비인증 빌키 발급 요청 파라미터

[//]: # (신용카드 비인증 빌키 발급 요청 파라미터)
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
    <td class="tg-0lax">goodsName</td>
    <td class="tg-0lax">상품명</td>
    <td class="tg-0lax">80</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">3</td>
    <td class="tg-0lax">price</td>
    <td class="tg-0lax">금액</td>
    <td class="tg-0lax">10</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax">buyerName</td>
    <td class="tg-0lax">구매자명</td>
    <td class="tg-0lax">30</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">5</td>
    <td class="tg-0lax">buyerTel</td>
    <td class="tg-0lax">구매자전화번호</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">6</td>
    <td class="tg-0lax">buyerEmail</td>
    <td class="tg-0lax">구매자이메일</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">7</td>
    <td class="tg-0lax">cardNumber</td>
    <td class="tg-0lax">카드번호</td>
    <td class="tg-0lax">16</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">8</td>
    <td class="tg-0lax">cardExpireYY</td>
    <td class="tg-0lax">유효기간(년)</td>
    <td class="tg-0lax">2</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">2자리</td>
  </tr>
  <tr>
    <td class="tg-0lax">9</td>
    <td class="tg-0lax">cardExpireMM</td>
    <td class="tg-0lax">유효기간(월)</td>
    <td class="tg-0lax">2</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">2자리</td>
  </tr>
  <tr>
    <td class="tg-0lax">10</td>
    <td class="tg-0lax">payPeriodCode</td>
    <td class="tg-0lax">결제주기코드</td>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"><a href="/payapi09.html#91-결제-주기-코드">*별첨 결제주기코드표 참고</a><br/>실제 빌링 승인 요청시에는 사용되지 않고 가맹점관리자에서 조회시에 참고용으로 입력하는 코드임</td>
  </tr>
  <tr>
    <td class="tg-0lax">11</td>
    <td class="tg-0lax">etc</td>
    <td class="tg-0lax">비고</td>
    <td class="tg-0lax">100</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">12</td>
    <td class="tg-0lax">timestamp</td>
    <td class="tg-0lax">타임스탬프</td>
    <td class="tg-0lax">14</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">예) 20190906110100</td>
  </tr>
  <tr>
    <td class="tg-0lax">13</td>
    <td class="tg-0lax">signature</td>
    <td class="tg-0lax">검증값</td>
    <td class="tg-0lax">N/A</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">SHA256<br>(mid+mkey+cardNumber+timestamp)</td>
  </tr>
</tbody>
</table>

#### 2) 신용카드 비인증 빌키 발급 응답 파라미터  

[//]: # (신용카드 빌키 발급 응답)
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
    <td class="tg-0lax">CardResultCode</td>
    <td class="tg-0lax">카드사 코드</td>
    <td class="tg-0lax">2</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"><a href="/code01.html">* 별첨 카드사(매입사) 코드 참고</a></td>
  </tr>
  <tr>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax">Billkey</td>
    <td class="tg-0lax">빌키</td>
    <td class="tg-0lax">40</td>
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
    <td class="tg-0lax">0</td>
  </tr>
  <tr>
    <td class="tg-0lax">6</td>
    <td class="tg-0lax">PayDate</td>
    <td class="tg-0lax">빌키발급날짜</td>
    <td class="tg-0lax">8</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">7</td>
    <td class="tg-0lax">PayTime</td>
    <td class="tg-0lax">빌키발급시간</td>
    <td class="tg-0lax">6</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">8</td>
    <td class="tg-0lax">tid</td>
    <td class="tg-0lax">거래번호</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
</tbody>
</table>

## 3.3 신용카드 빌링 승인 API  
발급된 빌키를 사용하여 승인하는 서비스입니다.

- 해당 API를 사용하기 위해서는 계약담당자를 통해 별도 사용요청 해주시기 바랍니다.
- 빌링용 테스트 MID : <a href="mailto:mainpg_support@welcomepayments.co.kr">메일로 문의하기</a>

[//]: # (신용카드 빌링 승인 API)
<table class="tg" style="width: 100%">
  <colgroup>
    <col style="width: 20%">
    <col style="width: 80%">
  </colgroup>
  <tbody>
    <tr>
      <td class="tg-0lax">운영</td>
      <td class="tg-0lax">https://payapi.paywelcome.co.kr/billing/billpay</td>
    </tr>
    <tr>
      <td class="tg-0lax">테스트</td>
      <td class="tg-0lax">https://tpayapi.paywelcome.co.kr/billing/billpay</td>
    </tr>
  </tbody>
</table>

#### 1) 신용카드 빌링 승인 요청 파라미터

[//]: # (신용카드 빌링 승인 요청 파라미터)
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
    <td class="tg-0lax">oid</td>
    <td class="tg-0lax">상점주문번호</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">3</td>
    <td class="tg-0lax">goodsName</td>
    <td class="tg-0lax">상품명</td>
    <td class="tg-0lax">80</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax">price</td>
    <td class="tg-0lax">금액</td>
    <td class="tg-0lax">10</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">5</td>
    <td class="tg-0lax">tax</td>
    <td class="tg-0lax">부가세</td>
    <td class="tg-0lax">10</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">대상: &#39;부가세업체정함&#39; 설정업체에 한함<br/>주의: 전체금액의 10%이하로 설정가맹점에서 등록시 VAT가 총 상품가격의 10% 초과할 경우는 거절됨</td>
  </tr>
  <tr>
    <td class="tg-0lax">6</td>
    <td class="tg-0lax">taxfree</td>
    <td class="tg-0lax">비과세</td>
    <td class="tg-0lax">10</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">대상: &#39;부가세업체정함&#39; 설정업체에 한함과세되지 않는 금액</td>
  </tr>
  <tr>
    <td class="tg-0lax">7</td>
    <td class="tg-0lax">buyerName</td>
    <td class="tg-0lax">구매자명</td>
    <td class="tg-0lax">30</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">8</td>
    <td class="tg-0lax">buyerTel</td>
    <td class="tg-0lax">구매자전화번호</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">9</td>
    <td class="tg-0lax">buyerEmail</td>
    <td class="tg-0lax">구매자이메일</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">10</td>
    <td class="tg-0lax">billkey</td>
    <td class="tg-0lax">빌키</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">11</td>
    <td class="tg-0lax">cardQuota</td>
    <td class="tg-0lax">할부개월수</td>
    <td class="tg-0lax">2</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">00:일시불, 02:2개월 …</td>
  </tr>
  <tr>
    <td class="tg-0lax">12</td>
    <td class="tg-0lax">quotaInterest</td>
    <td class="tg-0lax">무이자여부</td>
    <td class="tg-0lax">1</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">0:일반, 1:무이자</td>
  </tr>
  <tr>
    <td class="tg-0lax">12</td>
    <td class="tg-0lax">timestamp</td>
    <td class="tg-0lax">타임스탬프</td>
    <td class="tg-0lax">14</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">예) 20190906110100</td>
  </tr>
  <tr>
    <td class="tg-0lax">13</td>
    <td class="tg-0lax">signature</td>
    <td class="tg-0lax">검증값</td>
    <td class="tg-0lax">N/A</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">SHA256<br>(mid+mkey+oid+price+timestamp)</td>
  </tr>
</tbody>
</table>

#### 2) 신용카드 빌링 승인 응답 파라미터

[//]: # (신용카드 빌링 승인 응답)
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
    <td class="tg-0lax">빌링승인날짜</td>
    <td class="tg-0lax">8</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax">PayTime</td>
    <td class="tg-0lax">빌링승인시간</td>
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

## 3.4 신용카드 빌키 삭제 API  
발급된 빌키 삭제 시 사용하는 서비스입니다.

- 해당 API를 사용하기 위해서는 계약담당자를 통해 별도 사용요청 해주시기 바랍니다.
- 빌링용 테스트 MID : <a href="mailto:mainpg_support@welcomepayments.co.kr">메일로 문의하기</a>

[//]: # (신용카드 빌키 삭제 API)
<table class="tg" style="width: 100%">
  <colgroup>
    <col style="width: 20%">
    <col style="width: 80%">
  </colgroup>
  <tbody>
    <tr>
      <td class="tg-0lax">운영</td>
      <td class="tg-0lax">https://payapi.paywelcome.co.kr/billing/billkey/delete</td>
    </tr>
    <tr>
      <td class="tg-0lax">테스트</td>
      <td class="tg-0lax">https://tpayapi.paywelcome.co.kr/billing/billkey/delete</td>
    </tr>
  </tbody>
</table>

#### 1) 신용카드 빌키 삭제 요청 파라미터

[//]: # (신용카드 빌키 삭제 요청 파라미터)
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
    <td class="tg-0lax">billkey</td>
    <td class="tg-0lax">빌키</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">3</td>
    <td class="tg-0lax">timestamp</td>
    <td class="tg-0lax">타임스탬프</td>
    <td class="tg-0lax">14</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">예) 20190906110100</td>
  </tr>
  <tr>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax">signature</td>
    <td class="tg-0lax">검증값</td>
    <td class="tg-0lax">N/A</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">SHA256<br>(mid+mkey+timestamp)</td>
  </tr>
</tbody>
</table>

#### 2) 신용카드 빌키 삭제 응답 파라미터

[//]: # (빌키 삭제 응답)
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
</tbody>
</table>

## 3.5 휴대폰 빌키 승인 API
휴대폰 빌키 발급은 PC Web이나 Mobile Web을 통해서 진행한 후 발급된 빌키를 사용하여 승인하는 서비스입니다. 휴대폰 빌링은 빌키 발급시에 요청한 일자기준 매월 요청시에 전후 5일 이내(예: 1월 5일 발급시에 2월 5일 전후 5일 이내 요청 필요), 요청한 금액과 동일한 금액으로 승인 요청주셔야 정상 승인 처리 됩니다. (일자 및 금액 변경해서 요청할 경우 별도 심사가 필요하므로 영업담당자에 문의 바랍니다.)

- 휴대폰 빌키 승인 테스트 MID :<a href="mailto:mainpg_support@welcomepayments.co.kr">메일로 문의하기</a> (빌키 발급이후 가능)

[//]: # (휴대폰 빌키 승인 API)
<table class="tg" style="width: 100%">
  <colgroup>
    <col style="width: 20%">
    <col style="width: 80%">
  </colgroup>
  <tbody>
    <tr>
      <td class="tg-0lax">운영</td>
      <td class="tg-0lax">https://payapi.paywelcome.co.kr/billing/hppbillpay</td>
    </tr>
    <tr>
      <td class="tg-0lax">테스트</td>
      <td class="tg-0lax">https://tpayapi.paywelcome.co.kr/billing/hppbillpay</td>
    </tr>
  </tbody>
</table>

#### 1) 휴대폰 빌키 승인 요청 파라미터

[//]: # (휴대폰 빌키 승인 요청 파라미터)
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
    <td class="tg-0lax">oid</td>
    <td class="tg-0lax">상점주문번호</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">3</td>
    <td class="tg-0lax">goodsName</td>
    <td class="tg-0lax">상품명</td>
    <td class="tg-0lax">80</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax">price</td>
    <td class="tg-0lax">금액</td>
    <td class="tg-0lax">10</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">5</td>
    <td class="tg-0lax">buyerName</td>
    <td class="tg-0lax">구매자명</td>
    <td class="tg-0lax">30</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">6</td>
    <td class="tg-0lax">buyerTel</td>
    <td class="tg-0lax">구매자전화번호</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">7</td>
    <td class="tg-0lax">buyerEmail</td>
    <td class="tg-0lax">구매자이메일</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">8</td>
    <td class="tg-0lax">billkey</td>
    <td class="tg-0lax">빌키</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">9</td>
    <td class="tg-0lax">timestamp</td>
    <td class="tg-0lax">타임스탬프</td>
    <td class="tg-0lax">14</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">예) 20190906110100</td>
  </tr>
  <tr>
    <td class="tg-0lax">10</td>
    <td class="tg-0lax">signature</td>
    <td class="tg-0lax">검증값</td>
    <td class="tg-0lax">N/A</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">SHA256<br>(mid+mkey+oid+price+timestamp)</td>
  </tr>
</tbody>
</table>

#### 2) 휴대폰 빌키 승인 응답 파라미터

[//]: # (휴대폰 빌키 승인 응답 파라미터)
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
    <td class="tg-0lax">빌링승인날짜</td>
    <td class="tg-0lax">8</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax">PayTime</td>
    <td class="tg-0lax">빌링승인시간</td>
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
</tbody>
</table>