---
title: PAYAPI
permalink: payapi02.html
sidebar: payapi_sidebar
folder: payapi
toc: false
---

<div style="display: inline-block; width: 100%;">
  <a style="float:left;" href="/payapi01.html">◀이전페이지</a>
  <a style="float:right;" href="/payapi03.html">다음페이지▶</a>
</div>

# 2. 결제취소 API

## 2.1 전체 취소 API

승인 완료 후, 해당 승인 건에 대해 전체 취소 시 사용하는 서비스입니다.

[//]: # (취소 API URL)
<table class="tg" style="width: 100%">
  <colgroup>
    <col style="width: 20%">
    <col style="width: 80%">
  </colgroup>
  <tbody>
    <tr>
      <td class="tg-0lax">운영</td>
      <td class="tg-0lax">https://payapi.paywelcome.co.kr/cancel/cancel</td>
    </tr>
    <tr>
      <td class="tg-0lax">테스트</td>
      <td class="tg-0lax">https://tpayapi.paywelcome.co.kr/cancel/cancel</td>
    </tr>
  </tbody>
</table>

#### 1) 전체 취소 요청 파라미터

[//]: # (전체취소 요청)
<table class="tg" style="table-layout: fixed; width: 100%">
<colgroup>
<col style="text-align: center; width: 5%">
<col style="text-align: center; width: 12%">
<col style="text-align: center; width: 15%">
<col style="text-align: center; width: 8%">
<col style="text-align: center; width: 8%">
<col style="text-align: center; width: 8%">
<col style="text-align: center; width: 10%">
<col style="text-align: left; width: 34%">
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
    <td class="tg-0lax" style="text-align: center;">1</td>
    <td class="tg-0lax" style="text-align: center;">payType</td>
    <td class="tg-0lax" style="text-align: center;">결제수단</td>
    <td class="tg-0lax" style="text-align: center;">10</td>
    <td class="tg-0lax" style="text-align: center;">○</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">예) card(신용카드), hpp(휴대폰), vbank(가상계좌), bank(계좌이체)</td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">2</td>
    <td class="tg-0lax" style="text-align: center;">mid</td>
    <td class="tg-0lax" style="text-align: center;">가맹점ID</td>
    <td class="tg-0lax" style="text-align: center;">10</td>
    <td class="tg-0lax" style="text-align: center;">○</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">3</td>
    <td class="tg-0lax" style="text-align: center;">tid</td>
    <td class="tg-0lax" style="text-align: center;">거래ID</td>
    <td class="tg-0lax" style="text-align: center;">40</td>
    <td class="tg-0lax" style="text-align: center;">○</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">4</td>
    <td class="tg-0lax" style="text-align: center;">price</td>
    <td class="tg-0lax" style="text-align: center;">취소 금액</td>
    <td class="tg-0lax" style="text-align: center;">22</td>
    <td class="tg-0lax" style="text-align: center;">○</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">콤마(,) 필히 제거</td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;" >5</td>
    <td class="tg-0lax" style="text-align: center;" >currency</td>
    <td class="tg-0lax" style="text-align: center;" >통화</td>
    <td class="tg-0lax" style="text-align: center;" >3</td>
    <td class="tg-0lax" style="text-align: center;" >○</td>
    <td class="tg-0lax" style="text-align: center;" >X</td>
    <td class="tg-0lax" style="text-align: center;" >String</td>
    <td class="tg-0lax">WON / USD</td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">6</td>
    <td class="tg-0lax" style="text-align: center;">timestamp</td>
    <td class="tg-0lax" style="text-align: center;">타임스탬프</td>
    <td class="tg-0lax" style="text-align: center;">14</td>
    <td class="tg-0lax" style="text-align: center;">○</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">예) 20190906110100</td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">7</td>
    <td class="tg-0lax" style="text-align: center;">signature</td>
    <td class="tg-0lax" style="text-align: center;">검증값</td>
    <td class="tg-0lax" style="text-align: center;">N/A</td>
    <td class="tg-0lax" style="text-align: center;">○</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">SHA256<br>(mid+mkey+timestamp)</td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">8</td>
    <td class="tg-0lax" style="text-align: center;">cancelType</td>
    <td class="tg-0lax" style="text-align: center;">망취소옵션</td>
    <td class="tg-0lax" style="text-align: center;">1</td>
    <td class="tg-0lax" style="text-align: center;"></td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">모바일 망취소일 경우 사용<br>모바일망취소:C</td>
  </tr>
</tbody>
</table>

#### 1) 전체 취소 응답 파라미터

[//]: # (전체취소 응답)
<table class="tg" style="table-layout: fixed; width: 100%">
<colgroup>
<col style="text-align: center; width: 5%">
<col style="text-align: center; width: 12%">
<col style="text-align: center; width: 15%">
<col style="text-align: center; width: 8%">
<col style="text-align: center; width: 8%">
<col style="text-align: center; width: 8%">
<col style="text-align: center; width: 10%">
<col style="text-align: left; width: 34%">
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
    <td class="tg-0lax" style="text-align: center;">1</td>
    <td class="tg-0lax" style="text-align: center;">ResultCode</td>
    <td class="tg-0lax" style="text-align: center;">결과코드</td>
    <td class="tg-0lax" style="text-align: center;">6</td>
    <td class="tg-0lax" style="text-align: center;">○</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">00: 정상, 그 외 실패</td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">2</td>
    <td class="tg-0lax" style="text-align: center;">ResultMsg</td>
    <td class="tg-0lax" style="text-align: center;">결과메시지</td>
    <td class="tg-0lax" style="text-align: center;">100</td>
    <td class="tg-0lax" style="text-align: center;">○</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">3</td>
    <td class="tg-0lax" style="text-align: center;">Mid</td>
    <td class="tg-0lax" style="text-align: center;">가맹점 ID</td>
    <td class="tg-0lax" style="text-align: center;">10</td>
    <td class="tg-0lax" style="text-align: center;">△</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">성공 시에만 전달</td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">4</td>
    <td class="tg-0lax" style="text-align: center;">Tid</td>
    <td class="tg-0lax" style="text-align: center;">거래ID</td>
    <td class="tg-0lax" style="text-align: center;">40</td>
    <td class="tg-0lax" style="text-align: center;">△</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">성공 시에만 전달</td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">5</td>
    <td class="tg-0lax" style="text-align: center;">Moid</td>
    <td class="tg-0lax" style="text-align: center;">주문번호</td>
    <td class="tg-0lax" style="text-align: center;">64</td>
    <td class="tg-0lax" style="text-align: center;">△</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">성공 시에만 전달</td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">6</td>
    <td class="tg-0lax" style="text-align: center;">Price</td>
    <td class="tg-0lax" style="text-align: center;">취소 금액</td>
    <td class="tg-0lax" style="text-align: center;">22</td>
    <td class="tg-0lax" style="text-align: center;">△</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">성공 시에만 전달</td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">7</td>
    <td class="tg-0lax" style="text-align: center;">CancelDate</td>
    <td class="tg-0lax" style="text-align: center;">취소 날짜</td>
    <td class="tg-0lax" style="text-align: center;">8</td>
    <td class="tg-0lax" style="text-align: center;">△</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">성공 시에만 전달<br>(YYYYMMDD)</td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">8</td>
    <td class="tg-0lax" style="text-align: center;">CancelTime</td>
    <td class="tg-0lax" style="text-align: center;">취소 시간</td>
    <td class="tg-0lax" style="text-align: center;">6</td>
    <td class="tg-0lax" style="text-align: center;">△</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">성공 시에만 전달<br>(hhmmss)</td>
  </tr>
</tbody>
</table>

## 2.2 부분 취소 API  
승인 완료 후, 해당 승인 건에 대해 부분 취소 시 사용하는 서비스입니다. 부분취소 후 남은 금액 취소는 부분취소 API, Tid (거래ID) 를 사용합니다.

[//]: # (부분 취소 API URL)
<table class="tg" style="width: 100%">
  <colgroup>
    <col style="width: 20%">
    <col style="width: 80%">
  </colgroup>
  <tbody>
    <tr>
      <td class="tg-0lax">운영</td>
      <td class="tg-0lax">https://payapi.paywelcome.co.kr/cancel/repay</td>
    </tr>
    <tr>
      <td class="tg-0lax">테스트</td>
      <td class="tg-0lax">https://tpayapi.paywelcome.co.kr/cancel/repay</td>
    </tr>
  </tbody>
</table>

#### 1) 부분 취소 요청 파라미터

[//]: # (부분취소 요청)
<table class="tg" style="table-layout: fixed; width: 100%">
<colgroup>
<col style="text-align: center; width: 5%">
<col style="text-align: center; width: 12%">
<col style="text-align: center; width: 15%">
<col style="text-align: center; width: 8%">
<col style="text-align: center; width: 8%">
<col style="text-align: center; width: 8%">
<col style="text-align: center; width: 10%">
<col style="text-align: left; width: 34%">
</colgroup>
<thead>
  <tr>
    <th class="tg-0lax" >구분</th>
    <th class="tg-0lax" >필드</th>
    <th class="tg-0lax" >필드명</th>
    <th class="tg-0lax" >길이</th>
    <th class="tg-0lax" >필수</th>
    <th class="tg-0lax" >암호화</th>
    <th class="tg-0lax" >타입</th>
    <th class="tg-0lax">비고</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0lax" style="text-align: center;">1</td>
    <td class="tg-0lax" style="text-align: center;">payType</td>
    <td class="tg-0lax" style="text-align: center;">결제수단</td>
    <td class="tg-0lax" style="text-align: center;">10</td>
    <td class="tg-0lax" style="text-align: center;">○</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">예) card(신용카드), hpp(휴대폰), vbank(가상계좌), bank(계좌이체)</td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">2</td>
    <td class="tg-0lax" style="text-align: center;">mid</td>
    <td class="tg-0lax" style="text-align: center;">가맹점ID</td>
    <td class="tg-0lax" style="text-align: center;">10</td>
    <td class="tg-0lax" style="text-align: center;">○</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">3</td>
    <td class="tg-0lax" style="text-align: center;">tid</td>
    <td class="tg-0lax" style="text-align: center;">거래ID</td>
    <td class="tg-0lax" style="text-align: center;">40</td>
    <td class="tg-0lax" style="text-align: center;">○</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">4</td>
    <td class="tg-0lax" style="text-align: center;">cancelPrice</td>
    <td class="tg-0lax" style="text-align: center;">부분 취소 금액</td>
    <td class="tg-0lax" style="text-align: center;">22</td>
    <td class="tg-0lax" style="text-align: center;">○</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">콤마(,) 필히 제거</td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">5</td>
    <td class="tg-0lax" style="text-align: center;">confirmPrice</td>
    <td class="tg-0lax" style="text-align: center;">취소 후남은 금액</td>
    <td class="tg-0lax" style="text-align: center;">22</td>
    <td class="tg-0lax" style="text-align: center;">○</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">콤마(,) 필히 제거</td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">6</td>
    <td class="tg-0lax" style="text-align: center;">currency</td>
    <td class="tg-0lax" style="text-align: center;">통화</td>
    <td class="tg-0lax" style="text-align: center;">3</td>
    <td class="tg-0lax" style="text-align: center;">○</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">WON / USD</td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">7</td>
    <td class="tg-0lax" style="text-align: center;">tax</td>
    <td class="tg-0lax" style="text-align: center;">부가세</td>
    <td class="tg-0lax" style="text-align: center;">10</td>
    <td class="tg-0lax" style="text-align: center;"></td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">대상: &#39;부가세 업체정함&#39; 설정업체에 한함<br/>부가세 금액 미입력시 비과세 금액으로 표시됨</td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">8</td>
    <td class="tg-0lax" style="text-align: center;">taxfree</td>
    <td class="tg-0lax" style="text-align: center;">비과세</td>
    <td class="tg-0lax" style="text-align: center;">10</td>
    <td class="tg-0lax" style="text-align: center;"></td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">대상: &#39;부가세 업체정함&#39; 설정업체에 한함<br/>과세되지 않는 금액</td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">9</td>
    <td class="tg-0lax" style="text-align: center;">timestamp</td>
    <td class="tg-0lax" style="text-align: center;">타임스탬프</td>
    <td class="tg-0lax" style="text-align: center;">14</td>
    <td class="tg-0lax" style="text-align: center;">O</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">예) 20190906110100</td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">10</td>
    <td class="tg-0lax" style="text-align: center;">signature</td>
    <td class="tg-0lax" style="text-align: center;">검증값</td>
    <td class="tg-0lax" style="text-align: center;">N/A</td>
    <td class="tg-0lax" style="text-align: center;">O</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">Sha256 (mid+mkey+timestamp)</td>
  </tr>
</tbody>
</table>

#### 2) 부분 취소 응답 파라미터

[//]: # (부분취소 응답)
<table class="tg" style="table-layout: fixed; width: 100%">
<colgroup>
<col style="text-align: center; width: 5%">
<col style="text-align: center; width: 12%">
<col style="text-align: center; width: 15%">
<col style="text-align: center; width: 8%">
<col style="text-align: center; width: 8%">
<col style="text-align: center; width: 8%">
<col style="text-align: center; width: 10%">
<col style="text-align: left; width: 34%">
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
    <td class="tg-0lax" style="text-align: center;">1</td>
    <td class="tg-0lax" style="text-align: center;">ResultCode</td>
    <td class="tg-0lax" style="text-align: center;">결과코드</td>
    <td class="tg-0lax" style="text-align: center;">6</td>
    <td class="tg-0lax" style="text-align: center;">○</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">00: 정상, 그 외 실패</td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">2</td>
    <td class="tg-0lax" style="text-align: center;">ResultMsg</td>
    <td class="tg-0lax" style="text-align: center;">결과메시지</td>
    <td class="tg-0lax" style="text-align: center;">100</td>
    <td class="tg-0lax" style="text-align: center;">○</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">3</td>
    <td class="tg-0lax" style="text-align: center;">Mid</td>
    <td class="tg-0lax" style="text-align: center;">가맹점 ID</td>
    <td class="tg-0lax" style="text-align: center;">10</td>
    <td class="tg-0lax" style="text-align: center;">△</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">성공 시에만 전달</td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">4</td>
    <td class="tg-0lax" style="text-align: center;">Tid</td>
    <td class="tg-0lax" style="text-align: center;">거래ID</td>
    <td class="tg-0lax" style="text-align: center;">40</td>
    <td class="tg-0lax" style="text-align: center;">△</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">성공 시에만 전달</td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">5</td>
    <td class="tg-0lax" style="text-align: center;">C_Tid</td>
    <td class="tg-0lax" style="text-align: center;">취소거래ID</td>
    <td class="tg-0lax" style="text-align: center;">22</td>
    <td class="tg-0lax" style="text-align: center;">△</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">성공 시에만 전달</td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">6</td>
    <td class="tg-0lax" style="text-align: center;">Price</td>
    <td class="tg-0lax" style="text-align: center;">부분 취소 금액</td>
    <td class="tg-0lax" style="text-align: center;">22</td>
    <td class="tg-0lax" style="text-align: center;">△</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">성공 시에만 전달</td>
  </tr>
  <tr>
    <td class="tg-0lax" style="text-align: center;">7</td>
    <td class="tg-0lax" style="text-align: center;">RmainPrice</td>
    <td class="tg-0lax" style="text-align: center;">취소 후 남은 금액</td>
    <td class="tg-0lax" style="text-align: center;">22</td>
    <td class="tg-0lax" style="text-align: center;">△</td>
    <td class="tg-0lax" style="text-align: center;">X</td>
    <td class="tg-0lax" style="text-align: center;">String</td>
    <td class="tg-0lax">성공 시에만 전달</td>
  </tr>
  <tr>
    <td class="tg-0lax">8</td>
    <td class="tg-0lax">CancelDate</td>
    <td class="tg-0lax">취소 날짜</td>
    <td class="tg-0lax">8</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">성공 시에만 전달<br>(YYYYMMDD)</td>
  </tr>
  <tr>
    <td class="tg-0lax">9</td>
    <td class="tg-0lax">CancelTime</td>
    <td class="tg-0lax">취소 시간</td>
    <td class="tg-0lax">6</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">성공 시에만 전달<br>(hhmmss)</td>
  </tr>
</tbody>
</table>

<div style="display: inline-block; width: 100%;">
  <a style="float:left;" href="/payapi01.html">◀이전페이지</a>
  <a style="float:right;" href="/payapi03.html">다음페이지▶</a>
</div>
