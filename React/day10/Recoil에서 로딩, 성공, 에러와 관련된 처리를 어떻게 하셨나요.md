# Recoil에서 로딩, 성공, 에러와 관련된 처리를 어떻게 하셨나요?

<br />

> 목차

> [동우](#동우)

> [은지](#은지)

> [지연](#지연)

> [규란](규란)

<br />

### 동우

- Loadable로는 세가지 경우를 다 처리할 수 있다. 그리고 Suspense로는 loading. 즉, pending 상태일 때와 관련된 처리를 fallback을 통해 해줄 수 있다. Suspense를 쓸 때, 에러를 잡고싶다면, 에러 바운더리로 Suspense를 감싸서 해당 처리를 해줄 수 있다.

<br />

### 은지

- 로딩과 성공의 경우, 비동기 데이터를 관리하는 컴포넌트를 React.Suspense로 감싸 fallback UI를 통해 처리하였습니다.
- 에러의 경우, React의 ErrorBoundary로 감싸 에러를 잡을 수 있습니다.

<br />

### 지연

- loadable과 suspense로 처리
  [Recoil 비동기통신(Suspense, Loadable)](https://velog.io/@qnrl3442/Recoil-비동기통신Suspense-Loadable)

<br />

### 규란

- 비동기 상태를 관리하는 컴포넌트를 Suspense 컴포넌트로 감싸서 사용하거나 suspense를 사용하지 않고 loadable 객체를 사용하여 비동기 로직을 제어했습니다.

<br />

### 꼬리 질문 모음
