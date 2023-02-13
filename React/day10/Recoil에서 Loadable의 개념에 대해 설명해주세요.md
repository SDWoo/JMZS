# Recoil에서 Loadable의 개념에 대해 설명해주세요.

<br />

> 목차

> [동우](#동우)

> [은지](#은지)

> [지연](#지연)

> [규란](규란)

<br />

### 동우

- Loadable 객체는 리코일의 비동기 제어를 위해 사용된다. 비동기 값을 반환하는 atom이나 Selector 가 있을 때, 해당 아톰 또는 셀렉터의 현재 준비 상태와 값을 Loadable 인스턴스를 통해 알려준다. Loadable을 통한 상태는 hasValue, loading, hasError 세가지 비동기 상태(state)를 가질 수 있으며, 비동기 통신의 결과 값은 contents를 갖는다.
- useRecoilStateLoadable(state), useRecoilValueLoadable(state)로 사용한다.

<br />

### 은지

- recoil은 내부에서 비동기 요청이 발생할 경우, React의 suspense를 사용하도록 개발되었다. 이때 suspense를 감싸지 않고 Loadable을 사용해 비동기 데이터의 로딩 상태와 값에 따라 UI를 구성할 수도 있다. 다만, suspense와 다르지 않기 때문에 Loadable 또한 fallback UI가 필수적이다.
- useRecoilValueLoadable, useRecoilStateLoadable 함수를 이용해 Loadable을 구현할 수 있다.
- useRecoilValueLoadable는 데이터의 state와 contents를 반환하며, state는 3가지 값을 갖습니다. 데이터가 로드되었을 때는 hasValue, 로딩 중일때는 loading, 데이터 로드 중 에러가 발생했을 때 hasError의 값을 가진다.
- 또한, contents는 데이터의 값을 의미하며 데이터의 state가 hasValue이 데이터의 실제 값을 나타내고, 만약 state가 hasError이면 던져진 Error 객체를 의미하며, 상태가 loading이면 값의 Promise를 의미한다.

<br />

### 지연

- 비동기를 처리하고 있을 때 보여줄 로딩, 즉 fallback UI 처리를 할 수 있다.
- loadable은 atom이나 selector의 현재 상태를 나타내는 객체

<br />

### 규란

- loadable 객체는 Recoil atom, selector의 최신 상태를 대표합니다.
- state, contents 2가지 프로퍼티(인터페이스)를 가집니다.
  - state : atom, selector의 최신 상태입니다.
    - 가능한 값은 hasValue, hasError, loading 입니다.
  - contents : Loadable에 의해서 대표되는 값입니다. 상태에 따라 값이 달라집니다.
    - hasValue - 실제 값
    - hasError - Error 객체
    - loading - toPromise()를 사용하여 promise 객체
- loadable 객체를 사용하면 비동기 atom, selector라고 하더라도 suspense 없이 로딩 컴포넌트를 보여줄 수 있다.

<br />

### 꼬리 질문 모음
