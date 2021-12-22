---
title: 샘플 코드
permalink: sample01.html
sidebar: sample_siderbar
folder: sample
toc: false
---

# 샘플코드

## 1. Signature 샘플코드

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

## 2. PAYAPI 샘플코드

기본 통신코드는 서비스와 상관 없이 동일하며, URL과 요청 파라미터 값만 다릅니다. 다음의 샘플 코드는 취소 API를 기본으로 하고 있으니 참고만 하시기 바랍니다.

### node.js
```node
var request = require('request');
var api_url = 'https://payapi.paywelcome.co.kr/cancel/cancel';
var request_body = '';
request_body += 'payType=&';
request_body += 'mid=xxxxxxxxxx';
request_body += 'tid=INIMX_VBNKINIWelTest20190904111111111111&';
request_body += 'price=&';
request_body += 'currency=&';
request_body += 'timestamp=&';
request_body += 'siganture=&';

request.post({
    url: api_url,
    body: request_body,
    headers: {
        'Content-Type': 'application/x-www-form-urlencoded; charset=UTF-8'
        }
    },
    function (error, response, body) {
        console.log('HTTP STATUS CODE: ' + response.statusCode);
        console.log('HTTP HEADER:');
        console.log(response.headers);
        console.log('HTTP BODY:');
        console.log(body);
    }
);
```

### java
```java
try {
	String apiURL = "https://payapi.paywelcome.co.kr/cancel/cancel";
	String request_body = "";
	request_body += "payType=card&";
	request_body += "mid=xxxxxxxxxx
	request_body += "tid=StdpayCARDINIWelTest20190904115758995708&";
	request_body += "price=1000&";
	request_body += "currency=WON&";
	request_body += "timestamp=&";
	request_body += "signature=&";
	
	URL url = new URL(apiURL);
	HttpURLConnection con = (HttpURLConnection)url.openConnection();
	con.setRequestMethod("POST");
	con.setRequestProperty("Content-Type", "application/x-www-form-urlencoded; charset=UTF-8");
	con.setDoOutput(true);
			
	DataOutputStream wr = new DataOutputStream(con.getOutputStream());
	wr.writeBytes(request_body);
	wr.flush();
	wr.close();
	
	int responseCode = con.getResponseCode();
	BufferedReader br = null;
	if(responseCode==200) {
		br = new BufferedReader(new InputStreamReader(con.getInputStream(), "UTF-8"));
	} else { 
		br = new BufferedReader(new InputStreamReader(con.getErrorStream(), "UTF-8"));
	}
	
	String inputLine = null;
	StringBuffer response = new StringBuffer();
	while ((inputLine = br.readLine()) != null) {
		response.append(inputLine);
	}
	br.close();
	
	System.out.println(response.toString());
} catch (Exception e) {
	System.out.println(e);
}
```

### php

```PHP
<?php
	$url = "https://payapi.paywelcome.co.kr/cancel/cancel";
	
	$headers = array();
	$headers[] = "Content-Type: application/x-www-form-urlencoded; charset=UTF-8";
	
	$request_body = "";
	$request_body .= "payType=card&";
	$request_body .= "mid=xxxxxxxxxx
	$request_body .= "tid=StdpayCARDINIWelTest20190904115758995708&";
	$request_body .= "price=1000&";
	$request_body .= "currency=WON&";
	$request_body .= "timestamp=&";
	$request_body .= "signature=&";
	
	$ch = curl_init();
	curl_setopt($ch, CURLOPT_URL, $url);
	curl_setopt($ch, CURLOPT_POST, true);
	curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
	//SSL 이슈가 있을 경우 하단에 주석 해제 후 확인
//curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, 0);
	curl_setopt($ch, CURLOPT_HTTPHEADER, $headers);
	curl_setopt($ch, CURLOPT_POSTFIELDS, $request_body);
	
	$response = curl_exec($ch);
	$status_code = curl_getinfo($ch, CURLINFO_HTTP_CODE);
	curl_close ($ch);
	
	echo "Status_code: ".$status_code."<br>";
	
	if($status_code == 200) {
		echo $response;
	} else {
		echo "Error 내용:".$response."<br>";
	}
?>
```

### asp

```ASP
<%@Language="VBScript" CODEPAGE="949" %>
<%
dim xmlhttp, request_body

request_body = "payType=card&"
request_body = request_body & "mid=xxxxxxxxxx
request_body = request_body & "tid=StdpayCARDINIWelTest20190904115758995708&"
request_body = request_body & "price=1000&"
request_body = request_body & "currency=WON&"
request_body = request_body & "timestamp=&"
request_body = request_body & "signature=&"

Set xmlHttp = Server.CreateObject("Msxml2.XMLHTTP")
xmlhttp.Open "POST", "https://payapi.paywelcome.co.kr/cancel/cancel", False
xmlhttp.setRequestHeader "Content-Type", "application/x-www-form-urlencoded; charset=UTF-8"
xmlhttp.send request_body

Response.Write xmlHttp.responseText

set xmlhttp = nothing
%> 
```