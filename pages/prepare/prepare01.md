---
title: 연동 준비
permalink: prepare01.html
sidebar: prepare_sidebar
folder: prepare
toc: false
---
<style>
</style>

## 1.1 상점 연동시 주의사항

해킹시도 및 불법접속 차단 등의 보안을 위해 해외에서 접속 시에는 당사 서비스가 제한이 되며, 해외IP 차단해제를 위해서는 [ip-block@welcomepayments.co.kr](mailto:ip-block@welcomepayments.co.kr)로 아래 내용 작성해서 요청 주시기 바랍니다 .

| 업체명(MID)           | 접속 국가 | 접속 공인IP(대역) | 요청사항                 |
|--------------------| --------- | ----------------- | ------------------------ |
| xxxxx(xxxxxxxxmid) | 중국      | 111.111.111.111   | 해외아이피 차단해제 요청 |

## 1.2 signature 개요

{% include image.html file="pre_img01.png" %}

- 결제요청시 등 HTTPS post 요청시 가맹점의 요청이 정상적인 요청인지 여부 / 사용자의 위변조 방지를 위해 일부 데이터를 SHA256으로 Hash한 값

- signature는 form.submit 시 적용됩니다.signature생성은 Sample Source를 참고하여 작성하시기 바랍니다.

## 1.3 signature 첨부 대상
  Web Standard 서비스의 모든 요청
- 결제(인증), 승인APIsignature 생성 대상 필드(Target) 모든 요청의 signature의 생성방법 동일하며, 요청별로 생성 대상 필드가 다름
- 요청별로 명시된 signature 생성 대상(Target)필드 를 참조
- 인증요청(결제요청) : oid,price,timestamp
  [[TABLE 1-3] signature 생성 대상(Target) 필드 참조](/stdweb03.html#table-1-3-signature-생성-대상target-필드)
- 승인요청 : authToken, timestamp
  [[TABLE 2-3] 승인요청 signature 생성 대상(Target) 필드 참조](/stdweb03.html#table-2-3-승인요청-signature-생성-대상target-필드) 
  
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


### java
```java
// hash 알고리즘은 sha-256 사용
String algorithm = "SHA-256"; 

// hash 하기위한 plaintext를 변수에 담아준다.
String data = "mid=xxxxxxxxxx&mkey=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx&timestamp=1639118638775"; 

// SHA를 사용하기 위해 MessageDigest 클래스로부터 인스턴스를 얻는다.
MessageDigest md = MessageDigest.getInstance(algorithm); 

// 해싱할 byte배열을 넘겨준다.
// SHA-256의 경우 메시지로 전달할 수 있는 최대 bit 수는 2^64-1개 이다.
md.update(data.getBytes("UTF-8")); 

// 해싱된 byte 배열을 digest메서드의 반환값을 통해 얻는다.
byte[] hashbytes = md.digest(); 

// 보기 좋게 16진수로 만드는 작업
StringBuilder signatureStr = new StringBuilder();
for(int i=0 ; i&lt;hashbytes.length ; i++) { 
    // %02x 부분은 0 ~ f 값 까지는 한자리 수이므로 두자리 수로 보정하는 역할을 한다. 
    signatureStr.append(String.format("%02x", hashbytes[i] & 0xff));
} 

// signature 값 출력
System.out.println(signatureStr .toString());
```

### node
```javascript
// hash 하기위한 plaintext를 변수에 담아준다.
var plainText = "mid=xxxxxxxxxx&mkey=9xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx&timestamp=1639118638775"; 
// node.js 내장 암호화 함수 호출
var crypto = require('crypto'); 
// sha-256의 알고리즘으로 암호화하여 signature값 생성
var signature = crypto.createHash('sha256').update(plainText).digest('hex'); 
// 해당 값 출력시 signature 값 출력
console.log( signature); 
```

### php
```php
// hash 하기위한 plaintext를 변수에 담아준다.
$plainText = "mid=xxxxxxxxxx&mkey=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx&timestamp=1639118638775"; 
// sha-256 알고리즘으로 plainText를 암호화 하여 signature값 생성
$signature = hash("sha256", $plainText); 
// 해당 값 출력시 signature 값 출력
echo $signature;
```

### asp
```asp
// hash 알고리즘은 sha-256 사용
plainText = "mid=xxxxxxxxxx&mkey=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx&timestamp=1639118638775"; 
// 샘플소스 ASP_MOBILE\include\signature.asp 내부함수의 MakeSignature(sMessage)를 참고
MakeSignature(plainText);
```

## 1.6 서비스별 Signature 생성

서비스 별로 Signature생성 방식이 상이하므로 아래의 표를 참고해주시기 바랍니다.<br/>
**※ Signature 필드 생성 순서 중요** 

<table style="width: 100%;">
<colgroup>
  <col style="width: 30%;">
  <col style="width: 70%;">
</colgroup>
  <tbody>
    <tr>
      <th>PC</th>
      <td><code class="language-plaintext highlighter-rouge">mkey=&oid=&price=&timestamp=</code></td>
    </tr>
    <tr>
      <th>MOBILE</th>
      <td><code class="language-plaintext highlighter-rouge">mkey=&P_AMT=&P_OID=&P_TIMESTAMP=</code></td>
    </tr>
    <tr>
      <th>PAYAPI</th>
      <td><code class="language-plaintext highlighter-rouge">각 API명세서의 Signature 항목을 참조</code></td>
    </tr>
  </tbody>
</table>
