# Props와 State의 차이에 대해 설명해주세요.

<br />

> 목차

> [동우](#동우)

> [은지](#은지)

> [지연](#지연)

<br />

### 동우

- 일단 props 한 컴포넌트에서 다른 컴포넌트로 데이터를 인수형태로 보내는것, state는 컴포넌트 내에서 데이터나 상태를 관리하는데 쓰이는 업데이트 가능한 요소들을 말한다. props는 readonly라서 불변이고, state는 변경 가능한 값이며 비동기적으로 쓰일수도 있습니다,

<br />

### 은지

- state와 props 모두 랜더링에 영향을 주는 객체입니다.
- props는 (함수 매개변수처럼) 컴포넌트간 전달되는 반면 state는 (함수 내에 선언된 변수처럼) 컴포넌트 안에서 관리됩니다.

<br />

### 지연

- 둘 다 컴포넌트의 렌더링 결과물에 영향을 주는 데이터를 가지는 객체다.
- props: 상위 컴포넌트의 값을 하위 컴포넌트로 전달할 때 사용하며, 값의 변경이 불가능하다.
- state: 컴포넌트 내부에서 가변적인 데이터를 관리할 때 사용한다.

<br />
