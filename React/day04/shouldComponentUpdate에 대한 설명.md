# shouldComponentUpdate에 대해 설명해주세요.

<br />

> 목차

> [동우](#동우)

> [은지](#은지)

> [지연](#지연)

> [꼬리 질문 모음](#꼬리-질문-모음)

<br />

### 동우

- React에서 사용되는 라이프 사이클 메서드로,

1. props가 변경 되었을때
2. state가 변경 되었을때
3. 부모 컴포넌트가 렌더링 되었을때

- 이렇게 컴포넌트가 업데이트 되어야 할 때, 사용하는 라이프 사이클 메서드 이다.
- \*shouldComponentUpdate()**안에 **얕은 비교\*\*가 적용된 버전이다.

<br />

### 은지

- shouldComponentUpdate는 최적화를 위한 라이프사이클 메서드입니다.
  setState가 호출될 때마다 리렌더링이 일어나는 문제를 해결할 수 있습니다. `shouldComponentUpdate()`는 이전 props, state값과 현재 props, state값을 비교해 새로운 값으로 갱신된 경우, 렌더링이 발생하기 직전에 호출됩니다.
- 하지만 `shouldComponentUpdate()`의 내용을 직접 작성하는 대신에 `shouldComponentUpdate`가 구현되어 있는 `PureComponent`를 사용하는 것이 좋습니다.
- 이 메서드는 초기 렌더링 시점 또는 `forceUpdate()`가 사용될 때에는 호출되지 않습니다.

<br />

### 지연

- props 또는 state가 새로운 값으로 갱신되어서 렌더링이 발생하기 직전에 호출된다. 이 메서드를 이용해서 전 후 props, state, context 값을 비교해 불필요한 렌더링을 막을 수 있다.

<br />

### 꼬리 질문 모음

- **꼬리 질문 1 : 컴포넌트 리랜더링 시점?**
- **꼬리 질문 2 : 랜더링 최적화**
- **꼬리 질문 3 : pure component에서 shouldComponentUpdate는 어떻게 동작하나요?**
