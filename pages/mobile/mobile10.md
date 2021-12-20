---
title: MOBILE
permalink: mobile10.html
sidebar: mobile_sidebar
folder: mobile
toc: false
---

# 10. 노티수신(P_NOTI_URL) 사용방법 안내

>웰컴페이먼츠 지불서버는 지불 결과를 실시간으로 회원사 측의 노티페이지를 호출하여 지불 결과를 통보합니다.<br>
>노티페이지(P_NOTI_URL)는 정상적으로 결제 데이터를 받을 때까지 반복 호출됩니다.<br>
>노티페이지(P_NOTI_URL)페이지는 웰컴페이먼츠에서 백엔드(backend)로 호출을 하는 페이지로, 고객이 보는 결제 화면과는 무관합니다.<br>

[노티를 받을 때 전달되는 파라미터]

<table style="width: 100%;">
<colgroup>
    <col style="width: 10%;">
    <col style="width: 20%;">
    <col style="width: 20%;">
    <col style="width: 10%;">
    <col style="width: 40%;">
</colgroup>
<thead>
  <tr>
    <th>순번</th>
    <th>필드</th>
    <th>필드명</th>
    <th>타입</th>
    <th>비고</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>1</td>
    <td>P_STATUS</td>
    <td>거래상태</td>
    <td>char(2)</td>
    <td>성공: 00, 실패 : 01, 가상계좌 입금 통보 시 : 02</td>
  </tr>
  <tr>
    <td>2</td>
    <td>P_TID</td>
    <td>거래번호</td>
    <td>char(40)</td>
    <td></td>
  </tr>
  <tr>
    <td>3</td>
    <td>P_TYPE</td>
    <td>지불수단</td>
    <td>char(10)</td>
    <td>ISP(신용카드  ISP), CARD(신용카드 안심클릭 및 국민앱카드), VBANK( 가상계좌 )</td>
  </tr>
  <tr>
    <td>4</td>
    <td>P_AUTH_DT</td>
    <td>승인일자</td>
    <td>char(14)</td>
    <td>YYYYmmddHHmmss</td>
  </tr>
  <tr>
    <td>5</td>
    <td>P_MID</td>
    <td>상점아이디</td>
    <td>char(10)</td>
    <td></td>
  </tr>
  <tr>
    <td>6</td>
    <td>P_OID</td>
    <td>상점 주문번호</td>
    <td>char(100)</td>
    <td></td>
  </tr>
  <tr>
    <td>7</td>
    <td>P_FN_CD1</td>
    <td>금융사코드</td>
    <td>char(4)</td>
    <td>계좌이체, 가상계좌: 은행코드(계좌이체 내 뱅크월렛 결제 건은 BW로 전달) <br> 카드:카드코드, 핸드폰결제: 핸드폰 번호 앞 3자리</td>
  </tr>
  <tr>
    <td>8</td>
    <td>P_FN_CD2</td>
    <td>금융사코드</td>
    <td>char(10)</td>
    <td>계좌이체: 은행영문 코드 (계좌이체 내 뱅크월렛 결제 건은 BW로 전달) <br> 카드: P_FN_CD1과 동일 <br> 핸드폰결제: P_FN_CD1과 동일</td>
  </tr>
  <tr>
    <td>9</td>
    <td>P_FN_NM</td>
    <td>금융사명</td>
    <td>char(50)</td>
    <td>은행명, 카드사명, 이동통신사명</td>
  </tr>
  <tr>
    <td>10</td>
    <td>P_AMT</td>
    <td>거래금액</td>
    <td>char(12)</td>
    <td></td>
  </tr>
  <tr>
    <td>11</td>
    <td>P_UNAME</td>
    <td>주문자명</td>
    <td>char(30)</td>
    <td></td>
  </tr>
  <tr>
    <td>12</td>
    <td>P_RMESG1</td>
    <td>메시지1</td>
    <td>char(500)</td>
    <td>가상계좌 : 채번 된 가상계좌번호, 입금기한 예) <code>P_VACCT_NO=01440064018781P_EXP_DT=20100325</code></td>
  </tr>
  <tr>
    <td>13</td>
    <td>P_RMESG2</td>
    <td>메시지2</td>
    <td>char(500)</td>
    <td>신용카드의 경우, 할부 결제 시 할부 개월 수 표시  예) 02 (02개월)</td>
  </tr>
  <tr>
    <td>14</td>
    <td>P_RMESG3</td>
    <td>메시지3</td>
    <td>char(500)</td>
    <td>임의필드<code>(name^value|name^value|…)</code> <br> RM3_DISC_AMT : 할인금액 char(12)<br>RM3_PRICE : 실승인금액 char(12)<br>RM3_ORG_AMT : 원금액 char(12)<br>RM3_EVENT_CODE : 이벤트 코드 char(2)<br>RM3_INTEREST : 신용카드 무이자 여부 char(1)<br>RM3_ COUPONFLAG : 쿠폰사용여부 char(1)<br>RM3_COUPONPRICE : 쿠폰사용 실 승인금액 char(12)<br>RM3_COUPONDISCOUNT : 쿠폰 할인금액 char(12)</td>
  </tr>
  <tr>
    <td>15</td>
    <td>P_NOTI</td>
    <td>주문정보</td>
    <td>char(4000)</td>
    <td>거래요청시 입력한 P_NOTI의 값을 **그대로 반환**합니다.</td>
  </tr>
  <tr>
    <td>16</td>
    <td>P_AUTH_NO</td>
    <td>승인번호</td>
    <td>char(30)</td>
    <td>신용카드거래에서만 사용합니다.<br><strong>여신 승인거래에 대해서만 전달</strong></td>
  </tr>
  <tr>
    <td>17</td>
    <td>P_CARD_ISSUER_CODE</td>
    <td>발급사 코드</td>
    <td>char(4)</td>
    <td></td>
  </tr>
  <tr>
    <td>18</td>
    <td>P_CARD_NUM</td>
    <td>카드번호</td>
    <td>char(16)</td>
    <td>계약관계에 따라 틀림<br><strong>여신 승인거래에 대해서만 전달</strong></td>
  </tr>
  <tr>
    <td>19</td>
    <td>P_CARD_MEMBER_NUM</td>
    <td>가맹점번호</td>
    <td>char(15)</td>
    <td>자체 가맹점 일 경우만 해당</td>
  </tr>
  <tr>
    <td>20</td>
    <td>P_CARD_PURCHASE_CODE</td>
    <td>매입사코드</td>
    <td>char(2)</td>
    <td>자체 가맹점 일 경우만 해당</td>
  </tr>
  <tr>
    <td>21</td>
    <td>P_PRTC_CODE</td>
    <td>부분취소 가능여부</td>
    <td>char(1)</td>
    <td>부분취소가능 : 1, 부분취소불가능 : 0</td>
  </tr>
  <tr>
    <td>22</td>
    <td>P_SRC_CODE</td>
    <td>앱 연동 결제 구분</td>
    <td>char(3)</td>
    <td>K : 국민앱카드</td>
  </tr>
  <tr>
    <td>23</td>
    <td>P_ISP_CARDCODE</td>
    <td>VCARD코드</td>
    <td>char(25)</td>
    <td>ISP 발급사코드 및 기타 정보</td>
  </tr>
  <tr>
    <td>24</td>
    <td>P_CARD_PURCHASE_NAME</td>
    <td>매입사명</td>
    <td>char(22)</td>
    <td></td>
  </tr>
  <tr>
    <td>25</td>
    <td>P_CARD_ISSUER_NAME</td>
    <td>발급사명</td>
    <td>char(22)</td>
    <td></td>
  </tr>
  <tr>
    <td>26</td>
    <td>P_MERCHANT_RESERVED</td>
    <td>임시필드</td>
    <td>char(5000)</td>
    <td>1. pg에서 임의로 사용하는 필드<br>- <code>name^value|name^value|..</code><br>2. 현대M포인트, BC TOP포인트 등 사용 내역 표시(char12)<br>- <code>dXNlcG9pbnQ9MCY=(Base64encode) usepoint=0&(Base64decode)</code></td>
  </tr>
  <tr>
    <td>27</td>
    <td>P_CSHR_AMT</td>
    <td>현금영수증 거래 금액</td>
    <td>char(12)</td>
    <td>계좌이체, 가상계좌 현금영수증 거래 금액<br><strong>※ 가상계좌 채번 결과에 전달</strong></td>
  </tr>
  <tr>
    <td>28</td>
    <td>P_CSHR_SUP_AMT</td>
    <td>현금영수증 공급가액</td>
    <td>char(12)</td>
    <td>계좌이체, 가상계좌 현금영수증 공급가액<br><strong>※ 가상계좌 채번 결과에 전달</strong></td>
  </tr>
  <tr>
    <td>29</td>
    <td>P_CSHR_TAX</td>
    <td>현금영수증 부가가치세</td>
    <td>char(12)</td>
    <td>계좌이체, 가상계좌 현금영수증 부가가치세<br><strong>※ 가상계좌 채번 결과에 전달</strong></td>
  </tr>
  <tr>
    <td>30</td>
    <td>P_CSHR_SRVC_AMT</td>
    <td>현금영수증 봉사료</td>
    <td>char(12)</td>
    <td>계좌이체, 가상계좌 현금영수증 부가가치세<br><strong>※ 가상계좌 채번 결과에 전달</strong></td>
  </tr>
  <tr>
    <td>31</td>
    <td>P_CSHR_TYPE</td>
    <td>현금영수증 거래자 구분</td>
    <td>char(1)</td>
    <td>0 : 소비자 소득공제용 / 1 : 사업자 지출증빙용계좌이체, 가상계좌 현금영수증 거래자 구분<br>※ 가상계좌 채번 결과에 전달</td>
  </tr>
  <tr>
    <td>32</td>
    <td>P_CSHR_DT</td>
    <td>현금영수증 발행일자</td>
    <td>char(14)</td>
    <td>YYYYmmddHHmmss계좌이체, 가상계좌 현금영수증 발행일자※ 가상계좌 입금 결과에 전달</td>
  </tr>
  <tr>
    <td>33</td>
    <td>P_CSHR_AUTH_NO</td>
    <td>현금영수증 발행승인번호</td>
    <td>char(9)</td>
    <td>계좌이체, 가상계좌 현금영수증 발행승인번호※ 가상계좌 입금 결과에 전달</td>
  </tr>
</tbody>
</table>

- 16, 18번 항목의 승인번호 및 카드번호의 경우 페이코포인트 전액, 카카오머니 거래의 경우 여신승인 대상이 아님으로 전달되지 않습니다.

#### 주의사항

- WEB 방식의 가상계좌를 이용하는 경우에도 입금통보를 위해 Receive 페이지를 구성하게 되는데,
  입금통보 외에 가상 계좌 채번 시에도 P_NOTI_URL 로 설정된 주소로 결과가 전송되니 채번 시 전달되는 내용은 무시하시기 바랍니다.
- 또한, 입금 통보 수신 시, 기 수신받은 P_TID 인지 반드시 체크하는 로직을 구성하시길 바랍니다.
- 노티는 네트워크의 사정에 따라, 중복수신 될 수 있습니다.