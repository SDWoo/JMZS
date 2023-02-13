# Recoil에서 비동기로 데이터를 받아올 때 State를 어떻게 관리하셨나요?

<br />

> 목차

> [동우](#동우)

> [은지](#은지)

> [지연](#지연)

> [규란](규란)

<br />

### 동우

- Recoil에서 비동기로 데이터를 받아오려면 pending 상태에 대한 처리가 필요한데, Suspense와 Loadable로 해당 처리가 가능하다.
- Suspense는 React.Suspense를 비동기 호출하는 컴포넌트에 감싸서 사용한다. fallback 으로 받아온 요소를 pending 상태일때 보여준다.
- Loadable은 최신의 state에 따라 다른 작업을 해주며 Error나 Loading에 관한 처리를 해주고, hasValue 상태일때 해당 비동기 데이터를 다룰 수 있다.

<br />

### 은지

- selector를 이용해 비동기 데이터를 관리했습니다.
- selector의 경우 get 함수 내부에 작성한 atom값을 의존성으로 갖고 해당 atom값이 변경될 때마다 자동으로 새로운 값을 리턴한다.
- 반대로 selector의 경우 캐싱 기능을 지원하기 때문에 의존성으로 갖는 atom이 새로운 값이 아니라면 이전에 캐싱된 값을 리턴한다.
- 또한 매개변수가 있는 쿼리의 경우, selectorFamily를 이용해 데이터를 관리했습니다.

<br />

### 지연

- selector를 이용해 atom 값이 변경될 때마다 비동기 데이터를 받아오도록 했다.

<br />

### 규란

- selector, selectorFamily를 이용하는 방법이 있을 것 같습니다.
- selector를 이용한다면
  - selector의 get 프로퍼티에 비동기 함수를 정의합니다.
- 비동기 요청 시 파라미터가 필요하다면 selectorFamily를 사용합니다.
  - selectorFamily의 get 프로퍼티에 매개변수를 받고 비동기 selector 함수를 반환하는 로직을 구현합니다.

<br />

### 꼬리 질문 모음
