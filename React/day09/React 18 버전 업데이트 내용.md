# React 18 버전 업데이트 내용에 대해 말씀해주세요.

<br />

> 목차

> [동우](#동우)

> [은지](#은지)

> [지연](#지연)

> [규란](규란)

<br />

### 동우

- concurrent mode -> concurrent feature
  - 특정 state가 변경되었을 때, 현재 UI를 유지하고, 해당 변경에 따른 UI 업데이트를 동시에 준비함
  - 준비중인 UI의 렌더링 단계가 특정 조건을 만족하면, DOM에 반영된다.
  - 렌더링 단계 (렌더링을 유지하는 state 관점)
    - Transition: setState 직후에 일어날 수 있는 렌더링 단계, Pending, Recorded 상태 존재
      - Pending 상태: useTransition 훅을 사용하면 UI를 바로 변경하지 않고 현재 UI를 유지할 수 있는데 해당 상태를 Pending 상태라고 한다.
      - Recorded 상태: useTransition을 사용하지 않은 기본 상태, state 변경 직후 UI가 변경됨. **전체 페이지에 대한 로딩 화면**이라고 생각하면 이해하기 쉽다. Pending 상태에서도 Receded 상태로 넘어갈 수 있는데 Pending 상태의 시간이 useTransition 옵션으로 지정된 timeoutMs을 넘으면 강제로 Receded 상태로 넘어간다. (state에 대한 다음 페이지를 준비하는 단계)
    - Loading
      - Skeleton 상태 페이지의 일부만을 로딩하는 상태. 전체 화면을 모두 로딩으로 대체해버리는 Receded와는 다르다.
    - Done
      - Complete 상태 로딩 UI 없이 모든 정보가 사용자에게 보이는 상태를 의미한다. 우리가 최종적으로 목표하는 단계라고 볼 수 있다.
  - concurrent 모드를 쓰려면 ReactDOM.render()가 아닌 ReactDOM.reateRoot().render()로 구현해야 했는데, concurrent feature가 되니 기본적으로 이렇게 적용하는 것으로 바뀜
- Auto-Batching
  - 리액트가 여러개의 상태 업데이트를 하나의 리렌더링으로 그룹핑하는 것이다. 이전에는 이벤트 핸들러에만 Batching을 지원했는데, 이제 promise, setTimeout, native에서도 배칭이 지원된다.
  - useState에서 setState가 비동기로 작동하는 이유 => batch (state변경을 하나로 묶어서 리렌더링)
- Transition (useTransition, startTransition)
  - isPending: 보류중인 Transition이 있는지 (현재 UI를 유지시키고 있는 것이 있는지)확인하는 것
  - startTransition: 상태 업데이트를 Transition로 표시하는 것 (보류)
  - 입력, 클릭, 그리기와 같은 다이렉트 상호작용은 긴급한 업데이트, 그리고, UI의 전환은 전환 업데이트이다.
  - startTransition으로 setState를 감싸면, 해당 업데이트는 전환 업데이트가 되며, 긴급 업데이트가 발생하면 멈추게 된다.
  - 그렇게 현재 UI를 유지시키다가 긴급 업데이트가 끝나면 실행하게 된다.
- Suspense
  - 서버 렌더링에서의 기능을 지원했다.(Suspense 기능 확장)
- useId
  - client-server사이드에서 **hydration 미스매치를 피하기 위해서** unique ID를 만들어주는 훅
  - list의 key를 만들기 위한 key는 아니니 그렇게 사용하지 말자
- useDeferredValue
  - 급하지 않은 트리를 리렌더링 하는 것을 지연하게 해준다. 지연된 렌더링은 중단될 수 있고, 사용자의 입력을 방해하지 않는다. 디바운싱 / 쓰로틀링 기법과 유사하지만 timeout을 직접 지정할 필요 없이 리액트가 다른 급한 작업이 완료 되는 즉시 실행을 시킨다는 장점이 있다.

<br />

### 은지

1. useId hook
   - const id = useId();
   - 고유한 아이디를 생성할 수 있는 새로운 훅이다.
2. useTransition
   - 렌더링 성능을 높이는데 사용할 수 있다.
   - 바로 업데이트할 요소와 늦게 업데이트해도 될 요소를 파악해 사용자의 웹 경험을 높일 수 있다.
   - useTransition은 isPending값과 startTransition을 반환한다.
   - isPending: 우선 순위가 낮은 상태 업데이트가 아직 보류 중인지 여부를 알려준다.
   - startTransition: 내부에 특정 setState를 작성해 업데이트 우선 순위가 낮음을 알린다.
3. Suspense
   - 로드 상태를 선언적으로 지정할 수 있다.
   - 아직 랜더링이 준비되지 않은 컴포넌트라면 fallback에 작성한 컴포넌트를 보이고 로딩이 완료되면 해당 컴포넌트를 보이게 할 수 있다.
   - 동작 방식은 에러 바운더리와 유사하게 동작한다.하여 렌더링될 때마다 함수의 재생성을 막을 수 있습니다.

<br />

### 지연

- **Automatic Batching** : 여러 개의 상태 업데이트를 **한 번의 리렌더링**으로 묶는 작업으로, 불필요한 렌더링을 방지하고 의도치 않은 버그를 예방
- **Transitions** : 직접적인 상호 작용을 반영하는 **긴급 업데이트**와 하나의 뷰에서 다른 뷰로의 UI 전환이 일어나는 **전환 업데이트**를 명시적으로 구분할 수 있는 startTransitionAPI 제공
  긴급하지 않은 업데이트를 래핑하고, 긴급한 이벤트가 먼저 처리되도록 한다.
- **Suspense** : 트리의 일부 구성 요소가 아직 렌더링할 준비가 되지 않은 경우 **로딩 표시기**를 지정
- **useDeferredValue** : 현재 렌더링이 사용자 입력과 _같은_ 긴급 업데이트의 결과인 경우 React는 **이전 값을 반환**한 다음 긴급 렌더링이 완료된 후 새 값을 렌더링
  <br />

### 규란

1.  Auto Batching

---

- Batching 이란

  - 한 컴포넌트에서 여러 상태가 바뀌더라도 더 나은 앱 성능을 위해 한번만 리렌더링하는 것

- 리액트 이벤트 내에서만 batching된다

  _Until React 18, we only batched updates during the React event handlers._

  - 이벤트 핸들러 내에서 비동기 로직을 처리한다면 이벤트가 처리된 이후이니 배칭되지 않아서 각 상태마다 리렌더링이 발생한다.
  - Promise, setTImeout, native event handler 등에서 상태를 업데이트하면 React는 배칭하지 않는다.

- Auto Batching 이란

  - 상태 업데이트가 어디서 수행되던 상관없이 모든 상태 업데이트는 자동으로 batching 된다.
  - 그래서 out-of-the-box improvements 라는 표현을 쓰는듯?
  - `ReactDom.createRoot` 로 새로운 Root API를 호출해서 사용하면 auto batching을 사용할 수 있다.
  - 기존에는 API는 `ReactDom.render` 로 호출할 수 있다.

- batch를 원하지 않는다면?

  - `React.flushSync()` 를 사용하면 되지만, 일반적으로 이렇게 사용하길 기대하지 않는다.

2. Transitions

- transition은 긴급 업데이트와 비긴급 업데이트를 구분하는 새로운 컨셉이다.
- 긴급 업데이트 (urgent updates)
- 입력, 클릭, 누르기 같은 직접적인 상호작용을 반영한다
- 전환 업데이트 (transition updates)
- UI의 전환

  - 타이핑, 클릭, 누르기 같은 긴급 업데이트는 빠르게 업데이트 되지 않으면 버벅거리면서 앱이 이상하다는 느낌을 줄 수 있다. 하지만 화면은 곧바로 결과값을 볼거라고 기대하지 않기 때문에 전환 업데이트는 느리게 업데이트가 되어도 괜찮다.

  - `startTransition`으로 래핑된 업데이트는 전환 업데이트로 처리되며, 긴급한 업데이트가 들어오면 중단된다. 전환이 중단되면 리액트는 stale한 렌더링 작업을 버리고 마지막 업데이트만을 렌더링한다.

3. `Suspense`

- `Suspense`를 사용하면 로드 상태를 선언적으로 지정할 수 있다. `Suspense`는 v16에서 도입되었는데, 이전에는 `React.lazy`를 활용한 코드 스플리팅만 지원했으며 서버 렌더링은 지원하지 못했다. v18에서는 서버 렌더링에서의 지원을 추가했다고 한다.

- `Suspense`가 로드 상태를 나타내는 방법은 에러 바운더리가 에러 상태를 캐치하는 방법과 유사한데, 이 경우 데이터가 아직 fetch 되지 않았다거나 코드가 로드되지 않았다거나 해서 렌더링 될 준비가 되지 않았음을 나타낼 수 있다. 동작 또한 에러 바운더리와 유사하게 구성 요소 위에 가장 가까운 구성 요소가 캐치 되고 해당 `Suspense`의 `fallback` 컴포넌트로 대체된다.

- +) Concurrent Features
  - 주요 특징은 렌더링이 중단될 수 있다는 것이다.
  - 동기적인 렌더링의 경우 결과 화면이 보일 때 까지 렌더링이 중단될 수 없다.
  - 그러나 React 버전 18부터는 동시성 모드를 제공하는데, 렌더링 중간에 인터럽트가 발생하더라도 의도한 UI가 보여지는 것을 보장한다.

<br />

### 꼬리 질문 모음

- **꼬리 질문 1 : useTransition과 useDeferredValue의 차이점은 ?**

  - `useTransition`은 함수 실행의 우선순위를 지정하는 반면, `useDeferredValue`는 값의 업데이트 우선순위를 지정한다. 우선순위가 높은 작업을 실행하는 동안 `useMemo`와 유사하게 이전 값을 계속 들고 있으면서 업데이트를 지연시킨다.
  - [유리님 리액트 18](https://yrnana.dev/post/2022-04-12-react-18/)
