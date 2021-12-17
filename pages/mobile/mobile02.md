---
title: MOBILE
permalink: mobile02.html
sidebar: mobile_sidebar
folder: mobile
toc: false
---

# 2. 상점 모바일 결제 연동

## 2.1 전 지불수단 공통 필드

Mobile Web 서비스 접속 시, 결제페이지를 구성하기 위해서는 하기 Parameter를 필요로 합니다.

```javascript
양식 예시 : <input type="hidden" name="필드명" value="값 예시" />;
```

<table class="tg" style="table-layout: fixed; width: 100%; text-align: center">
<colgroup>
<col style="width: 15%;">
<col style="width: 15%;">
<col style="width: 15%;">
<col style="width: 20%;">
<col style="width: 40%;">
</colgroup>
<thead>
  <tr style="text-align: center">
    <th>필드명</th>
    <th>목&nbsp;&nbsp;적</th>
    <th>크&nbsp;&nbsp;기</th>
    <th>필수여부</th>
    <th>부가설명 및 주의사항</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>P_MID</td>
    <td>상점아이디</td>
    <td>주문번호</td>
    <td>char(10)</td>
    <td>계약된 당사발급 아이디</td>
  </tr>
  <tr>
    <td>P_OID</td>
    <td>주문번호</td>
    <td>Char(40)</td>
    <td>필수대상 외 선택</td>
    <td>한글을 제외한, 숫자/영문/특수기호의 형태<br>필수대상 : 가상계좌</td>
  </tr>
  <tr>
    <td>P_AMT</td>
    <td>거래금액</td>
    <td>Char(8)</td>
    <td>필수</td>
    <td>단위 표시 기호(콤마) 를 반드시 제거 요망</td>
  </tr>
  <tr>
    <td>P_UNAME</td>
    <td>고객성명</td>
    <td>Char(30)</td>
    <td>필수</td>
    <td></td>
  </tr>
  <tr>
    <td>P_MNAME</td>
    <td>가맹점 이름</td>
    <td>Char(30)</td>
    <td>선택</td>
    <td></td>
  </tr>
  <tr>
    <td>P_NOTI</td>
    <td>기타주문정보</td>
    <td>Char(800)</td>
    <td>선택</td>
    <td>이 값은 가맹점에서 이용하는 추가 정보 필드로 전달한 값이 그대로 반환됩니다. 결제처리 시, 꼭 필요한 내용만 사용하세요.<br> 800byte를 초과하는 P_NOTI의 값은 차후 문제가 생길 여지가 있으니 반드시 800byte를 초과하지 않도록 설정해야 합니다.</td>
  </tr>
  <tr>
    <td>P_GOODS</td>
    <td>결제상품명</td>
    <td>Char(80)</td>
    <td>필수</td>
    <td></td>
  </tr>
  <tr>
    <td>P_MOBILE</td>
    <td>구매자  휴대폰번호</td>
    <td>Char(20)</td>
    <td>선택</td>
    <td>'-' 를 포함한 번호를 적어주세요.구현 예시 : 000-0000-0000</td>
  </tr>
  <tr>
    <td>P_EMAIL</td>
    <td>구매자 E-mail</td>
    <td>Char(60)</td>
    <td>선택</td>
    <td>구현 예시 : abc@abc.com</td>
  </tr>
  <tr>
    <td>P_NEXT_URL</td>
    <td>인증결과수신</td>
    <td>Char(250)</td>
    <td>예외대상 외 필수</td>
    <td>사용자의 인증이 완료될 때, 이 Url 로 인증결과를 전달합니다.<br> Method : post or get (issue : 1-24보기) <br> Scheme : https (issue : 1-22보기)<br>Parameters : 0.<br>인증결과수신 (only 2 Transaction)참고 <br> 예외대상 : Kpay <br>한글도메인 사용불가 <br>https  권장</td>
  </tr>
  <tr>
    <td>P_NOTI_URL</td>
    <td>승인결과통보Url</td>
    <td>Char(250)</td>
    <td>적용대상 필수</td>
    <td>가맹점과 인증/승인과정을 거치지 않고 승인결과를 통보하는 용도로 사용합니다.<br> 단, 가상계좌의 경우, 입금완료시각이 비동기식 이므로, 입금완료 통보를 위해 사용됩니다.<br> Method : post<br> 적용대상 : 가상계좌의 NOTI Url 은 네트워크 사정에 따라 중복전송 될 수 있으니, 중복수신여부 체크루틴을 반드시 구현하시기 바랍니다.<br> * 한글도메인 사용불가</td>
  </tr>
  <tr>
    <td>P_TAX</td>
    <td>부가세</td>
    <td>Char(8)</td>
    <td>선택</td>
    <td>영수증에 표기할 부가세 금액<>br</td>
  </tr>
  <tr>
    <td>P_TAXFREE</td>
    <td>비과세</td>
    <td>Char(8)</td>
    <td>선택</td>
    <td>과세 되지 않는 금액 대상 : &#39;부가세업체정함&#39; 설정업체에 한함</td>
  </tr>
  <tr>
    <td rowspan="6">P_OFFER_PERIOD</td>
    <td rowspan="6">제공기간</td>
    <td></td>
    <td rowspan="6">선택</td>
    <td rowspan="6">상품의 제공기간을 설정해야 하는 경우, 사용되는 옵션으로, Mobile Web 서비스에 디스플레이 하는 용도로만 사용됩니다.</td>
  </tr>
  <tr>
    <td></td>
  </tr>
 <tr>
    <td></td>
  </tr>
 <tr>
    <td></td>
  </tr>
 <tr>
    <td></td>
  </tr>
 <tr>
    <td></td>
  </tr>
</tbody>
</table>