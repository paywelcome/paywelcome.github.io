---
title: 연동 준비
permalink: prepare01.html
sidebar: prepare_sidebar
folder: prepare
toc: false
---
<style>
</style>

# 1. Signature 생성 
## 1.1. signature 개요

- 결제요청시 등 HTTPS post 요청시 가맹점의 요청이 정상적인 요청인지 여부 / 사용자의 위변조 방지를 위해 일부 데이터를 SHA256으로 Hash한 값

- signature는 form.submit 시 적용됩니다.signature생성은 Sample Source를 참고하여 작성하시기 바랍니다.

## 1.2 signature 첨부 대상
  Web Standard 서비스의 모든 요청
- 결제(인증), 승인APIsignature 생성 대상 필드(Target) 모든 요청의 signature의 생성방법 동일하며, 요청별로 생성 대상 필드가 다름
- 요청별로 명시된 signature 생성 대상(Target)필드 를 참조
- 인증요청(결제요청) : oid,price,timestamp
  [[TABLE 1-3] signature 생성 대상(Target) 필드 참조](/stdweb03.html#table-1-3-signature-생성-대상target-필드)
- 승인요청 : authToken, timestamp
  [[TABLE 2-3] 승인요청 signature 생성 대상(Target) 필드 참조](/stdweb03.html#table-2-3-승인요청-signature-생성-대상target-필드) 
  
## 1.3 signature 생성 방법
- 위변조 방지를 위한 보안조치로서 필수 체크 데이터를 NVP 방식으로 연결한 데이터를SHA256으로 Hash한 값
- NVP : nameandvalue parameters
  ex) name=value&amp;name=value&amp;name=value&amp;name=value
- 필드 순서유지(알파벳순), 마지막 &amp;는 생략, 공백생략, 모든대상 필드는 Form에 설정되는 데이터와 동일한 값을 이용

## 1.4 signature 생성 샘플(결제요청)
- 언어별 제공된 라이브러리 소스를 통해서 생성가능합니다.

### signature 생성 예
- Target 데이터(signParam)

  |   mKey=12345&amp;oid=INIWelTest_1361252896871&amp;price=1004&amp;&amp;timestamp=1361252896871  |
    
- Hash 데이터 (위 Target데이터를 SHA256 Hash한 값)

  | 2883da372a7ccf6cdad99b4b9d52ef67cb4cc52d77192e36d8cce8258bcdecdf |

### 잘못된 Target 데이터 생성 예

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

