---
title: MOBILE
permalink: mobile04.html
sidebar: mobile_sidebar
folder: mobile
toc: false
---

# 4. 승인요청 송신 및 승인처리결과 수신 (only 2 Transaction)

## 4.1 승인 요청 송신

>승인요청 및 결과 수신&quot; 이란, 하기의 Step을 의미합니다.

{% include image.html file="mobile_img07.png" %}

승인요청 시에 사용되는 P_REQ_URL(승인요청 Url) 은 Front-End 단에서 Submit 을 하지 않고, Http-Socket 통신을 통해 Back-End 단으로 요청하셔야 합니다.
당사 P_REQ_URL 은 승인과정을 거친 후, 가맹점의 특정 Url 로 승인결과를 전송하지 않고, 페이지 상에, echo 를 통해 결과를 출력하기만 합니다.
따라서, 승인결과 메시지는 Http-Socket 의 Receive-Data 로 수신받으셔야 합니다. 인증요청을 받은 후, 승인 요청하는 Flow 는 하기의 방식을 참고 하십시오.

{% include image.html file="mobile_img08.png" %}

승인요청 시, 사용하는 통신 규격은 하기와 같습니다.

<table style="table-layout: fixed; width: 100%; text-align: center">
<colgroup>
<col style="width: 30%;">
<col style="width: 70%;">
</colgroup>
  <thead>
    <tr>
      <th style="text-align: center">통신수단</th>
      <th style="text-align: center">통신방식</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">Http-Socket</td>
      <td style="text-align: center">post</td>
    </tr>
  </tbody>
</table>

승인요청 시, 하기의 필드를 반드시 첨부하셔야 합니다.

<table style="table-layout: fixed; width: 100%; text-align: center">
<colgroup>
<col style="width: 30%;">
<col style="width: 25%;">
<col style="width: 55%;">
</colgroup>
  <thead>
    <tr>
      <th style="text-align: center">필드명</th>
      <th style="text-align: center">목 적</th>
      <th style="text-align: left">비 고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">P_TID</td>
      <td style="text-align: center">인증거래번호</td>
      <td style="text-align: left">인증결과 수신 시, 포함된 인증거래번호(P_TID)</td>
    </tr>
    <tr>
      <td style="text-align: center">P_MID</td>
      <td style="text-align: center">상점아이디</td>
      <td style="text-align: left">거래 시 사용된, 당사발급 아이디</td>
    </tr>
  </tbody>
</table>

Http-Socket 을 이용한 승인요청의 샘플 코드는 하기와 같습니다.
_( __하기 코드 내 함수는 직접 구현하셔야 합니다__._ _하기 코드는 로직안내를 위해 작성된 예시입니다__)_

```php
$P_STATUS = $_POST[‘P_STATUS’];
$P_REQ_URL = $_POST[‘P_REQ_URL’];
$P_TID = $_POST[‘P_TID’];
$P_MID = $_POST[‘P_MID’];

function makeParam($P_TID, $P_MID){ 
return “P_TID=”.$P_TID.”&P_MID=”.$P_MID;
}
function parseData($receiveMsg) { //승인결과 Parse
	$returnArr = explode(“&”,$receiveMsg);
	foreach($returnArr as $value){
		$tmpArr = explode(“=”,$value);
		$returnArr[] = $tmpArr;
	}
}
function chkTid($P_TID);		//기승인 TID 여부 확인
function saveTid($P_TID);		//승인된 TID 를 DB 에 저장
function setSocket($host, $port); 	//소켓 생성
function connectSocket($sock);		//소켓 연결
function requestSocket($sock,$param);		//데이터 송신
function responseSocket();		//데이터 수신

if($P_STATUS=="00" && chkTid($P_TID)){
    $sock = setSocket($P_REQ_URL,443);	//https connection
    connectSocket($sock);
    requestSocket($sock,makeParam($P_TID, $P_MID));
    $returnData = responseSocket();
    $returnDataArr = parseData($returnData);	//$returnDataArr 에 승인결과 저장
    saveTid($P_TID);
}
?>
```

## 4.2 승인 결과 수신

### 승인결과 수신필드 상세 (only 2 Transaction)

#### 1) 공통 지불 수신 필드
<table style="table-layout: fixed; width: 100%; text-align: center">
<colgroup>
<col style="width: 30%;">
<col style="width: 25%;">
<col style="width: 55%;">
</colgroup>
  <thead>
    <tr>
      <th style="text-align: center">필 드 명</th>
      <th style="text-align: center">목 적</th>
      <th style="text-align: left">비 고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">P_STATUS</td>
      <td style="text-align: center">거래상태</td>
      <td style="text-align: left">성공: 00</td>
    </tr>
    <tr>
      <td style="text-align: center">P_TID</td>
      <td style="text-align: center">거래번호</td>
      <td style="text-align: left">char(40)</td>
    </tr>
    <tr>
      <td style="text-align: center">P_TYPE</td>
      <td style="text-align: center">지불수단</td>
      <td style="text-align: left">char(10)</td>
    </tr>
    <tr>
      <td style="text-align: center">P_TYPE</td>
      <td style="text-align: center">지불수단</td>
      <td style="text-align: left">CARD(ISP,안심클릭,국민앱카드)<br />VBANK(가상계좌)<br />MOBILE(휴대폰)<br />BANK(계좌이체)</td>
    </tr>
    <tr>
      <td style="text-align: center">P_AUTH_DT</td>
      <td style="text-align: center">승인일자</td>
      <td style="text-align: left">char(14)<br />YYYYmmddHHmmss</td>
    </tr>
    <tr>
      <td style="text-align: center">P_MID</td>
      <td style="text-align: center">상점아이디</td>
      <td style="text-align: left">char(10)</td>
    </tr>
    <tr>
      <td style="text-align: center">P_OID</td>
      <td style="text-align: center">상점주문번호</td>
      <td style="text-align: left">char(100)</td>
    </tr>
    <tr>
      <td style="text-align: center">P_AMT</td>
      <td style="text-align: center">거래금액</td>
      <td style="text-align: left">char(8)</td>
    </tr>
    <tr>
      <td style="text-align: center">P_UNAME</td>
      <td style="text-align: center">주문자명</td>
      <td style="text-align: left">char(30)</td>
    </tr>
    <tr>
      <td style="text-align: center">P_MNAME</td>
      <td style="text-align: center">가맹점 이름</td>
      <td style="text-align: left">주문정보에 입력한 값 반환</td>
    </tr>
    <tr>
      <td style="text-align: center">P_RMESG1</td>
      <td style="text-align: center">메시지1</td>
      <td style="text-align: left">char(500)<br />지불 결과 메시지</td>
    </tr>
    <tr>
      <td style="text-align: center">P_NOTI</td>
      <td style="text-align: center">주문정보</td>
      <td style="text-align: left">char(800)<br />주문정보에 입력한 값 반환</td>
    </tr>
    <tr>
      <td style="text-align: center">P_NOTEURL</td>
      <td style="text-align: center">가맹점 전달 NOTI URL</td>
      <td style="text-align: left">거래요청 시 입력한 값을 <strong>그대로 반환</strong> 합니다.</td>
    </tr>
    <tr>
      <td style="text-align: center">P_NEXT_URL</td>
      <td style="text-align: center">가맹점 전달 NEXT URL</td>
      <td style="text-align: left">거래요청 시 입력한 값을 <strong>그대로 반환</strong> 합니다.</td>
    </tr>
  </tbody>
</table>

#### 2) 신용카드U포인트 지불 수신 필드
<table style="table-layout: fixed; width: 100%; text-align: center">
<colgroup>
<col style="width: 30%;">
<col style="width: 25%;">
<col style="width: 55%;">
</colgroup>
  <thead>
    <tr>
      <th style="text-align: center">필 드 명</th>
      <th style="text-align: center">목 적</th>
      <th style="text-align: left">비 고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">P_CARD_NUM</td>
      <td style="text-align: center">카드번호</td>
      <td style="text-align: left">계약관계에 따라 틀림</td>
    </tr>
  </tbody>
</table>

#### 3) 신용카드 지불 수신 필드

<table style="table-layout: fixed; width: 100%; text-align: center">
<colgroup>
<col style="width: 30%;">
<col style="width: 25%;">
<col style="width: 55%;">
</colgroup>
  <thead>
    <tr>
      <th style="text-align: center">필 드 명</th>
      <th style="text-align: center">목 적</th>
      <th style="text-align: left">비 고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">P_CARD_ISSUER_CODE</td>
      <td style="text-align: center">발급사 코드</td>
      <td style="text-align: left">char(2)</td>
    </tr>
    <tr>
      <td style="text-align: center">P_CARD_MEMBER_NUM</td>
      <td style="text-align: center">가맹점번호</td>
      <td style="text-align: left">자체 가맹점 일 경우만 해당</td>
    </tr>
    <tr>
      <td style="text-align: center">P_CARD_PURCHASE_CODE</td>
      <td style="text-align: center">매입사 코드</td>
      <td style="text-align: left">자체 가맹점 일 경우만 해당</td>
    </tr>
    <tr>
      <td style="text-align: center">P_CARD_PRTC_CODE</td>
      <td style="text-align: center">부분취소 가능여부</td>
      <td style="text-align: left">부분취소가능 : 1 , 부분취소불가능 : 0</td>
    </tr>
    <tr>
      <td style="text-align: center">P_CARD_INTEREST</td>
      <td style="text-align: center">무이자 할부여부</td>
      <td style="text-align: left">0 : 일반, 1 : 무이자</td>
    </tr>
    <tr>
      <td style="text-align: center">P_CARD_CHECKFLAG</td>
      <td style="text-align: center">체크카드 여부</td>
      <td style="text-align: left">0 : 신용카드,1 : 체크카드2 : 기프트카드</td>
    </tr>
    <tr>
      <td style="text-align: center">P_RMESG2</td>
      <td style="text-align: center">메시지2</td>
      <td style="text-align: left">char(500)<br />신용카드 할부 개월 수</td>
    </tr>
    <tr>
      <td style="text-align: center">P_FN_CD1</td>
      <td style="text-align: center">카드코드</td>
      <td style="text-align: left">char(4)</td>
    </tr>
    <tr>
      <td style="text-align: center">P_AUTH_NO</td>
      <td style="text-align: center">승인번호</td>
      <td style="text-align: left">char(30)<br />신용카드거래에서만 사용합니다.</td>
    </tr>
    <tr>
      <td style="text-align: center">P_ISP_CARDCODE</td>
      <td style="text-align: center">VP 카드코드</td>
      <td style="text-align: left"> </td>
    </tr>
    <tr>
      <td style="text-align: center">P_FN_NM</td>
      <td style="text-align: center">결제카드한글명</td>
      <td style="text-align: left">BC카드</td>
    </tr>
  </tbody>
</table>

#### 4) 계좌이체 지불 수신 필드

<table style="table-layout: fixed; width: 100%; text-align: center">
<colgroup>
<col style="width: 30%;">
<col style="width: 25%;">
<col style="width: 55%;">
</colgroup>
  <thead>
    <tr>
      <th style="text-align: center">필 드 명</th>
      <th style="text-align: center">목 적</th>
      <th style="text-align: left">비 고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">P_FN_CD1</td>
      <td style="text-align: center">은행코드</td>
      <td style="text-align: left"></td>
    </tr>
    <tr>
      <td style="text-align: center">P_FN_NM</td>
      <td style="text-align: center">카드번호</td>
      <td style="text-align: left">결제은행한글명</td>
    </tr>
  </tbody>
</table>

#### 5) 휴대폰 지불 수신 필드

<table style="table-layout: fixed; width: 100%; text-align: center">
<colgroup>
<col style="width: 30%;">
<col style="width: 25%;">
<col style="width: 55%;">
</colgroup>
  <thead>
    <tr>
      <th style="text-align: center">필 드 명</th>
      <th style="text-align: center">목 적</th>
      <th style="text-align: left">비 고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">P_HPP_CORP</td>
      <td style="text-align: center">휴대폰통신사</td>
      <td style="text-align: left">char(3)</td>
    </tr>
    <tr>
      <td style="text-align: center">P_HPP_NUM</td>
      <td style="text-align: center">결제 휴대폰 번호</td>
      <td style="text-align: left"> </td>
    </tr>
    <tr>
      <td style="text-align: center">P_HPP_BILLKEY</td>
      <td style="text-align: center">휴대폰 빌키</td>
      <td style="text-align: left">휴대폰 빌링 사용시 휴대폰 빌키( 승인은 PAYAPI 통해서 진행)</td>
    </tr>
  </tbody>
</table>

#### 6) 앱연동 결제구분 수신 필드

<table style="table-layout: fixed; width: 100%; text-align: center">
<colgroup>
<col style="width: 30%;">
<col style="width: 25%;">
<col style="width: 55%;">
</colgroup>
  <thead>
    <tr>
      <th style="text-align: center">필 드 명</th>
      <th style="text-align: center">목 적</th>
      <th style="text-align: left">비 고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">P_SRC_CODE</td>
      <td style="text-align: center">앱연동여부</td>
      <td style="text-align: left">P : 페이핀<br />K : 국민앱카드<br />C: 페이코<br />B: 삼성페이<br />L: LPAY<br />O: 카카오페이<br />G: SSGPAY</td>
    </tr>
  </tbody>
</table>

#### 7) 현금영수증 수신 필드

<table style="table-layout: fixed; width: 100%; text-align: center">
<colgroup>
<col style="width: 30%;">
<col style="width: 25%;">
<col style="width: 55%;">
</colgroup>
  <thead>
    <tr>
      <th style="text-align: center">필 드 명</th>
      <th style="text-align: center">목 적</th>
      <th style="text-align: left">비 고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">P_CSHR_CODE</td>
      <td style="text-align: center">처리상태</td>
      <td style="text-align: left">220000 : 정상, 그 외 : 오류</td>
    </tr>
    <tr>
      <td style="text-align: center">P_CSHR_MSG</td>
      <td style="text-align: center">처리메시지</td>
      <td style="text-align: left"> </td>
    </tr>
    <tr>
      <td style="text-align: center">P_CSHR_AMT</td>
      <td style="text-align: center">현금영수증 총 금액</td>
      <td style="text-align: left">총금액 = 공급가액+세금+봉사료</td>
    </tr>
    <tr>
      <td style="text-align: center">P_CSHR_SUP_AMT</td>
      <td style="text-align: center">공급가액</td>
      <td style="text-align: left"> </td>
    </tr>
    <tr>
      <td style="text-align: center">P_CSHR_TAX</td>
      <td style="text-align: center">세금</td>
      <td style="text-align: left"> </td>
    </tr>
    <tr>
      <td style="text-align: center">P_CSHR_SRVC_AMT</td>
      <td style="text-align: center">봉사료</td>
      <td style="text-align: left"> </td>
    </tr>
    <tr>
      <td style="text-align: center">P_CSHR_TYPE</td>
      <td style="text-align: center">용도구분</td>
      <td style="text-align: left">0:소득공제용, 1:지출증빙용</td>
    </tr>
    <tr>
      <td style="text-align: center">P_CSHR_DT</td>
      <td style="text-align: center">발행시간</td>
      <td style="text-align: left"> </td>
    </tr>
    <tr>
      <td style="text-align: center">P_CSHR_AUTH_NO</td>
      <td style="text-align: center">발행번호</td>
      <td style="text-align: left">가상계좌의 경우,입금 완료 시, 생성되어 모바일 내 채번시에는 전달되지 않습니다.</td>
    </tr>
  </tbody>
</table>

#### 8) 가상계좌 수신 필드 및 상세안내

"가상계좌 방식" 과 "계좌이체 방식" 은 입금 통보 등의 과정을 필요로 하기 때문에, 상기에 안내한 방식과 다소 다른 점이 있습니다.
하기에는 가상계좌와 계좌이체에서 각기 사용하는 "인증완료 후, 이동페이지" 와, "입금통보 혹은 승인완료 통보" 방식에 대하여 안내합니다.

<table style="table-layout: fixed; width: 100%; text-align: center">
<colgroup>
<col style="width: 30%;">
<col style="width: 25%;">
<col style="width: 55%;">
</colgroup>
  <thead>
    <tr>
      <th> </th>
      <th>인증완료 후 이동 URL(Front단)</th>
      <th>입금사실 통보 URL(Back 단)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>가상계좌</td>
      <td>P_NEXT_URL(인증결과송신)</td>
      <td>P_NOTI_URL(,채번정보송신, 입금완료송신)</td>
    </tr>
  </tbody>
</table>

하기에는 호출 된, P_NEXT_URL 에 전달될 파라미터 입니다.

<p style="font-size: 80%">(1-8 . 승인결과 수신필드 상세 (only 2 Transaction) 의 공통 필드 )외 하기필드</p>
<table style="table-layout: fixed; width: 100%; text-align: center">
<colgroup>
<col style="width: 30%;">
<col style="width: 25%;">
<col style="width: 55%;">
</colgroup>
  <thead>
    <tr>
      <th style="text-align: center">필드명</th>
      <th style="text-align: center">목 적</th>
      <th style="text-align: left">비고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">P_VACT_NUM</td>
      <td style="text-align: center">입금할 계좌 번호</td>
      <td style="text-align: left">char(20)</td>
    </tr>
    <tr>
      <td style="text-align: center">P_VACT_DATE</td>
      <td style="text-align: center">입금마감일자</td>
      <td style="text-align: left">char(8) : yyyymmdd</td>
    </tr>
    <tr>
      <td style="text-align: center">P_VACT_TIME</td>
      <td style="text-align: center">입금마감시간</td>
      <td style="text-align: left">char(6) hhmmss</td>
    </tr>
    <tr>
      <td style="text-align: center">P_VACT_NAME</td>
      <td style="text-align: center">계좌주명</td>
      <td style="text-align: left"> </td>
    </tr>
    <tr>
      <td style="text-align: center">P_VACT_BANK_CODE</td>
      <td style="text-align: center">은행코드</td>
      <td style="text-align: left">char(2)</td>
    </tr>
  </tbody>
</table>

P_NOTI_URL로 전송되는 승인결과는 하단의 노티 수신 사용법 안내에 대한 내용을 참고 바랍니다.
_가상계좌_ _Flo_w 는 하기와 같습니다.

{% include image.html file="mobile_img09.png" %}

가상계좌는 상기와 같이 채번 시 1회, 입금 확인 후 1회, 총 2회 노티를 통해 통보합니다.

상기에 안내한 바와 같이, 가상계좌 방식과 계좌이체 방식, 그리고 기타 방식(신용카드 등) 의 차이점이 있사오니, 이점 유의 하시기 바랍니다.



## 4.3 1 Transaction 방식에서 결제 완료 후 결과 수신

P_NOTI_URL 로 전송되는 파라미터 및 값은 하단의 노티 수신 사용방법 안내 내용을 참고하여 주시기 바랍니다.

-  :warning:<red>P_NOTI_URL은 네트워크 사정에 따라 1회 이상 발생될 수 있사오니, 중복호출여부를 체크하는 루틴을 반드시 구현하십시오.</red>
-  NOTI 를 통한 결과 송신은 하기의 조건에 따라 수행됩니다.
   24시간 이내 재전송 가능 | 24시간 이후 시퀀스 종료 | 재전송 주기 약 10분


## 4.4 P_NOTI_URL  수신 후 ,  처리방법

당사 Back 단에서 전송된 Noti 는 하기의 조건을 충족하지 않을 경우, 재전송 루틴을 수행하게 됩니다.
따라서, (1-10.1 Transaction 방식에서 결제 완료 후 결과 수신)장에서 안내한 바와 같이 중복체크 루틴을 반드시 구현하시고, 하기의 조건을 충족하여 주시기 바랍니다.

- Noti 수신 후, P_NOTI_URL 에 OK 만 출력 요망.

- <red>대문자 OK 외 html 및 공백, 개행문자 불허<red>