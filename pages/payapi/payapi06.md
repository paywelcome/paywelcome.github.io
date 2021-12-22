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
    <td class="tg-0lax">clientIp</td>
    <td class="tg-0lax">IP</td>
    <td class="tg-0lax">15</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">3</td>
    <td class="tg-0lax">tid</td>
    <td class="tg-0lax">거래ID</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax">oid</td>
    <td class="tg-0lax">주문번호</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">5</td>
    <td class="tg-0lax">soid</td>
    <td class="tg-0lax">주문번호 순번</td>
    <td class="tg-0lax">2</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">같은 oid로 여러개 등록시</td>
  </tr>
  <tr>
    <td class="tg-0lax">6</td>
    <td class="tg-0lax">report</td>
    <td class="tg-0lax">에스크로등록형태</td>
    <td class="tg-0lax">1</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">I:등록, U:변경</td>
  </tr>
  <tr>
    <td class="tg-0lax">7</td>
    <td class="tg-0lax">invoice</td>
    <td class="tg-0lax">운송장번호</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">8</td>
    <td class="tg-0lax">registName</td>
    <td class="tg-0lax">배송등록자</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">9</td>
    <td class="tg-0lax">exCode</td>
    <td class="tg-0lax">택배사코드</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"><a href="/payapi09.html#92-에스크로-배송등록-택배사-코드">별첨 에스크로 배송등록 택배사 코드 참고</a></td>
  </tr>
  <tr>
    <td class="tg-0lax">10</td>
    <td class="tg-0lax">exName</td>
    <td class="tg-0lax">택배사명</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">11</td>
    <td class="tg-0lax">charge</td>
    <td class="tg-0lax">배송비지급</td>
    <td class="tg-0lax">1</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">S:판매자부담, B:구매자부담</td>
  </tr>
  <tr>
    <td class="tg-0lax">12</td>
    <td class="tg-0lax">invoiceDay</td>
    <td class="tg-0lax">배송등록 확인일자</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">13</td>
    <td class="tg-0lax">sendName</td>
    <td class="tg-0lax">송신자 이름</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">14</td>
    <td class="tg-0lax">sendPost</td>
    <td class="tg-0lax">송신자 우편번호</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">구분자없이</td>
  </tr>
  <tr>
    <td class="tg-0lax">15</td>
    <td class="tg-0lax">sendAddr1</td>
    <td class="tg-0lax">송신자 주소1</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">16</td>
    <td class="tg-0lax">sendAddr2</td>
    <td class="tg-0lax">송신자 주소2</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">17</td>
    <td class="tg-0lax">sendTel</td>
    <td class="tg-0lax">송신자 전화번호</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">18</td>
    <td class="tg-0lax">recvName</td>
    <td class="tg-0lax">수신자 이름</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">19</td>
    <td class="tg-0lax">recvPost</td>
    <td class="tg-0lax">수신자 우편번호</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">구분자없이</td>
  </tr>
  <tr>
    <td class="tg-0lax">20</td>
    <td class="tg-0lax">recvAddr</td>
    <td class="tg-0lax">수신자 주소</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">21</td>
    <td class="tg-0lax">recvTel</td>
    <td class="tg-0lax">수신자 전화번호</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">22</td>
    <td class="tg-0lax">goodsCode</td>
    <td class="tg-0lax">상품코드</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">23</td>
    <td class="tg-0lax">goods</td>
    <td class="tg-0lax">상품명</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">24</td>
    <td class="tg-0lax">goodsCnt</td>
    <td class="tg-0lax">상품수량</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">25</td>
    <td class="tg-0lax">price</td>
    <td class="tg-0lax">가격</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">26</td>
    <td class="tg-0lax">timestamp</td>
    <td class="tg-0lax">타임스탬프</td>
    <td class="tg-0lax">14</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">예) 20190906110100</td>
  </tr>
  <tr>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax">signature</td>
    <td class="tg-0lax">검증값</td>
    <td class="tg-0lax">N/A</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">Sha256<br>(mid+mkey+timestamp)</td>
  </tr>
</tbody>
</table>

#### 2) 에스크로 배송등록 응답 파라미터

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
    <td class="tg-0lax">310000: 정상, 그 외 실패</td>
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
    <td class="tg-0lax">ResultDate</td>
    <td class="tg-0lax">등록날짜</td>
    <td class="tg-0lax">8</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax">ResultTime</td>
    <td class="tg-0lax">등록시간</td>
    <td class="tg-0lax">6</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
</tbody>
</table>

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
    <td class="tg-0lax">clientIp</td>
    <td class="tg-0lax">IP</td>
    <td class="tg-0lax">15</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">3</td>
    <td class="tg-0lax">originalTid</td>
    <td class="tg-0lax">거래ID</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax">buyName</td>
    <td class="tg-0lax">처리자 이름</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">5</td>
    <td class="tg-0lax">timestamp</td>
    <td class="tg-0lax">타임스탬프</td>
    <td class="tg-0lax">14</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">예) 20190906110100</td>
  </tr>
  <tr>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax">signature</td>
    <td class="tg-0lax">검증값</td>
    <td class="tg-0lax">N/A</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">Sha256<br>(mid+mkey+timestamp)</td>
  </tr>
</tbody>
</table>

#### 2) 에스크로 구매확정 응답 파라미터

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
    <td class="tg-0lax">310000: 정상, 그 외 실패</td>
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
    <td class="tg-0lax">ResultDate</td>
    <td class="tg-0lax">구매확정날짜</td>
    <td class="tg-0lax">8</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax">ResultTime</td>
    <td class="tg-0lax">구매확정시간</td>
    <td class="tg-0lax">6</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
</tbody>
</table>

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
    <td class="tg-0lax">clientIp</td>
    <td class="tg-0lax">IP</td>
    <td class="tg-0lax">15</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">3</td>
    <td class="tg-0lax">originalTid</td>
    <td class="tg-0lax">거래ID</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax">buyName</td>
    <td class="tg-0lax">처리자 이름</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">5</td>
    <td class="tg-0lax">denyMsg</td>
    <td class="tg-0lax">구매거절 사유</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">6</td>
    <td class="tg-0lax">refundBankCode</td>
    <td class="tg-0lax">환불 은행 코드</td>
    <td class="tg-0lax">2</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"><a href="/code01.html#92-카드-발급사은행사-코드">* 별첨 카드/발급사(은행사) 코드</a></td>
  </tr>
  <tr>
    <td class="tg-0lax">7</td>
    <td class="tg-0lax">refundAccount</td>
    <td class="tg-0lax">환불 계좌번호</td>
    <td class="tg-0lax">13</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">8</td>
    <td class="tg-0lax">refundName</td>
    <td class="tg-0lax">환불 계좌주명</td>
    <td class="tg-0lax"></td>
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
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">예) 20190906110100</td>
  </tr>
  <tr>
    <td class="tg-0lax">10</td>
    <td class="tg-0lax">signature</td>
    <td class="tg-0lax">검증값</td>
    <td class="tg-0lax">N/A</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">Sha256<br>(mid+mkey+timestamp)</td>
  </tr>
</tbody>
</table>

#### 2) 에스크로 구매거절 응답 파라미터

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
    <td class="tg-0lax">310000: 정상, 그 외 실패</td>
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
    <td class="tg-0lax">ResultDate</td>
    <td class="tg-0lax">구매거절날짜</td>
    <td class="tg-0lax">8</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax">ResultTime</td>
    <td class="tg-0lax">구매거절시간</td>
    <td class="tg-0lax">6</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
</tbody>
</table>

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
      <td class="tg-0lax">https://payapi.paywelcome.co.kr/escrow/denyconfirm</td>
    </tr>
    <tr>
      <td class="tg-0lax">테스트</td>
      <td class="tg-0lax">https://tpayapi.paywelcome.co.kr/escrow/denyconfirm</td>
    </tr>
  </tbody>
</table>

#### 1) 에스크로 구매거절 확인 요청 파라미터

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
    <td class="tg-0lax">clientIp</td>
    <td class="tg-0lax">IP</td>
    <td class="tg-0lax">15</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">3</td>
    <td class="tg-0lax">originalTid</td>
    <td class="tg-0lax">거래ID</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax">dcnfName</td>
    <td class="tg-0lax">처리자 이름</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">5</td>
    <td class="tg-0lax">timestamp</td>
    <td class="tg-0lax">타임스탬프</td>
    <td class="tg-0lax">14</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">예) 20190906110100</td>
  </tr>
  <tr>
    <td class="tg-0lax">6</td>
    <td class="tg-0lax">signature</td>
    <td class="tg-0lax">검증값</td>
    <td class="tg-0lax">N/A</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">Sha256<br>(mid+mkey+timestamp)</td>
  </tr>
</tbody>
</table>

#### 2) 에스크로 구매거절 확인 응답 파라미터

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
    <td class="tg-0lax">310000: 정상, 그 외 실패</td>
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
    <td class="tg-0lax">ResultDate</td>
    <td class="tg-0lax">확인날짜</td>
    <td class="tg-0lax">8</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax">ResultTime</td>
    <td class="tg-0lax">확인시간</td>
    <td class="tg-0lax">6</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
</tbody>
</table>

## 6.5 에스크로 상태조회 API

에스크로 상태조회시 사용하는 서비스입니다.

- 해당 API를 사용하기 위해서는 계약담당자를 통해 별도 사용요청 해주시기 바랍니다.

20211216 확인필요

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
    <td class="tg-0lax">clientIp</td>
    <td class="tg-0lax">IP</td>
    <td class="tg-0lax">15</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">3</td>
    <td class="tg-0lax">tid</td>
    <td class="tg-0lax">거래ID</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax">timestamp</td>
    <td class="tg-0lax">타임스탬프</td>
    <td class="tg-0lax">14</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">예) 20190906110100</td>
  </tr>
  <tr>
    <td class="tg-0lax">5</td>
    <td class="tg-0lax">signature</td>
    <td class="tg-0lax">검증값</td>
    <td class="tg-0lax">N/A</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">Sha256<br>(mid+mkey+timestamp)</td>
  </tr>
</tbody>
</table>

#### 2) 에스크로 상태조회 응답 파라미터

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
    <td class="tg-0lax">idMerchant</td>
    <td class="tg-0lax">가맹점ID</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax">noOid</td>
    <td class="tg-0lax">주문번호</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">5</td>
    <td class="tg-0lax">noTid</td>
    <td class="tg-0lax">거래ID</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">6</td>
    <td class="tg-0lax">clStatus</td>
    <td class="tg-0lax">거래상태</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">0:승인, 1:당일취소, 2:익일취소, 10:구매거절, 3:구매확정</td>
  </tr>
  <tr>
    <td class="tg-0lax">7</td>
    <td class="tg-0lax">dtAppl</td>
    <td class="tg-0lax">승인일자</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">8</td>
    <td class="tg-0lax">clPaymethod</td>
    <td class="tg-0lax">지불수단코드</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">0:신용카드, 16:계좌이체, 17:가상계좌</td>
  </tr>
  <tr>
    <td class="tg-0lax">9</td>
    <td class="tg-0lax">price</td>
    <td class="tg-0lax">가격</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">10</td>
    <td class="tg-0lax">msgDeny</td>
    <td class="tg-0lax">구매거절사유</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
</tbody>
</table>

<div style="display: inline-block; width: 100%;">
  <a style="float:left;" href="/payapi05.html">◀이전페이지</a>
  <a style="float:right;" href="/payapi07.html">다음페이지▶</a>
</div>