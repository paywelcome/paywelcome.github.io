---
title: PC(웹표준)
permalink: stdweb03.html
sidebar: stdweb_sidebar
folder: stdweb
toc: false
keywords: 코드, 결제수단, 옵션
---

<div style="display: inline-block; width: 100%;">
  <a style="float:left;" href="/stdweb02.html">◀이전페이지</a>
</div>

# 3. 부록

## 3.1 카드결제 직접호출

- 카드 결제 직접호출을 원하실 경우 해당 옵션을 설정하시기 바랍니다.
- 이 외 정보는 상기 본 매뉴얼과 동일합니다.

<table>
  <thead>
    <tr>
      <th style="text-align: center; width:30%">필드명</th>
      <th style="text-align: center; width:15%">코드</th>
      <th style="text-align: left; width:55%">설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">gopaymethod(택1)</td>
      <td style="text-align: center">onlyacard</td>
      <td style="text-align: left">안심결제 결제창</td>
    </tr>
    <tr>
      <td style="text-align: center">onlyvcard</td>
      <td style="text-align: center">ISP 결제창</td>
      <td style="text-align: left"> </td>
    </tr>
    <tr>
      <td style="text-align: center">acceptmethod</td>
      <td style="text-align: center">cardonly</td>
      <td style="text-align: left">옵션추가</td>
    </tr>
    <tr>
      <td style="text-align: center">d_card</td>
      <td style="text-align: center">[String]</td>
      <td style="text-align: left">직접 호출할 카드사 코드<a href="/code02.html#24-카드사-승인코드"><strong>[참조-카드사 승인코드]</strong></a>
      </td>
    </tr>
    <tr>
      <td style="text-align: center">d_quota</td>
      <td style="text-align: center">[String]</td>
      <td style="text-align: left">직접호출 할부 설정,필수 입력, “00” 일시불도 필수 입력, “02” 2개월..</td>
    </tr>
  </tbody>
</table>

#### 예시
```javascript
<input type="hidden" name="gopaymethod" value="onlyacard">
<input type="hidden" name="acceptmethod" value="cardonly">
<input type="hidden" name="d_card" value="01">
<input type="hidden" name="d_quota" value="00">
```

## 3.2 간편결제 직접호출

- 간편결제 직접호출을 원하실 경우 해당 옵션을 설정하시기 바랍니다.
- 간편결제 직접호출 연동 시, 웰컴페이먼츠 계약담당자와 사전 협의가 이루어져야 합니다.(별도 사용 설정 필요)
- 간편 결제 직접 호출 연동 시,전자금융거래 이용약관은 가맹점 페이지에서 동의 받아주셔야 합니다.
- 이 외 정보는 상기 본 매뉴얼과 동일합니다.

| 필드명                  | 코드           | 설명        |
| :--------------------: | :------------: | :--------- |
| gopaymethod(간편결제 택1) | onlykakaopay | 카카오페이 결제창 |
| onlylpay             | 엘페이 결제창      |           |
| onlypayco            | 페이코결제창       |           |
| acceptmethod         | cardonly     | 옵션추가      |

#### 예시
```javascript
<input type="hidden" name="gopaymethod" value="onlykakaopay">
<input type="hidden" name="acceptmethod" value="cardonly">
```

## 3.3 PHP연동 시 SSL 통신 오류 조치

- php 5.6 이상 버전에서 인증서를 확인하는 옵션인 verify_peer 의 값이 flase => true로 변경이 되었습니다. 때문에 서버의 PHP버전이 5.6이상이고 외부로 HTTPS 통신시 아래와 같은 에러 메시지가 발생할 수 있습니다.

## 3.4 가상계좌 NONE UI 방식 호출

<table>
  <thead>
    <tr>
      <th style="text-align: center; width:20%">필드명</th>
      <th style="text-align: center; width:20%">코드</th>
      <th style="text-align: left; width:60%">설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">gopaymethod(택1)</td>
      <td style="text-align: center">onlyvbanknone</td>
      <td style="text-align: left">가상계좌의 결제창없이 연동</td>
    </tr>
    <tr>
      <td  rowspan="2" style="text-align: center; vertical-align: middle">acceptmethod</td>
      <td style="text-align: center">va_bankcd(은행코드)</td>
      <td style="text-align: left">가상계좌 채번에 필요한 은행코드 은햅(코드값은 은행 코드 표 참고)</td>
    </tr>
    <tr>
      <td style="text-align: center">va_receipt(발급옵션)</td>
      <td style="text-align: left">va_receipt(1) : 소득공제용 / va_receipt(2) : 지출증빙용</td>
    </tr>
    <tr>
      <td style="text-align: center">INIregno</td>
      <td style="text-align: center"> </td>
      <td style="text-align: left">현금영수증 발급을 위한 신분인식번호 입력(미입력시 자진 발급 처리)<br>소득공제용 : 주민등록번호,카드번호,휴대폰 번호 / 지출증빙용 : 사업자번호</td>
    </tr>
  </tbody>
</table>

- 그외옵션은 기존가상계좌추가필드와 동일

#### 예시
```javascript
<input type="hidden" name="gopaymethod" value="onlyvbanknone">
<input type="hidden" name="acceptmethod" value="va_bankcd(20):va_receipt(1)">
```

<div style="display: inline-block; width: 100%; margin-top: 50px;">
  <a style="float:left;" href="/stdweb02.html">◀이전페이지</a>
</div>