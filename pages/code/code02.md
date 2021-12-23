---
title: 웹표준(PC) 코드
permalink: code02.html
sidebar: code_siderbar
folder: code
toc: false
---

<div style="display: inline-block; width: 100%;">
  <a style="float:left;" href="/code01.html">◀이전페이지</a>
  <a style="float:right;" href="/code03.html">다음페이지▶</a>
</div>

# 2. 웹표준(PC) 코드

## 2.1 결제수단코드 (gopaymethod)

| 지불수단 이름 | 키워드    |
| :-----------: | :----------: |
| 신용카드        | Card       |
| ---         | ---        |
| 휴대폰결제       | HPP        |
| 계좌이체        | DirectBank |
| 가상계좌        | VBank      |

## 2.2 결제수단코드 (paymethod)

| 지 불수단 이름  |  키워드   |
| :-----------------: | :----------: |
| 신용카드(ISP)         | VCard      |
| ---               | ---        |
| 신용카드(안심클릭)        | Card       |
| 실시간계좌이체(K계좌이체)    | DirectBank |
| 무통장입금(가상계좌)       | VBank      |
| 휴대폰               | HPP        |

## 2.3 gopaymethod 옵션

| 지불수단 이름 | 키워드    |
| :-----------: | :----------: |
| 신용카드(모든)    | Card       |
| ---         | ---        |
| 신용카드(안심결제)  | ACard      |
| 신용카드(ISP)   | VCard      |
| 신용카드(간편결제)  | EasyPay    |
| 휴대폰결제       | HPP        |
| 계좌이체        | DirectBank |
| 가상계좌 | VBank |

## 2.4 카드사 승인코드

| 코드   | 카드사 이름 | 코드   | 카드사 이름 |
| :----: | :------: | :----: | :------: |
| 01   | 하나(외한) | 03   | 롯데     |
| 04   | 현대     | 06   | 국민     |
| 11   | BC     | 12   | 삼성     |
| 14   | 신한     | 15   | 한미     |
| 16   | NH     | 17   | 하나카드   |
| 21   | 해외비자   | 22   | 해외마스터  |
| 23   | JCB    | 24   | 해외아멕스  |
| 25 | 해외다이너스 | | |

## 2.5 카드사 코드(결제창 호출시 제어코드)

| 코드   | 직접호출구분    | 카드사 이름 | 코드   | 직접호출 구분   | 카드사 이름    |
| :----: | :---------: | :------: | :----: | :---------: | :---------: |
| 01   | onlyacard | 하나(외환) | 03   | onlyacard | 롯데        |
| 04   | onlyacard | 현대     | 06   | onlyvcard | 국민        |
| 11   | onlyvcard | BC     | 12   | onlyacard | 삼성        |
| 14   | onlyacard | 신한     | 21   | 미사용       | 해외 VISA   |
| 22   | 미사용       | 해외마스터  | 23   | 미사용       | 해외JCB     |
| 26   | 미사용       | 중국은련   | 32   | onlyvcard | 광주        |
| 33   | onlyvcard | 전북     | 34   | onlyacard | 하나        |
| 35   | onlyvcard | 산업카드   | 41   | onlyacard | NH        |
| 43   | onlyacard | 씨티     | 44   | onlyvcard | 우리        |
| 48   | onlyvcard | 신협체크   | 51   | onlyvcard | 수협        |
| 52   | onlyvcard | 제주     | 54   | onlyvcard | MG새마을금고체크 |
| 55   | onlyvcard | 케이뱅크   | 56   | onlyvcard | 카카오뱅크     |
| 71   | onlyvcard | 우체국체크  | 81   | onlyvcard | 하나BC      |
| 95 | onlyvcard | 저축은행체크 | | | | 

## 2.6 카드 발급사(은행) 코드

| 코드   | 카드사 이름        | 코드   | 카드사 이름      |
| :----: | :-------------: | :----: | :-----------: |
| 02   | 한국산업은행        | 03   | 기업은행        |
| 04   | 국민은행          | 05   | 하나은행 (구외환)  |
| 06   | 국민은행 (구 주택)   | 07   | 수협중앙회       |
| 11   | 농협중앙회         | 12   | 단위농협        |
| 16   | 축협중앙회         | 20   | 우리은행        |
| 21   | 신한은행 (조흥은행)   | 23   | 제일은행        |
| 25   | 하나은행 (서울은행)   | 26   | 신한은행        |
| 27   | 한국씨티은행 (한미은행) | 31   | 대구은행        |
| 32   | 부산은행          | 34   | 광주은행        |
| 35   | 제주은행          | 37   | 전북은행        |
| 38   | 강원은행          | 39   | 경남은행        |
| 41   | 비씨카드          | 53   | 씨티은행        |
| 54   | 홍콩상하이은행       | 71   | 우체국         |
| 81   | 하나은행          | 83   | 평화은행        |
| 87   | 신세계           | 88   | 신한은행(조흥 통합) |
| 97 | 카카오 머니 | 98 | 페이코 (포인트 100% 사용) |


## 2.7 은행(증권사) 코드

| 코드   | 카드사 이름               | 코드   | 카드사 이름      |
| :----: | :--------------------: | :----: | :-----------: |
| 02   | 한국산업은행               | 03   | 기업은행        |
| 04   | 국민은행                 | 05   | 하나은행 (구 외환) |
| 06   | 국민은행 (구 주택)          | 07   | 수협중앙회       |
| 11   | 농협중앙회                | 12   | 단위농협        |
| 16   | 축협중앙회                | 20   | 우리은행        |
| 21   | 구)조흥은행               | 22   | 상업은행        |
| 23   | SC제일은행               | 24   | 한일은행        |
| 25   | 서울은행                 | 26   | 구)신한은행      |
| 27   | 한국씨티은행 (구 한미)        | 31   | 대구은행        |
| 32   | 부산은행                 | 34   | 광주은행        |
| 35   | 제주은행                 | 37   | 전북은행        |
| 38   | 강원은행                 | 39   | 경남은행        |
| 41   | 비씨카드                 | 45   | 새마을금고       |
| 48   | 신용협동조합중앙회            | 50   | 상호저축은행      |
| 53   | 한국씨티은행               | 54   | 홍콩상하이은행     |
| 55   | 도이치은행                | 56   | ABN 암로      |
| 57   | JP모건                 | 59   | 미쓰비시도쿄은행    |
| 60   | BOA(Bank of America) | 64   | 산림조합        |
| 70   | 신안상호저축은행             | 71   | 우체국         |
| 81   | 하나은행                 | 83   | 평화은행        |
| 87   | 신세계                  | 88   | 신한(통합)은행    |
| 89   | 케이뱅크                 | 90   | 카카오뱅크       |
| D1   | 유안타증권(구 동양증권)        | D2   | 현대증권        |
| D3   | 미래에셋증권               | D4   | 한국투자증권      |
| D5   | 우리투자증권               | D6   | 하이투자증권      |
| D7   | HMC 투자증권             | D8   | SK 증권       |
| D9   | 대신증권                 | DA   | 하나대투증권      |
| DB   | 굿모닝신한증권              | DC   | 동부증권        |
| DD   | 유진투자증권               | DE   | 메리츠증권       |
| DF   | 신영증권                 | DG   | 대우증권        |
| DH   | 삼성증권                 | DI   | 교보증권        |
| DJ   | 키움증권                 | DK   | 이트레이드       |
| DL   | 솔로몬증권                | DM   | 한화증권        |
| DN   | NH증권                 | DO   | 부국증권        |
| DP | LIG증권 | | |

## 2.8 신용카드 간편결제 코드

| 코드       | 간편결제 이름 | 
| :--------: | :-------: | 
| kakaopay | 카카오페이   |
|  lpay | 엘페이     |
| payco | 페이코  | 

## 2.9 카드 이벤트 적용 코드

- 해당 코드는 참조용으로, 모든 에러코드에 대한 명시되 있지 않으며, 언제든이 변경될 수 있습니다.

<table>
  <thead>
    <tr>
      <th style="text-align: center; width:20%">코드</th>
      <th style="text-align: left; width:80%">설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">1</td>
      <td style="text-align: left">당사&amp;카드사부담 일반 무이자 할부 이벤트</td>
    </tr>
    <tr>
      <td style="text-align: center">12</td>
      <td style="text-align: left">카드사부담 일반 무이자 + 상점 일반 할인 이벤트</td>
    </tr>
    <tr>
      <td style="text-align: center">14</td>
      <td style="text-align: left">카드사부담 일반 무이자 + 카드번호별 할인 이벤트</td>
    </tr>
    <tr>
      <td style="text-align: center">24</td>
      <td style="text-align: left">카드사부담 일반 무이자 + 카드 Prefix별 할인 이벤트</td>
    </tr>
    <tr>
      <td style="text-align: center">A1</td>
      <td style="text-align: left">상점부담 일반 무이자 할부 이벤트</td>
    </tr>
    <tr>
      <td style="text-align: center">A2</td>
      <td style="text-align: left">상점 일반 할인 이벤트</td>
    </tr>
    <tr>
      <td style="text-align: center">A3</td>
      <td style="text-align: left">상점 무이자 + 상점 일반 할인 이벤트</td>
    </tr>
    <tr>
      <td style="text-align: center">A4</td>
      <td style="text-align: left">상점 무이자 + 카드번호별 할인 이벤트</td>
    </tr>
    <tr>
      <td style="text-align: center">A5</td>
      <td style="text-align: left">카드번호별 할인 이벤트</td>
    </tr>
    <tr>
      <td style="text-align: center">B4</td>
      <td style="text-align: left">상점 무이자 + 카드 Prefix별 할인 이벤트</td>
    </tr>
    <tr>
      <td style="text-align: center">B5</td>
      <td style="text-align: left">카드 Prefix별 할인 이벤트</td>
    </tr>
    <tr>
      <td style="text-align: center">C0</td>
      <td style="text-align: left">당사 &amp; 카드사부담 특별 무이자 할부 이벤트</td>
    </tr>
    <tr>
      <td style="text-align: center">C1</td>
      <td style="text-align: left">상점부담 특별 무이자 할부 이벤트</td>
    </tr>
  </tbody>
</table>


## 2.10 인증 결과코드

- 해당 코드는 참조용으로, 모든 에러코드에 대한 명시되 있지 않으며, 언제든이 변경될 수 있습니다.

`소스에 코딩하지 마시기 바랍니다.`

<table>
  <thead>
    <tr>
      <th style="text-align :center; width: 20%">구분</th>
      <th style="text-align :center; width: 20%">결과코드</th>
      <th style="text-align :center; width: 20%">사유</th>
      <th style="text-align :left; width: 40%">비고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align :center; vertical-align: middle">인증성공</td>
      <td style="text-align :center">0000</td>
      <td style="text-align :center">성공</td>
      <td>정상적으로 결제창을 통해 인증이 완료된 경우<br>(승인요청 가능)</td>
    </tr>
    <tr>
      <td rowspan="5" style="text-align :center; vertical-align: middle">인증실패기타
<br><br><br><br>
</td>
      <td  style="text-align :center">V000 ~ V099</td>
      <td  style="text-align :center">결제 요청 실패</td>
      <td>필수 파라미터 누락, 규칙에 맞지 않는 파라미터, 주문번호 중복 등</td>
    </tr>
    <tr>
      <td style="text-align :center">V100 ~ V199</td>
      <td style="text-align :center">결제창 표시 실패</td>
      <td>표시가능 결제수단 없음 등</td>
    </tr>
    <tr>
      <td style="text-align :center">V200 ~ V299</td>
      <td style="text-align :center">인증완료후 실패</td>
      <td>인증완료후 가맹점 인증결과 전송중 실패 등</td>
    </tr>
    <tr>
      <td style="text-align :center">V800 ~ V899</td>
      <td style="text-align :center">결제 종료</td>
      <td>사용자 취소, 결제 요청 시간 초과, 위변조 시 등</td>
    </tr>
    <tr>
      <td style="text-align :center">R900 ~ V999</td>
      <td style="text-align :center">기타</td>
      <td>예상치 못한 실패 등</td>
    </tr>
  </tbody>
</table>

## 2.11 승인 결과코드

- 해당 코드는 참조용으로, 모든 에러코드에 대한 명시되 있지 않으며, 언제든이 변경될 수 있습니다.

`소스에 코딩하지 마시기 바랍니다.`

<table>
  <thead>
    <tr>
      <th style="text-align :center; width: 20%">구분</th>
      <th style="text-align :center; width: 20%">결과코드</th>
      <th style="text-align :center; width: 20%">사유</th>
      <th style="text-align :left; width: 40%">비고</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align :center;vertical-align: middle">승인성공</td>
      <td style="text-align :center">0000</td>
      <td> </td>
      <td>정상적으로 승인이 완료된 경우</td>
    </tr>
    <tr>
      <td rowspan="4" style="text-align :center;vertical-align: middle">승인 요청전실패</td>
      <td style="text-align :center;">R100 ~ R199</td>
      <td style="text-align :center;">승인 요청 실패</td>
      <td>필수 파라미터 누락, 규칙에 맞지 않는 파라미터 등</td>
    </tr>
    <tr>
      <td style="text-align :center;">R200 ~ R299</td>
      <td style="text-align :center;">승인 처리 불가 실패</td>
      <td>재승인 요청 등</td>
    </tr>
    <tr>
      <td style="text-align :center;">R300 ~ R399</td>
      <td style="text-align :center;">승인 처리중 실패</td>
      <td>내부 장애 등</td>
    </tr>
    <tr>
      <td style="text-align :center;">R900 ~ R999</td>
      <td style="text-align :center;">기타</td>
      <td>예상치 못한 실패</td>
    </tr>
  </tbody>
</table>

<div style="display: inline-block; width: 100%;">
  <a style="float:left;" href="/code01.html">◀이전페이지</a>
  <a style="float:right;" href="/code03.html">다음페이지▶</a>
</div>
