# 리덕스(Redux)

현업에서 그리고 많은 개발자들이 리덕스를 사용하고 있기 때문에 리덕스를 공부하고자 한다.
프로젝트에 적용하기 앞서 왜 리덕스를 사용하는지, 리덕스의 컨셉과 특징이 무엇인지에 대해 공부하고 기록하고자한다.

---

## 리덕스란?

리덕스는 리액트 생태계에서 가장 사용률이 높은 상태관리 라이브러리이다.

리덕스를 사용하면 만들게 될 컴포넌트들의 상태 관련 로직들을 다른 파일들로 분리시켜서 더욱 효율적으로 관리 할 수 있으며 글로벌 상태 관리도 손쉽게 할 수 있다.

> `yarn add redux react-redux @types/react-redux` 로 리덕스 라이브러리 추가
>
> 리덕스 개발자 도구를 사용하면 현재 스토어의 상태를 개발자 도구에서 조회 할 수 있고 지금까지 어떤 액션들이 디스패치 되었는지, 그리고 액션에 따라 상태가 어떻게 변화했는지 확인 할 수 있다. 추가적으로, 액션을 직접 디스패치 할 수도 있다.
>
> 1. 크롬 웹 스토어에서 확장프로그램을 설치한다.
> 2. `yarn add redux-devtools-extension` 로 라이브러리 추가한다.
> 3. index.tsx에 `const store = createStore(rootReducer, composeWithDevTools());`로 수정한다.

---

## 리덕스가 필요한 이유는?

리액트 프로젝트에서는 대부분의 작업을 할 때 부모 `component`가 중간자 역할을 한다. (컴포넌트끼리 직접 소통하는 방법도 있지만 권장하지 않는 방식이다.) 부모 컴포넌트에서 `state` 및 `state`를 업데이트하는 함수를 생성하고 이를 자식 `component`에 전달하는 방식으로 `state`를 관리하는데, 이러한 방식은 꽤나 직관적이고 편리하다. 하지만 문제는 프로젝트의 규모가 커졌을 때 발생한다. 다루는 `component`와 `props`가 늘어나면 `props`를 부모에서 자식으로, 또 자식에서 그 자식으로, 또 자식에서 자식으로... 매번 중복되는 코드를 작성하게되며 코드량이 증가한다. 또한 `props`의 이름을 수정하려면 `props`전달에 관련된 모든 `component` 파일을 열어서 이름을 수정해야 하는 번거로움이 발생한다. 이처럼 유지보수에도 큰 어려움이 발생한다.

<img width="400" alt="캡처" src="https://user-images.githubusercontent.com/80657819/170632774-9ccdc57a-1cbd-40af-97be-41d16d0732c0.PNG">

리덕스를 사용하면 `state`관련 로직을 다른 파일로 분리하기 때문에 `props`를 `component`에 종속시키지 않아도 된다.
즉 부모에서 자식으로 `props`를 전달하는 과정이 필요가 없고, 유지보수에 큰 도움이 된다.

---

## 리덕스의 세가지 규칙

### 하나의 애플리케이션에선 단 한개의 스토어를 만들어서 사용한다.

여러개의 스토어를 사용하는것은 사실 가능하기는 하나, 권장되지 않는다. 특정 업데이트가 너무 빈번하게 일어나거나, 애플리케이션의 특정 부분을 완전히 분리시키게 될 때 여러개의 스토어를 만들 수도 있다. 하지만 그렇게 하면, 개발 도구를 활용하지 못하게 된다.

### 상태는 읽기전용이다.

리액트에서 state 를 업데이트 해야 할 때, setState 를 사용하고, 배열을 업데이트 해야 할 때는 배열 자체에 push 를 직접 하지 않고, concat 같은 함수를 사용하여 기존의 배열은 수정하지 않고 새로운 배열을 만들어서 교체하는 방식으로 업데이트를 한다 엄청 깊은 구조로 되어있는 객체를 업데이트를 할 때도 마찬가지로, 기존의 객체는 건드리지 않고 Object.assign 을 사용하거나 spread 연산자 (...) 를 사용하여 업데이트 한다.

리덕스에서도 마찬가지로 기존의 상태는 건드리지 않고 새로운 상태를 생성하여 업데이트 해주는 방식으로 해주면, 나중에 개발자 도구를 통해서 뒤로 돌릴 수도 있고 다시 앞으로 돌릴 수도 있다.

리덕스에서 불변성을 유지해야 하는 이유는 내부적으로 데이터가 변경 되는 것을 감지하기 위하여 shallow equality 검사를 하기 때문이다. 이를 통하여 객체의 변화를 감지 할 때 객체의 깊숙한 안쪽까지 비교를 하는 것이 아니라 겉핥기 식으로 비교를 하여 좋은 성능을 유지할 수 있다.

### 변화를 일으키는 함수, 리듀서는 순수한 함수여야 한다.

리듀서 함수는 이전 상태와, 액션 객체를 파라미터로 받는다.
이전의 상태는 절대로 건들이지 않고, 변화를 일으킨 새로운 상태 객체를 만들어서 반환한다.
똑같은 파라미터로 호출된 리듀서 함수는 언제나 똑같은 결과값을 반환해야만 한다.

> **3가지 주의사항**<br/>
> 동일한 인풋이라면 언제나 동일한 아웃풋이 있어야 한다. 일부 로직들 중에서는 실행 할 때마다 다른 결과값이 나타날 수도 있는데,
> new Date() 를 사용한다던지 랜덤 숫자를 생성한다던지 혹은, 네트워크에 요청을 한다던지 그러한 작업은 결코 순수하지 않은 작업이므로,
> 리듀서 함수의 바깥에서 처리해줘야 한다. 그런것을 하기 위해서, 리덕스 미들웨어 를 사용하곤 한다.
> <br/>_본 페이지에서는 미들웨어를 다루지 않는다._

---

## 리덕스에서 사용되는 키워드

### 액션 (Action)

상태에 어떠한 변화가 필요하게 될 땐, 액션을 발생시킨다. 이는 하나의 객체로 다음과 같은 형식으로 이루어져 있다.

```javascript
{
  type: "TOGGLE_VALUE";
}
```

액션 객체는 `type` 필드를 필수적으로 가지고 있어야하고, 그 외의 값들은 개발자 마음대로 넣을 수 있다.

```javascript
{
  type: "ADD_TODO",
  data: {
    id: 0,
    text: "리덕스 배우기"
  }
}
```

```javascript
{
  type: "CHANGE_INPUT",
  text: "안녕하세요"
}
```

### 액션 생성 함수 (Action creator)

액션 생성함수는, 액션을 만드는 함수이다. 단순히 파라미터를 받아와서 액션 객체 형태로 만들어준다.

```javascript
export function addTodo(data) {
  return {
    type: "ADD_TODO",
    data,
  };
}

// 화살표 함수로도 만들 수 있다.
export const changeInput = (text) => ({
  type: "CHANGE_INPUT",
  text,
});
```

이러한 액션 생성 함수를 만들어서 사용하는 이유는 나중에 컴포넌트에서 더욱 쉽게 액션을 발생시키기 위함이다. 그래서 보통 함수앞에 `export`키워드를 붙여서 다른 파일에서 불러와서 사용한다.

리덕스를 사용할 때 액션 생성 함수를 사용하는 것이 필수적이진 않다.
액션을 발생시킬 때마다 직접 액션 객체를 작성할 수도 있다.

### 리듀서 (Reducer)

리듀서는 변화를 일으키는 함수이다. 리듀서는 두가지 파라미터를 받아온다.

```javascript
function reducer(state, action) {
  // 상태 업데이트 로직
  return alteredState;
}
```

리듀서는 현재의 상태와 전달받은 액션을 참고하여 새로운 상태를 만들어서 반환한다.

만약 카운터를 위한 리듀서를 작성한다면 다음과 같이 작성할 수 있다.

```javascript
function counter(state, action) {
  switch (action.type) {
    case "INCREASE":
      return state + 1;
    case "DECREASE":
      return state - 1;
    default:
      return state;
  }
}
```

> 리덕스를 사용 할 때에는 여러개의 리듀서를 만들고 이를 합쳐서 루트 리듀서 (Root Reducer)를 만들 수 있다. (루트 리듀서 안의 작은 리듀서들은 서브 리듀서라고 부른다.)

### 스토어 (Store)

스토어 안에는 현재의 앱 `state`, `reducer`가 들어가 있고, 추가적으로 몇가지 내장 함수가 있다.

### 디스패치 (dispatch)

디스패치는 스토어의 내장함수 중 하나로, 액션을 발생 시킨다. `dispatch` 라는 함수에는 액션을 파라미터로 전달한다. `dispatch(action)` 이런식이다.
호출을 하면 스토어는 리듀서 함수를 실행시켜서 해당 액션을 처리하는 로직이 있다면 액션을 참고하여 새로운 상태를 만들어준다.

### 구독 (subscribe)

구독 또한 스토어의 내장함수 중 하나로, 함수 형태의 값을 파라미터로 받아온다. `subscribe` 함수에 특정 함수를 전달해주면, 액션이 디스패치 되었을 때 마다 전달해준 함수가 호출된다.

리액트에서 리덕스를 사용하게 될 때 보통 이 함수를 직접 사용하는 일은 별로 없다. 그 대신에 `react-redux` 라는 라이브러리에서 제공하는 `connect` 함수 또는 `useSelector Hook` 을 사용하여 리덕스 스토어의 상태에 구독한다.

---

## 예제 (리덕스 모듈 만들기)

리덕스를 타입스크립트와 함께 사용하고, 마우스 호버에 대한 상태를 리덕스 모듈로 작성하는 기본적인 예제를 직접 작성해 보았다.

리덕스를 모듈로 나누어 개발할 때는 `modules`라는 폴더 안에 각각의 모듈을 작성하고, `modules/index.ts`안에 `rootReducer`를 작성하면 된다.

> 주석을 잘 읽어보길 바란다.

### index.tsx

```typescript
// 한개의 앱에 하나의 스토어만 사용한다.
const store = createStore(rootReducer);

// 리액트와 리덕스로 개발할 때는 App을 Provider로 감싸주고 props로 store를 전달한다.
root.render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>
);
```

### modules/hover.ts

```typescript
// 뒤에 as const 를 붙여줌으로써 나중에 액션 객체를 만들게 action.type 의 값을 추론하는 과정에서
// action.type 이 string 으로 추론되지 않고 'counter/INCREASE' 와 같이 실제 문자열 값으로 추론 되도록 해준다.
const MOUSE_ENTER = "hover/MOUSE_ENTER" as const;
const MOUSE_LEAVE = "hover/MOUSE_LEAVE" as const;

// 액션 생성함수의 부가적인 데이터 payload 통일
// 이는 FSA (https://github.com/redux-utilities/flux-standard-action) 라는 규칙이다.
export const mouseEnter = () => ({
  type: MOUSE_ENTER,
  // payload:{

  // },
});

export const mouseLeave = () => ({
  type: MOUSE_LEAVE,
});

// 모든 액션 겍체들에 대한 타입
// ReturnType<typeof _____> 는 특정 함수의 반환값을 추론한다.
// 상단부에서 액션타입을 선언 할 떄 as const 를 하지 않으면 이 부분이 제대로 작동하지 않는다.
type hoverAction =
  | ReturnType<typeof mouseEnter>
  | ReturnType<typeof mouseLeave>;

const initialState = {
  isHover: false,
  msg: "",
};

// 초기상태 선언
type hoverState = {
  isHover: boolean;
  msg: string;
};

// 리듀서 작성
// 리듀서에서는 state 와 함수의 반환값이 일치하도록 작성한다.
// 액션에서는 우리가 방금 만든 CounterAction 을 타입으로 설정한다.
const hover = (
  state: hoverState = initialState,
  action: hoverAction
): hoverState => {
  switch (action.type) {
    case MOUSE_ENTER:
      return {
        isHover: true,
        msg: "mouse enter!",
      };
    case MOUSE_LEAVE:
      return {
        isHover: false,
        msg: "mouse leave!",
      };
    default:
      return state;
  }
};

export default hover;
```

### modules/index.ts

```typescript
import { combineReducers } from "redux";
import hover from "./hover";

const rootReducer = combineReducers({
  hover,
});

// 루트 리듀서를 내보내기.
export default rootReducer;

// 루트 리듀서의 반환값를 유추한다.
// 추후 이 타입을 컨테이너 컴포넌트에서 불러와서 사용해야 하므로 내보내준다.
export type RootState = ReturnType<typeof rootReducer>;
```

### components/test.tsx

```typescript
import React, { useEffect } from "react";
import { useDispatch, useSelector } from "react-redux";
import { RootState } from "../modules";
import { mouseEnter, mouseLeave } from "../modules/hover";
import styles from "./test.module.css";

const Test = () => {
  // 랜더링체크를 위한 로그.
  console.log("Rendering!");

  // 상태를 조회한다. 상태를 조회 할 때에는 state 의 타입을 RootState 로 지정해야한다.
  const { isHover, msg } = useSelector((state: RootState) => ({
    ...state.hover,
  }));
  // 디스패치 함수를 가져온다.
  const dispatch = useDispatch();

  // 각 액션들을 디스패치하는 함수들을 만들어준다.
  const onMouseEnter = () => {
    dispatch(mouseEnter());
  };

  const onMouseLeave = () => {
    dispatch(mouseLeave());
  };

  // 어떻게 반응하는지 알아보기 위해 작성된 로그
  // store안의 상태가 궁금하다면 devtools를 설치하면 된다.
  useEffect(() => {
    console.log(isHover);
    console.log(msg);
  });

  // 이부분은 따로 리덕스 프레젠테이셔널/컨테이너 컴포넌트 두가지로 분리해서 작성해도 되는데
  // 개발할때 번거로울 것으로 판단되어 한 파일에 작성했다. (공식문서에서 굳이 분리할 필요 없다고 함)
  return (
    <div
      className={styles.box}
      onMouseEnter={onMouseEnter}
      onMouseLeave={onMouseLeave}
    ></div>
  );
};

export default React.memo(Test);
```

---

## 참고문헌

(https://react.vlpt.us/redux/)<br/>
(https://velopert.com/3528)<br/>
(https://ridicorp.com/story/how-to-use-redux-in-ridi/)<br/>
