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

| 업체명(MID)     | 접속 국가 | 접속 공인IP(대역) | 요청사항                 |
|--------------| --------- | ----------------- | ------------------------ |
| xxxxx(xxxxx) | 중국      | 111.111.111.111   | 해외아이피 차단해제 요청 |

## 1.2 PayAPI 서비스 흐름도

{% include image.html file="payapi_img01.png" %}

## 1.3 PayAPI 개요

PayAPI는 다음과 같은 사항을 기본으로 합니다.

#### 1) 공통 HTTPS 통신 규약
- 프로토콜 : HTTPS
- 포트번호 : 443
- HTTP Method : POST
- CHARSET : UTF-8

#### 2) 공통 HTTPS Request Header

- Content-Type: application/x-www-form-urlencoded; charset=utf-8

#### 3) 공통 HTTPS Request Body

- 서비스 별로 요청 파라미터가 상이하므로 자세한 내용은 각 서비스의 요청 파라미터를 참고하시기 바랍니다.

#### 4) 공통 HTTPS Response Header

- Content-Type: application/json; charset=utf-8

#### 5) 공통 HTTPS Response Body

- 응답 결과값을 JSON 형식으로 반환합니다.
- 응답 결과값은 서비스 별 응답 파라미터 내용을 참고하시기 바랍니다.

#### 6) PAYAPI 응답코드

PAYAPI의 주요 응답 코드는 아래와 같습니다.

<table class="tg" style="width: 100%">
  <colgroup>
    <col style="width: 20%">
    <col style="width: 20%">
    <col style="width: 20%">
    <col style="width: 40%">
  </colgroup>
  <thead>
    <tr>
      <th class="tg-0lax">PG 응답코드</th>
      <th class="tg-0lax">HTTP 상태 코드</th>
      <th class="tg-0lax">메시지</th>
      <th class="tg-0lax">설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="tg-0lax">00</td>
      <td class="tg-0lax">200</td>
      <td class="tg-0lax">정상</td>
      <td class="tg-0lax">처리 완료</td>
    </tr>
    <tr>
      <td class="tg-0lax">그외</td>
      <td class="tg-0lax">200</td>
      <td class="tg-0lax">실패</td>
      <td class="tg-0lax">처리 실패</td>
    </tr>
    <tr>
      <td class="tg-0lax">-</td>
      <td class="tg-0lax">4XX</td>
      <td class="tg-0lax">잘못된 요청</td>
      <td class="tg-0lax">API 요청 URL의 프로토콜, 파라미터 등에<br>오류가 있는지 확인합니다.</td>
    </tr>
    <tr>
      <td class="tg-0lax">-</td>
      <td class="tg-0lax">5XX</td>
      <td class="tg-0lax">서버 내부 오류</td>
      <td class="tg-0lax">서버 내부에 오류가 발생했습니다<br>관리자에게 문의하세요.</td>
    </tr>
  </tbody>
</table>