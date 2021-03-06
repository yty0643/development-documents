# 들어가며

비동기 HTTP 통신 라이브러리인 Axios에 대해 조사하다
동기, 비동기 통신, Ajax 에 대한 정리도 필요성을 느껴서 본 문서에 작성했다.

---

# 통신 방법

## 동기(Synchronous)

동기식 통신 및 동기식 프로그래밍이란 동시에 일어난다는 뜻이다.
동시에 일어난다는 것은 `Request` 이후 얼마가 걸리든 `Response`를 기다리겠다는 말로 클라이언트, 서버 사이의 Transaction을 맞추겠다는 뜻이다.

그 뜻은 `Request`를 보낸 Thread는 `Response`가 도착하기 전까지는 아무것도 하지 못하는 Block 상태가 됨을 의미한다.
​
그렇게 되면 해당 Thread는 `Request`를 보내고 `Response`를 받고 `Request`를 다시 보내는 작업을 수행하게 된다.
이는 요청과 응답값의 순서를 보장하게 된다. 또한 보낸 `Request`에 대한 처리 결과 값을 보장 받을 수 있다. 이는 요청 값에 대해 성공, 실패 및 처리 결과에 대해 변경되는 사항이 있는 경우엔 굉장히 중요한 요소이다.
​
이러한 특징의 단점으로는 `Response`가 지연되게 된다면 `Request`를 보낸 Thread는 해당 `Response`를 무작정 기다리는 상태가 된다는 것이다. 순차적으로 `Response`를 받고 `Request`를 받는 구조로 `Response`가 계속 지연되게 된다면 뒤에 들어오는 요청들은 Connection 가능한 Thread가 없어 연결을 맺지 못하는 성능 적인 이슈가 발생 할 수 있다.

## 비동기(Asynchronous)

비동기식 통신 및 동기식 프로그래밍이란 동시에 수행하지 않는다는 뜻이다.
동기식과는 반대로 `Request` 이후에 `Response`를 기다리지 않는 상태이다.
​
`Response`를 기다리지 않으니 `Request`를 보낸 Thread는 다른 일을 할 수 있다. 이러한 상태를 `Non Block` 상태라고 한다.
​
Thread가 `Response`를 받지 않고 여러가지 `Request`를 보냈을때 뒤에 보낸 `Request`가 먼저 처리가 되었다면 뒤에 `Request`에 대한 `Response`이 먼저 올 수도 있다. 이러한 특징으로 비동기식 통신은 순서를 보장 하지 않는다.
​
비동기식 방식은 동기식 방식에 비해 성능적으로 좋을 수 밖에 없다. 하지만 `Response`에 대한 처리 결과를 보장받고 처리해야 되는 서비스에는 적합하지 않다.

---

# Ajax

기존의 웹 애플리케이션은 브라우저에서 폼을 채우고 이를 웹 서버로 제출(submit)을 하면 하나의 요청으로 웹 서버는 요청된 내용에 따라서 데이터를 가공하여 새로운 웹 페이지를 작성하고 응답으로 되돌려준다. 이때 최초에 폼을 가지고 있던 페이지와 사용자가 이 폼을 채워 결과물로서 되돌려 받은 페이지는 일반적으로 유사한 내용을 가지고 있는 경우가 많다. 결과적으로 중복되는 HTML 코드를 다시 한번 전송을 받음으로써 많은 대역폭을 낭비하게 된다. 대역폭의 낭비는 금전적 손실을 야기할 수 있으며 사용자와 대화(상호 반응)하는 서비스를 만들기 어렵게도 한다.

반면에 `Ajax` 애플리케이션은 필요한 데이터만을 웹서버에 요청해서 받은 후 클라이언트에서 데이터에 대한 처리를 할 수 있다. 보통 SOAP이나 XML 기반의 웹 서비스 프로토콜이 사용되며, 웹 서버의 응답을 처리하기 위해 클라이언트 쪽에서는 자바스크립트를 쓴다. 웹 서버에서 전적으로 처리되던 데이터 처리의 일부분이 클라이언트 쪽에서 처리 되므로 웹 브라우저와 웹 서버 사이에 교환되는 데이터량과 웹서버의 데이터 처리량도 줄어들기 때문에 애플리케이션의 응답성이 좋아진다. 또한 웹서버의 데이터 처리에 대한 부하를 줄여주는 일이 요청을 주는 수많은 컴퓨터에 대해서 일어나기 때문에 전체적인 웹 서버 처리량도 줄어들게 된다.

**요약하자면** `Ajax`란, Javascript의 라이브러리중 하나로 Asynchronous Javascript And Xml (비동기식 자바스크립트와 xml)의 약자이다. 브라우저가 가진 XMLHttpRequest객체를 이용해서 전체 페이지를 새로 고치지 않고도 페이지의 일부만을 위한 데이터를 로드하는 기법이며, Javascript를 사용한 통신, 클라이언트와 서버간에 XML 데이터를 주고받는 기술이다.

---

# Axios

Axios는 브라우저, Node.js를 위해서 만들어진 Promise API를 활요하는 HTTP 비동기 통신 라이브러리이다. (백엔드와 프론드엔드간에 통신을 위해서 만들어진 AJAX도 더불어 사용하기도 한다.)

`Fetch`와의 차이점

- Axios는 요청 객체에 URL을 가지고 있습니다.
  > Fetch는 요청 개체에 URL이 없습니다.
- Axios는 쉽게 설치할 수 있는 독립 실행형 타사 패키지 입니다.
  > Fetch는 대부분의 최신 브라우저에 내장되어 있습니다.
- Axios는 내장된 XSRF 보호 기능이 있다.
  > Fetch는 없습니다.
- Axios는 데이터 속성을 사용합니다.
  > Fetch는 body 속성을 사용합니다.
- Axios의 데이터에는 객체가 포함되어 있습니다.
  > Fetch의 본문은 문자열화 되어야 합니다.
- Axios는 상태가 200 이고 statusText가 'OK' 일 때 요청이 정상 입니다.
  > Fetch는 응답 객체에 ok 속성이 포함되어 있으면 요청이 정상 입니다.
- Axios 는 JSON 데이터의 자동 변환을 수행합니다 .
  > Fetch는 응답에서 .json() 메서드를 호출합니다.
- Axios는 요청 취소 및 요청 시간 초과를 허용 합니다.
  > Fetch는 허용하지 않습니다.
- Axios에는 HTTP 요청을 가로챌 수 있는 기능이 있습니다.
  > Fetch는 기본적으로 요청을 가로채는 방법을 제공하지 않습니다.
- Axios에는 다운로드 진행률에 대한 지원이 내장되어 있습니다.
  > Fetch는 업로드 진행률을 지원하지 않습니다.
- Axios는 광범위한 브라우저를 지원 합니다.
  > Fetch.AI는 Chrome 42 이상, Firefox 39 이상, Edge 14 이상 및 Safari 10.1 이상만 지원합니다(이를 이전 버전과의 호환성이라고 함).

```bash
$ yarn add axios
```

> @types/axios를 설치하려고 하면 다음과 같은 문구가 나온다. <br/>
> axios provides its own type definitions, so you don't need @types/axios installed! <br/>
> axios는 자체적인 유형 정의를 제공하므로 @types/codos를 설치할 필요가 없습니다! <br/> > **즉, @types/axios를 따로 설치할 필요가 없다.**

### Axios 예제

```typescript
import axios from "axios";

export default class Finance {
  auth() {
    // get method를 사용하는 가장 기본적인 형식이다.
    const config = {
      // url의 경우 필자는 proxy server를 사용중이라 origin은 작성하지 않는다.
      url: "/v2.0/user/me",
      method: "get",
      data: {
        foo: "diary",
      },
    };

    axios(config);
  }
}
```

```typescript
import axios from "axios";

export default class Finance {
  auth() {
    // 다음과 같이 method를 분리하여 사용함으로써 더욱 직관적인 작성이 가능하다.
    axios.get("/v2.0/user/me", {
      params: {
        user_seq_no: "1101007181",
      },
      headers: {
        // "key": "value",
      },
    });
  }
}
```

```typescript
import axios from "axios";

export default class Finance {
  // async/await을 사용하고 싶다면 다음과 같다.
  async auth() {
    try(
      const res = await axios.get('/v2.0/user/me', {
        params: {
          'user_seq_no': '1101007181'
        },
        headers: {
          // "key": "value",
        }
      });
      console.log(res);
    )catch(error){
      console.log(error);
    }
  }
}

```

---
