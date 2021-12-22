---
title: PAYAPI 결제취소 API
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
      <td class="center-align">운영</td>
      <td class="center-align">https://payapi.paywelcome.co.kr/cancel/cancel</td>
    </tr>
    <tr>
      <td class="center-align">테스트</td>
      <td class="center-align">https://tpayapi.paywelcome.co.kr/cancel/cancel</td>
    </tr>
  </tbody>
</table>

#### 1) 전체 취소 요청 파라미터

[//]: # (전체취소 요청)
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
    <td class="center-align">payType</td>
    <td class="center-align">결제수단</td>
    <td class="center-align">10</td>
    <td class="center-align">○</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">예) card(신용카드), hpp(휴대폰), vbank(가상계좌), bank(계좌이체)</td>
  </tr>
  <tr>
    <td class="center-align">2</td>
    <td class="center-align">mid</td>
    <td class="center-align">가맹점ID</td>
    <td class="center-align">10</td>
    <td class="center-align">○</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="center-align"></td>
  </tr>
  <tr>
    <td class="center-align" >3</td>
    <td class="center-align" >tid</td>
    <td class="center-align" >거래ID</td>
    <td class="center-align" >40</td>
    <td class="center-align" >○</td>
    <td class="center-align" >X</td>
    <td class="center-align" >String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align" >4</td>
    <td class="center-align" >price</td>
    <td class="center-align" >취소 금액</td>
    <td class="center-align" >22</td>
    <td class="center-align" >○</td>
    <td class="center-align" >X</td>
    <td class="center-align" >String</td>
    <td class="left-align">콤마(,) 필히 제거</td>
  </tr>
  <tr>
    <td class="center-align"  >5</td>
    <td class="center-align"  >currency</td>
    <td class="center-align"  >통화</td>
    <td class="center-align"  >3</td>
    <td class="center-align"  >○</td>
    <td class="center-align"  >X</td>
    <td class="center-align"  >String</td>
    <td class="left-align">WON / USD</td>
  </tr>
  <tr>
    <td class="center-align" >6</td>
    <td class="center-align" >timestamp</td>
    <td class="center-align" >타임스탬프</td>
    <td class="center-align" >14</td>
    <td class="center-align" >○</td>
    <td class="center-align" >X</td>
    <td class="center-align" >String</td>
    <td class="left-align">예) 20190906110100</td>
  </tr>
  <tr>
    <td class="center-align" >7</td>
    <td class="center-align" >signature</td>
    <td class="center-align" >검증값</td>
    <td class="center-align" >N/A</td>
    <td class="center-align" >○</td>
    <td class="center-align" >X</td>
    <td class="center-align" >String</td>
    <td class="left-align">SHA256<br>(mid+mkey+timestamp)</td>
  </tr>
  <tr>
    <td class="center-align" >8</td>
    <td class="center-align" >cancelType</td>
    <td class="center-align" >망취소옵션</td>
    <td class="center-align" >1</td>
    <td class="center-align" ></td>
    <td class="center-align" >X</td>
    <td class="center-align" >String</td>
    <td class="left-align">모바일 망취소일 경우 사용<br>모바일망취소:C</td>
  </tr>
</tbody>
</table>

#### 1) 전체 취소 응답 파라미터

[//]: # (전체취소 응답)
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
    <td class="center-align">Mid</td>
    <td class="center-align">가맹점 ID</td>
    <td class="center-align">10</td>
    <td class="center-align">△</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">성공 시에만 전달</td>
  </tr>
  <tr>
    <td class="center-align">4</td>
    <td class="center-align">Tid</td>
    <td class="center-align">거래ID</td>
    <td class="center-align">40</td>
    <td class="center-align">△</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">성공 시에만 전달</td>
  </tr>
  <tr>
    <td class="center-align">5</td>
    <td class="center-align">Moid</td>
    <td class="center-align">주문번호</td>
    <td class="center-align">64</td>
    <td class="center-align">△</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">성공 시에만 전달</td>
  </tr>
  <tr>
    <td class="center-align">6</td>
    <td class="center-align">Price</td>
    <td class="center-align">취소 금액</td>
    <td class="center-align">22</td>
    <td class="center-align">△</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">성공 시에만 전달</td>
  </tr>
  <tr>
    <td class="center-align">7</td>
    <td class="center-align">CancelDate</td>
    <td class="center-align">취소 날짜</td>
    <td class="center-align">8</td>
    <td class="center-align">△</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">성공 시에만 전달<br>(YYYYMMDD)</td>
  </tr>
  <tr>
    <td class="center-align" >8</td>
    <td class="center-align" >CancelTime</td>
    <td class="center-align" >취소 시간</td>
    <td class="center-align" >6</td>
    <td class="center-align" >△</td>
    <td class="center-align" >X</td>
    <td class="center-align" >String</td>
    <td class="left-align">성공 시에만 전달<br>(hhmmss)</td>
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
      <td class="center-align">운영</td>
      <td class="center-align">https://payapi.paywelcome.co.kr/cancel/repay</td>
    </tr>
    <tr>
      <td class="center-align">테스트</td>
      <td class="center-align">https://tpayapi.paywelcome.co.kr/cancel/repay</td>
    </tr>
  </tbody>
</table>

#### 1) 부분 취소 요청 파라미터

[//]: # (부분취소 요청)
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
    <th class="center-align" >구분</th>
    <th class="center-align" >필드</th>
    <th class="center-align" >필드명</th>
    <th class="center-align" >길이</th>
    <th class="center-align" >필수</th>
    <th class="center-align" >암호화</th>
    <th class="center-align" >타입</th>
    <th class="left-align">비고</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="center-align" >1</td>
    <td class="center-align" >payType</td>
    <td class="center-align" >결제수단</td>
    <td class="center-align" >10</td>
    <td class="center-align" >○</td>
    <td class="center-align" >X</td>
    <td class="center-align" >String</td>
    <td class="left-align">예) card(신용카드), hpp(휴대폰), vbank(가상계좌), bank(계좌이체)</td>
  </tr>
  <tr>
    <td class="center-align" >2</td>
    <td class="center-align" >mid</td>
    <td class="center-align" >가맹점ID</td>
    <td class="center-align" >10</td>
    <td class="center-align" >○</td>
    <td class="center-align" >X</td>
    <td class="center-align" >String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align" >3</td>
    <td class="center-align" >tid</td>
    <td class="center-align" >거래ID</td>
    <td class="center-align" >40</td>
    <td class="center-align" >○</td>
    <td class="center-align" >X</td>
    <td class="center-align" >String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align" >4</td>
    <td class="center-align" >cancelPrice</td>
    <td class="center-align" >부분 취소 금액</td>
    <td class="center-align" >22</td>
    <td class="center-align" >○</td>
    <td class="center-align" >X</td>
    <td class="center-align" >String</td>
    <td class="left-align">콤마(,) 필히 제거</td>
  </tr>
  <tr>
    <td class="center-align" >5</td>
    <td class="center-align" >confirmPrice</td>
    <td class="center-align" >취소 후남은 금액</td>
    <td class="center-align" >22</td>
    <td class="center-align" >○</td>
    <td class="center-align" >X</td>
    <td class="center-align" >String</td>
    <td class="left-align">콤마(,) 필히 제거</td>
  </tr>
  <tr>
    <td class="center-align" >6</td>
    <td class="center-align" >currency</td>
    <td class="center-align" >통화</td>
    <td class="center-align" >3</td>
    <td class="center-align" >○</td>
    <td class="center-align" >X</td>
    <td class="center-align" >String</td>
    <td class="left-align">WON / USD</td>
  </tr>
  <tr>
    <td class="center-align" >7</td>
    <td class="center-align" >tax</td>
    <td class="center-align" >부가세</td>
    <td class="center-align" >10</td>
    <td class="center-align" ></td>
    <td class="center-align" >X</td>
    <td class="center-align" >String</td>
    <td class="left-align">대상: &#39;부가세 업체정함&#39; 설정업체에 한함<br/>부가세 금액 미입력시 비과세 금액으로 표시됨</td>
  </tr>
  <tr>
    <td class="center-align" >8</td>
    <td class="center-align" >taxfree</td>
    <td class="center-align" >비과세</td>
    <td class="center-align" >10</td>
    <td class="center-align" ></td>
    <td class="center-align" >X</td>
    <td class="center-align" >String</td>
    <td class="left-align">대상: &#39;부가세 업체정함&#39; 설정업체에 한함<br/>과세되지 않는 금액</td>
  </tr>
  <tr>
    <td class="center-align" >9</td>
    <td class="center-align" >timestamp</td>
    <td class="center-align" >타임스탬프</td>
    <td class="center-align" >14</td>
    <td class="center-align" >O</td>
    <td class="center-align" >X</td>
    <td class="center-align" >String</td>
    <td class="left-align">예) 20190906110100</td>
  </tr>
  <tr>
    <td class="center-align" >10</td>
    <td class="center-align" >signature</td>
    <td class="center-align" >검증값</td>
    <td class="center-align" >N/A</td>
    <td class="center-align" >O</td>
    <td class="center-align" >X</td>
    <td class="center-align" >String</td>
    <td class="left-align">Sha256 (mid+mkey+timestamp)</td>
  </tr>
</tbody>
</table>

#### 2) 부분 취소 응답 파라미터

[//]: # (부분취소 응답)
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
    <th class="center-align">길이</th>
    <th class="center-align">필수</th>
    <th class="center-align">암호화</th>
    <th class="center-align">타입</th>
    <th class="left-align">비고</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="center-align" >1</td>
    <td class="center-align" >ResultCode</td>
    <td class="center-align" >결과코드</td>
    <td class="center-align" >6</td>
    <td class="center-align" >○</td>
    <td class="center-align" >X</td>
    <td class="center-align" >String</td>
    <td class="left-align">00: 정상, 그 외 실패</td>
  </tr>
  <tr>
    <td class="center-align" >2</td>
    <td class="center-align" >ResultMsg</td>
    <td class="center-align" >결과메시지</td>
    <td class="center-align" >100</td>
    <td class="center-align" >○</td>
    <td class="center-align" >X</td>
    <td class="center-align" >String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align" >3</td>
    <td class="center-align" >Mid</td>
    <td class="center-align" >가맹점 ID</td>
    <td class="center-align" >10</td>
    <td class="center-align" >△</td>
    <td class="center-align" >X</td>
    <td class="center-align" >String</td>
    <td class="left-align">성공 시에만 전달</td>
  </tr>
  <tr>
    <td class="center-align" >4</td>
    <td class="center-align" >Tid</td>
    <td class="center-align" >거래ID</td>
    <td class="center-align" >40</td>
    <td class="center-align" >△</td>
    <td class="center-align" >X</td>
    <td class="center-align" >String</td>
    <td class="left-align">성공 시에만 전달</td>
  </tr>
  <tr>
    <td class="center-align" >5</td>
    <td class="center-align" >C_Tid</td>
    <td class="center-align" >취소거래ID</td>
    <td class="center-align" >22</td>
    <td class="center-align" >△</td>
    <td class="center-align" >X</td>
    <td class="center-align" >String</td>
    <td class="left-align">성공 시에만 전달</td>
  </tr>
  <tr>
    <td class="center-align" >6</td>
    <td class="center-align" >Price</td>
    <td class="center-align" >부분 취소 금액</td>
    <td class="center-align" >22</td>
    <td class="center-align" >△</td>
    <td class="center-align" >X</td>
    <td class="center-align" >String</td>
    <td class="left-align">성공 시에만 전달</td>
  </tr>
  <tr>
    <td class="center-align" >7</td>
    <td class="center-align" >RmainPrice</td>
    <td class="center-align" >취소 후 남은 금액</td>
    <td class="center-align" >22</td>
    <td class="center-align" >△</td>
    <td class="center-align" >X</td>
    <td class="center-align" >String</td>
    <td class="left-align">성공 시에만 전달</td>
  </tr>
  <tr>
    <td class="center-align">8</td>
    <td class="center-align">CancelDate</td>
    <td class="center-align">취소 날짜</td>
    <td class="center-align">8</td>
    <td class="center-align">△</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">성공 시에만 전달<br>(YYYYMMDD)</td>
  </tr>
  <tr>
    <td class="center-align">9</td>
    <td class="center-align">CancelTime</td>
    <td class="center-align">취소 시간</td>
    <td class="center-align">6</td>
    <td class="center-align">△</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">성공 시에만 전달<br>(hhmmss)</td>
  </tr>
</tbody>
</table>

<div style="display: inline-block; width: 100%;">
  <a style="float:left;" href="/payapi01.html">◀이전페이지</a>
  <a style="float:right;" href="/payapi03.html">다음페이지▶</a>
</div>
