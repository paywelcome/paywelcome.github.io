---
title: 연동 준비
permalink: prepare02.html
sidebar: prepare_sidebar
folder: prepare
toc: false
---


# 1. Signature 생성 
## 1.1 P_SIGNATURE 생성

## 원본 예시

```
 mkey=028264c3ce073608de30a7b2b7ec7500e43c6d5e063784075e54fba43e1eec6e&P_AMT=1000&P_OID=xxxxx_1361252896871&P_TIMESTAMP=1361252896871
```

## Hash 데이터
```
 d3390ab2283e86cd1405c47b86b08fd7ca359f53a5086a4b00fdbf6412be3a10 
```
## signature 필드 구성

| 순번 | 필드명 | 승인필드명 | 설명 | 필수 |
| --- | --- | --- | --- | --- |
| 1 | mkey |  Sha256(signkey) | `signke 값은 담당자에게 문의 바랍니다.` | 필수 |
| 2 | P_AMT | P_AMT(금액) | 가맹점 주문번호/결제단위 Unique | 필수 |
| 3 | P_OID | P_OID(주문번호) | 주문단위 unique한 값 ( mid+"_"+timestamp ) | 필수 |
| 4 | P_TIMESTAMP | P_TIMESTAMP(타임스탬프) | TimeInMillis(Long형) | 필수 |