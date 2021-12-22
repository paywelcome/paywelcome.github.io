---
title: PAYAPI 신용카드 PREFIX 조회 API
permalink: payapi05.html
sidebar: payapi_sidebar
folder: payapi
toc: false
keywords: 신용카드 조회, 조회, prefix, 앞번호, 신용카드
---

<div style="display: inline-block; width: 100%;">
  <a style="float:left;" href="/payapi04.html">◀이전페이지</a>
  <a style="float:right;" href="/payapi06.html">다음페이지▶</a>
</div>

# 5. 신용카드 PREFIX 조회 API

## 5.1 신용카드 PREFIX 조회 API

신용카드 PREFIX 조회 시 사용하는 서비스입니다.

[//]: # (신용카드 PREFIX API URL)
<table class="tg" style="width: 100%">
  <colgroup>
    <col style="width: 20%">
    <col style="width: 80%">
  </colgroup>
  <tbody>
    <tr>
      <td class="center-align">운영</td>
      <td class="center-align">https://payapi.paywelcome.co.kr/search/card/prefix</td>
    </tr>
    <tr>
      <td class="center-align">테스트</td>
      <td class="center-align">https://tpayapi.paywelcome.co.kr/search/card/prefix</td>
    </tr>
  </tbody>
</table>

#### 1) 신용카드 PREFIX 요청 파라미터

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

[//]: # (신용카드 PREFIX 요청)
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
    <td class="center-align">cardNumber</td>
    <td class="center-align">카드번호</td>
    <td class="center-align">6</td>
    <td class="center-align">○</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">카드 번호 앞 6자리만 기재</td>
  </tr>
  <tr>
    <td class="center-align">3</td>
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
    <td class="left-align">Sha256<br>(mid+mkey+cardNumber+timestamp)</td>
  </tr>
</tbody>
</table>

</div>
</details>

#### 2) 신용카드 PREFIX 조회 응답 파라미터

<details style="cursor:pointer;" open>
<summary><strong>&nbsp;상세보기</strong></summary>
<div markdown="1">

[//]: # (신용카드 PREFIX 조회 응답 파라미터)
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
    <td class="center-align">CardCode</td>
    <td class="center-align">카드코드</td>
    <td class="center-align">2</td>
    <td class="center-align">△</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align"><a href="/code01.html">* 별첨 카드사(매입사) 코드 참고</a></td>
  </tr>
  <tr>
    <td class="center-align">4</td>
    <td class="center-align">CardType</td>
    <td class="center-align">카드종류</td>
    <td class="center-align">1</td>
    <td class="center-align">△</td>
    <td class="center-align">X</td>
    <td class="center-align">String</td>
    <td class="left-align">0:신용카드<br/>1:체크카드<br/>2:기프트카드</td>
  </tr>
  <tr>
    <td class="center-align">5</td>
    <td class="center-align">CardName</td>
    <td class="center-align">카드명</td>
    <td class="center-align"></td>
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
  <a style="float:left;" href="/payapi04.html">◀이전페이지</a>
  <a style="float:right;" href="/payapi06.html">다음페이지▶</a>
</div>