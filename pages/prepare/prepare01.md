---
title: 연동 준비
permalink: prepare01.html
sidebar: prepare_sidebar
folder: prepare
toc: false
---

## 1.1 상점 연동시 주의사항

해킹시도 및 불법접속 차단 등의 보안을 위해 해외에서 접속 시에는 당사 서비스가 제한이 되며, 해외IP 차단해제를 위해서는 [ip-block@welcomepayments.co.kr](mailto:ip-block@welcomepayments.co.kr)로 아래 내용 작성해서 요청 주시기 바랍니다 .

| 업체명(MID)    | 접속 국가 | 접속 공인IP(대역) | 요청사항                 |
|-------------| --------- | ----------------- | ------------------------ |
| 계약가맹점 별도 전달 | 중국      | 111.111.111.111   | 해외아이피 차단해제 요청 |

## 1.2 signature 개요

{% include image.html file="pre_img01.png" %}

- 결제요청시 등 HTTPS post 요청시 가맹점의 요청이 정상적인 요청인지 여부 / 사용자의 위변조 방지를 위해 일부 데이터를 SHA256으로 Hash한 값

- signature는 form.submit 시 적용됩니다.signature생성은 Sample Source를 참고하여 작성하시기 바랍니다.

## 1.3 signature 첨부 대상
서비스 별로 Signature생성 방식이 상이하므로 아래의 표를 참고해주시기 바랍니다.<br/>

Signature생성에 필요한 mid와 signkey는 계약 가맹점에 한해 별도로 전달됩니다.

**※ Signature 필드 생성 순서 중요**

### Web Standard(PC) 서비스의 Signature 생성

#### 결제 인증요청(결제요청)시 PC의 Signature 생성

결제 인증(결제)요청시 signature필드의 구성은 다음과 같습니다.

생성 순서 : <code class="language-plaintext highlighter-rouge">mkey=&oid=&price=&timestamp=</code><br/>
<img class="emoji" title=":warning:" alt=":warning:" src="https://github.githubassets.com/images/icons/emoji/unicode/26a0.png"><code class="language-plaintext highlighter-rouge">필드 순서유지(알파벳순)</code>

<table>
  <thead>
    <tr>
      <th style="text-align: center; width: 15%">필드명</th>
      <th style="text-align: center; width: 10%">한글명칭</th>
      <th style="text-align: left; width: 65%">비고</th>
      <th style="text-align: center; width: 10%">필수여부</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">mKey</td>
      <td style="text-align: center">검증값</td>
      <td>SHA256방식으로 생성한 값 → 제공라이브러리로 생성가능
      <br><code class="language-plaintext highlighter-rouge">"346eaecb81e3a1629805b9d55fe0431dc25a06aaa2d48366b404939a3d4330a3"
      </code>
      </td>
      <td style="text-align: center">Yes</td>
    </tr>
    <tr>
      <td style="text-align: center">oid</td>
      <td style="text-align: center">주문번호</td>
      <td>xxx_1335247243103</td>
      <td style="text-align: center">Yes</td>
    </tr>
    <tr>
      <td style="text-align: center">price</td>
      <td style="text-align: center">가격</td>
      <td>가맹점 주문번호 / 결제단위 Unique <br>
      <code class="language-plaintext highlighter-rouge">"10000"</code>
      </td>
      <td style="text-align: center">Yes</td>
    </tr>
    <tr>
      <td style="text-align: center">timestamp</td>
      <td style="text-align: center">타임스탬프</td>
      <td>TimeInMillis(Long형) → 제공라이브러리로 생성가능(샘플소스참조)<br><code class="language-plaintext highlighter-rouge">1335233672723</code></td>
      <td style="text-align: center">Yes</td>
    </tr>
  </tbody>
</table>

##### Target 데이터 예시 : `mKey=346eaecb81e3a1629805b9d55f...&oid=xxx_1335247243103&price=1000&timestamp=2020110222`

<br/>

#### 결제 승인요청시 PC의 Signature 생성

결제 승인시 요청데이터의 signature필드의 구성은 다음과 같습니다.

생성 순서 : <code class="language-plaintext highlighter-rouge">authToken=&timestamp=</code><br/>
<img class="emoji" title=":warning:" alt=":warning:" src="https://github.githubassets.com/images/icons/emoji/unicode/26a0.png"><code class="language-plaintext highlighter-rouge">필드 순서유지(알파벳순)</code>

<table>
  <thead>
    <tr>
      <th style="text-align:center; width: 15%">필드명</th>
      <th style="text-align:center; width: 20%">한글명칭</th>
      <th style="text-align:left; width: 55%">비고</th>
      <th style="text-align:center; width: 10%">필수 여부</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">authToken</td>
      <td style="text-align: left">인증 결과 수신 후 생성된 토큰 값</td>
      <td>인증결과 수신한 authToken<br>sgnWSY9uZ3c9lbkJItgiP4VdD5L+dM0+dmuv+R707vExQC5XjwjSCUOa/QumiTMW Y8+aLvjFu …….</td>
      <td style="text-align: center">Yes</td>
    </tr>
    <tr>
      <td style="text-align: center">timestamp</td>
      <td style="text-align: left">타임스탬프</td>
      <td>TimeInMillis(Long)밀리세컨드 타임스템프를 Long형으로 변환한 숫자<br>제공라이브러리로 생성가능<br>1335247243103</td>
      <td style="text-align: center">Yes</td>
    </tr>
  </tbody>
</table>

##### Target 데이터 예시 : `authToken=sgnWSY9uZ3c9lbkJItgiP4VdD5L+dM0+dmuv+R707vExQC5XjwjSCUOa/iT……&timestamp=2020110222`

#### Signature 생성방법은 아래의 [3.3 signature 생성] 참조
>Web Standard 서비스의 모든 요청<br/>
>결제(인증), 승인APIsignature 생성 대상 필드(Target) 모든 요청의 signature의 생성방법 동일하며, 요청별로 생성 대상 필드가 다름<br/>
>요청별로 명시된 signature 생성 대상(Target)필드 를 참조<br/>
>인증요청(결제요청) : oid,price,timestamp<br/>
>승인요청 : authToken, timestamp<br/>

[//]: # (          <a href="/stdweb03.html#table-1-3-signature-생성-대상target-필드">[TABLE 1-3] signature 생성 대상&#40;Target&#41; 필드 참조]</a><br/>)
[//]: # (          <a href="/stdweb03.html#table-2-3-승인요청-signature-생성-대상target-필드">[TABLE 2-3] 승인요청 signature 생성 대상&#40;Target&#41; 필드 참조]</a></td>)

### MOBILE 서비스의 Signature 생성

생성 순서 : <code class="language-plaintext highlighter-rouge">mkey=&P_AMT=&P_OID=&P_TIMESTAMP=</code><br/>
필드 순서유지(명시된순으로)

<table style="width: 100%;">
<colgroup>
  <col style="width: 10%;">
  <col style="width: 20%;">
  <col style="width: 30%;">
  <col style="width: 30%;">
  <col style="width: 10%;">
</colgroup>
  <thead>
    <tr>
      <th>순번</th>
      <th>필드명</th>
      <th>승인필드명</th>
      <th>설명</th>
      <th>필수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>mkey</td>
      <td></td>
      <td>sha256(signkey)<br/>(signkey값은 계약가맹점에 한해 별도 전달 예정)</td>
      <td>필수</td>
    </tr>
    <tr>
      <td>2</td>
      <td>P_AMT</td>
      <td>P_AMT(금액)</td>
      <td>가맹점 주문번호/결제단위 Unique</td>
      <td>필수</td>
    </tr>
    <tr>
      <td>3</td>
      <td>P_OID</td>
      <td>P_OID(주문번호)</td>
      <td>주문단위 unique한 값</td>
      <td>필수</td>
    </tr>
    <tr>
      <td>4</td>
      <td>P_TIMESTAMP</td>
      <td>P_TIMESTAMP(타임스탬프)</td>
      <td>TimeInMillis(Long형)</td>
      <td>필수</td>
    </tr>
  </tbody>
</table>

##### Target 데이터 예시 : `mkey=346eaecb81e3a1629805b9d55f...&P_AMT=1000&P_OID=xxx_1335247243103&P_TIMESTAMP=2020110222`

### PAYAPI 서비스의 Signature 생성

필드 순서유지(API별로 명시된 순으로)

<table style="width: 100%;">
<colgroup>
  <col style="width: 10%;">
  <col style="width: 35%;">
  <col style="width: 55%;">
</colgroup>
  <thead>
    <tr>
      <th>순번</th>
      <th>API명</th>
      <th>Signature 생성 필드</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>결제 전체 취소 API</td>
      <td>mid+mkey+timestamp</td>
    </tr>
    <tr>
      <td>2</td>
      <td>결제 부분 취소 API</td>
      <td>mid+mkey+timestamp</td>
    </tr>
    <tr>
      <td>3</td>
      <td>신용카드 빌키 발급 API</td>
      <td>mid+mkey+cardNumber+timestamp</td>
    </tr>
    <tr>
      <td>4</td>
      <td>신용카드 비인증 빌키 발급 API</td>
      <td>mid+mkey+cardNumber+timestamp</td>
    </tr>
    <tr>
      <td>5</td>
      <td>신용카드 빌링 승인 API</td>
      <td>mid+mkey+oid+price+timestamp</td>
    </tr>
    <tr>
      <td>6</td>
      <td>신용카드 빌키 삭제 API</td>
      <td>mid+mkey+timestamp</td>
    </tr>
    <tr>
      <td>7</td>
      <td>휴대폰 빌키 승인 API</td>
      <td>mid+mkey+oid+price+timestamp</td>
    </tr>
    <tr>
      <td>8</td>
      <td>신용카드 키인결제 API</td>
      <td>mid+mkey+oid+price+timestamp</td>
    </tr>
    <tr>
      <td>9</td>
      <td>신용카드 PREFIX 조회 API</td>
      <td>mid+mkey+cardNumber+timestamp</td>
    </tr>
    <tr>
      <td>10</td>
      <td>에스크로 배송등록 API</td>
      <td>mid+mkey+timestamp</td>
    </tr>
    <tr>
      <td>11</td>
      <td>에스크로 구매확정 API</td>
      <td>mid+mkey+timestamp</td>
    </tr>
    <tr>
      <td>12</td>
      <td>에스크로 구매거절 API</td>
      <td>mid+mkey+timestamp</td>
    </tr>
    <tr>
      <td>13</td>
      <td>에스크로 구매거절 확인 API</td>
      <td>mid+mkey+timestamp</td>
    </tr>
    <tr>
      <td>14</td>
      <td>에스크로 상태조회 API</td>
      <td>mid+mkey+timestamp</td>
    </tr>
    <tr>
      <td>15</td>
      <td>SMS결제용 단축 URL생성 API</td>
      <td>mid+mkey+P_OID+P_AMT+timestamp</td>
    </tr>
  </tbody>
</table>
<strong>※자세한 필드는 각 API명세서를 참고 바랍니다.</strong>

## 1.4 signature 생성 방법
- 위변조 방지를 위한 보안조치로서 필수 체크 데이터를 NVP 방식으로 연결한 데이터를SHA256으로 Hash한 값
- NVP : nameandvalue parameters
  ex) name=value&amp;name=value&amp;name=value&amp;name=value
- 필드 순서유지(알파벳순), 마지막 &amp;는 생략, 공백생략, 모든대상 필드는 Form에 설정되는 데이터와 동일한 값을 이용

## 1.5 signature 생성 샘플(결제요청)
- 언어별 제공된 라이브러리 소스를 통해서 생성가능합니다.

#### signature 생성 예
- Target 데이터(signParam)

  |   mKey=12345&amp;oid=INIWelTest_1361252896871&amp;price=1004&amp;&amp;timestamp=1361252896871  |
    
- Hash 데이터 (위 Target데이터를 SHA256 Hash한 값)

  | 2883da372a7ccf6cdad99b4b9d52ef67cb4cc52d77192e36d8cce8258bcdecdf |

#### 잘못된 Target 데이터 생성 예

#### 띄어쓰기 및 & 중복의 경우
##### 원본 

|mKey=xxxxxxxxxx&amp;oid=1231231&amp;price=10000 **&amp; &amp;** timestamp=1335247243103   |

##### 수정   

| mKey=xxxxxxxxxx&amp;oid=1231231&amp;price=10000&amp;timestamp=1335247243103 |

#### 마지막에 & 가 붙는 경우
##### 원본 

| mKey=xxxxxxxxxx&amp;oid=1231231&amp;price=10000&amp;timestamp=1335247243103 **&amp;** |

##### 수정 

| mKey=xxxxxxxxxx&amp;oid=1231231&amp;price=10000&amp;timestamp=1335247243103 |


