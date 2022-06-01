# VAC pattern

어플리케이션의 원활한 유지보수와 디자이너, FE개발자 간의 원활한 협업(코드 충돌 방지)을 위해 디자인 패턴을 참고하여 설계하고자 한다.

또한 `react-vac`를 활용하여 개발 하고자 한다. `react-vac`컴포넌트는 View(JSX) 없이 컴포넌트를 개발할 수 있도록 도와주는 디버깅 도구로, VAC Pattern 개발 을 위한 최적의 솔루션을 제공한다.

> yarn add react-vac --dev

여러 패턴 중 `VAC`패턴을 채택하여 개발하고자 한다.
`VAC`는 View Asset Component의 약자로 렌더링에 필요한 JSX와 스타일을 관리하는 컴포넌트를 의미한다.
`VAC`패턴은 View 컴포넌트에서 JSX 영역을 Props Object로 추상화하고, JSX를 `VAC`로 분리해서 개발하는 설계 방법이다.
이런 설계는 비즈니스 로직 뿐만 아니라 UI 기능 같은 View 로직에서도 렌더링 관심사를 분리하는데 목적이 있다.

`VAC`는 다음과 같은 특징을 가지고 있다.

- 반복이나 조건부 노출, 스타일 제어와 같은 렌더링과 관련된 처리만을 수행한다.
- 오직props를 통해서만 제어되며 스스로의 상태를 관리하거나 변경하지 않는 stateless 컴포넌트이다.
- 이벤트에 함수를 바인딩할 때 어떠한 추가 처리도 하지 않는다.

VAC pattern
![vac_pattern_s1](https://user-images.githubusercontent.com/80657819/164623685-acf58bde-463a-47ff-b219-167c66252bc5.png)

`VAC`는 state를 가질 수 없지만 state를 가진 컴포넌트를 자식으로 가지는 것은 가능합니다. 이 경우 `VAC`는 부모 컴포넌트와 자식 컴포넌트 중간에서 개입하지 않고 단순히 props를 전달하는 역할만 한다.

# 구현 예제

간단한 예제를 통해 구현했다.

```javascript
const box = () => {
  const [value, setValue] = useState(0);

  return (
    <div>
      <button onClick={() => setValue(value - 1)}>-</button>
      <span>{value}</span>
      <button onClick={() => setValue(value + 1)}>+</button>
    </div>
  );
};
```

예제는 +, -버튼을 클릭하면 값이 1씩 증가 또는 감소하는 UI 기능을 포함하고 있다.

## Props Object 정의

View 컴포넌트에서 JSX를 추상화한 Props Object를 생성하고 JSX에서 사용할 상태정보나 이벤트 핸들러를 정의한다.

```javascript
const SpinBox = () => {
  const [value, setValue] = useState(0);

  // JSX를 추상화한 Props Object
  const props = {
    value,
    onDecrease: () => setValue(value - 1),
    onIncrease: () => setValue(value + 1),
  };

  // JSX의 유무는 중요하지 않음
  return <div></div>;
};
```

## JSX를 VAC로 분리

JSX영역을 분리하여 `VAC`로 만듭니다. 이때 View 컴포넌트에 생성한 Props Object 속성을 참고하여 `VAC`의 Props를 정의합니다.
반대로 이미 만들어진 `VAC`를 View 컴포넌트에 적용할 때는 `VAC`의 Props를 참고하여 View 컴포넌트의 Props Object 속성을 정의합니다.

```javascript
// VAC
const SpinBoxView = ({ value, onIncrease, onDecrease }) => (
  <div>
    <button onClick={onDecrease}>-</button>
    <span>{value}</span>
    <button onClick={onIncrease}>+</button>
  </div>
);
```

```javascript
// View Component
const SpinBox = () => {
  const [value, setValue] = useState(0);

  const props = {
    value,
    onDecrease: () => setValue(value - 1),
    onIncrease: () => setValue(value + 1),
  };

  // JSX를 VAC로 교체
  return <SpinBoxView {...props} />;
};
```

# VAC pattern 사용 이유

### 역할에 따른 작업공간의 분리

FE개발자는 View component 에서 개발을 진행하고
UI개발자는 VAC에서 개발을 진행해서 둘의 코드 중복을 피할 수 있다.

## 참고문헌

- <https://tv.naver.com/v/23162062>
- <https://wit.nts-corp.com/2021/08/11/6461>
- <https://www.npmjs.com/package/react-vac>
