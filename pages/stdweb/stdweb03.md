---
title: PC(웹표준)결제
permalink: stdweb03.html
sidebar: stdweb_sidebar
folder: stdweb
toc: false
---


# 3. 결제 연동
## 3.1 결제 요청 페이지 작성(PayRequest)
### 3.1.1 결제 요청 데이터

- 내부 처리용 데이터 별도 저장
- form 데이터 처리가 필요한 경우 페이지 표시전에 별도로 DB 또는 세션 등에 저장해 두시기 바랍니다.
#### signkey 값 설정
- 웹 표준 결제 이용시 패스워드 기능을 하는 코드로 MID 번호별로 부여됩니다.

```java
String mid = "welcometst"; // 가맹점 ID(가맹점 수정후 고정)
// 가맹점에 제공된 웹 표준 사인키(가맹점 수정후 고정)
String signKey = "QjZXWDZDRmxYUXJPYnMvelEvSjJ5QT09";
```
#### signkey 발급 방법
- 관리자 페이지의 상점정보 :arrow_forward: 계약정보 :arrow_forward: 부가정보의 웹결제 signkey생성 조회 버튼 클릭 후
  팝업창에서 생성 버튼 클릭 후 해당 값 소스에 반영하시기 바랍니다.

#### 표준결제 스크립트 Import
- 실서버( 실반영시 반드시 수정)

  `<script language="javascript" type="text/javascript" src="HTTPS://stdpay.paywelcome.co.kr/stdjs/INIStdPay.js" charset="UTF-8"></script>`
- 테스트 서버 연동(샘플로 제공 되는 테스트 MID 전용으로 상용 MID사용불가)

   `<script language="javascript" type="text/javascript" src="HTTPS://tstdpay.paywelcome.co.kr/stdjs/INIStdPay.js" charset="UTF-8"></script>`

- head Tag안에 설정
- 페이지 인코딩에 관계없이 고정 charset="UTF-8"(실 테스트 용 구분 후 사용)

```javascript
<head>
….
<script language="javascript" type="text/javascript" src="HTTPS://stdpay.paywelcome.co.kr/stdjs/INIStdPay.js" charset="UTF-8"></script>
….
</head>….

```

#### Iframe, Popup 사이즈
- iframe의 경우 ( 사용 권장)
  `width:820px; height=600px;`
- popup 의 경우 ( 팝업 사용을 권장하지 않으며, 브라우저별 이슈 발생 시 대응불가 )
  `width=820px;height=600px`

#### Popup 허용 여부 체크 기능
- 팝업 허용 설정이 안되어 있을 경우, 가맹점의 요청페이지가 허용시 리프레시됨으로, 로딩 완료 후 가 팝업을 띄워주는 기능
- `<body ... onload="INIStdPay.allowpopup();">` 추가
#### INIStdpay.pay 함수호출
- INIStdpay.pay 함수 호출은 submit 이 아닌 단순 action 형태로 진행
  `<button onclick="INIStdPay.pay('SendPayForm_id')" style="padding:10px">결제요청</button>`
#### Form에 결제 요청 데이터 생성
- Form Tag에 ID설정(결제요청 스크립트 실행시 사용됨)
- 필드명 대소문자 구분
  (일부 가맹점에서 필요에 의해 사용자가 변경하는 경우를 제외하고 모두 type="hidden"을 사용)

- 아래 요청데이터 / Sample Source를 참조
```javascript
<form id=" SendPayForm_id" name="SendPayForm_name" method="POST">
  <input type="hidden" name="mid" value="welcometst"/>
  <input type="hidden" name="price" value="1004"/>
   ……….. 
</form>
```

| :warning: | Web Standard 서비스는 Form Post로 결제 요청되며, `<form>` 태그에 action 속성 설정 / submit 등의 모든 동작은 Import 된 스크립트에 의해서 자동 처리됩니다 |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |

- 결제 인증 기본 요청데이터 필드는 아래와 같습니다.

#### [TABLE 1-1] 기본 요청데이터 필드
|     필드명      | 한글명칭              | Data Type | 예시 / `기본값`                               | 설명                                       | 필수여부       | 크기(최대)        |
| :----------: | ----------------- | --------- | ---------------------------------------- | ---------------------------------------- | ---------- | ------------- |
|   version    | 버전                | String    | "1.0"                                    | 전문 버전                                    | Yes        | 20 Byte       |
|     mid      | 상점아이디             | String    | "welcometst"                             | 제공된 mid<br>10자리 고정                       | Yes(위변조검증) | 10 Byte Fixed |
|     oid      | 주문번호              | String    | "welcometst_1335233672723"               | 주문단위 unique한 값<br>( mid+"_"+timestamp )  | Yes        | 40 Byte       |
|   goodname   | 상품명               | String    | "키보드/마우스"                                | 한글/특수기호 입력가능<br>40Byte 초과 요청시 37Byte+…으로 자동 변환 | Yes        | 80 Byte       |
|    price     | 결제금액              | Number    | 1004                                     | 숫자만 입력<br>1달러는 100으로 시작                  | Yes(위변조검증) | 8Byte         |
|     tax      | 부가세               | Number    | 1004                                     | 숫자만 입력<br>대상: '부가세업체정함' 설정업체에 한함<br>주의: 전체금액의 10%이하로 설정<br>가맹점에서 등록시 VAT가 총 상품가격의 10% 초과할 경우는 거절됨 | No         | 8Byte         |
|   taxfree    | 비과세               | Number    | 1004                                     | 숫자만 입력<br>대상: '부가세업체정함' 설정업체에 한함과세되지 않는 금액 | No         | 8Byte         |
|   currency   | 통화구분              | String    | "WON"<br>[WON:한화,USD:달러]                 | \* USD는 카드 결제만 가능(ISP는 결제안됨)             | Yes        | 3 Byte        |
|  buyername   | 구매자명              | String    | "홍길동"                                    | 한글/특수기호 입력가능\* 30Byte 초과 요청시 27Byte+…으로 자동 변환 | Yes        | 30 Byte       |
|   buyertel   | 구매자Mobile번호       | String    | "010-2000-1234"                          | 숫자와 "-"만 허용                              | Yes        | 20 Byte       |
|  buyeremail  | 구매자Email          | String    | "buyer@example.com"                      | 이메일 형식에 맞도록                              | No         | 60 Byte       |
| parentemail  | 보호자Email          | String    | "parent@example.com"                     | 14세 미만 필수                                |            | 60 Byte       |
|  timestamp   | 타임스탬프             | Number    | 1335233672723                            | TimeInMillis(Long형)<br>→ 제공라이브러로 생성가능(샘플소스참조) | Yes(위변조검증) | 20 Byte       |
|  signature   | signature         | String    | "8ca9e064777ea2fc0d4b79a5c891f3bdf30edd45c129dcfc226ba5e7e85cd5f3" | 위변조 방지 SHA256 Hash 값<br>[TABLE 1-3] signature 생성 대상(Target) 필드 참조 | Yes        | 64 ByteFixed  |
|  returnUrl   | 리턴Url(인증결과수신Url)  | String    | "HTTPS://www.exsample.com/INIpayStandardSample/INIpayResult.jsp" | 결제창을 통해 인증완료된 결과를 수신받고 승인요청을 해서 결과를 표시할 페이지 URL→ 3.3 리턴 페이지(인증수신/승인API) 작성(PayReturn) 참조 | Yes        | N/A           |
|     mKey     | signkey에 대한 hash값 | String    | "3a9503069192f207491d4b19bd743fc249a761ed94246c8c42fed06c3cd15a33" | signkey에 대한 검증값                          | Yes        | N/A           |
| gopaymethod  | 요청결제수단표시          | String    | "Card"<br>별첨 "A.2 gopaymethod 옵션" 참조     | 결제 수단 중 선택적 표시<br>옵션생략시 전체 결제 수단 표시      | No         | N/A           |
| offerPeriod  | 제공기간              | String    | "20130101-20130331"<br>[Y2:년단위결제, M2:월단위결제, yyyyMMdd-yyyyMMdd : 시작일-종료일] | 가맹점에서 판매상품에 대한 제공기한 설정                   | No         | N/A           |
| languageView | 초기 표시 언어          | String    | "ko"<br>[ko:한국어, en:영어]                  | 결제창 표시 언어<br>PC는 결제창내 언어변경 버튼 존재         | No         | 2Byte         |
|   charset    | 결과 인코딩            | String    | "UTF-8" / [`UTF-8`, EUC-KR]              | 결과 수신 charset                            | No         | 5Byte         |
| payViewType  | 결제창 표시방법          | String    | [overlay]                                | Default:overlay                          | No         | N/A           |
|   closeUrl   | 결제창 닫기처리Url       | String    | "HTTPS://www.exsample.com/inipaysmart/close.jsp" | close.jsp 샘플사용(소스 수정 불필요)                | Yes        | N/A           |
|   popupUrl   | 팝업처리Url           | String    | "HTTPS://www.exsample.com/inipaysmart/popup.jsp" | popup.jsp 샘플사용(소스 수정 불필요 : 비권장)          | Yes        | N/A           |
| merchantData | 가맹점데이터            | String    | "a=A&b=B"                                | 인증 성공시 가맹점으로 리턴                          | No         | 2000Byte      |
| acceptmethod | acceptmethod      | String    | CARDPOINT:va_receipt:vbank(20150425):SKIN(ORIGINAL):FONT(ORIGINAL): poptargetself | 결제수단별 추가 옵션값                             | No         | N/A           |



#### [TABLE 1-2] acceptmethod 공통 추가 옵션
|     필드명      | 한글명칭        | Data Type | 예시            | 설명                                       | 필수여부 |
| :----------: | ----------- | --------- | ------------- | ---------------------------------------- | ---- |
| acceptmethod | 배경색상        | String    | SKIN(BLUE)    | 결제창의 배경 색상을 변경 / 색상표 값으로 설정 가능(미 설정 시 기본값 : #c1272c) | NO   |
|      "       | 인증 결과 처리 방식 | String    | poptargetself | 인증완료 후 returnUrl 호출 시 타켓을 self로 변경 결제창 내에서 페이지 전환 옵션(미 설정 시 기본값 : top) | NO   |
|      "       | 에스크로결제여부    | String    | useescrow     | 설정시"에스크로약관동의"와"구매자본인확인"페이지가포함된에스크로결제창을호출합니다.(미설정시일반거래,에스크로사용설정된가맹점만사용가능합니다.) | NO   |

- 기본 요청데이터의 signature필드의 구성은 다음과 같습니다.
#### [TABLE 1-3] signature 생성 대상(Target) 필드
| 필드명       | 한글명칭  | 예시                                       | 비고                                       | **필수여부** |
| --------- | :---: | ---------------------------------------- | ---------------------------------------- | -------- |
| mKey      |  검증값  | 346eaecb81e3a1629805b9d55fe0431dc25a06aaa2d48366b404939a3d4330a3 | SHA256방식으로 생성한 값<br>\* 제공라이브러리로 생성가능     | Yes      |
| oid       | 주문번호  | welcometst_1335247243103                 |                                          | Yes      |
| price     |  가격   | 10000                                    | 가맹점 주문번호 / 결제단위 Unique                   | Yes      |
| timestamp | 타임스탬프 | 1335247243103                            | TimeInMillis(Long)밀리세컨드 타임스템프를 Long형으로 변환한 숫자<br>제공라이브러리로 생성가능 | Yes      |
- Signature 생성방법은 아래의 [3.3 signature 생성] 참조
  기본 요청데이터 외에 다음과 같이 결제 수단별로 옵션 값을 추가하여 결제 요청할 수 있습니다.

#### [TABLE 1-4] 신용카드 추가 요청필드 (선택)
|     필드명      |       하위필드       | 한글명칭            | Data Type | 예시, **`기본값`**                            | 설명                                       |
| :----------: | :--------------: | --------------- | :-------: | :--------------------------------------- | ---------------------------------------- |
|  quotabase   |                  | 할부 개월           |  String   | "2:3:4", "2:0"<br>* 개월수를 `:` 로 구분된 값     | 일시불은 기본적으로 표시, 생략시 일시불만<br>현대카드 1만원,그 외 5만원 이상시에만 동작 |
|  nointerest  |                  | 가맹점 부담 무이자 할부설정 |  String   | "11-2:3:5:6,34-2:6", "04-2:6"<br>* 카드사코드-할부개월:할부개월…<br>여러카드는 공백없이 `,`로 구분 | \* 5만원 이상시에만 동작 / 카드사 무이자와 무관<br>[→ 별첨 "A.4카드사코드" 참조] |
| acceptmethod |    below1000     | 1000원이하 결제      |  String   | " below1000"                             | 기본적으로 1000원이하 결제 불가능                     |
|      "       | ini_onlycardcode | 결제 카드사 선택       |  String   | "01:03:04:06"\* 카드사코드를 ":"로 구분된 값        | 생략 시 결제 가능한 모든 카드사 표시<br>[→ 별첨"A.4카드사코드"참조] |
|      "       | onlyeasypaycode  | 결제 간편결제 선택      |  String   | "kakaopay:lpay:payco"\* 간편결제코드를 ":"로 구분된 값 | 생략 시 결제 가능한 모든 간편결제 표시<br>[→ 별첨 "A.7 신용카드 간편결제코드" 참조] |
|      "       |    CARDPOINT     | 카드포인트 사용유무      |  String   | "cardpoint"                              | 포인트를 사용하는 카드를 선택시 신용카드 메인 화면에 카드포인트를 사용할지에 대한 선택창이 표시된다. |
|      "       |    SLIMQUOTA     | 부분무이자설정         |  String   | "SLIMQUOTA (11-2:3^34-2:3)"              | 슬림할부를 지정한다.<br>SLIMQUOTA(코드-개월:개월) 로 사용한다.<br>`^`구분자로 카드코드를 구분한다. |
|      "       |     PAYPOPUP     | 안심클릭 뷰옵션        |  String   | "PAYPOPUP"                               | 안심클릭을 Popup 형태로 서비스를 제공한다.<br>Edge의 경우 자동 설정됩니다. |
|      "       |     hidebar      | 프로그래스바뷰옵션       |  String   | "hidebar"                                | 결제진행시 노출되는 프로그래스 바를 안보이도록 설정된다.          |

### [TABLE 1-5] 휴대폰결제 추가 요청필드 (선택)
|     필드명      |      하위필드      |      한글명칭      | Data Type | 예시, **`기본값`**                       | 설명                                       |
| :----------: | :------------: | :------------: | --------- | ----------------------------------- | ---------------------------------------- |
| acceptmethod |      HPP       |  휴대폰 결제 상품 유형  | String    | "HPP(1)"[1:컨텐츠,2:실물,4:빌링컨텐츠,5:빌링실물] | 휴대폰 결제 상품 유형<br>컨텐츠/실물/빌링컨텐츠/빌링실물여부는 계약담당자에게 확인요 |
|      "       |  hppablecorp   |  표시될 통신사 리스트   | String    | "hppablecorp(SKT:KTF:LGT:MVNO)"     | SKT : S텔레콤, KTF : KT, LGT : LG U+, MVNO : 알뜰폰<br>MVNO중일부만 설정 시 MVNO 제외 후 CJH(헬로모바일),KCT(티플러스),SKL(SK7mobile) 중 일부만 선택 |
|      "       | hppdefaultcorp |   휴대폰통신사기본선택   | String    | "hppdefaultcorp(SKT)"               | 통신사 리스트에서 입력 통신사가 기본 선택 되어짐<br>SKT, KTF, LGT, MVNO 중 하나만 설정 가능<br>MVNO 중 선택 시 CJH, KCT, SKL로 설정가능<br>미입력시나 공백으로 입력시 선택된 통신사 없음 |
|      "       |    hppnofix    | 휴대폰 번호 수정불가여부  | String    | hppnofix(N)                         | 휴대폰 번호 수정불가여부<br>N : 수정가능, Y : 수정불가능     |
|      "       |  hppauthtype   | 휴대폰 결제 인증방법 선택 | String    | hppauthtype(ARS)                    | 휴대폰 결제시 문자/ARS 인증 선택(옵션없을시 SMS)<br>ARS : ARS인증, SMS : 문자인증(해당 옵션은 모빌리언스만 가능) |
|      "       |    billauth    |   휴대폰 빌키 발급    | String    | billauth(HPP)                       | 휴대폰 빌키 발급시 사용상품유형 HPP(4) 또는 HPP(5)로 설정 필요<br>휴대폰 빌링 사용은 별도 사용 설정 필요 |

### [TABLE 1-6] 계좌이체 추가 요청필드 (선택)
| 필드명          | 하위필드       | 한글명칭      | Data Type | 예시, **`기본값`** | 설명                                       |
| ------------ | ---------- | --------- | --------- | ------------- | ---------------------------------------- |
| acceptmethod | no_receipt | 현금영수증 미발행 | String    | "no\_receipt" | 현금영수증 발행 차단 옵션<br>계좌이체 시 사용하는 현금영수증 미발행 여부 확인 필드 – 옵션을 사용시 현금 영수증 UI 출력하지 않음 |

### [TABLE 1-7] 가상계좌 추가 요청필드 (선택)
| 필드명          | 하위필드        | 한글명칭                  | Data Type | 예시, **`기본값`**         | 설명                                       |
| ------------ | ----------- | --------------------- | --------- | --------------------- | ---------------------------------------- |
| INIregno     |             | 주민번호 설정 기능            | String    | "201504161111111"     | 13자리(주민번호),10자리(사업자번호),미입력시(화면에서입력가능)    |
| acceptmethod | vbank       | 입금기한 및 입금시간 (초 설정 불가) | String    | "vbank(20150416)&#39; | 입금기한 및 입금 시간 설정 옵션<br> EX) vbank(20211216) 또는 vbank(202112261900) 시분까지지정 |
| "            | va\_receipt | 현금영수증 발급 UI 옵션        | String    | "va\_receipt"         | 현금영수증 발급 UI 표시 옵션<br> (CASHRECEIPT 옵션이 기준정보에 있는 경우)<br>–주민번호만 표시 |
| "            | va\_ckprice | 주민번호 채번 시 금액 확인       | String    | "va\_ckprice"         | 주민번호 채번시 금액 체크 기능                        |
