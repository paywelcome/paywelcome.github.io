---
title: 거래알림(noti)
permalink: noti01.html
sidebar: noti_sidebar
folder: noti
toc: false
---

# 1. 거래알림(노티)

- 가맹점관리자에 설정된 노티페이지를 호출하여 거래결과를 통보합니다.
- 거래알림(노티)은 중복 전송 될수 있으므로 로그용으로 사용 하실 것을 권고 드립니다.

## 1.1 방화벽 정보
>실시간 거래 알림수신을 위해서는 아래의 가맹점 방화벽이 허용되어 있어야합니다.

<table>
  <thead>
    <tr>
      <th style="text-align: center; width: 40%">구분</th>
      <th style="text-align: center; width: 60%">IP</th>
    </tr>
  </thead>
   <tbody>
   <tr>
   <td class="center-align">테스트</td>
   <td class="center-align">118.130.130.26</td>
   </tr>
   <tr>
   <td class="center-align" rowspan="2">운영</td>
   <td class="center-align">118.129.171.152</td>
   </tr>
   <tr>
   <td class="center-align">118.129.171.153</td>
   </tr>
   </tbody>
</table>


## 1.1 거래알림 사용 설정

`가맹점관리자 > 상점정보 > 결제수단 정보 > 결제수단 거래알림` 메뉴에서 필요한 옵션입력 및 선택후 변경버튼으로 설정가능합니다.

{% include image.html file="noti_img01.png" %}

- **수신 URL** : http:// 또는 https:// 까지 붙여서 알림 수신 받을 URL
- **수신컨텐츠 형식** : JSON 또는 KEY-VALUE(KEY=VALUE&amp;KEY=VALUE) 중 선택 가능
- **인코딩 방식** : 한글 인코딩방식 UTF-8 이나 EUC-KR 중 선택가능
- **취소거래 수신여부** : 취소거래 알림 수신 / 미수신 중 선택 가능
- **실패거래 수신여부** : 실패거래 알림 수신/ 미수신 중 선택 가능
- **수신실패건 재전송 여부** : 알림수신 실패시 재전송 여부( <img class="emoji" title=":warning:" alt=":warning:" src="https://github.githubassets.com/images/icons/emoji/unicode/26a0.png"><code class="language-plaintext highlighter-rouge">재전송 선택시 가맹점 DB에 중복으로 적재될 수 있으므로 주의요함</code>)

## 1.2 위변조 방지 검증

- 가맹점의 주문정보에 대한 위/변조 방지를 위해 일부 주요 데이터에 한해서 SHA256으로 Hash 암호화하여 Signature 필드 값으로 받아 위/변조 여부를 체크하실 수 있습니다.

### 테스트 서버 위변조 방지 설정용 데이터
```java
String mid = "xxxxxxxxxx"; // 가맹점 ID(가맹점 수정후 고정)
// 가맹점에 제공된 웹 표준 사인키(가맹점 수정후 고정)
String signKey = "xxxxx";
```

### 상점 연동을 위한 테스트 MID

>Test mid와 signkey값은 계약가맹점에 한해 별도 전달 예정입니다.

[//]: # (MID 연동 table)
<table class="tg" style="table-layout: fixed; width: 100%">
<tbody>
  <tr>
    <td class="center-align">Test mid</td>
    <td class="center-align" rowspan="2"><a href="mailto:mainpg_support@welcomepayments.co.kr">메일로 문의하기(support@welcomepayments.co.kr)</a></td>
  </tr>
  <tr>
    <td class="center-align">signKey</td>
  </tr>
</tbody>
</table>


`샘플로 제공 되는 테스트 MID만 사용가능하며 운영 MID 사용 불가`

### signkey 발급 방법
- 관리자 페이지(https://wbiz.paywelcome.co.kr)의 상점정보 > 계약정보 > 부가정보의 웹결제 signkey생성 조회 버튼 클릭 후<br>
  팝업창에서 생성 버튼 클릭 후 해당 값 소스에 반영하시기 바랍니다.

1.
# 2. 유의사항

- 위변조 방지를 위해서 전달된 Signature 로 위변조 검증을 진행해주셔야 합니다 .
- 리턴 메시지를 반드시 보내주시기 바랍니다.
- 거래알림 ( 노티 ) 은 네트워크 사정에 따라 중복수신 될수 있으므로 기 처리 데이터인지 검증 후 저장하시기 바랍니다.
- 거래알림은 알림 실패시 최대 20회까지 재발송됩니다.

# 3.거래 알림(노티) 파라미터

## 3.1 전달 파라미터

<table class="tb2">
<thead> 
    <tr>
        <th class="center-align" rowspan="2" style="width: 15%">필드</th>
        <th class="center-align" rowspan="2" style="width: 15%">필드명</th>
        <th class="center-align" rowspan="2">타입</th>
        <th class="center-align" rowspan="2" style="width: 20%">설명</th>
        <th class="center-align" style="width: 6%">카드<br>ISP</th>
        <th class="center-align" style="width: 7%">핸드폰</th>
        <th class="center-align" style="width: 6%">계좌이체</th>
        <th class="center-align" colspan="2" style="width: 6%">가상계좌</th>
        <th class="center-align" rowspan="2" style="width: 6%">취소</th>
        <th class="center-align" rowspan="2" style="width: 6%">부분취소</th>
    </tr>        
    <tr>
        <th class="center-align">승인</th>
        <th class="center-align">승인</th>
        <th class="center-align">승인</th>
        <th class="center-align">입금</th>
        <th class="center-align">채번</th>
    </tr>
</thead>
    <tbody>
    
<tr>
      <td class="center-align">transType</td>
      <td class="center-align">거래구분</td>
      <td class="center-align">String(2)</td>
      <td class="left-align">승인: 00<br>취소: 01<br>부분취소: 11<br>가상계좌 입금: 02<br>가상계좌 채번:03<br></td>
      <td class="center-align">○</td>
      <td class="center-align">○</td>
      <td class="center-align">○</td>
      <td class="center-align">○</td>
      <td class="center-align">○</td>
      <td class="center-align">○</td>
      <td class="center-align">○</td>
    </tr>
    </tbody>
</table>


