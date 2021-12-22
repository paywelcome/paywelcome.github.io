---
title: PAYAPI 에스크로 API
permalink: payapi06.html
sidebar: payapi_sidebar
folder: payapi
toc: false
---

<div style="display: inline-block; width: 100%;">
  <a style="float:left;" href="/payapi05.html">◀이전페이지</a>
  <a style="float:right;" href="/payapi07.html">다음페이지▶</a>
</div>

# 6. 에스크로 API

## 6.1 에스크로 배송등록 API

에스크로 배송등록시 사용하는 서비스입니다.

- 해당 API를 사용하기 위해서는 계약담당자를 통해 별도 사용요청 해주시기 바랍니다.

[//]: # (에스크로 배송등록 API URL)
<table class="tg" style="width: 100%">
  <colgroup>
    <col style="width: 20%">
    <col style="width: 80%">
  </colgroup>
  <tbody>
    <tr>
      <td class="tg-0lax">운영</td>
      <td class="tg-0lax">https://payapi.paywelcome.co.kr/escrow/delivery</td>
    </tr>
    <tr>
      <td class="tg-0lax">테스트</td>
      <td class="tg-0lax">https://tpayapi.paywelcome.co.kr/escrow/delivery</td>
    </tr>
  </tbody>
</table>

#### 1) 에스크로 배송등록 요청 파라미터

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

[//]: # (에스크로 배송등록 요청 파라미터)
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
    <th class="center-align">길이</th>
    <th class="center-align">필수</th>
    <th class="center-align">암호화</th>
    <th class="center-align">타입</th>
    <th class="left-align">비고</th>
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
    <td class="center-align">clientIp</td>
    <td class="center-align">IP</td>
    <td class="center-align">15</td>
    <td class="center-align">○</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">3</td>
    <td class="center-align">tid</td>
    <td class="center-align">거래ID</td>
    <td class="center-align">40</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">4</td>
    <td class="center-align">oid</td>
    <td class="center-align">주문번호</td>
    <td class="center-align">40</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">5</td>
    <td class="center-align">soid</td>
    <td class="center-align">주문번호 순번</td>
    <td class="center-align">2</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">같은 oid로 여러개 등록시</td>
  </tr>
  <tr>
    <td class="center-align">6</td>
    <td class="center-align">report</td>
    <td class="center-align">에스크로등록형태</td>
    <td class="center-align">1</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">I:등록, U:변경</td>
  </tr>
  <tr>
    <td class="center-align">7</td>
    <td class="center-align">invoice</td>
    <td class="center-align">운송장번호</td>
    <td class="center-align"></td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">8</td>
    <td class="center-align">registName</td>
    <td class="center-align">배송등록자</td>
    <td class="center-align"></td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">9</td>
    <td class="center-align">exCode</td>
    <td class="center-align">택배사코드</td>
    <td class="center-align"></td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"><a href="/code01.html#4-에스크로-배송등록-택배사-코드">별첨 에스크로 배송등록 택배사 코드 참고</a></td>
  </tr>
  <tr>
    <td class="center-align">10</td>
    <td class="center-align">exName</td>
    <td class="center-align">택배사명</td>
    <td class="center-align"></td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">11</td>
    <td class="center-align">charge</td>
    <td class="center-align">배송비지급</td>
    <td class="center-align">1</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">S:판매자부담, B:구매자부담</td>
  </tr>
  <tr>
    <td class="center-align">12</td>
    <td class="center-align">invoiceDay</td>
    <td class="center-align">배송등록 확인일자</td>
    <td class="center-align"></td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">13</td>
    <td class="center-align">sendName</td>
    <td class="center-align">송신자 이름</td>
    <td class="center-align"></td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">14</td>
    <td class="center-align">sendPost</td>
    <td class="center-align">송신자 우편번호</td>
    <td class="center-align"></td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">구분자없이</td>
  </tr>
  <tr>
    <td class="center-align">15</td>
    <td class="center-align">sendAddr1</td>
    <td class="center-align">송신자 주소1</td>
    <td class="center-align"></td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">16</td>
    <td class="center-align">sendAddr2</td>
    <td class="center-align">송신자 주소2</td>
    <td class="center-align"></td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">17</td>
    <td class="center-align">sendTel</td>
    <td class="center-align">송신자 전화번호</td>
    <td class="center-align"></td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">18</td>
    <td class="center-align">recvName</td>
    <td class="center-align">수신자 이름</td>
    <td class="center-align"></td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">19</td>
    <td class="center-align">recvPost</td>
    <td class="center-align">수신자 우편번호</td>
    <td class="center-align">40</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">구분자없이</td>
  </tr>
  <tr>
    <td class="center-align">20</td>
    <td class="center-align">recvAddr</td>
    <td class="center-align">수신자 주소</td>
    <td class="center-align"></td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">21</td>
    <td class="center-align">recvTel</td>
    <td class="center-align">수신자 전화번호</td>
    <td class="center-align"></td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">22</td>
    <td class="center-align">goodsCode</td>
    <td class="center-align">상품코드</td>
    <td class="center-align"></td>
    <td class="center-align"></td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">23</td>
    <td class="center-align">goods</td>
    <td class="center-align">상품명</td>
    <td class="center-align"></td>
    <td class="center-align"></td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">24</td>
    <td class="center-align">goodsCnt</td>
    <td class="center-align">상품수량</td>
    <td class="center-align"></td>
    <td class="center-align"></td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">25</td>
    <td class="center-align">price</td>
    <td class="center-align">가격</td>
    <td class="center-align"></td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">26</td>
    <td class="center-align">timestamp</td>
    <td class="center-align">타임스탬프</td>
    <td class="center-align">14</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">예) 20190906110100</td>
  </tr>
  <tr>
    <td class="center-align">4</td>
    <td class="center-align">signature</td>
    <td class="center-align">검증값</td>
    <td class="center-align">N/A</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">Sha256<br>(mid+mkey+timestamp)</td>
  </tr>
</tbody>
</table>

</div>
</details>

#### 2) 에스크로 배송등록 응답 파라미터

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

[//]: # (에스크로 배송등록 응답 파라미터)
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
    <th class="center-align">길이</th>
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
    <td class="left-align">310000: 정상, 그 외 실패</td>
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
    <td class="center-align">ResultDate</td>
    <td class="center-align">등록날짜</td>
    <td class="center-align">8</td>
    <td class="center-align">△</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">4</td>
    <td class="center-align">ResultTime</td>
    <td class="center-align">등록시간</td>
    <td class="center-align">6</td>
    <td class="center-align">△</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
</tbody>
</table>

</div>
</details>

## 6.2 에스크로 구매확정 API

에스크로 구매확정시 사용하는 서비스입니다.

- 해당 API를 사용하기 위해서는 계약담당자를 통해 별도 사용요청 해주시기 바랍니다.

[//]: # (에스크로 구매확정 API URL)
<table class="tg" style="width: 100%">
  <colgroup>
    <col style="width: 20%">
    <col style="width: 80%">
  </colgroup>
   <tbody>
    <tr>
      <td class="tg-0lax">운영</td>
      <td class="tg-0lax">https://payapi.paywelcome.co.kr/escrow/buyconfirm</td>
    </tr>
    <tr>
      <td class="tg-0lax">테스트</td>
      <td class="tg-0lax">https://tpayapi.paywelcome.co.kr/escrow/buyconfirm</td>
    </tr>
  </tbody>
</table>

#### 1) 에스크로 구매확정 요청 파라미터

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

[//]: # (에스크로 구매확정 요청 파라미터)
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
    <th class="center-align">길이</th>
    <th class="center-align">필수</th>
    <th class="center-align">암호화</th>
    <th class="center-align">타입</th>
    <th class="left-align">비고</th>
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
    <td class="center-align">clientIp</td>
    <td class="center-align">IP</td>
    <td class="center-align">15</td>
    <td class="center-align">○</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">3</td>
    <td class="center-align">originalTid</td>
    <td class="center-align">거래ID</td>
    <td class="center-align">40</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">4</td>
    <td class="center-align">buyName</td>
    <td class="center-align">처리자 이름</td>
    <td class="center-align"></td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">5</td>
    <td class="center-align">timestamp</td>
    <td class="center-align">타임스탬프</td>
    <td class="center-align">14</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">예) 20190906110100</td>
  </tr>
  <tr>
    <td class="center-align">4</td>
    <td class="center-align">signature</td>
    <td class="center-align">검증값</td>
    <td class="center-align">N/A</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">Sha256<br>(mid+mkey+timestamp)</td>
  </tr>
</tbody>
</table>

</div>
</details>

#### 2) 에스크로 구매확정 응답 파라미터

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

[//]: # (에스크로 구매확정 응답 파라미터)
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
    <th class="center-align">길이</th>
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
    <td class="left-align">310000: 정상, 그 외 실패</td>
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
    <td class="center-align">ResultDate</td>
    <td class="center-align">구매확정날짜</td>
    <td class="center-align">8</td>
    <td class="center-align">△</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">4</td>
    <td class="center-align">ResultTime</td>
    <td class="center-align">구매확정시간</td>
    <td class="center-align">6</td>
    <td class="center-align">△</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
</tbody>
</table>

</div>
</details>

## 6.3 에스크로 구매거절 API

에스크로 구매거절시 사용하는 서비스입니다.

- 해당 API를 사용하기 위해서는 계약담당자를 통해 별도 사용요청 해주시기 바랍니다.

[//]: # (에스크로 구매거절 API URL)
<table class="tg" style="width: 100%">
  <colgroup>
    <col style="width: 20%">
    <col style="width: 80%">
  </colgroup>
  <tbody>
    <tr>
      <td class="tg-0lax">운영</td>
      <td class="tg-0lax">https://payapi.paywelcome.co.kr/escrow/buydeny</td>
    </tr>
    <tr>
      <td class="tg-0lax">테스트</td>
      <td class="tg-0lax">https://tpayapi.paywelcome.co.kr/escrow/buydeny</td>
    </tr>
  </tbody>
</table>

#### 1) 에스크로 구매거절 요청 파라미터

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

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
    <th class="center-align">길이</th>
    <th class="center-align">필수</th>
    <th class="center-align">암호화</th>
    <th class="center-align">타입</th>
    <th class="left-align">비고</th>
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
    <td class="center-align">clientIp</td>
    <td class="center-align">IP</td>
    <td class="center-align">15</td>
    <td class="center-align">○</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">3</td>
    <td class="center-align">originalTid</td>
    <td class="center-align">거래ID</td>
    <td class="center-align">40</td>
    <td class="center-align">○</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">4</td>
    <td class="center-align">buyName</td>
    <td class="center-align">처리자 이름</td>
    <td class="center-align"></td>
    <td class="center-align">○</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">5</td>
    <td class="center-align">denyMsg</td>
    <td class="center-align">구매거절 사유</td>
    <td class="center-align"></td>
    <td class="center-align"></td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">6</td>
    <td class="center-align">refundBankCode</td>
    <td class="center-align">환불 은행 코드</td>
    <td class="center-align">2</td>
    <td class="center-align"></td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"><a href="/code01.html#92-카드-발급사은행사-코드">* 별첨 카드/발급사(은행사) 코드</a></td>
  </tr>
  <tr>
    <td class="center-align">7</td>
    <td class="center-align">refundAccount</td>
    <td class="center-align">환불 계좌번호</td>
    <td class="center-align">13</td>
    <td class="center-align"></td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">8</td>
    <td class="center-align">refundName</td>
    <td class="center-align">환불 계좌주명</td>
    <td class="center-align"></td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">9</td>
    <td class="center-align">timestamp</td>
    <td class="center-align">타임스탬프</td>
    <td class="center-align">14</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">예) 20190906110100</td>
  </tr>
  <tr>
    <td class="center-align">10</td>
    <td class="center-align">signature</td>
    <td class="center-align">검증값</td>
    <td class="center-align">N/A</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">Sha256<br>(mid+mkey+timestamp)</td>
  </tr>
</tbody>
</table>

</div>
</details>

#### 2) 에스크로 구매거절 응답 파라미터

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

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
    <th class="center-align">길이</th>
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
    <td class="left-align">310000: 정상, 그 외 실패</td>
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
    <td class="center-align">ResultDate</td>
    <td class="center-align">구매거절날짜</td>
    <td class="center-align">8</td>
    <td class="center-align">△</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">4</td>
    <td class="center-align">ResultTime</td>
    <td class="center-align">구매거절시간</td>
    <td class="center-align">6</td>
    <td class="center-align">△</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
</tbody>
</table>

</div>
</details>

## 6.4 에스크로 구매거절 확인 API

에스크로 구매거절 확인시 사용하는 서비스입니다.

- 해당 API를 사용하기 위해서는 계약담당자를 통해 별도 사용요청 해주시기 바랍니다.

[//]: # (에스크로 구매거절 확인 API URL)
<table class="tg" style="width: 100%">
  <colgroup>
    <col style="width: 20%">
    <col style="width: 80%">
  </colgroup>
  <tbody>
    <tr>
      <td class="tg-0lax">운영</td>
      <td class="tg-0lax">https://payapi.paywelcome.co.kr/escrow/buydeny</td>
    </tr>
    <tr>
      <td class="tg-0lax">테스트</td>
      <td class="tg-0lax">https://tpayapi.paywelcome.co.kr/escrow/buydeny</td>
    </tr>
  </tbody>
</table>

#### 1) 에스크로 구매거절 확인 요청 파라미터

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

[//]: # (에스크로 구매거절 확인 요청 파라미터)
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
    <th class="center-align">길이</th>
    <th class="center-align">필수</th>
    <th class="center-align">암호화</th>
    <th class="center-align">타입</th>
    <th class="left-align">비고</th>
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
    <td class="center-align">clientIp</td>
    <td class="center-align">IP</td>
    <td class="center-align">15</td>
    <td class="center-align">○</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">3</td>
    <td class="center-align">originalTid</td>
    <td class="center-align">거래ID</td>
    <td class="center-align">40</td>
    <td class="center-align">○</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">4</td>
    <td class="center-align">dcnfName</td>
    <td class="center-align">처리자 이름</td>
    <td class="center-align"></td>
    <td class="center-align">○</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">5</td>
    <td class="center-align">timestamp</td>
    <td class="center-align">타임스탬프</td>
    <td class="center-align">14</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">예) 20190906110100</td>
  </tr>
  <tr>
    <td class="center-align">6</td>
    <td class="center-align">signature</td>
    <td class="center-align">검증값</td>
    <td class="center-align">N/A</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">Sha256<br>(mid+mkey+timestamp)</td>
  </tr>
</tbody>
</table>

</div>
</details>

#### 2) 에스크로 구매거절 확인 응답 파라미터

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

[//]: # (에스크로 구매거절 확인 응답 파라미터)
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
    <th class="center-align">길이</th>
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
    <td class="left-align">310000: 정상, 그 외 실패</td>
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
    <td class="center-align">ResultDate</td>
    <td class="center-align">확인날짜</td>
    <td class="center-align">8</td>
    <td class="center-align">△</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">4</td>
    <td class="center-align">ResultTime</td>
    <td class="center-align">확인시간</td>
    <td class="center-align">6</td>
    <td class="center-align">△</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
</tbody>
</table>

</div>
</details>

## 6.5 에스크로 상태조회 API

에스크로 상태조회시 사용하는 서비스입니다.

- 해당 API를 사용하기 위해서는 계약담당자를 통해 별도 사용요청 해주시기 바랍니다.

[//]: # (에스크로 상태조회 API URL)
<table class="tg" style="width: 100%">
  <colgroup>
    <col style="width: 20%">
    <col style="width: 80%">
  </colgroup>
  <tbody>
    <tr>
      <td class="tg-0lax">운영</td>
      <td class="tg-0lax">https://payapi.paywelcome.co.kr/escrow/checkstatus</td>
    </tr>
    <tr>
      <td class="tg-0lax">테스트</td>
      <td class="tg-0lax">https://tpayapi.paywelcome.co.kr/escrow/checkstatus</td>
    </tr>
  </tbody>
</table>

#### 1) 에스크로 상태조회 요청 파라미터

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

[//]: # (에스크로 상태조회 요청 파라미터)
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
    <th class="center-align">길이</th>
    <th class="center-align">필수</th>
    <th class="center-align">암호화</th>
    <th class="center-align">타입</th>
    <th class="left-align">비고</th>
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
    <td class="center-align">clientIp</td>
    <td class="center-align">IP</td>
    <td class="center-align">15</td>
    <td class="center-align">○</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">3</td>
    <td class="center-align">tid</td>
    <td class="center-align">거래ID</td>
    <td class="center-align">40</td>
    <td class="center-align">○</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">4</td>
    <td class="center-align">timestamp</td>
    <td class="center-align">타임스탬프</td>
    <td class="center-align">14</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">예) 20190906110100</td>
  </tr>
  <tr>
    <td class="center-align">5</td>
    <td class="center-align">signature</td>
    <td class="center-align">검증값</td>
    <td class="center-align">N/A</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">Sha256<br>(mid+mkey+timestamp)</td>
  </tr>
</tbody>
</table>

</div>
</details>

#### 2) 에스크로 상태조회 응답 파라미터

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

[//]: # (에스크로 상태조회 응답 파라미터)
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
    <th class="center-align">길이</th>
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
    <td class="center-align">idMerchant</td>
    <td class="center-align">가맹점ID</td>
    <td class="center-align"></td>
    <td class="center-align"></td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">4</td>
    <td class="center-align">noOid</td>
    <td class="center-align">주문번호</td>
    <td class="center-align"></td>
    <td class="center-align"></td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">5</td>
    <td class="center-align">noTid</td>
    <td class="center-align">거래ID</td>
    <td class="center-align"></td>
    <td class="center-align"></td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">6</td>
    <td class="center-align">clStatus</td>
    <td class="center-align">거래상태</td>
    <td class="center-align"></td>
    <td class="center-align"></td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">0:승인, 1:당일취소, 2:익일취소, 10:구매거절, 3:구매확정</td>
  </tr>
  <tr>
    <td class="center-align">7</td>
    <td class="center-align">dtAppl</td>
    <td class="center-align">승인일자</td>
    <td class="center-align"></td>
    <td class="center-align"></td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">8</td>
    <td class="center-align">clPaymethod</td>
    <td class="center-align">지불수단코드</td>
    <td class="center-align"></td>
    <td class="center-align"></td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">0:신용카드, 16:계좌이체, 17:가상계좌</td>
  </tr>
  <tr>
    <td class="center-align">9</td>
    <td class="center-align">price</td>
    <td class="center-align">가격</td>
    <td class="center-align"></td>
    <td class="center-align"></td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">10</td>
    <td class="center-align">msgDeny</td>
    <td class="center-align">구매거절사유</td>
    <td class="center-align"></td>
    <td class="center-align"></td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
</tbody>
</table>

</div>
</details>

<div style="display: inline-block; width: 100%;">
  <a style="float:left;" href="/payapi05.html">◀이전페이지</a>
  <a style="float:right;" href="/payapi07.html">다음페이지▶</a>
</div>