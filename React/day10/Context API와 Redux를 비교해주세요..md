# Context API와 Redux를 비교해주세요.

<br />

> 목차

> [동우](#동우)

> [은지](#은지)

> [지연](#지연)

> [규란](규란)

<br />

### 동우

- Context API는 리액트 내장 기능이기 때문에 리액트에서만 사용이 가능하고, Redux는 자바스크립트를 사용하는 다양한 라이브러리나 프레임워크에서 사용이 가능하다.
- 둘은 사용법과 구조에서 조금 차이가 있을 뿐 전역 상태를 관리한다는 점에서는 비슷하다.
- Context API는 따로 라이브러리 설치가 필요가 없어서 가볍게 사용하게 좋아서, 단순 전역 상태 관리만을 사용한다면 Context API가 좋다고 생각하고,
- Redux는 Redux saga, thunk와 같은 미들웨어를 추가적으로 사용할 수 있어서 비동기 처리를 따로 Util로 처리할 수 있습니다. 이렇게 상태에 관해 추가 설정을 더 하는 경우에는 Redux가 더 좋다고 생각합니다.

<br />

### 은지

- context api
  - react가 제공하는 built-in 도구이다.
  - 주로 자주 업데이트되지 않는 정적 데이터에 사용한다.
  - context의 사용 목적은 상태 관리가 아니라 prop-drilling을 피하기 위해 사용된다.
  - context에 액세스하고자 하는 컴포넌트에 Provider로 래핑하며 context 데이터 값을 하위 컴포넌트로 전달할 수 있다.
- redux
  - 리덕스에는 미들웨어 개념이 존재한다.
  - redux-thunk, redux-saga를 통해 비동기 처리를 할 수 있다.

<br />

### 지연

- 사용처
  - context API : 오직 react에서만 사용 가능
  - redux : react 뿐만 아니라 angular, vuew에서도 사용 가능
- 상태 관리
  - context API : 일반적으로 기능별로 context를 만들어서 사용
  - redux : 모든 글로벌 상태를 하나의 커다란 상태 객체에 넣어 사용
- 미들웨어
  - context API : 해당 사항 없음
  - redux : 액션 객체가 리듀서에서 처리되기 전에 우리가 원하는 작업들을 수행할 수 있음

<br />

### 규란

- Context API

  - context는 react 컴포넌트 트리 안에서 전역적으로 데이터가 공유되는 방식을 의미합니다.
  - 주요 목적은 다양한 레벨에 네스팅된 많은 컴포넌트들에게 props drilling을 피해 데이터를 전달하는 것이다.
  - context api를 통해 context 객체를 생성하고 provider, consumer 컴포넌트를 사용하여 변화를 알리고 context를 구독할 수 있습니다.
  - 그러나 context api가 상태관리 도구는 아닙니다. 일반적으로 useState, useReducer hook과 함께 상태관리는 발생합니다. context 자체는 종속성 주입의 한 형태일 뿐 아무것도 관리하지 않습니다.

- Context 단점

  - 컴포넌트 재사용이 어려워진다.

- 상태관리란?

  - 상태관리는 시간이 지남에 따라 상태가 변경되는 방식을 의미합니다.
    - 초기값을 저장하고, 현재 값을 읽을 수 있고, 값 업데이트가 가능합니다.
  - [https://blog.isquaredsoftware.com/2021/01/context-redux-differences/](https://blog.isquaredsoftware.com/2021/01/context-redux-differences/)
  - 리코일에서는 이런 최적화 작업을 진행해주거든요

- Redux

  - Redux는 애플리케이션 전체에 대한 상태 중앙 저장소 역할을 합니다.
  - 애플리케이션의 모든 react 요소들이 redux 저장소에 접근이 가능한데, react-redux 내부에서 context를 통해 redux 저장소 인스턴스를 전달하기 때문입니다.

- 결론

  - 단순 props drilling을 피하는 것이 목적이라면 context를 사용합니다.
  - 적당히 복잡한 컴포넌트라면, context + useReducer를 사용합니다.
  - 이런 경우 redux를 사용합니다.
    - 여러 위치에 많은 양의 상태 값이 존재 할 때
    - 업데이트 로직이 복잡 할 때
    - 거대한 코드 베이스를 여러 사람이 작업 할 때
    - 상태 변경 시각화가 필요 할 때
    - 사이드이펙트, 메모이제이션, 데이터 직렬화등 관리를 위해 더 강력한 기능이 필요 할 때

<br />

### 꼬리 질문 모음

- **꼬리 질문 1 - context API의 단점**

  1. 랜더링 이슈(Provider hell) : Provider 하위에서 context를 구독하는 모든 컴포넌트는 Provider의 value prop이 변경될 때마다 다시 랜더링된다.
  2. 성능 문제 : 상태가 자주 바뀌는 경우 context를 사용하는 것은 옳지 않다.
