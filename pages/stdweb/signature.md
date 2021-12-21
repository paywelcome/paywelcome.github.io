- 기본 요청데이터의 signature필드의 구성은 다음과 같습니다.

#### [1-3] signature 생성 대상(Target) 필드

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

- Signature 생성방법은 아래의 [3.3 signature 생성] 참조
  기본 요청데이터 외에 다음과 같이 결제 수단별로 옵션 값을 추가하여 결제 요청할 수 있습니다.

  
- 결제 승인 요청데이터의 signature필드의 구성은 다음과 같습니다.

#### [2-3] 승인요청 signature 생성 대상(Target) 필드
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

##### Target 데이터 예시 : `authToken=sgnWSY9uZ3c9lbkJItgiP4VdD5L+dM0+dmuv+R707vExQC5XjwjSCUOa/iT…… `

#### Signature 생성방법은 아래의 [3.3 signature 생성] 참조
