---
title: PC(웹표준)결제
permalink: stdweb02.html
sidebar: stdweb_sidebar
folder: stdweb
toc: false
---

# 2. 설치
## 2.1 설치 가능한 운영체제
- Java, php, asp.net등 HTTPS 통신이 가능한 웹서버 환경의 모든 운영체제에서 사용이 가능합니다.
  다만, 개인용 PC에서는 운영을 권장하지 않습니다.

## 2.2 소프트웨어 요구사항
**Web Server**
웹서버 (또는 웹 컨테이너)
- SHA256 Hash값의 생성 httpClient(http Background) 통신이 가능한 웹서버

**DBMS**
- 거래내역 및 처리결과를 데이터베이스에 저장하길 원하신다면, 데이터베이스 소프트웨어가 별도로 필요합니다.
- Web Standard서비스는 데이터베이스 연동 작업을 위한 기능이 포함되어 있지 않습니다.(데이터베이스 연동을 위한 지불 결과 데이터만 제공)

## 2.3 하드웨어 요구사항
일반적인 서버 운영체제의 운용환경에 준하며, 특별한 하드웨어 요구사항은 없습니다.
## 2.4 방화벽 설정
- 이용 가맹점 서버 앞에 방화벽이 있는 경우 반드시 결제승인, 결제취소에 대한 통신이 가능하도록 방화벽 설정을 해야 합니다.
  
**결제 인증**

|              연결대상            | 프로토콜 | 포트번호 |       연결방향        |
| :-----------------------------: | :------: | :-----: | :---------------: |
| https://stdpay.paywelcome.co.kr |   HTTPS  |    443  | INBOUND, OUTBOUND |

**결제승인**

|              연결대상               | 프로토콜  | 포트번호 |       연결방향        |
| :-----------------------------: | :---: | :--: | :---------------: |
| https://stdpay.paywelcome.co.kr | HTTPS | 443  | INBOUND, OUTBOUND |


## 2.5 샘플소스
- 샘플소스는 가맹점의 환경에 맞도록 수정하여 사용할 수 있습니다.
- Web Standard서비스는 표준 웹 통신만을 사용합니다.
- 결제요청시에는 페이지이동(Form POST Action), API통신시에는 httpClient 통신을 이용합니다.
> -POST Action Content-Type : application/x-www-form-urlencoded; charset=UTF-8
> -HTTPS API Request(httpClient 통신) = httpClient 등의 http Background 통신이 가능한 유틸을 통해서 웹페이지를 요청후 그 결과를 수신

- 본 샘플소스에는 통신에 대한 별도의 로그(Log) 기능이 존재하지 않습니다.
- 가맹점에서 환경에 맞게 로그를 개발하시기 바랍니다.

#### 주요 연동 파일 설명 

|         파일명          | 설명                                 |
| :------------------: | ---------------------------------- |
| INIStdPayRequest.xxx | 결제요청 샘플페이지                         |
|      popup.xxx       | 결제창을 팝업으로 표시할 때 사용 (권장하지 않음)       |
|      close.xxx       | 결제창(팝업,오버레이)을 닫을 때 사용 ( **수정금지** ) |
| WelStdPayReturn.xxx  | 결제 인증결과 수신 / 승인요청 API 연동 샘플페이지     |

### 2.5.1 Java         
- WelStdweb_JAVA.zip의 압축을 풀어 설치합니다. 이때 설치 절대 경로를 확인합니다.
- WelStdweb 결제 연동 프로그램은 다음과 같이 파일과 디렉터리가 생성됩니다.
- WenContent 이하 소스를 웹 Root 아래 넣고 이를 참고해 결제 모듈을 연동합니다.



> **Welpay0_Sample_v1.4.jar : 해당 라이브러리는 샘플페이지 구동을 위한 라이브러리로 참고만 부탁드리며, 실제 반영시엔 가맹점 환경에 맞게 직접 생성 부탁드립니다.**
> **샘플 라이브러리만을 이용하여 연동시, 가맹점 환경에 따른 오작동은 당사 확인이 어려울수 있습니다.**
**WelpayStdSample : HTML, JSP Sample 이 위치하는 폴더 입니다.**

### 2.5.2 ASP.net
- WelStdweb_ASP.zip의 압축을 풀어 설치합니다. 이때 설치 절대 경로를 확인합니다.
- WelStdweb 결제 연동 프로그램은 다음과 같이 파일과 디렉터리가 생성됩니다.
- INIcrypto.dll, INIpayNet.dll: 암복호화에 사용하는 dll 파일

### 2.5.3 ASP
- INIStdweb_ASP_Sample_v2.x.zip의 압축을 풀어 설치합니다. 이때 설치 절대 경로를 확인합니다.
- INIStdweb 결제 연동 프로그램은 다음과 같이 파일과 디렉터리가 생성됩니다.
- function 기본 제공 함수
- signature 위변조 방지체크 기능의 signature 생성

### 2.5.4 PHP
- libs : Welpay 암복호화 및 결제에서 사용하는 library 파일
- WelStdPaySample : HTML, PHP Sample이 위치하는 폴더입니다.

## 2.6 승인 테스트
1. 웹 브라우저에서 http://127.0.0.1/WelStdPaySample/WelStdPayRequest.xxx페이지를 호출합니다.
- Ie11의 경우 localhost로 진행할 경우 팝업창의 문제가 발생 할 수 있음
2. 승인 테스트를 위해 필수 값 및 기본 옵션 값을 매뉴얼을 참조 후 확인 후 결제 요청 버튼을 누릅니다.
3. 설치 과정 없이 지불 방법을 선택 후 필요한 정보를 기입하고 "확인"을 눌러 진행합니다. (해당 사이트 팝업을 사용으로 하지 않을 시 초기화면으로 로딩 될 수 있습니다. )
4. 지불 과정중 필요에 따라 추가적인 모듈을 다운로드 하는 경우도 있습니다. 정상적으로 지불결과 메시지가 나타나는지 확인하십시오.
5. 계좌이체(뱅크페이) 테스트서버에서테스트의경우지정된테스트정보로만테스트가능.
- 웹결제 > 간편결제(X), **일반결제 (O)**
- 테스트주민등록번호: <a href="mailto:mainpg_support@welcomepayments.co.kr">메일로 문의하기</a>
- **취소/조회 테스트를 위해 거래번호(TID)를 기록해 두십시오.**

## 2.7 상점 연동시 주의사항
1. 해킹 시도 및 불법접속 차단 등의 보안을 위해 해외에서 접속 시에는 당사 서비스가 제한이 되며, 해와 IP차단해제를 위해서는 [ip-block@welcomepayments.co.kr](mailto:ip-block@welcomepayments.co.kr)로 아래 내용 작성해서 요청 주시기 바랍니다.

| 업체명(MID)          | 접속 국가 | 접속 공인IP(대역)     | 요청사항          |
| ----------------- | ----- | --------------- | ------------- |
| xxxxx(welcometst) | 중국    | 111.111.111.111 | 해외아이피 차단해제 요청 |

2. 승인 테스트를 위해 필수 값 및 기본 옵션 값을 매뉴얼을 참조 후 확인 후 결제 요청 버튼을 누릅니다.
3. 설치 과정 없이 지불 방법을 선택 후 필요한 정보를 기입하고 "확인"을 눌러 진행합니다. (해당 사이트 팝업을 사용으로 하지 않을 시 초기화면으로 로딩 될 수 있습니다. )
4. 지불 과정중 필요에 따라 추가적인 모듈을 다운로드 하는 경우도 있습니다. 정상적으로 지불결과 메시지가 나타나는지 확인하십시오.
5. 계좌이체(뱅크페이) 테스트서버에서테스트의경우지정된테스트정보로만테스트가능.
- 웹결제 > 간편결제(X), **일반결제 (O)**
- 테스트주민등록번호:  <a href="mailto:mainpg_support@welcomepayments.co.kr">메일로 문의하기</a>
- **취소/조회 테스트를 위해 거래번호(TID)를 기록해 두십시오.**