# useReducer

useReducer란 Hook함수로 컴포넌트의 상태 업데이트 로직을 컴포넌트에서 분리시키도록 도와주는 함수이다.

상태 업데이트 로직을 컴포넌트 바깥에 작성하거나 다른 파일에 작성하고 불러와서 사용할 수 있다.

reducer 는 현재 상태와 액션 객체를 파라미터로 받아와서 새로운 상태를 반환해주는 함수이다.

```javascript
function reducer(state, action) {
  // 새로운 상태를 만드는 로직
  // const nextState = ...
  return nextState;
}
```

reducer 에서 반환하는 상태는 곧 컴포넌트가 지닐 새로운 상태가 된다.

여기서 action 은 업데이트를 위한 정보를 가지고 있다. 주로 type 값을 지닌 객체 형태로 사용하지만, 꼭 따라야 할 규칙은 따로 없다.

```javascript
// 카운터에 1을 더하는 액션
{
    type: 'INCREMENT'
}
// 카운터에 1을 빼는 액션
{
    type: 'DECREMENT'
}
// input 값을 바꾸는 액션
{
    type: 'CHANGE_INPUT',
    key: 'email',
    value: 'tester@react.com'
}
// 새 할 일을 등록하는 액션
{
    type: 'ADD_TODO',
    todo: {
        id: 1,
        text: 'useReducer 배우기',
        done: false,
    }
}
```

useReducer의 사용법은 다음과 같다.

```javascript
const [state, dispatch] = useReducer(reducer, initialState);
```

여기서 state는 우리가 앞으로 컴포넌트에서 사용할 수 있는 상태를 가르키고, dispatch는 액션을 발생시키는 함수라고 이해하면 된다.
이 함수는 다음과 같이 사용한다
dispatch({ type: 'INCREMENT' })
그리고 useReducer 에 넣는 첫번째 파라미터는 reducer 함수이고, 두번째 파라미터는 초기 상태이다.

```javascript
function reducer(state, action) {
  switch (action.type) {
    case "INCREMENT":
      return state + 1;
    // 액션 로직...
    default:
      return state;
  }
}

function Counter() {
  const [number, dispatch] = useReducer(reducer, 0);

  const onIncrease = () => {
    dispatch({ type: "INCREMENT" });
  };

  // ...
}
```

useState, useReducer 상황에맞게 선택해서 사용하면 될것이다.

- 참고문헌
  <https://react.vlpt.us/basic/20-useReducer.html>
