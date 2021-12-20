---
title: MOBILE
permalink: mobile06.html
sidebar: mobile_sidebar
folder: mobile
toc: false
---

# 6. 앱 환경의 설치방법(안드로이드)

## 6.1 기본적인 설치방법

안드로이드 어플리케이션 내 WebView (이하 WebView) 에서 Mobile Web 서비스를 구현하는 경우에 해당됩니다.<br>
Mobile Web 서비스를 WebView 내에 구현하는 경우, 발생할 수 있는 Encoding Issue 는 ( 1-13. 주의사항 &lt;UrlEncode issue&gt; ) 를 참조하셔 주십시오.<br>
WebView 에서 Mobile Web 서비스를 띄우는 방식은 앞 장에서 설명한 (0.기본적인 설치 방법) 의 방법과 동일합니다.<br>
이에 이번 장 에서는 ISP 앱 호출 시 주의사항, 카드사 백신 앱 스키마 호출 및 &quot;미설치 시, 앱스토어 이동 이슈&quot; 등의 내용을 주로 다룹니다.<br>

## 6.2 ISP 연동방법 - 앱 미설치 체크로직 직접구현 or 자동체크

- ISP 앱의 기본정보는 하기와 같습니다.

<table style="width: 100%;">
<colgroup>
  <col style="width: 30%;">
  <col style="width: 70%;">
</colgroup>
  <thead>
    <tr>
      <th>Application Scheme</th>
      <th>iInstallUrl</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>ispmobile://</td>
      <td>http://mobile.vpay.co.kr/jsp/MISP/andown.jsp</td>
    </tr>
  </tbody>
</table>

- 상기 Scheme 과 Install Url 정보로 구현가능한 안드로이드 코드는 하기와 같습니다.

1. WebViewClient 를 상속받은 클래스를 구현하시고, shouldOverrideUrlLoading() 을 호출 하십시오.
```java
private class INIP2PWebView extends WebViewClient {
    @Override     
    public boolean shouldOverrideUrlLoading(WebView view, String url) {
    ….
    }
```

2. 상기 shouldOverrideUrlLoading() 함수 내에, try{} catch{e} 를 통해, try 내에서는 startActivity(intent) 를 구현하시고, catch Event 발생 시, 앱 스토어로 이동할 수 있도록 조치하시면 됩니다.
하기에 안내되는 소스는 상기 방식에 대한 Full-Source 입니다. 

<p style="font-size: 80%">[shouldOverrideUrlLoading 부]</p>

```java
private class INIP2PWebView extends WebViewClient {
@Override     
public boolean shouldOverrideUrlLoading(WebView view, String url) {
  ...   
  Uri uri = Uri.parse(url);     
  Intent intent = new Intent(Intent.ACTION_VIEW, uri);
  try{     
    startActivity(intent); 
    //삼성카드 안심클릭을 위해 추가
    if( url.startsWith("ispmobile://")) finish();
}
catch(ActivityNotFoundException e)
  {
     //url prefix가 ispmobile 일겨우만 alert를 띄움
     if( url.startsWith("ispmobile://"))
     {
        view.loadData("<html><body></body></html>", "text/html", "euc-kr"); 
        alertIsp.show();
        return true;
     }
  }
  ...
  return true;     
  }

```

<p style="font-size: 80%">[ISP 앱스토어 이동처리 부] - alertIsp</p>

```java
protected void onCreate(Bundle savedInstanceState) {
...
alertIsp = new AlertDialog.Builder(PaymentView.this)
.setIcon(android.R.drawable.ic_dialog_alert) 
.setTitle("알림")
.setMessage("모바일 ISP 어플리케이션이 설치되어 있지 않습니다. \n설치를 
눌러 진행 해 주십시요.\n취소를 누르면 결제가 취소 됩니다.")     
.setPositiveButton("설치", new DialogInterface.OnClickListener() { 
     @Override
     public void onClick(DialogInterface dialog, int which) { 
            //ISP 설치 페이지 URL     
            paymentView.loadUrl("http://mobile.vpay.co.kr/jsp/MISP/andown.jsp");
            finish();
        }
 
})     
  .setNegativeButton("취소", new DialogInterface.OnClickListener() {
     @Override
     public void onClick(DialogInterface dialog, int which) {     
        Toast.makeText(PaymentView.this, "(-1)결제를 취소 하셨습니다." , Toast.LENGTH_SHORT).show();     
        finish();     
     }
}).create();     
...
}

```

3. ISP 가 단말기에 기 설치되어 있는 경우, ISP 가 정상구동 될 것이며,
4. ISP 가 단말기에 미 설치되어 있는 경우, 설치 후, Mobile Web 서비스를 다시 띄워주시면 됩니다.
23 페이지의 예시[shouldOverrideUrlLoading 부] 의 에 대하여 true 혹은 false 를 설정하는 것은 하기의 표를 참고하십시요.

<table style="width: 100%;">
<colgroup>
  <col style="width: 15%">
  <col style="width: 30%">
  <col style="width: 30%">
  <col style="width: 25s%">
</colgroup>
  <thead>
    <tr>
      <th style="text-align: center">apprun_check</th>
      <th style="text-align: center">작동방식</th>
      <th>앱 미설치 시, 앱스토어 이동 후 결제페이지 잔존여부</th>
      <th style="text-align: center">true / false 설정</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">Y</td>
      <td style="text-align: center">ISP,  계좌이체앱<br>- intent  작동</td>
      <td>상태 유지</td>
      <td style="text-align: center">true</td>
    </tr>
    <tr>
      <td style="text-align: center">N or  미설정</td>
      <td style="text-align: center">ISP,  계좌이체앱<br>? appScheme  작동</td>
      <td>하기 [그림 1]  과 같이  Display  됨</td>
      <td style="text-align: center">false</td>
    </tr>
  </tbody>
</table>

- [shouldOverrideUrlLoading 부] 의 을 true 로 할 경우, Mobile Web 서비스를 띄운 WebView 는 사라집니다.
  따라서, app Scheme 형태로 결제 앱을 호출할 경우에는 &quot;그림 1&quot; 과 같이 오류 페이지가 Display 되기 때문에, WebView 를 remove 하는 것이 좋습니다.

{% include image.html file="mobile_img10.jpg" %}
[그림1] 

- [shouldOverrideUrlLoading 부] 의 을 false 로 할 경우, Mobile Web 서비스를 띄운 WebView 는 사라지지 않기 때문에,
  apprun_check=Y 를 통해 현 결제 페이지가 유지되는 방식을 사용 하는 것이 좋습니다. 이 방법을 자동체크방식이라 합니다.
- 단, apprun_check 옵션을 통해 설치체크로직이 작동되므로, alertIsp 함수는 구현될 필요가 없습니다.
  apprun_check 로직에 대하여 상세히 확인하시려면 ( 0.결제창 Open (주문정보 전달) ? 복합필드 ) 를 확인하여 주십시오. 또한, Intent 호출에 대하여 예외처리를 반드시 체크하셔야 합니다.

## 6.3 ISP 연동방법 - 인증결과 전송

- ISP 앱에서 인증과정이 완료되면, 다시 당사 모바일 결제창으로 돌아와서 하기의 이미지와 같이 &#39;확인&#39; 버튼을 클릭해야, 승인과정을 시작하게 됩니다.

- 안드로이드는 운영체제 특성 상, 현재 앱이 종료될 경우, 이 앱을 실행시킨 이전 앱이 다시 자동으로 수행됩니다.
  (LIFO 방식) 따라서, ISP 앱이 종료되면, 가맹점의 앱은 자동으로 다시 활성화될 것입니다.

## 6.4 안심클릭 결제 시, 카드사 백신 앱 연동

- Mobile Web 서비스는 BC 계열을 제외한, 나머지 카드사의 결제창은 카드사 페이지에서 결제가 이루어지고 있습니다.
  이에, 카드사에서 개별적으로 사용하는 백신 앱의 경우, 가맹점 앱에서도 하기의 유의사항을 반드시 체크하셔야 합니다.

1. WebView 내에서 http와 https URL, 그리고 App Url 을 분기하여 처리해야 함.
2. shouldOverrideUrlLoading() 처리로직을 하기와 같이 구현함.

<table style="width: 100%">
<colgroup>
  <col style="width: 50%">
  <col style="width: 50%">
</colgroup>
  <thead>
    <tr>
      <th>App Url  일 경우</th>
      <th>Web Url 일 경우</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>activity 호출</td>
      <td>WebView 에서 Loading</td>
    </tr>
  </tbody>
</table>

상기의 유의사항을 고려한 샘플 코드는 하기와 같습니다. (_Kitkat_ _이하 정상구동여부 확인됨_)

<details style="cursor:pointer;">
<summary><strong>[&nbsp;펼치기&nbsp;]</strong></summary>
<div markdown="1">

```java
private class SampleWebViewClient extends WebViewClient {
  @Override
  public boolean shouldOverrideUrlLoading(WebView view, String url) {
    Log.d("<INICIS_TEST>","URL : "+url);
    /*
    * URL별로 분기가 필요합니다. 어플리케이션을 로딩하는 것과
    * WEB PAGE를 로딩하는 것을 분리하여 처리해야 합니다.
    * 만일 가맹점 특정 어플 URL이 들어온다면 
    * 조건을 더 추가하여 처리해 주십시요.
    */
    if( !url.startsWith("http://") && !url.startsWith("https://") && !url.startsWith("javascript:") )
    {    		
      Intent intent; 
      try{
        intent = Intent.parseUri(url, Intent.URI_INTENT_SCHEME);
        Log.d("<INICIS_TEST>", "intent getDataString : " + intent.getDataString());
      } catch (URISyntaxException ex) {
        Log.e("<INICIS_TEST>", "URI syntax error : " + url + ":" + ex.getMessage());
        return false;
      } 
      try{ 
        startActivity(intent); 
      }catch(ActivityNotFoundException e){
        /* ISP어플이 현재 폰에 없다면 아래 처리에서 
        * 알림을 통해 처리하도록 하였습니다.
        * 삼성카드 및 기타 안심클릭에서는 
        * 카드사 웹페이지에서 알아서 처리하기때문에
        * WEBVIEW에서는 별다른 처리를 하지 않아도 처리됩니다.
        */
        if( url.startsWith("ispmobile://"))
        { 
        //onCreateDialog에서 정의한 ISP 어플리케이션 알럿을 띄워줍니다.
        //(ISP 어플리케이션이 없을 경우)
          showDialog(DIALOG_ISP);
          return false;
        }else if (url.startsWith("intent")) {
            //일부카드사의 경우 ,intent:// 형식의 intent 스키마를 내려주지 않음
          //ex) 현대카드 intent:hdcardappcardansimclick://
          try {
            Intent tempIntent = Intent.parseUri(url, Intent.URI_INTENT_SCHEME);
            String strParams = tempIntent.getDataString();
            
            Intent intent = new Intent(Intent.ACTION_VIEW);
            intent.setData(Uri.parse(strParams));
            
            startActivity(intent);
            
            return true;
          } catch (Exception e) {
            e.printStackTrace();
            
            Intent intent = null;
            
            try {
              intent = Intent.parseUri(url, Intent.URI_INTENT_SCHEME);
              Intent marketIntent = new Intent(Intent.ACTION_VIEW);
              marketIntent.setData(Uri.parse("market://details?id=" + intent.getPackage()));
              startActivity(marketIntent);
            } catch (Exception e1) {
               e1.printStackTrace();
            }
            return true;
          } 
        }
      } 
    }
    else
    {	
      view.loadUrl(url);
      return false;
    }
    return true;
  }
}
```
</div>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             
</details>

## 6.5 결제 금액이 30 만원 이상일 때의 공인인증 앱 연동 방법

- 만약 상점에서의 판매가격이 30만원 이상일 수 있고 카드로 결제할 경우, 사용자는 공인인증서 서명과정을 거쳐야 합니다.<br>
- 안드로이드의 경우, 개별 카드사 앱에서 공인인증서 서명을 할 수 있습니다. 이에, 카드사 창 내에서 호출하는 intent 혹은 app Scheme 를 허용할 수 있도록 가맹점 앱에서 처리해줘야 합니다.<br>이는 (3.B . 안심클릭 결제 시, 카드사 백신 앱 연동)의 코드를 반영하면 해결됩니다.

## 6.6 Android API Level 21  이상 일 때 ,  체크사항

- Android API Level 21 (Lollipop 출시 때 배포) 부터는 webview 에서 Insecurity Page 에 대한 Access 및 Mixed contents, Third party cookies 사용을 차단할 수 있게 업데이트 되었습니다.
  먼저, Insecurity Page 에 대한 Access 차단으로 P_NEXT_URL 의 Scheme 을 Http 로 하는 경우, 페이지가 호출되지 않아 인증결과가 전달되지 않을 수 있습니다.
  하기의 설정을 확인하십시오.

<table style="width: 100%">
<colgroup>
  <col style="width: 30%">
  <col style="width: 70%">
</colgroup>
  <thead>
    <tr>
      <th>상태</th>
      <th>코드</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Insecurity  페이지 차단</td>
      <td><code class="language-plaintext highlighter-rouge">WebSettings web = paymentView.getSettings(); web.setMixedContentMode(web.MIXED_CONTENT_NEVER_ALLOW);</code></td>
    </tr>
    <tr>
      <td>Insecurity  페이지 허용</td>
      <td><code class="language-plaintext highlighter-rouge">WebSettings web = paymentView.getSettings(); web.setMixedContentMode(web.MIXED_CONTENT_ALWAYS_ALLOW);</code></td>
    </tr>
  </tbody>
</table>

- P_NEXT_URL 의 Scheme 이 Http 일 경우, 반드시 &quot;Insecurity 페이지 허용&quot; 으로 설정되어야 합니다.
  또한, Third party cookies 사용의 차단으로 안심클릭 카드 결제 시, 보안 키보드를 불러오지 못 하는 이슈 등이 발생할 수 있으니 하기 설정을 확인하십시오.

<table style="width: 100%">
<colgroup>
  <col style="width: 40%">
  <col style="width: 60%">
</colgroup>
  <thead>
    <tr>
      <th>상태</th>
      <th>코드</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Third party cookies  허용</td>
      <td>
<code class="language-plaintext highlighter-rouge">CookieManager cookieManager = CookieManager.getInstance();<br>cookieManager.setAcceptCookie(true);<br>cookieManager.setAcceptThirdPartyCookies(sampleWebView, true);</code><br> // false 설정 시 오류 발생</td>
    </tr>
  </tbody>
</table>

