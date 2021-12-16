---
title: PAYAPI
permalink: payapi01.html
sidebar: payapi_sidebar
folder: payapi
toc: false
---
# 1. PayAPI서비스

PayAPI는 HTTPS 요청으로 활용할 수 있는 다양한 서비스를 제공하고 있으며, 본 문서는 PayAPI에서 지원하는 각각의 서비스들에 대한 기능별 상세 설명을 포함하고 있습니다.

## 1.1상점 연동시 주의사항

해킹시도 및 불법접속 차단 등의 보안을 위해 해외에서 접속 시에는 당사 서비스가 제한이 되며, 해외IP 차단해제를 위해서는 [ip-block@welcomepayments.co.kr](mailto:ip-block@welcomepayments.co.kr)로 아래 내용 작성해서 요청 주시기 바랍니다 .

| 업체명(MID)       | 접속 국가 | 접속 공인IP(대역) | 요청사항                 |
| ----------------- | --------- | ----------------- | ------------------------ |
| xxxxx(welcometst) | 중국      | 111.111.111.111   | 해외아이피 차단해제 요청 |

## 1.2 PayAPI 서비스 흐름도



# 2. PayAPI Hash검증 처리

PayAPI 서비스에서는 가맹점 주문정보 대한 위/변조 방지를 위해 일부 주요 데이터에 한해서 암호화 처리하고 있습니다. 서비스 별로 암호화 처리 필드 구성이 다르므로 해당 서비스의 상세 내용을 참고하시기 바랍니다.

## 2.1 기본 Hash검증 구성도

