# useMemo와 useCallback에 대해 설명해주세요.

<br />

> 목차

> [동우](#동우)

> [은지](#은지)

> [지연](#지연)

<br />

### 동우

- useMemo는 함수의 반환값을 메모이제이션 하는 것
- useCallback은 콜백 함수 자체를 메모이제이션을 하는 것

<br />

### 은지

- useMemo의 경우 컴포넌트 내부의 함수가 반환하는 값을 메모이징하는 훅이며, useCallbak은 컴포넌트 내부의 함수 자체를 메모이징하여 렌더링될 때마다 함수의 재생성을 막을 수 있습니다.

<br />

### 지연

- useMemo : 메모이제이션된 **값**을 반환한다. 컴포넌트의 렌더링 결과를 저장해, props가 바뀌지 않았으면 리렌더링하지 않고 기존의 것을 보여준다.
- useCallback : 메모이제이션된 **콜백**을 반환한다. 함수를 prop으로 넘겨줄 때, 해당 함수를 다시 생성하기 때문에 리렌더링이 발생하는데, 이때 useCallback을 사용함으로써 함수가 계속 새로 만들어지는 것을 방지할 수 있다.

<br />

### 꼬리 질문 모음

- **꼬리 질문 1 : useMemo와 useCallback을 사용하지 말아야 할 경우에 대해 설명해주세요.**
  ⇒ leaf 컴포넌트(html 태그만 렌더링하는 컴포넌트), 의존성 배열에 매번 새롭게 생성되는 객체를 작성한 경우
  [useMemo, useCallback 관련 자료](https://yceffort.kr/2022/04/best-practice-useCallback-useMemo)

- **꼬리 질문 2 : useMemo, useCallback의 차이에 대해 설명해주세요.**
  ⇒ useMemo는 작성된 dependency에 의존해, 해당 값이 변경될 때마다 함수를 실행하고 결과 값을 반환한다. useCallback은 작성된 dependency의 변화에 따라 새로운 함수를 반환한다.
