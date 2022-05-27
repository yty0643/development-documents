# 리덕스 툴킷 (Redux Toolkit | RTK)

리덕스 툴킷은 리덕스 로직을 작성하는 표준 방식으로 만들어졌고, 리덕스에 대한 세 가지 일반적인 문제를 해결하기 위해 만들어졌다.

- 리덕스 스토어 구성이 너무 복잡하다.
- 리덕스에서 유용한 작업을 수행하려면 많은 패키지를 추가해야한다.
- 리덕스에는 너무 많은 상용구 코드가 필요하다. (많은 보일러플레이트)

**결국 `RTK`는 리덕스 코드를 개선하기 위해 만들어진 것이다.**

---

# Create React App

React 및 Redux로 새 앱을 시작하는 권장 방법은 공식 Redux+JS 템플릿 또는 Create React App 용 Redux+TS 템플릿 을 사용하는 것이다. 이 템플릿 은 Redux Toolkit 및 React Redux와 React 구성 요소의 통합을 활용한다.

```bash
# Redux + Plain JS template
npx create-react-app my-app --template redux

# Redux + TypeScript template
npx create-react-app my-app --template redux-typescript
```

Redux Toolkit은 모듈 번들러 또는 노드 애플리케이션과 함께 사용하기 위해 NPM에서 패키지로 사용할 수 있다.

```bash
# NPM
npm install @reduxjs/toolkit

# Yarn
yarn add @reduxjs/toolkit
```

# RTK 키워드

- configureStore()createStore: 단순화된 구성 옵션과 좋은 기본값을 제공하기 위해 래핑 합니다. 슬라이스 리듀서를 자동으로 결합하고, 제공하는 모든 Redux 미들웨어를 추가하고, redux-thunk기본적으로 포함하고, Redux DevTools Extension을 사용할 수 있습니다.
- createReducer(): switch 문을 작성하는 대신 대소문자 감소 함수에 작업 유형의 조회 테이블을 제공할 수 있습니다. 또한 immer라이브러리 를 자동으로 사용하여 state.todos[3].completed = true.
- createAction(): 주어진 액션 유형 문자열에 대한 액션 생성자 함수를 생성합니다. 함수 자체가 toString()정의되어 있으므로 형식 상수 대신 사용할 수 있습니다.
- createSlice(): 리듀서 함수의 객체, 슬라이스 이름, 초기 상태 값을 받아들이고 해당 액션 생성자와 액션 유형으로 슬라이스 리듀서를 자동으로 생성합니다.
- createAsyncThunk: 작업 유형 문자열과 약속을 반환하는 함수를 수락하고 pending/fulfilled/rejected해당 약속을 기반으로 작업 유형 을 전달하는 썽크를 생성합니다.
- createEntityAdapter: 저장소에서 정규화된 데이터를 관리하기 위해 재사용 가능한 리듀서 및 선택기 세트를 생성합니다.
  Reselect 라이브러리 의 createSelector유틸리티 는 사용하기 쉽도록 다시 내보냅니다.
