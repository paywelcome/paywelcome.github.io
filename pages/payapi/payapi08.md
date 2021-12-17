---
title: PAYAPI
permalink: payapi08.html
sidebar: payapi_sidebar
folder: payapi
toc: false
---

# 8. 샘플소스

기본 통신코드는 서비스와 상관 없이 동일하며, URL과 요청 파라미터 값만 다릅니다. 다음의 샘플 코드는 취소 API를 기본으로 하고 있으니 참고만 하시기 바랍니다.

## 8.1 Node.js
```node
var request = require('request');
var api_url = 'https://payapi.paywelcome.co.kr/cancel/cancel';
var request_body = '';
request_body += 'payType=&';
request_body += 'mid=welcometst';
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

## 8.2 JAVA
```java
try {
	String apiURL = "https://payapi.paywelcome.co.kr/cancel/cancel";
	String request_body = "";
	request_body += "payType=card&";
	request_body += "mid=welcometst
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

## 8.3 PHP

```PHP
<?php
	$url = "https://payapi.paywelcome.co.kr/cancel/cancel";
	
	$headers = array();
	$headers[] = "Content-Type: application/x-www-form-urlencoded; charset=UTF-8";
	
	$request_body = "";
	$request_body .= "payType=card&";
	$request_body .= "mid=welcometst
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

## 8.4 ASP

```ASP
<%@Language="VBScript" CODEPAGE="949" %>
<%
dim xmlhttp, request_body

request_body = "payType=card&"
request_body = request_body & "mid=welcometst
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