# CORS

교차 출처 리소스 공유 (Cross-Origin Resource Sharing, CORS)는 추가 HTTP 헤더를 사용하여, 한 출처에서 실행 중인 웹 어플리케이션이 다른 출처의 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제이다. 웹 애플리케이션은 리소스가 자신의 출처(도메인, 프로토콜, 포트)와 다를 때 교차 출처 HTTP 요청을 실행한다.

> ## 출처 (Origin)
>
> ![origin](https://user-images.githubusercontent.com/80657819/171400716-6498ad5f-6740-4c9f-b1cf-ded7c9f79db5.jpg)
> 교차 출처 요청의 예시 https://domain-a.com의 프론트 엔드 JavaScript 코드가 XMLHttpRequest를 사용하여 https://domain-b.com/data.json을 요청하는 경우.

보안 상의 이유로 브라우저는 스크립트에서 시작한 교차 출처 HTTP 요청을 제한한다. 예를 들어, XMLHttpRequest와 Fetch API는 동일 출처 정책을 따른다. 즉, 이 API를 사용하는 웹 어플리케이션은 자신의 출처와 동일한 리소스만 불러올 수 있으며, 다른 출처의 리소스를 불러오려면 그 출처에서 올바른 CORS 헤더를 포함한 응답을 반환해야 한다.

CORS 체제는 브라우저와 서버 간의 안전한 교차 출처 요청 및 데이터 전송을 지원한다. 최신 브라우저는 XMLHttpRequest 또는 Fetch와 같은 API에서 CORS를 사용하여 교차 출처 HTTP 요청의 위험을 완화한다.

> HTML에서는 기본적으로 Cross-Origin-Resurce-Sharing 따름
>
> XMLHTTPRequest, Fetch API 등 script 태그 내에서는 Same-Origin-Policy 따름
>
> 옳바르지 않은 방법으로 다른 출처의 리소를 불러오려는 시도를 하면 다음과 같은 에러가 발생한다. (웹 개발자라면 누구나 한번쯤은 겪는 에러라고 생각한다.)
>
> Access to fetch at ‘https://...api.com/auth...’Visit Website from origin ‘http://localhost:3000’ has been blocked by CORS policy: No ‘Access-Control-Allow-Origin’ header is present on the requested resource. If an opaque response serves your needs, set the request’s mode to ‘no-cors’ to fetch the resource with CORS disabled.
>
> 'https://...api.com/auth...'에서 오리진 'https://localhost:3000'으로 가져올 수 있는 액세스가 CORS 정책에 의해 차단되었습니다. 요청된 리소스에 'Access-Control-Allow-Origin' 헤더가 없습니다. 불투명한 응답이 필요에 적합한 경우, 요청 모드를 '노코어'로 설정하여 CORS가 비활성화된 리소스를 가져오십시오.

---

## SOP (Same-Origin-Policy)

SOP는 "동일한 출처에서만 리소스를 공유할 수 있다"는 정책이다.

> 두개의 출처를 비교하는 방법은 URL의 구성요소 중 Protocol, Host, Port 이 세가지가 동일한지 확인하면 된다.

출처를 비교하는 로직은 서버에 구현된 스펙이 아닌 브라우저에 구현된 스펙이다.
만약 CORS정책을 위반하는 요청에 서버가 정상적으로 응답을 하더라도 브라우저가 이 응답을 분석해서 CORS정책에 위반되면 그 응답은 처리하지 않게 된다.

---

## CORS 3가지 시나리오

- 예비요청 (Preflight Request)
- 단순요청 (Simple Request)
- 인증된 요청 (Credentialed Request)

### 에비요청

브라우저는 요청을 한번에 보내지 않고, 예비요청과 본요청으로 나누어 서버에 전달한다.

이때 브라우저가 예비요청을 보내는 것을 Preflight라고 부르며
이 예비요청의 메소드에는 OPTIONS가 사용된다.

예비요청의 역할은 본 요청을 보내기 전에 브라우저 스스로 안전한 요청인지 확인하는 것이다.

> 예비 요청은 보통 PUT DELETE 같은 요청을 보낼떄 이용된다.PUT이나 DELETE는 서버의 데이터를 변경해 버리는 요청이기 때문에, 코드가 돌아가게 하는 요청을 보내기전에 예비 요청을 보내서 우선 인증부터하고 본 요청을 받아 서버에서 코드가 돌아가게 하는 원리이다.

### 단순요청

단순요청은 예비 요청(Prefilght)을 보내지 않고 바로 서버에 본 요청을 한 후,
서버가 이에 대한 응답의 헤더에 Access-Control-Allow-Origin과 같은 같을 보내주면 브라우저가 CORS정책 위반여부를 검사하는 방식이다.

> 단순 요청은 GET POST같은 서버 자체 데이터가 변경될 일이 적은 요청에서 작동된다고 보면 된다.

예비요청 생략은 아부때나 할 수 있는것이 아니고 아래 3가지 경우를 만족할때만 가능하다.

- 요청의 메소드는 GET, HEAD, POST 중 하나여야 한다.
- 유저 에이전트가 자동으로 설정한 헤더외에, 수동으로 설정할 수 있는 헤더는 Fetch 명세에서 "CORS-safelisted request-header"로 정의한 헤더만 사용할 수 있다.

  > - Accept
  > - Accept-Language
  > - Content-Language
  > - Content-Type
  > - DPR
  > - Downlink
  > - Save-Data
  > - Viewport-Width
  > - Width

- Content-Type 을 사용하는 경우에는 다음의 값들만 허용된다.
  > - application/x-www-form-urlencoded
  > - multipart/form-data
  > - text/plain

### 인증된 요청

기존 예비요청에서 보안을 더 강화하고 싶을 때 사용한다.

기본적으로 브라우저가 제공하는 비동기 리소스 요청 API인 XMLHttpRequest 객체나 fetch API는
별도의 옵션 없이 브라우저의 쿠키 정보나 인증과 관련된 헤더를 함부로 요청에 담지 않는다.

요청에 인증과 관련된 정보를 담을 수 있게 해주는 옵션이 있는데 바로 credentials 옵션이다.
이 옵션은 총 3가지 값을 사용할 수 있다. (same-origin, include, omit)

만약 same-origin 이나 include와 같은 옵션을 사용하여 리소스 요청에 인증 정보가 포함된다면, 브라우저는 다른 출처의 리소를 요청할 Access-Control-Allow-Origin만 확인하는 것이 아니라 다른 조건을 추가로 검사한다.

요청에 인증정보가 담겨있는 상태에서 다른 출처의 리소스를 요청하게 되면,
브라우저는 CORS정책 위반 여부를 검사하는 룰에 다음 두가지를 추가하게 된다.

- Access-Control-Allow-Origin 에는 모든 요청을 허용하는 \* 을 사용할 수 없으며, 명시적인 URL이어야 한다
- 응답 헤더에는 반드시 Access-Control-Allow-Credentials: true가 존재해야 한다

> fetch를 사용하지 않고 axios를 사용할 땐 withCredentials:true 를 사용하여 쿠키를 전송할 수 있다.

## CORS 해결방법

- 크롬 확장 프로그램 이용
- 서버에서 Access-Control-Allow-Origin 세팅하기
- proxy 사용

---

## 참고문헌

- https://developer.mozilla.org/ko/docs/Web/HTTP/CORS

- https://inpa.tistory.com/entry/WEB-%F0%9F%93%9A-CORS-%F0%9F%92%AF-%EC%A0%95%EB%A6%AC-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95-%F0%9F%91%8F
