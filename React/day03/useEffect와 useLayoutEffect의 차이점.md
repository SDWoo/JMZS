# useEffect와 useLayoutEffect의 차이점에 대해 설명해주세요.

<br />

> 목차

> [동우](#동우)

> [은지](#은지)

> [지연](#지연)

> [꼬리 질문 모음](#꼬리-질문-모음)

<br />

### 동우

두 코드의 가장 큰 차이점은 실행 시점입니다.

- useEffect는 컴포넌트들이 render와 paint 된 후 비동기적(asynchronous) 으로 실행됩니다. paint 된 후 실행되기 때문에, useEffect 내부에 dom에 영향을 주는 코드가 있을 경우 사용자 입장에서는 화면의 깜빡임을 보게됩니다.
- useLayoutEffect는 컴포넌트들이 render 된 후 실행되며, 그 이후에 paint 가 됩니다. 이 작업은 동기적(synchronous)으로 실행됩니다. paint 가 되기 전에 실행되기 때문에 dom을 조작하는 코드가 존재하더라도 사용자는 깜빡임을 경험하지 않습니다.

<br />

### 은지

가장 큰 차이점은 실행 시점이다.

- useEffect: 컴포넌트들이 render와 paint된 후에 실행되며 비동기적으로 실행됩니다. paint 이후에 실행되므로 DOM을 조작하는 로직이 포함되었더라면 유저는 화면의 깜빡임을 경험하게 됩니다.
- useLayoutEffect: 컴포넌트들이 render된 후에 실행되며 그 이후에 paint가 실행된다. 이는 동기적으로 실행됩니다. 즉, paint 이전에 실행되기 때문에 DOM을 조작하는 로직이 포함되었더라도 유저는 화면의 깜빡임을 경험하지 않습니다. 만약 함수 로직이 복잡한 경우, 로딩 시간이 너무 느려져서 사용자에게 좋지 않은 웹 경험을 제공할 수 있습니다.

<br />

### 지연

- useEffect : 리액트 컴포넌트가 렌더링될 때마다 특정 작업을 수행하도록 설정할 수 있는 훅
  레이아웃 배치와 그리기를 완료한 후 이펙트 함수를 호출해, 상태값이 이펙트에 의존할 경우 약간 불편한 사용자 경험으로 이어질 수 있음
  특히, 화면이 복잡해지면 체감할 수 있을 정도로 렌더링 시간이 증가
- useLayoutEffect : 브라우저가 화면에 DOM을 그리기 전에 이펙트를 수행
  따라서, 렌더링할 상태가 이펙트 내에서 초기화되어야 할 경우, 사용자 경험을 위해 useLayoutEffect를 사용해야 한다.

<br />

### 꼬리 질문 모음

- **꼬리 질문 1 : useLayoutEffect의 단점은 무엇인가요?**
  ⇒ 이펙트 내부 로직이 복잡한 경우에는 사용자가 레이아웃을 보는 데까지 시간이 오래 걸릴 수 있다는 단점이 존재한다.
- **꼬리 질문 2 : 언제 useLayoutEffect를 사용해야 하나요?**
  ⇒ 일반적인 경우에는 useEffect를 사용하되, state가 조건에 따라 첫 페인팅 시 다르게 렌더링되어야 할 때 useLayoutEffect를 사용해야 한다.
