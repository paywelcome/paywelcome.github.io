---
title: PAYAPI SMS결제용 단축 URL생성 API
permalink: payapi07.html
sidebar: payapi_sidebar
folder: payapi
toc: false
---

<div style="display: inline-block; width: 100%;">
  <a style="float:left;" href="/payapi06.html">◀이전페이지</a>
  <a style="float:right;" href="/payapi08.html">다음페이지▶</a>
</div>

# 7. SMS결제용 단축 URL생성 API

## 7.1 SMS결제용 단축 URL생성 API

SMS 결제용 단축 URL을 생성하는 서비스입니다.

- SMS결제URL은 72시간 동안 유효합니다.
- 해당 API를 사용하기 위해서는 계약담당자를 통해 별도 사용요청 해주시기 바랍니다.

[//]: # (SMS결제용 단축 URL생성 URL)
<table class="tg" style="width: 100%">
  <colgroup>
    <col style="width: 20%">
    <col style="width: 80%">
  </colgroup>
  <tbody>
    <tr>
      <td class="center-align">운영</td>
      <td class="center-align">https://payapi.paywelcome.co.kr/smspay/makeUrl</td>
    </tr>
    <tr>
      <td class="center-align">테스트</td>
      <td class="center-align">https://tpayapi.paywelcome.co.kr/smspay/makeUrl</td>
    </tr>
  </tbody>
</table>

#### 1) SMS결제용 단축 URL생성 요청 파라미터

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

[//]: # (SMS결제용 단축 URL생성 요청)
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
    <td class="center-align">payType</td>
    <td class="center-align">결제수단</td>
    <td class="center-align">5</td>
    <td class="center-align">○</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">예) card(신용카드), hpp(휴대폰), vbank(가상계좌), bank(계좌이체)</td>
  </tr>
  <tr>
    <td class="center-align">3</td>
    <td class="center-align">P_GOODS</td>
    <td class="center-align">상품명</td>
    <td class="center-align">40</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">4</td>
    <td class="center-align">P_OID</td>
    <td class="center-align">상점주문번호</td>
    <td class="center-align">30</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">5</td>
    <td class="center-align">P_AMT</td>
    <td class="center-align">승인금액</td>
    <td class="center-align">9</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">6</td>
    <td class="center-align">P_HPP_METHOD</td>
    <td class="center-align">휴대폰 결제 상품유형</td>
    <td class="center-align">1</td>
    <td class="center-align"></td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">컨텐츠 :1, 실물:2<br/>(휴대폰 결제시만 사용)</td>
  </tr>
  <tr>
    <td class="center-align">7</td>
    <td class="center-align">P_QUOTABASE</td>
    <td class="center-align">신용카드 할부기간 지정</td>
    <td class="center-align">100</td>
    <td class="center-align"></td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">50,000원 이상 결제 시, 할부기간 지정 (36개월 MAX)<br/>Ex. 01:02:03:04.. 01은 일시불, 02는 2개월, 99 는 일시불 제거 등등</td>
  </tr>
  <tr>
    <td class="center-align">8</td>
    <td class="center-align">P_NOTI_URL</td>
    <td class="center-align">노티결과수신</td>
    <td class="center-align">100</td>
    <td class="center-align"></td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">결제수단 가상계좌 입금 확인API<br/>요청 업체시 필요<br/>(가맹점 관리자연동시 필요X)</td>
  </tr>
  <tr>
    <td class="center-align">9</td>
    <td class="center-align">P_RETURN_URL</td>
    <td class="center-align">승인결과수신</td>
    <td class="center-align">100</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">API요청 업체시 필요<br/>(가맹점 관리자연동시 필요X)</td>
  </tr>
  <tr>
    <td class="center-align">10</td>
    <td class="center-align">P_NEXT_URL</td>
    <td class="center-align">인증결과수신</td>
    <td class="center-align">100</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">API요청 업체시 필요<br/>(가맹점 관리자연동시<br/>&quot;https://{test}m.paywelcome.co.kr/smsNextUrl.jsp&quot; 로 처리함)</td>
  </tr>
  <tr>
    <td class="center-align">11</td>
    <td class="center-align">P_RESERVED</td>
    <td class="center-align">복합파리미터</td>
    <td class="center-align">300</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"></td>
  </tr>
  <tr>
    <td class="center-align">12</td>
    <td class="center-align">P_CHARSET</td>
    <td class="center-align">인증/승인 결과 캐릭터셋</td>
    <td class="center-align">6</td>
    <td class="center-align"></td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">default : euc-kr<br/>인증/승인결과를 utf8로 받기를 원할시 utf8</td>
  </tr>
  <tr>
    <td class="center-align">13</td>
    <td class="center-align">timestamp</td>
    <td class="center-align">타임스탬프</td>
    <td class="center-align">14</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">예) 20190906110100</td>
  </tr>
  <tr>
    <td class="center-align">14</td>
    <td class="center-align">signature</td>
    <td class="center-align">검증값</td>
    <td class="center-align">N/A</td>
    <td class="center-align">O</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">Sha256<br>(mid+mkey+P\_OID+P\_AMT+timestamp)</td>
  </tr>
</tbody>
</table>

</div>
</details>

#### 2) SMS결제용 단축 URL생성 응답 파라미터

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

[//]: # (SMS결제용 단축 URL생성 응답 파라미터)
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
    <td class="center-align">MsgSend</td>
    <td class="center-align">결제URL</td>
    <td class="center-align">50</td>
    <td class="center-align">△</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">ex) https://m.welpg.com/s/97T9</td>
  </tr>
</tbody>
</table>

</div>
</details>

<div style="display: inline-block; width: 100%;">
  <a style="float:left;" href="/payapi06.html">◀이전페이지</a>
  <a style="float:right;" href="/payapi08.html">다음페이지▶</a>
</div>

