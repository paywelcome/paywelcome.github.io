---
title: MOBILE
permalink: mobile01.html
sidebar: mobile_sidebar
folder: mobile
toc: false
---

# 1. 기본적인 설치 방법

## 1.1 연동  Flow

Mobile Web 서비스는 복잡한 카드사와의 연계를 당사에서 처리하고, 가맹점에는 통일화 된 규격을 제시함에 따라, 보다 편리하게 모바일 결제시스템을 구축할 수 있게 합니다. &quot;인증/승인분리 방식 (이하 2 Transaction 이라 명명) &quot; 을 기본 Flow 로 하며, 일부 지불수단에 한하여, &quot;인증/승인통합 방식 (이하 1 Transaction 이라 명명) 을 사용합니다.

[2 Transaction  방식  Flow,  신용카드 ,  휴대폰 ,  계좌이체]

사진

[1 Transaction  방식  Flow,  가상계좌]

사진

## 1.2 결제창 Open (주문정보 전달) - 접속 주소 및 일반필드

사진

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

- 상점 연동을 위한 테스트 MID

[//]: # (MID 연동 table)
<table class="tg" style="table-layout: fixed; width: 100%">
<tbody>
  <tr>
    <th class="tg-0lax">Test MID</th>
    <th class="tg-0lax">signKey</th>
  </tr>
  <tr>
    <td class="tg-0lax">메일로 문의</td>
    <td class="tg-0lax">메일로 문의</td>
  </tr>
</tbody>
</table>

`샘플로 제공되는 테스트  MID  전용으로 상용  MID 사용불가`

## 1.3 상점 연동 시 주의사항
해킹시도 및 불법접속 차단 등의 보안을 위해 해외에서 접속 시에는 당사 서비스가 제한이 되며, 해외IP 차단해제를 위해서는 [ip-block@welcomepayments.co.kr](mailto:ip-block@welcomepayments.co.kr)로 아래 내용 작성해서 요청 주시기 바랍니다 .

[//]: # (해외 차단 IP table)
<table class="tg" style="table-layout: fixed; width: 100%">
<thead>
  <tr>
    <th>업체명</th>
    <th>접속 국가</th>
    <th>접속 공인 IP(대역)</th>
    <th>요청사항</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>xxxxx(전달받은mid)</td>
    <td>중국</td>
    <td>111.111.111.111</td>
    <td>해외아이피 차단해제 요청</td>
  </tr>
</tbody>
</table>