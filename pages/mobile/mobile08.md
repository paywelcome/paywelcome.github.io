---
title: MOBILE
permalink: mobile08.html
sidebar: mobile_sidebar
folder: mobile
toc: false
---

# 8. 계좌이체 연동 유의사항 안내

## 8.1 계좌이체 연동시 유의사항

- 맹점 안드로이드/IOS 앱에서 계좌이체를 연동하시는 경우 아래의 앱스키마 정보에 대해 가맹점앱에서 처리 가능하도록 구현되어 있어야 하며,<br>OS별 상세 처리는 아래를 참고바랍니다.

<table style="width: 100%;">
<colgroup>
  <col style="width: 30%">
  <col style="width: 70%">
</colgroup>
  <thead>
    <tr>
      <th style="text-align: center">App</th>
      <th>custom scheme</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">뱅크페이<br>(  기본 )</td>
      <td><code class="language-plaintext highlighter-rouge">kftc-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">뱅크윌렛</td>
      <td><code class="language-plaintext highlighter-rouge">bankwallet://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">케이뱅크 페이</td>
      <td><code class="language-plaintext highlighter-rouge">ukbanksmartbanknonloginpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">산업</td>
      <td><code class="language-plaintext highlighter-rouge">kdb-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">기업</td>
      <td><code class="language-plaintext highlighter-rouge">ibk-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">국민</td>
      <td><code class="language-plaintext highlighter-rouge">kb-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">KEB 하나</td>
      <td><code class="language-plaintext highlighter-rouge">keb-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">수협</td>
      <td><code class="language-plaintext highlighter-rouge">sh-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">NH 농협</td>
      <td><code class="language-plaintext highlighter-rouge">nhb-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">농축협</td>
      <td><code class="language-plaintext highlighter-rouge">nh-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">우리</td>
      <td><code class="language-plaintext highlighter-rouge">wr-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">SC</td>
      <td><code class="language-plaintext highlighter-rouge">sc-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">신한</td>
      <td><code class="language-plaintext highlighter-rouge">s-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">씨티</td>
      <td><code class="language-plaintext highlighter-rouge">ct-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">대구</td>
      <td><code class="language-plaintext highlighter-rouge">dg-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">부산</td>
      <td><code class="language-plaintext highlighter-rouge">bnk-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">광주</td>
      <td><code class="language-plaintext highlighter-rouge">kj-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">제주</td>
      <td><code class="language-plaintext highlighter-rouge">jj-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">전북</td>
      <td><code class="language-plaintext highlighter-rouge">jb-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">경남</td>
      <td><code class="language-plaintext highlighter-rouge">kn-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">우정사업본부</td>
      <td><code class="language-plaintext highlighter-rouge">kp-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">신협</td>
      <td><code class="language-plaintext highlighter-rouge">cu-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">새마을</td>
      <td><code class="language-plaintext highlighter-rouge">mg-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">K 뱅크</td>
      <td><code class="language-plaintext highlighter-rouge">kbn-bankpay://</code></td>
    </tr>
    <tr>
      <td style="text-align: center">카카오뱅크</td>
      <td><code class="language-plaintext highlighter-rouge">kkb-bankpay://</code></td>
    </tr>
  </tbody>
</table>

## 8.2 안드로이드 연동 시 유의사항

- 계좌이체 결제 스키마 정보는 기본적으로 intent스키마가 아닌 URL 스키마로 호출됩니다. 가맹점에서는 특정 스키마에 대해서만 허용되도록 개발되어 있는 경우라면 위 명시되어 있는 URL스키마가 호출되는 경우에도 앱이 정상적으로 호출될 수 있도록 처리해 주셔야 합니다.<br>
  각각의 처리가 어려워 intent스키마로 연동이 필요하신 경우 아래 옵션을 통해 각 스키마 정보에 대해 intent 스키마로 처리가 가능합니다.

- 안드로이드 계좌이체  intent 스키마 호출 옵션정보

<table style="width: 100%;">
<colgroup>
  <col style="width: 50%;">
  <col style="width: 50%;">
</colgroup>
  <thead>
    <tr>
      <th style="text-align: center">필드명</th>
      <th style="text-align: center">값</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">P_RESERVED</td>
      <td style="text-align: center">apprun_check=Y</td>
    </tr>
  </tbody>
</table>

## 8.3 IOS 연동 시 유의사항

IOS 가맹점 앱에서 계좌이체 앱 실행을 위해서는 위의 스키마정보가 info.plist 파일에 White List로 등록되어 있어야합니다.<br>
해당 스키마 설정 추가와 관련하여 상세 내용은 이전 장에서 안내된 가이드를 참고바랍니다.

## 8.4 계좌이체 연동 시 권장 옵션

앱 및 웹 환경의 사용자 페이지의 자연스러운 전환을 위해 모바일 계좌이체 결제 진행 시 아래 옵션추가를 권장합니다.

<table style="width: 100%;">
<colgroup>
  <col style="width: 30%;">
  <col style="width: 70%;">
</colgroup>
  <thead>
    <tr>
      <th style="text-align: center">환경</th>
      <th>필드 및 옵션</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">안드로이드 웹/앱, 아이폰 웹</td>
      <td><code class="language-plaintext highlighter-rouge">P_RESERVED=twotrs_bank=Y&amp;apprun_check=Y</code></td>
    </tr>
    <tr>
      <td style="text-align: center">아이폰 앱</td>
      <td>
<code class="language-plaintext highlighter-rouge">P_RESERVED=twotrs_bank=Y&amp;iosapp=Y&amp;app_scheme={가맹점앱스키마}://</code><br><code class="language-plaintext highlighter-rouge">P_RETURN_URL={가맹점앱스키마}://</code>
</td>
    </tr>
  </tbody>
</table>

