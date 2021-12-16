---
title: PAYAPI
permalink: payapi07.html
sidebar: payapi_sidebar
folder: payapi
toc: false
---

# 7. SMS결제용 단축URL생성 API

## 7.1 SMS결제용 단축URL생성 API

SMS 결제용 단축 URL을 생성하는 서비스입니다.

- SMS결제URL은 72시간 동안 유효합니다.
- 해당 API를 사용하기 위해서는 계약담당자를 통해 별도 사용요청 해주시기 바랍니다.

[//]: # (부분 취소 API URL)
<table class="tg" style="width: 100%">
  <colgroup>
    <col style="width: 20%">
    <col style="width: 80%">
  </colgroup>
  <tbody>
    <tr>
      <td class="tg-0lax">운영</td>
      <td class="tg-0lax">https://payapi.paywelcome.co.kr/smspay/makeUrl</td>
    </tr>
    <tr>
      <td class="tg-0lax">테스트</td>
      <td class="tg-0lax">https://tpayapi.paywelcome.co.kr/smspay/makeUrl</td>
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
    <td class="tg-0lax">payType</td>
    <td class="tg-0lax">결제수단</td>
    <td class="tg-0lax">5</td>
    <td class="tg-0lax">○</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">예) card(신용카드), hpp(휴대폰), vbank(가상계좌), bank(계좌이체)</td>
  </tr>
  <tr>
    <td class="tg-0lax">3</td>
    <td class="tg-0lax">timestamp</td>
    <td class="tg-0lax">타임스탬프</td>
    <td class="tg-0lax">14</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">예) 20190906110100</td>
  </tr>
  <tr>
    <td class="tg-0lax">3</td>
    <td class="tg-0lax">P_GOODS</td>
    <td class="tg-0lax">상품명</td>
    <td class="tg-0lax">40</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">4</td>
    <td class="tg-0lax">P_OID</td>
    <td class="tg-0lax">상점주문번호</td>
    <td class="tg-0lax">30</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">5</td>
    <td class="tg-0lax">P_AMT</td>
    <td class="tg-0lax">승인금액</td>
    <td class="tg-0lax">9</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">예) 20190906110100</td>
  </tr>
  <tr>
    <td class="tg-0lax">6</td>
    <td class="tg-0lax">P_HPP_METHOD</td>
    <td class="tg-0lax">휴대폰 결제 상품유형</td>
    <td class="tg-0lax">1</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">컨텐츠 :1, 실물:2(휴대폰 결제시만 사용)</td>
  </tr>
  <tr>
    <td class="tg-0lax">7</td>
    <td class="tg-0lax">P_QUOTABASE</td>
    <td class="tg-0lax">신용카드 할부기간 지정</td>
    <td class="tg-0lax">100</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">50,000원 이상 결제 시, 할부기간 지정 (36개월 MAX)Ex. 01:02:03:04.. 01은 일시불, 02는 2개월, 99 는 일시불 제거 등등</td>
  </tr>
  <tr>
    <td class="tg-0lax">8</td>
    <td class="tg-0lax">P_NOTI_URL</td>
    <td class="tg-0lax">노티결과수신</td>
    <td class="tg-0lax">100</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">결제수단 가상계좌 입금 확인API요청 업체시 필요(가맹점 관리자연동시 필요X)</td>
  </tr>
  <tr>
    <td class="tg-0lax">9</td>
    <td class="tg-0lax">P_RETURN_URL</td>
    <td class="tg-0lax">승인결과수신</td>
    <td class="tg-0lax">100</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">API요청 업체시 필요(가맹점 관리자연동시 &quot;https://{test}m.paywelcome.co.kr/smsNextUrl.jsp&quot; 로 처리함)</td>
  </tr>
  <tr>
    <td class="tg-0lax">10</td>
    <td class="tg-0lax">P_NEXT_URL</td>
    <td class="tg-0lax">인증결과수신</td>
    <td class="tg-0lax">100</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">API요청 업체시 필요(가맹점 관리자연동시 &quot;https://{test}m.paywelcome.co.kr/smsNextUrl.jsp&quot; 로 처리함)</td>
  </tr>
  <tr>
    <td class="tg-0lax">11</td>
    <td class="tg-0lax">P_RESERVED</td>
    <td class="tg-0lax">복합파리미터</td>
    <td class="tg-0lax">300</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">12</td>
    <td class="tg-0lax">P_CHARSET</td>
    <td class="tg-0lax">인증/승인 결과 캐릭터셋</td>
    <td class="tg-0lax">6</td>
    <td class="tg-0lax"></td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">default : euc-kr인증/승인결과를 utf8로 받기를 원할시 utf8</td>
  </tr>
  <tr>
    <td class="tg-0lax">13</td>
    <td class="tg-0lax">timestamp</td>
    <td class="tg-0lax">타임스탬프</td>
    <td class="tg-0lax">14</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">예) 20190906110100</td>
  </tr>
  <tr>
    <td class="tg-0lax">14</td>
    <td class="tg-0lax">signature</td>
    <td class="tg-0lax">검증값</td>
    <td class="tg-0lax">N/A</td>
    <td class="tg-0lax">O</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">Sha256<br>(mid+mkey+P\_OID+P\_AMT+timestamp)</td>
  </tr>
</tbody>
</table>

#### 2) SMS결제용 단축URL 생성 응답 파라미터

[//]: # (SMS결제용 단축URL 생성 응답 파라미터)
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
    <td class="tg-0lax">MsgSend</td>
    <td class="tg-0lax">결제URL</td>
    <td class="tg-0lax">50</td>
    <td class="tg-0lax">△</td>
    <td class="tg-0lax">X</td>
    <td class="tg-0lax">String</td>
    <td class="tg-0lax">ex) https://m.welpg.com/s/97T9</td>
  </tr>
</tbody>
</table>
