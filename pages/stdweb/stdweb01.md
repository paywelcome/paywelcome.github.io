---
title: PC(웹표준)
permalink: stdweb01.html
sidebar: stdweb_sidebar
folder: stdweb
toc: false
keywords: 개요, PC, 특징, 웹, 연동
---

<div style="display: inline-block; width: 100%;">
  <a style="float:right;" href="/stdweb02.html">다음페이지▶</a>
</div>

# 1. 제품의 개요 및 특징 

## 1.1. 제품의 개요
>Web Standard서비스는 가맹점에서 별도의 모듈 설치(Non-ActiveX)가 없으며, 가상 키보드의 사용으로 기존 보안키보드 등 별도의 보안 프로그램 설치 없이 이용이 가능합니다. <br> 또한 SHA256 Hash를 통한 위변조 방지와 HTTPS(SSL) 통신을 이용하여 보안이 한층 더 강화된 전자지불 시스템 입니다.
>사용자의 PC (Windows, MAC (삼성, 롯데, 현대, NH, 신한)) 환경에 따라 자동으로 웹표준 결제창을 표시하며, 어떠한 브라우저(IE, Chrome, Firefox, Safari 등)에서도 추가적인 설치 없이 원스톱 사용이 가능한 전자 지불 솔루션 입니다.

## 1.2. 제품의 특징
>Web Standard서비스는 가맹점에서 시스템의 언어에 구애받지 않으며, 별도의 모듈 설치가 필요 없습니다. <br>
또한 SHA256 hash, form POST 액션, HTTPS 통신 만을 이용한 연동이 가능합니다. Any Browser, Any OS 환경에서 웰컴페이먼츠 결제 서비스를 이용할 수 있습니다.<br>
`현재 지원 OS : windows, MacOS (삼성, 롯데, 현대, NH, 신한), 추후 확대 예정, 지원브라우저 : IE, Chrome, Firefox, Safari.` <br>
>Web Standard서비스는 웰컴페이먼츠 내부시스템에는 웹 표준기술만을 사용하므로 자체 ActiveX 프로그램(플래쉬 포함)을 설치하지 않습니다. 하지만 현재 특정 결제수단(카드)은 인증기관(카드사, 은행 등)의 정책으로 인해 별도의 ActiveX 설치가 필요할 수 있습니다.<br>
>그러나 차후 원천사에서 웹 표준을 통한 연동 기술을 도입 시 가맹점에서는 새로운 모듈 연동의 필요하지 않으며, 일부 결제요청 전문의 수정만으로 웹표준 서비스를 제공받을 수 있습니다.

## 1.3. 지불수단
>Web Standard서비스는 결제의 약95%를 차지하는 지불수단을 지원합니다.<br>
- 신용카드 - 안심클릭, ISP, 비인증 신용카드
- 무통장 입금(가상계좌)
- 실시간 계좌이체
- 휴대폰 결제

### 신용카드

국내에서 발급된 모든 신용카드를 사용하실 수 있습니다.

<img class="emoji" title=":warning:" alt=":warning:" src="https://github.githubassets.com/images/icons/emoji/unicode/26a0.png"> <code class="language-plaintext highlighter-rouge">법인카드 및 직불형 신용카드는 할부이용이 불가합니다.</code>


### ISP(인터넷안전결제)

신용카드사에서 인증서를 발급받아 신용카드 번호를 입력하지 않고 본인확인만으로 결제하는 보다 안전한 결제방식입니다.<br>
  이용금액은 신용카드와 동일하게 청구됩니다.<br>

### 무통장입금(가상계좌)

고객이 인터넷 쇼핑몰에서 물품 대금의 결제 시 대금입금을 위한 은행계좌번호(예금주 웰컴페이먼츠)를 부여받은 후<br>
해당 가상계좌로 물품대금을 무통장 입금하거나 폰뱅킹, PC뱅킹 또는 인터넷뱅킹 등을 이용하여 온라인 입금하는 서비스입니다.<br>
(입금 통보는 별도의 수신데몬모듈 또는 수신 페이지를 사용합니다.)

### 휴대폰 결제
고객이 지정한 휴대폰으로 인증번호를 발송하여 인증번호를 받아 소액결제가 가능하도록 합니다.<br>
결제 청구는 휴대폰 요금에 합산되어 청구됩니다. (통신사마다 지정한 한도 금액이 정해 있음)

### 실시간 계좌이체
인터넷 뱅킹과 관련된 파일, 인증서 등이 설치된 PC에서 인터넷 뱅킹 시스템을 이용하여 계좌이체로 지불하는 방식이며,<br>
금결원에서 제공하는 인증창을 이용하며, 이용금액은 고객의 계좌에서 실시간으로 차감됩니다.

<img class="emoji" title=":warning:" alt=":warning:" src="https://github.githubassets.com/images/icons/emoji/unicode/26a0.png"> <code class="language-plaintext highlighter-rouge">인터넷 뱅킹에 가입한 사용자가 각 은행의 인터넷 뱅킹 이용 시간에만 이용할 수 있습니다.</code>

## 1.4 구조와 결제 처리 흐름
> Web Standard서비스는 다음과 작은 작업을 수행합니다.


### 1.4.1 결제요청
- 가맹점에서 SHA256 Hash를 이용하여 위변조 방지를 포함한 결제데이터를 생성합니다.
- 결제페이지에서 제공되는 스크립트를 Import한 후 결제요청 스크립트를 실행하면,
  스크립트에 의해서form 데이터를 Web Standard서비스로HTTPS(SSL) Post액션을 발생시켜 결제요청 데이터로 보냅니다.
- 웰컴페이먼츠는 결제요청을 받아 사용자의 디바이스에 따른 결제창을 표시하고 사용자가 결제(인증)를 진행할 수 있도록 합니다.
- 인증이 완료되면 인증결과 파라미터를 가맹점 결과페이지로 POST요청합니다.
- 수신한 인증결과에서 인증키(authToken)와 hash한 signature를 인증결과에 함께
  수신한 승인 API Url(authUrl)로 "HTTPS API request"를 통해서 승인 요청합니다.
- 리턴된 승인결과를 가맹점에 표시합니다.

<img src="../images/stdweb/img03.png">

<div style="display: inline-block; width: 100%; margin-top: 50px;">
  <a style="float:right;" href="/stdweb02.html">다음페이지▶</a>
</div>