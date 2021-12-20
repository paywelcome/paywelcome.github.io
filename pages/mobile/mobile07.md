---
title: MOBILE
permalink: mobile07.html
sidebar: mobile_sidebar
folder: mobile
toc: false
---

# 7. 앱 환경의 설치방법(IOS)

## 7.1 기본적인 설치방법

IOS 어플리케이션 내 WebView (이하 WebView) 에서 Mobile Web 서비스를 구현하는 경우에 해당됩니다.<br>
Mobile Web 서비스를 WebView 내에 구현하는 경우, 발생할 수 있는 Encoding Issue 는 ( 1-13. 주의사항 &lt;UrlEncode issue&gt; ) 를 참조하셔 주십시오.<br>
WebView 에서 Mobile Web 서비스를 띄우는 방식은 앞 장에서 설명한 (0.기본적인 설치 방법) 의 방법과 동일합니다. 이에 이번 장 에서는 ISP 앱 호출 시 주의사항, 카드사 백신 앱 스키마 호출 및 &quot;미설치 시, 앱스토어 이동 이슈&quot; 등의 내용을 주로 다룹니다.

## 7.2 신용카드  ISP,  계좌이체 연동방법

- 신용카드 ISP 및 계좌이체 앱이 종료 된 뒤, 가맹점 앱을 다시 띄우기 위한 조치사항을 안내합니다.
- IOS 는 Android 계열과 다르게도 ISP 및 계좌이체 앱이 종료된 뒤, 가맹점 앱은 Background 에 머문 채, 바탕화면이 개제됩니다.
  (IOS의 운영체제 특성에 기반) 이 때문에, 결제 앱이 종료되면서, 가맹점 appScheme 을 호출하도록 구성해야 합니다. 하기와 같이 셋팅 시, 요구사항과 같이 가맹점 앱이 다시 기동 됩니다. ( 신용카드, 계좌이체 동기옵션 사용시에만 설정 가능)

<table style="width: 100%;">
<colgroup>
  <col style="width: 45%;">
  <col style="width: 55%;">
</colgroup>
  <thead>
    <tr>
      <th>신용카드</th>
      <th>계좌이체</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">P_RESERVED=app_scheme=가맹점스키마명://</code></td>
      <td>
<code class="language-plaintext highlighter-rouge">P_RESERVED=iosapp=Y&amp;app_scheme=가맹점스키마명://</code><br> <code class="language-plaintext highlighter-rouge">P_RETURN_URL=가맹점스키마명://</code>
</td>
    </tr>
  </tbody>
</table>

- P_RESERVED 옵션에 대한 설명은 ([1-3. 결제창 Open (주문정보 전달) - 복합필드](/mobile02.html#6-복합-필드)) 를 참조 부탁 드립니다.<br>
  더불어 상기 옵션 셋팅 시, 가맹점스키마명 뒤 ://은 필수로 입력해 주셔야 ISP 앱 종료 후 가맹점 앱이 호출 됩니다.<br>
  (Ex. 가맹점 스키마명이 WelcomeMobile일 경우 app_scheme=WelcomeMobile:// 로 셋팅 해 주시면 됩니다.)

## 7.3 안심클릭 결제 시, 카드사 백신 앱 연동

IOS 환경에서는 카드사에서 별도로 백신을 구동하지 않습니다.<br>
따라서, 해당 부분은 체크하실 부분이 없습니다.

## 7.4 카드사 앱 연동 방법

- 안심클릭 결제 진행에 필요한 Application (앱카드 등의) 호출이 필요할 경우 아래 샘플코드를 참고 바랍니다.

<table style="width: 100%;">
<colgroup>
  <col style="width: 45%;">
  <col style="width: 55%;">
</colgroup>
  <thead>
    <tr>
      <th>주 문 정 보</th>
      <th>앱 내 소스</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>(결제창 Open (주문정보 전달) ? 복합필드) 내 참조</td>
      <td>하기 샘플 참조</td>
    </tr>
  </tbody>
</table>

<details style="cursor:pointer;">
<summary><strong>[&nbsp;펼치기&nbsp;]</strong></summary>
<div markdown="1">

```
#pragma mark UIWebViewDelegate 
-(BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType
{
    //쿠키 강제 허용
    NSHTTPCookieStorage *cookieSto = [NSHTTPCookieStorage sharedHTTPCookieStorage];
    [cookieSto setCookieAcceptPolicy:NSHTTPCookieAcceptPolicyAlways];
    
    //웰컴페이먼츠를 통해 전달되는 URL   
    NSString *URLString = [NSString stringWithString:[request.URL absoluteString]];
        
    
    //URL을 읽어왔을 때 애플 스토어 주소인 경우 사파리에 해당 URL을 넘겨서 앱스토어에서 설치 할 수 있도록 유도
    BOOL isStoreURL = ([URLString rangeOfString:@"phobos.apple.com" options:NSCaseInsensitiveSearch].location != NSNotFound);
    BOOL isStoreURL2 = ([URLString rangeOfString:@"itunes.apple.com" options:NSCaseInsensitiveSearch].location != NSNotFound);
        
    //앱스토어 이동
    if (isStoreURL || isStoreURL2) {
        [[UIApplication sharedApplication]openURL:request.URL];
        return NO;
    }   
    else if([URLString hasPrefix:@"http"] || [URLString hasPrefix:@"https"] || [URLString hasPrefix:@"about"] )      //일반적인 웹url 형태인 경우 진행
    {
        return YES;
    }    
    else{     //그 외의 값은 앱스키마로 간주하여 앱 호출
        
        NSURL *appURL = [NSURL URLWithString:URLString];    //NSString to NSURL      
 
	//앱스키마인 경우 앱 호출
        BOOL bAppScheme =  [[UIApplication sharedApplication] canOpenURL:appURL];   
        
        if (!bAppScheme) {
//앱이 설치되지 않은 경우 앱스토어로 이동 또는 안내 알럿 표출   
            
            return NO;
            
        }
        
    }
    
    return YES;
}

```
</div>
</details>

- 해당 샘플은 참고용으로 각 가맹점 앱에 맞게 구현하시면 됩니다.
- 또한, 하기의 조건을 충족하는 경우에 결제가 가능하오니, 이점 유의 바랍니다.

    1. 고객 단말기의 OS 버전이 4.x 이상인 경우
    2. 가맹점 Application 이 Multi switching 이 지원되는 경우
    3. OS 버전이 9.x 이상일 경우 하기 &#39;[1-6. IOS9 Application 구현 시, 확인사항](#76-ios9-버전-application-구현-시-주의-사항)&#39; 내용을 참고 바랍니다.

## 7.5 쿠키 설정

Mobile Web 서비스를 IOS WebView 에서 호출하고, 안심클릭 계열 서비스를 사용하는 경우,<br>
세션만료 오류경고가 발생할 수 있습니다. 이에, 하기의 샘플과 같이 쿠키를 허용해야 합니다.

```
(BOOL)application:(UIApplication *)application
didFinishLaunchingWithOptions:(NSDictionary  *)launchOptions    
{
  [[NSHTTPCookieStorage sharedHTTPCookieStorage]
  setCookieAcceptPolicy:NSHTTPCookieAcceptPolicyAlways];  
  ...
  return YES;
}
```

## 7.6 IOS9 버전 Application 구현 시, 주의 사항

- IOS9 업데이트 이후, APP 내 보안정책 강화로 canOpenUrl 또는 openUrl 함수 사용 시, info.plist 파일에 LSApplicationQueriesSchemes 배열을 정의하여 호출할 App scheme list를 등록 해주셔야 합니다. (White List 등록)
  아래는 LSApplicationQueriesSchemes 등록 예시이며, 기존 앱 스키마에서 `://` 부분을 제거 후, 등록하시면 됩니다.

예시 1. XCODE info.plist
```javascript
<key> LSApplicationQueriesSchemes </key>
     <array>
           <string> fbapi </string>
<string> fbauth2 </string>
<string> fbshareextension </string>
<string> fb-messenger-api </string>
<string> twitter </string>
<string> whatsapp </string>
<string> wechat </string>
<string> line </string>
<string> instagram </string>
<string> kakaotalk </string>
<string> mqq </string>
<string> vk </string>
<string> mqq </string>
     </array>
```

예시 2. XML info.plist

- 아래 MOBILETX 에서 사용 중인 Custom Scheme List를 참고하셔서 지불수단 별, 필요한 부분사용 바랍니다.

&lt;2021.09.06 Custom Scheme List&gt;

#### Custom Scheme List (지불수단 : 신용카드)

<details style="cursor:pointer;">
<summary><strong>[&nbsp;펼치기&nbsp;]</strong></summary>
<div markdown="1">

<table style="width: 100%;">
<colgroup>
  <col style="width: 40%;">
  <col style="width: 60%;">
</colgroup>
  <thead>
    <tr>
      <th>App</th>
      <th>custom scheme</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>신한 앱카드</td>
      <td><code class="language-plaintext highlighter-rouge">shinhan-sr-ansimclick://</code></td>
    </tr>
    <tr>
      <td>신한 공인인증 앱<br>( 일반결제 )</td>
      <td><code class="language-plaintext highlighter-rouge">smshinhanansimclick://</code></td>
    </tr>
    <tr>
      <td>현대 앱카드</td>
      <td><code class="language-plaintext highlighter-rouge">hdcardappcardansimclick://</code></td>
    </tr>
    <tr>
      <td>현대 공인인증 앱<br>( 일반결제 )</td>
      <td><code class="language-plaintext highlighter-rouge">smhyundaiansimclick://</code></td>
    </tr>
    <tr>
      <td>삼성 앱카드</td>
      <td><code class="language-plaintext highlighter-rouge">mpocket.online.ansimclick://</code></td>
    </tr>
    <tr>
      <td>삼성 공인인증 앱<br>( 일반결제 )</td>
      <td><code class="language-plaintext highlighter-rouge">scardcertiapp://</code></td>
    </tr>
    <tr>
      <td>하나 앱카드</td>
      <td><code class="language-plaintext highlighter-rouge">cloudpay://</code></td>
    </tr>
    <tr>
      <td>하나 공인인증 앱<br>( 일반결제 )</td>
      <td><code class="language-plaintext highlighter-rouge">hanaskcardmobileportal://</code></td>
    </tr>
    <tr>
      <td>농협 공인인증 앱<br>( 일반결제 )</td>
      <td><code class="language-plaintext highlighter-rouge">nonghyupcardansimclick://</code></td>
    </tr>
    <tr>
      <td>국민 앱카드</td>
      <td><code class="language-plaintext highlighter-rouge">kb-acp://</code></td>
    </tr>
    <tr>
      <td>롯데 앱카드</td>
      <td><code class="language-plaintext highlighter-rouge">lotteappcard://</code></td>
    </tr>
    <tr>
      <td>롯데 스마트 페이</td>
      <td><code class="language-plaintext highlighter-rouge">lottesmartpay://</code></td>
    </tr>
    <tr>
      <td>KPAY</td>
      <td><code class="language-plaintext highlighter-rouge">kpay://</code></td>
    </tr>
    <tr>
      <td>ISP</td>
      <td><code class="language-plaintext highlighter-rouge">ispmobile://</code></td>
    </tr>
    <tr>
      <td>PayPin</td>
      <td><code class="language-plaintext highlighter-rouge">paypin://</code></td>
    </tr>
    <tr>
      <td>PAYCO</td>
      <td><code class="language-plaintext highlighter-rouge">payco://</code></td>
    </tr>
    <tr>
      <td>Syrup 앱카드</td>
      <td><code class="language-plaintext highlighter-rouge">tswansimclick://</code></td>
    </tr>
    <tr>
      <td>농협 앱카드<br>(  올원페이 )</td>
      <td><code class="language-plaintext highlighter-rouge">nhallonepayansimclick://</code></td>
    </tr>
    <tr>
      <td>씨티 앱카드</td>
      <td><code class="language-plaintext highlighter-rouge">citimobileapp://</code></td>
    </tr>
    <tr>
      <td>LPAY LPOINT</td>
      <td><code class="language-plaintext highlighter-rouge">lpayapp:// lmslpay://</code></td>
    </tr>
    <tr>
      <td>카카오페이</td>
      <td><code class="language-plaintext highlighter-rouge">kakaotalk://</code></td>
    </tr>
    <tr>
      <td>SSGPAY</td>
      <td><code class="language-plaintext highlighter-rouge">shinsegaeeasypayment://</code></td>
    </tr>
    <tr>
      <td>우리 WON 카드</td>
      <td><code class="language-plaintext highlighter-rouge">com.wooricard.wcard://</code></td>
    </tr>
    <tr>
      <td>Liiv(KB국민은행)</td>
      <td><code class="language-plaintext highlighter-rouge">liivbank://</code></td>
    </tr>
    <tr>
      <td>토스뱅크 ( 하나카드 )</td>
      <td><code class="language-plaintext highlighter-rouge">supertoss://</code></td>
    </tr>
    <tr>
      <td>KB 국민은행  Liiv Reboot</td>
      <td><code class="language-plaintext highlighter-rouge">newliiv://</code></td>
    </tr>
    <tr>
      <td>우리  WON  뱅킹</td>
      <td><code class="language-plaintext highlighter-rouge">NewSmartPib://</code></td>
    </tr>
  </tbody>
</table>

</div>
</details>