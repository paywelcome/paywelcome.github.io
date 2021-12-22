---
title: PayAPI 서비스
permalink: payapi01.html
sidebar: payapi_sidebar
folder: payapi
toc: false
---

<div style="display: inline-block; width: 100%;">
  <a style="float:right;" href="/payapi02.html">다음페이지▶</a>
</div>

# 1. PayAPI서비스

PayAPI는 HTTPS 요청으로 활용할 수 있는 다양한 서비스를 제공하고 있으며, 본 문서는 PayAPI에서 지원하는 각각의 서비스들에 대한 기능별 상세 설명을 포함하고 있습니다.

## 1.1 PayAPI 서비스 흐름도

{% include image.html file="payapi_img01.png" %}

## 1.2 PayAPI 개요

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
    <col style="text-align: center; width: 20%">
    <col style="text-align: center; width: 20%">
    <col style="text-align: center; width: 20%">
    <col style="text-align: center; width: 40%">
  </colgroup>
  <thead>
    <tr>
      <th class="tg-0lax">PG 응답코드</th>
      <th class="tg-0lax">HTTP 상태 코드</th>
      <th class="tg-0lax">메시지</th>
      <th class="tg-02ax">설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="tg-0lax">00</td>
      <td class="tg-0lax">200</td>
      <td class="tg-0lax">정상</td>
      <td class="tg-01ax">처리 완료</td>
    </tr>
    <tr>
      <td class="tg-0lax" rowspan="3" style="text-align :center;vertical-align: middle">그외</td>
      <td class="tg-0lax">200</td>
      <td class="tg-0lax">실패</td>
      <td class="tg-0lax">처리 실패</td>
    </tr>
    <tr>
      <td class="tg-0lax" style="text-align: center; vertical-align: middle">4XX</td>
      <td class="tg-0lax" style="text-align: center;">잘못된 요청</td>
      <td class="tg-0lax">API 요청 URL의 프로토콜, 파라미터 등에 오류가 있는지 확인합니다.</td>
    </tr>
    <tr>
      <td class="tg-0lax" style="text-align: center; vertical-align: middle">5XX</td>
      <td class="tg-0lax" style="text-align: center;">서버 내부 오류</td>
      <td class="tg-0lax">서버 내부에 오류가 발생했습니다.<br>관리자에게 문의하세요.</td>
    </tr>
  </tbody>
</table>

<div style="display: inline-block; width: 100%;">
  <a style="float:right;" href="/payapi02.html">다음페이지▶</a>
</div>