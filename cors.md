# CORS

교차 출처 리소스 공유 (Cross-Origin Resource Sharing, CORS)는 추가 HTTP 헤더를 사용하여, 한 출처에서 실행 중인 웹 어플리케이션이 다른 출처의 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제이다. 웹 애플리케이션은 리소스가 자신의 출처(도메인, 프로토콜, 포트)와 다를 때 교차 출처 HTTP 요청을 실행한다.

> ## 출처 (Origin)
>
> ![origin](https://user-images.githubusercontent.com/80657819/171400716-6498ad5f-6740-4c9f-b1cf-ded7c9f79db5.jpg)
> 교차 출처 요청의 예시 https://domain-a.com의 프론트 엔드 JavaScript 코드가 XMLHttpRequest를 사용하여 https://domain-b.com/data.json을 요청하는 경우.

보안 상의 이유로 브라우저는 스크립트에서 시작한 교차 출처 HTTP 요청을 제한한다. 예를 들어, XMLHttpRequest와 Fetch API는 동일 출처 정책을 따른다. 즉, 이 API를 사용하는 웹 어플리케이션은 자신의 출처와 동일한 리소스만 불러올 수 있으며, 다른 출처의 리소스를 불러오려면 그 출처에서 올바른 CORS 헤더를 포함한 응답을 반환해야 한다.

CORS 체제는 브라우저와 서버 간의 안전한 교차 출처 요청 및 데이터 전송을 지원한다. 최신 브라우저는 XMLHttpRequest 또는 Fetch와 같은 API에서 CORS를 사용하여 교차 출처 HTTP 요청의 위험을 완화한다.

> 옳바르지 않은 방법으로 다른 출처의 리소를 불러오려는 시도를 하면 다음과 같은 에러가 발생한다. (웹 개발자라면 누구나 한번쯤은 겪는 에러라고 생각한다.)
>
> Access to fetch at ‘https://...api.com/auth...’Visit Website from origin ‘http://localhost:3000’ has been blocked by CORS policy: No ‘Access-Control-Allow-Origin’ header is present on the requested resource. If an opaque response serves your needs, set the request’s mode to ‘no-cors’ to fetch the resource with CORS disabled.
> 'https://...api.com/auth...'에서 오리진 'https://localhost:3000'으로 가져올 수 있는 액세스가 CORS 정책에 의해 차단되었습니다. 요청된 리소스에 'Access-Control-Allow-Origin' 헤더가 없습니다. 불투명한 응답이 필요에 적합한 경우, 요청 모드를 '노코어'로 설정하여 CORS가 비활성화된 리소스를 가져오십시오.
