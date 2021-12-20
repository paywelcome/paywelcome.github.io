---
title: 공통 코드
permalink: code01.html
sidebar: code_siderbar
folder: code
toc: false
---

## 승인 시 카드사 코드
- 카드거래 후 승인응답 시 사용되는 코드입니다.

| 코드   | 카드사 이름 | 코드   | 카드사 이름 |
| ---- | ------ | ---- | ------ |
| 01   | 하나(외한) | 03   | 롯데     |
| ---  | ---    | ---  | ---    |
| 04   | 현대     | 06   | 국민     |
| 11   | BC     | 12   | 삼성     |
| 14   | 신한     | 15   | 한미     |
| 16   | NH     | 17   | 하나카드   |
| 21   | 해외비자   | 22   | 해외마스터  |
| 23   | JCB    | 24   | 해외아멕스  |
| 25 | 해외다이너스 | | |


## 결제창 호출 시 카드사 코드

| 코드   | 직접호출구분    | 카드사 이름 | 코드   | 직접호출 구분   | 카드사 이름    |
| ---- | --------- | ------ | ---- | --------- | --------- |
| 01   | onlyacard | 하나(외환) | 03   | onlyacard | 롯데        |
| ---  | ---       | ---    | ---  | ---       | ---       |
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

## 카드 발급사 ( 은행 )  코드

| 코드   | 카드사 이름        | 코드   | 카드사 이름      |
| ---- | ------------- | ---- | ----------- |
| 02   | 한국산업은행        | 03   | 기업은행        |
| ---  | ---           | ---  | ---         |
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

## 은행 ( 증권사 )  코드

| 코드   | 카드사 이름               | 코드   | 카드사 이름      |
| ---- | -------------------- | ---- | ----------- |
| 02   | 한국산업은행               | 03   | 기업은행        |
| ---  | ---                  | ---  | ---         |
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

## 신용카드간편결제코드

| 코드       | 간편결제 이름 | 
| :--------: | :-------: | 
| kakaopay | 카카오페이   |
|  lpay | 엘페이     |
| payco | 페이코 | | | 

 ## 카드 이벤트 적용 코드


## 에스크로 배송등록 택배사 코드
 
| 코드     | 카드사명 | 코드  | 카드사명     |
| ---------- | -------- | ------- | ------------ |
| 9999       | 기타택배     | kgb     | 로젠택배         |
| cjgls      | CJ대한통운   | hyundai | 롯데택배(구 현대택배) |
| registpost | 우편등기     | EPOST   | 우체국택배        |
| hanjin     | 한진택배     | kdexp   | 경동택배         |
| chunil     | 천일택배     | daesin  | 대신택배         |
| ilyang     | 일양로지스    | honam   | 호남택배         |
| cvsnet     | 편의점택배    | hdexp   | 합동택배         |