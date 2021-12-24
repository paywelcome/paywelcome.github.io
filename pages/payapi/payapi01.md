---
title: PAYAPI 서비스
permalink: payapi01.html
sidebar: payapi_sidebar
folder: payapi
toc: false
---

<div style="display: inline-block; width: 100%;">
  <a style="float:right;" href="/payapi02.html">다음페이지▶</a>
</div>

# 1. PAYAPI서비스

>PAYAPI는 HTTPS 요청으로 활용할 수 있는 다양한 서비스를 제공하고 있으며, 본 문서는 PAYAPI에서 지원하는 각각의 서비스들에 대한 기능별 상세 설명을 포함하고 있습니다.

## 1.1 PAYAPI 서비스 흐름도

{% include image.html file="payapi_img01.png" %}

## 1.2 PAYAPI 개요

>PAYAPI는 다음과 같은 사항을 기본으로 합니다.

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

#### 6) PAYAPI 요청시 Signature생성 

<p style="color: red;"><strong>Signature 생성 방식에 따라서는 <a href="/prepare01.html#12-signature-개요">연동 준비하기 - 1.2 Signature</a>를 참고 바랍니다.</strong></p>

#### 7) PAYAPI 응답코드

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
      <th class="tg-01ax">PG 응답코드</th>
      <th class="tg-01ax">HTTP 상태 코드</th>
      <th class="tg-01ax">메시지</th>
      <th class="tg-02ax">설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="center-align">00</td>
      <td class="center-align">200</td>
      <td class="center-align">정상</td>
      <td class="left-align">처리 완료</td>
    </tr>
    <tr>
      <td class="center-align" rowspan="3" style="text-align :center;vertical-align: middle">그외</td>
      <td class="center-align">200</td>
      <td class="center-align">실패</td>
      <td class="left-align">처리 실패</td>
    </tr>
    <tr>
      <td class="center-align">4XX</td>
      <td class="center-align">잘못된 요청</td>
      <td class="left-align">API 요청 URL의 프로토콜, 파라미터 등에 오류가 있는지 확인합니다.</td>
    </tr>
    <tr>
      <td class="center-align" style="text-align: center; vertical-align: middle">5XX</td>
      <td class="center-align" style="text-align: center;">서버 내부 오류</td>
      <td class="left-align">서버 내부에 오류가 발생했습니다.<br>관리자에게 문의하세요.</td>
    </tr>
  </tbody>
</table>


## 1.3 개인정보 암호화(필드 암호화)

>고객들의 개인정보보호를 위해 주문정보 중 특정 필드에 한하여 AES256, CBC, 5 Padding으로 암호화 처리합니다. 빌링 정보에 관한 암호화 시 aes256 iv, key는 암호화 여부에 따른 암호화 키 값이며 하기 표를 참조 바랍니다.
또한 대상 필드는 서비스 별로 다르므로 상세한 내용은 해당 서비스의 요청 필드를 참고하시기 바랍니다.
`Test mid와 iv,key값은 계약가맹점에 한해 별도 전달 예정입니다.`

- 암호화 정보 예시
<table>
<tbody>
  <tr>
    <td class="center-align">mid</td>
    <td class="center-align" rowspan="3"><a href="mailto:mainpg_support@welcomepayments.co.kr">메일로 문의하기(support@welcomepayments.co.kr)</a></td>
  </tr>
  <tr>
    <td class="center-align">api iv</td>
  </tr>
    <tr>
    <td class="center-align">api key</td>
  </tr>
</tbody>
</table>

- 암호화 처리 예시
- 'test' 기입 후 처리 값 예시
<table>
<tbody>
  <tr>
    <td class="center-align">test</td>
    <td class="center-align">oijMQxRyQIcHc1qJ+Um2DA==</td>
  </tr>
</tbody>
</table>


- 암호화 처리 이후 문자들에는 `+` 등의 기호가 들어가므로 url encoding 을 하지 않으면 url decoding 시에 공백등으로 변환되므로 요청시에 url encoding 처리를 하신후 보내주셔야 데이터 전달이 정상적으로 됩니다.

<div style="display: inline-block; width: 100%; margin-top: 50px;">
  <a style="float:right;" href="/payapi02.html">다음페이지▶</a>
</div>