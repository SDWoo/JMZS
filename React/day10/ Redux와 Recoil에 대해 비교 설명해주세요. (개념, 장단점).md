# Redux와 Recoil에 대해 비교 설명해주세요. (개념, 장단점)

<br />

> 목차

> [동우](#동우)

> [은지](#은지)

> [지연](#지연)

> [규란](규란)

<br />

### 동우

- Recoil은 리액트를 위한 상태관리 라이브러리로, 우리에게 익숙한 hook 형식으로 직관적이면서 간단한 구조를 갖기 때문에 코드의 양이 상당히 줄 수 있다. 아직 devtools가 미흡해서 디버깅에 살짝 불리하다.
- Redux는 자바스크립트 상태관리 라이브러리로, Flux 구조에서 살짝 변형된 방식으로 이루어져 있다. 초기에 action, reducer, store 등을 설정해야되어 코드의 양이 늘어나게 된다. redux는 디버깅 툴이 있어 디버깅에는 유리하다.

<br />

### 은지

1. Recoil은 Redux보다 러닝커브가 낮다.
   - React를 아는 사람이라면 쉽게 적용할 수 있는 상태 라이브러리이기 때문이다.
   - Recoil은 단순하다.
2. Redux는 store를 구성하기 위해 많은 양의 코드를 작성해야 한다.
   - 비동기 처리의 경우 별도의 라이브러리가 필요하다.
   - Recoil은 보일러플레이트가 없는 API
3. Recoil은 컴포넌트가 사용하는 데이터 조각만 사용할 수 있다.
4. Recoil은 Concurrent Mode를 제공하는 유일한 라이브러리이다.
5. Recoil은 devtool 없어서 데이터 디버깅을 할 수 없다.

<br />

### 지연

- 차이 1 : redux는 리액트 라이브러리가 아니다.
- 차이 2 : recoil은 러닝커브가 낮고, useState를 사용하는 것 만큼 사용이 간단하고 상태 관리에 효율적이다.
- 차이 3 : redux는 상태 값의 변경 사항을 redux devtool을 이용해 직관적으로 확인할 수 있기 때문에, 상태값이 많아질 경우 디버깅이 상대적으로 용이하다.

<br />

### 규란

- Redux

- 장점

  - 전역 상태를 수정하기 위해서는 반드시 액션을 선언해서 수행해야 하므로 데이터의 흐름을 좀 더 쉽게 예측 가능합니다.
  - 좋은 개발자 도구가 있어서 문제가 생긴 경우 빠르게 어느 시점에 무슨 컴포넌트가 어떤 데이터를 변경하는지 확인할 수 있습니다.

- 단점

  - RTK(Redux Toolkit)가 출시되어 사용하기 비교적 쉬워졌지만 상태를 업데이트하거나 구독하기 위해 여전히 boilerplate 코드가 많이 사용된다.
  - 여러 라이브러리를 함께 사용하는 경우가 있기 때문에 러닝커브가 높은 편이다.
  - 비동기 처리를 위해 여러 액션을 구현하거나 다른 미들웨어를 추가적으로 사용해야 한다.
  - React concurrent renderer를 지원하지 않습니다.

- Recoil

- 장점
  - React에 친화적이며 React의 concurrent renderer를 공식 지원하는 유일한 상태 관리 라이브러리이다.
  - 우리는 공유상태도 React의 내부상태처럼 간단한 get/set 인터페이스로 사용할 수 있도록 boilerplate-free API를 제공합니다.
  - 내부 API를 통해 비동기 처리를 비교적 간단하게 할 수 있다.
- 단점
  - 함수형 컴포넌트에서만 사용 가능하다
  - 전역 상태의 변경을 예측하기가 어렵다.
  - 예측 가능성을 달성하기 위해 Container/Presentational 패턴과 React의 custom hooks를 조합한 상태관리 방법이 사용되기도 한다.
  - Recoil은 공식 개발자 도구가 없으므로 상태의 변경을 파악하기 더 어렵다.

<br />

### 꼬리 질문 모음
