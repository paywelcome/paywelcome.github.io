---
title: MOBILE
permalink: mobile03.html
sidebar: mobile_sidebar
folder: mobile
toc: false
---

# 3. 인증 결과 수신

## 3.1 인증 결과 수신

- 1-7 ~ 1-8 장은 2 Transaction 을 위한 설명 페이지 입니다.
- 1 Transaction 방식은 1-1. 연동 Flow장 을 참고하세요.

{% include image.html file="mobile_img06.png" %}

2 Transaction 거래의 경우, &quot;1-2. 결제창 Open (주문정보 전달) ? 접속 주소 및 일반필드장 에 기재된, P_NEXT_URL 로 인증결과를 전달합니다. 이때 Mobile Web 서비스에서 P_NEXT_URL 로 전달하는 Parameter 는 하기와 같습니다.

<table class="tg" style="table-layout: fixed; width: 100%">
<colgroup>
<col style="width: 25%">
<col style="width: 25%">
<col style="width: 50%">
</colgroup>
<thead>
  <tr>
    <th class="tg-0lax">필드명</th>
    <th class="tg-0lax">목적</th>
    <th class="tg-0lax">비고</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0lax">P_STATUS</td>
    <td class="tg-0lax">인증상태</td>
    <td class="tg-0lax">성공 시 00, 그 외 실패</td>
  </tr>
  <tr>
    <td class="tg-0lax">P_RMESG1</td>
    <td class="tg-0lax">결과메시지</td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0lax">P_TID</td>
    <td class="tg-0lax">인증거래번호</td>
    <td class="tg-0lax">Char(40) / 성공시에만 반환</td>
  </tr>
  <tr>
    <td class="tg-0lax">P_REQ_URL</td>
    <td class="tg-0lax">승인요청 Url</td>
    <td class="tg-0lax">가맹점에서 Mobile Web 서비스로 승인요청을 할 때, 사용되는 Url 입니다.<br> 거래 건 마다 상이한 URL 이 전달됩니다.<br><red>따라서, 절대 고정하여 사용하지 마십시오.</red><br> Http Scheme 은 https 를 사용합니다.<br> <red>보안을 위해 https프로토콜 사용을 통한 통신만 지원하며, https 보안 프로토콜 적용이 불가능한IP 기반의 통신은 제공하지 않습니다.</red></td>
  </tr>
  <tr>
    <td class="tg-0lax">P_NOTI</td>
    <td class="tg-0lax">기타주문정보</td>
    <td class="tg-0lax">최초 거래 시 주문정보에 P_NOTI 를 설정하셨다면, 그 값을 전달받을 수 있습니다. 이 값은 P_NOTI 값을 그대로 리턴합니다.</td>
  </tr>
  <tr>
    <td class="tg-0lax">P_AMT</td>
    <td class="tg-0lax">거래금액</td>
    <td class="tg-0lax">최초 거래 시 주문정보에 설정한 P_AMT 전달(주요 지불수단인 신용카드, 휴대폰, 계좌이체, 가상계좌 등 일부만 전달)</td>
  </tr>
</tbody>
</table>

또한, 당사에서 인증결과 송신 시 사용하는 Method 는 post, get 을 선택적으로 사용하오니, 두가지 방식을 모두 수용할 수 있도록 처리 바랍니다.