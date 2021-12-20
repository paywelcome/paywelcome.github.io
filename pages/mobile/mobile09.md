---
title: MOBILE
permalink: mobile09.html
sidebar: mobile_sidebar
folder: mobile
toc: false
---

# 9. 모바일 에스크로 사용방법 안내

>Mobile Web 서비스 화면에서, 에스크로 서비스를 호출하는 옵션입니다.<br>
>배송 등록, 결제 취소, 거절 확인은 PayAPI 모듈로 진행되므로 (배포본)PAYAPI 연동메뉴얼과 함께 참고하여 개발 진행 부탁드립니다.<br>
>가맹점에서 거래에 따라 일반 결제와 에스크로 결제의 구분 결제를 희망하시면 에스크로로 신규 또는 전환계약이 필요합니다. (단, 일부 호스팅 가맹점은 신 에스크로 설정에, 제한이 있을 수 있음)<br>
>에스크로 계약에 문의가 있거나 자세한 사항은 계약 담당자에게 문의하여 주시기 바랍니다.

## 9.1 모바일 에스크로 사용가능 지불수단

- 신용카드
- 계좌이체
- 가상계좌

 **※ 에스크로 결제 진행 시에는 당사에서 제공하는 간편결제는 사용 불가합니다.**
**(카드사 결제 창 내 제공하는 간편결제가 아닌 당사 결제페이지 내 노출되는 부분에 한함)**

#### A. 설정 방법

- 매뉴얼 결제창 Open (주문정보 전달) ? 복합필드섹션을 보면, P_RESERVED 파라미터 항목이 있습니다.
  참고 하시어, 동일하게 상위의 옵션을 설정하시면 됩니다.

>예) `<INPUT type=”hidden” name=”P_RESERVED” value=”useescrow=Y”/> `
 
## 9.2 모바일 에스크로 구매결정 연동

- 모바일 결제창을 통한 에스크로 구매결정 연동을 안내합니다.
  가맹점 페이지내에 구며결정 버튼을 클릭하여 에스크로 구매결정 창이 호출되도록 구현하시면 됩니다.

[구매결정 요청 URL]
<table style="width: 100%;">
<colgroup>
  <col style="width: 20%;">
  <col style="width: 20%;">
  <col style="width: 60%;">
</colgroup>
<tbody>
  <tr>
    <th rowspan="2">HOST</th>
    <td>테스트</td>
    <td>tmobile.paywelcome.co.kr</td>
  </tr>
  <tr>
    <td>운영</td>
    <td>mobile.paywelcome.co.kr</td>
  </tr>
  <tr>
    <th>에스크로</th>
    <td>구매결정</td>
    <td>https://{HOST}/smart/escrow_confirm/</td>
  </tr>
  <tr>
    <td colspan="3">ex) 에스크로 구매결정 연동 시 :<br>https://mobile.paywelcome.co.kr/smart/escrow_confirm/</td>
  </tr>
</tbody>
</table>

#### [구매결정 요청 파라메터]
<table style="width: 100%;">
<colgroup>
  <col style="width: 30%;">
  <col style="width: 15%;">
  <col style="width: 15%;">
  <col style="width: 40%;">
</colgroup>
  <thead>
    <tr>
      <th style="text-align: center">필드명</th>
      <th style="text-align: center">크 기</th>
      <th style="text-align: center">필수여부</th>
      <th>비고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">P_MID</td>
      <td style="text-align: center">Char(10)</td>
      <td style="text-align: center">필수</td>
      <td>주문요청시 사용한 P_MID</td>
    </tr>
    <tr>
      <td style="text-align: center">P_ESCROW_TID</td>
      <td style="text-align: center">Char(40)</td>
      <td style="text-align: center">필수</td>
      <td>에스크로 결제 승인 TID</td>
    </tr>
    <tr>
      <td style="text-align: center">P_NEXT_URL</td>
      <td style="text-align: center">Char(800)</td>
      <td style="text-align: center">필수</td>
      <td>결과수신 URLhttps(http)가 포함된 전체 URL이며, URL내 get 방식의 파라미터는 사용불가 합니다.</td>
    </tr>
    <tr>
      <td style="text-align: center">P_NEXT_URL_TAGET</td>
      <td style="text-align: center">Char(10)</td>
      <td style="text-align: center">필수</td>
      <td>결과 수신 URL선택 값 : socket, get, post(미입력 시 기본값:socket)<br>get,post 방식은 완료 후 가맹점 페이지로 해당 방식으로 전환되며, socket 방식은 NOTI로 해당 값을 통보하여, 사용자페이지는 닫힙니다.</td>
    </tr>
    <tr>
      <td style="text-align: center">P_RESERVED</td>
      <td style="text-align: center">Char(100)</td>
      <td style="text-align: center">선택</td>
      <td>복합파라미터정보P_RESERVED=escrow_purchase_opt=vertify(구매확인버튼만 표시) P_RESERVED=escrow_purchase_opt=deny(구매거절버튼만 표시)옵션 미지정 시 구매확인/거절 모두 표시</td>
    </tr>
  </tbody>
</table>

#### [구매결정 응답 파라메터]
<table style="width: 100%;">
<colgroup>
  <col style="width: 30%">
  <col style="width: 30%">
  <col style="width: 40%">
</colgroup>
  <thead>
    <tr>
      <th style="text-align: center">필드명</th>
      <th style="text-align: center">설명</th>
      <th>비고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">P_ESCROW_TID</td>
      <td style="text-align: center">전달된 에스크로 TID</td>
      <td> </td>
    </tr>
    <tr>
      <td style="text-align: center">P_CL_STATUS</td>
      <td style="text-align: center">구매결정/구매거절여부</td>
      <td>buyComplete / denyComplete</td>
    </tr>
    <tr>
      <td style="text-align: center">P_STATUS</td>
      <td style="text-align: center">상태값</td>
      <td>구매결정, 구매거절에 대한 코드값(하단 코드표 참조)</td>
    </tr>
    <tr>
      <td style="text-align: center">P_RMESG1</td>
      <td style="text-align: center">처리결과메세지</td>
      <td>urlEncode 전달</td>
    </tr>
    <tr>
      <td style="text-align: center">P_PG_IP</td>
      <td style="text-align: center">처리된 승인서버 IP</td>
      <td> </td>
    </tr>
  </tbody>
</table>

## 9.3 에스크로 상태변경 노티 수신

에스크로 주요 시점(예&gt;구매자가 구매결정을 완료 등)에 가맹점 측으로 해당 내역을 통보해주는 기능입니다. 상점 측에서는 정상수신 여부를 응답(NOTI CONFIRM)하여야합니다.<br>
해당 기능을 이용하려면 계약 담당자를 통해, 수신 받을 상점 측 URL을 등록하셔야 합니다.<br>

-지불수단별, 승인요청 시점의 주문번호를 기준으로 응답하며, 배송등록 시점에 사용되는 주문번호와 동일하게 설정을 권장합니다.
-거래금액은 에스크로 상태에 따라 거래취소 시에는 취소금액, 그 외는 승인 금액입니다.
-원거래TID는 부분취소거래만 설정됩니다.

[노티발송 웰컴페이먼츠 &gt; 가맹점]
<table style="width: 100%">
<colgroup>
  <col style="width: 20%;">
  <col style="width: 20%;">
  <col style="width: 15%;">
  <col style="width: 45%;">
</colgroup>
  <thead>
    <tr>
      <th style="text-align: center">필드</th>
      <th style="text-align: center">필드명</th>
      <th>크 기</th>
      <th>부 가 설 명 및 주 의 사 항</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">id_merchant</td>
      <td style="text-align: center">상점아이디</td>
      <td>Char(10)</td>
      <td>P_MID로 전달한 값</td>
    </tr>
    <tr>
      <td style="text-align: center">no_oid</td>
      <td style="text-align: center">주문번호</td>
      <td>Char(40)</td>
      <td>가맹점주문번호</td>
    </tr>
    <tr>
      <td style="text-align: center">no_tid</td>
      <td style="text-align: center">거래번호</td>
      <td>Char(40)</td>
      <td>승인 시 전달된 TID</td>
    </tr>
    <tr>
      <td style="text-align: center">cl_status</td>
      <td style="text-align: center">에스크로 상태</td>
      <td>Char(2)</td>
      <td>배송등록(2), 구매확인(3), 자동구매확인(31), 강제구매확인(32), 구매거절(4), 거래취소(8), 거절확인(10)</td>
    </tr>
    <tr>
      <td style="text-align: center">dt_req</td>
      <td style="text-align: center">요청일자</td>
      <td>Char(14)</td>
      <td>YYYYMMDDhhmmss</td>
    </tr>
    <tr>
      <td style="text-align: center">cl_paymethod</td>
      <td style="text-align: center">결제수단</td>
      <td>Char(2)</td>
      <td>신용카드(0), ISP(1), 계좌이체(16), 가상계좌(17)</td>
    </tr>
    <tr>
      <td style="text-align: center">msg_deny</td>
      <td style="text-align: center">구매거절사유</td>
      <td> </td>
      <td> </td>
    </tr>
    <tr>
      <td style="text-align: center">Char(256)</td>
      <td style="text-align: center"> </td>
      <td> </td>
      <td> </td>
    </tr>
    <tr>
      <td style="text-align: center">price</td>
      <td style="text-align: center">거래금액</td>
      <td> </td>
      <td> </td>
    </tr>
    <tr>
      <td style="text-align: center">Char(12)</td>
      <td style="text-align: center"> </td>
      <td> </td>
      <td> </td>
    </tr>
    <tr>
      <td style="text-align: center">tid_org</td>
      <td style="text-align: center">원거래 거래번호</td>
      <td>Char(40)</td>
      <td>부분취소시 원거래 거래번호</td>
    </tr>
  </tbody>
</table>

[노티응답 가맹점 &gt; 웰컴페이먼츠]
<table style="width: 100%;">
<colgroup>
  <col style="width: 20%;">
  <col style="width: 20%;">
  <col style="width: 15%;">
  <col style="width: 45%;">
</colgroup>
  <thead>
    <tr>
      <th style="text-align: center">파라미터</th>
      <th style="text-align: center">설명</th>
      <th>크기</th>
      <th style="text-align: center">비고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">cd_rslt</td>
      <td style="text-align: center">결과코드</td>
      <td>Char(4)</td>
      <td style="text-align: center">0000:정상처리, 9999:처리실패</td>
    </tr>
    <tr>
      <td style="text-align: center">msg_rslt</td>
      <td style="text-align: center">결과메세지</td>
      <td>Char(1000)</td>
      <td style="text-align: center">처리실패시 상세 오류 메세지</td>
    </tr>
  </tbody>
</table>

## 9.4 에스크로 관련 코드

[구매결정 상태별 코드]
<table style="width: 100%;">
<colgroup>
  <col style="width: 30%;">
  <col style="width: 70%;">
</colgroup>
  <thead>
    <tr>
      <th style="text-align: center">P_STATUS</th>
      <th style="text-align: center">P_RMESGI</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">00</td>
      <td style="text-align: center">정상처리완료</td>
    </tr>
    <tr>
      <td style="text-align: center">00</td>
      <td style="text-align: center">기 구매거절 거래</td>
    </tr>
    <tr>
      <td style="text-align: center">310004</td>
      <td style="text-align: center">결제 기통보 거래</td>
    </tr>
    <tr>
      <td style="text-align: center">310006</td>
      <td style="text-align: center">취소 불가 지불수단</td>
    </tr>
    <tr>
      <td style="text-align: center">310014</td>
      <td style="text-align: center">기 구매확인 거래</td>
    </tr>
    <tr>
      <td style="text-align: center">310015</td>
      <td style="text-align: center">구매확인 불가 거래상태</td>
    </tr>
    <tr>
      <td style="text-align: center">310017</td>
      <td style="text-align: center">구매거절 불가 거래상태</td>
    </tr>
    <tr>
      <td style="text-align: center">310020</td>
      <td style="text-align: center">구매결정 할 수 없는 상태</td>
    </tr>
    <tr>
      <td style="text-align: center">310026</td>
      <td style="text-align: center">원거래 없음</td>
    </tr>
  </tbody>
</table>

[거래 상태별 응답]
<table style="width: 100%;">
<colgroup>
  <col style="width: 15%;">
  <col style="width: 30%;">
  <col style="width: 10%;">
  <col style="width: 25%;">
  <col style="width: 20%;">
</colgroup>
  <thead>
    <tr>
      <th style="text-align: center">기존상태</th>
      <th style="text-align: center">처리 요청 상태</th>
      <th style="text-align: center">P_STATUS</th>
      <th style="text-align: center">P_CL_STATUS</th>
      <th style="text-align: center">P_RMESG1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">미정</td>
      <td style="text-align: center">구매결정 성공</td>
      <td style="text-align: center">00</td>
      <td style="text-align: center">buyComplete</td>
      <td style="text-align: center">정상처리완료</td>
    </tr>
    <tr>
      <td style="text-align: center">미정</td>
      <td style="text-align: center">구매결정실패, 구매거부실패</td>
      <td style="text-align: center">에러코드</td>
      <td style="text-align: center">buyComplete, denyComplete</td>
      <td style="text-align: center">에러메세지, 가변적</td>
    </tr>
    <tr>
      <td style="text-align: center">미정</td>
      <td style="text-align: center">구매거부성공</td>
      <td style="text-align: center">00</td>
      <td style="text-align: center">denyComplete</td>
      <td style="text-align: center">정상처리완료</td>
    </tr>
    <tr>
      <td style="text-align: center">기 구매거부</td>
      <td style="text-align: center">구매결정성공</td>
      <td style="text-align: center">00</td>
      <td style="text-align: center">buyComplete</td>
      <td style="text-align: center">기 구매거절 거래</td>
    </tr>
    <tr>
      <td style="text-align: center">기 구매거부</td>
      <td style="text-align: center">구매결정실패, 구매거부실패</td>
      <td style="text-align: center">에러코드</td>
      <td style="text-align: center">buyComplete, denyComplete</td>
      <td style="text-align: center">에러메세지, 가변적</td>
    </tr>
    <tr>
      <td style="text-align: center">기 구매거부</td>
      <td style="text-align: center">구매거부성공</td>
      <td style="text-align: center">00</td>
      <td style="text-align: center">denyComplete</td>
      <td style="text-align: center">기 구매거절 거래</td>
    </tr>
  </tbody>
</table>
