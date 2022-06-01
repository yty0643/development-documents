# 들어가며

[CORS](https://github.com/yty0643/development-documents/blob/main/cors.md)문서에서 다루었듯 CORS에러가 발생하면 해결하는 방법이 여러가지 있다.
그 중에서 proxy를 활용하는 방법을 기록하고자 한다.

---

# 프록시 (proxy)

프록시 는 '대리', '대신' 이라는 뜻을 가진다.
주로 보안상의 문제를 방지하기 위해, 직접 통신하지 않고 중계자를 거친다는 개념이다.
이 때 중계의 기능을 하는 것이 프록시 서버 이다.

**클라이언트가 프록시 서버를 서버와 같은 Origin으로 등록하고 리소스를 받아오면 브라우저 입장에선 프록시 서버와 서버의 origin을 same-origin으로 판단하고 cors에러를 일으키지 않는 것이다.**

---

# 구성 방법

CRA로 앱을 구성하면 `package.json`에 다음 한 줄을 추가하는 것으로 proxy설정을 할 수 있다.

```javascript
"proxy": "https://testapi.openbanking.or.kr"
```

하지만 Typescript template을 추가하여 CRA를 구성할 경우 위의 방법으로는 해결할 수 없고,
proxy 미들웨어를 설치하고 `src/setupProxy.js`를 작성해야 한다.

```bash
npm install http-proxy-middleware --save
# or
yarn add http-proxy-middleware

```

`src/setupProxy.js`을 다음과 같이 추가한다.

```javascript
const { createProxyMiddleware } = require("http-proxy-middleware");

module.exports = function (app) {
  app.use(
    "/api",
    createProxyMiddleware({
      target: "https://testapi.openbanking.or.kr",
      changeOrigin: true,
    })
  );
};
```

---

## 참고문헌

- https://create-react-app.dev/docs/proxying-api-requests-in-development/#configuring-the-proxy-manually
