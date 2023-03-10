# React.memo와 useMemo의 차이에 대해 설명해주세요.

<br />

> 목차

> [동우](#동우)

> [은지](#은지)

> [지연](#지연)

<br />

### 동우

- React.memo 컴포넌트의 Props를 메모이제이션 하는 것

<br />

### 은지

- React.memo는 고차 컴포넌트로(higher-order component), React.memo로 특정 컴포넌트를 감싸 렌더링의 비용을 최적화할 수 있습니다.
- React.memo로 래핑된 컴포넌트는 렌더링의 결과를 메모이징하고 이전 props와 현재 props를 비교해 props가 변경되지 않았다면 React는 메모이징된 렌더링 값을 사용하게 됩니다. 반면에 이전 props와 현재 props를 비교해 변경되었을 경우에는 컴포넌트를 재실행하고 재평가하도록 한다. 따라서 자식 컴포넌트의 props는 변경되지 않았지만 부모 컴포넌트가 리렌더링되어 자식 컴포넌트까지 리렌더링되는 문제를 막을 수 있다.
- useMemo는 hook의 일종이며, 컴포넌트 내부의 함수를 감싸 사용할 수 있습니다. useMemo의 의존성 배열에 작성한 값이 변경될 때마다 함수가 반환하는 값을 재계산하도록 한다. 주로 컴포넌트가 렌더링될 때마다 계산하지 않아도 되는 함수에 적용해 최적화를 이룰 수 있다.

<br />

### 지연

- React.memo는 HOC 이기 때문에 클래스형 컴포넌트, 함수형 컴포넌트에서 모두 사용할 수 있지만, useMemo는 hook이기 때문에 오직 함수형 컴포넌트에서 사용할 수 있다.

<br />

### 꼬리 질문 모음

- **꼬리 질문 1 : React.memo와 usememo의 공통점에 대해 설명해주세요.**
  ⇒ 둘 다 props가 변경되지 않으면 , 인자로 넘긴 함수는 실행되지 않으며 메모이즈된 결과를 반환한다.
- **꼬리 질문 2 : 클래스형 컴포넌트에서 메모이제이션을 어떻게 구현할 수 있을까요?**
  ⇒ 기술적으로는 React.memo를 이용해 클래스 기반의 컴포넌트를 래핑할 수는 있지만 이는 적절하지 않은 방법입니다. 따라서 클래스 컴포넌트에서 메모이제이션이 필요하다면 PureComponent를 확장해 사용하거나 shouldComponentUpdate() 메서드를 구현하는 것이 좋습니다.

- **꼬리 질문 3 : React.memo를 사용하는 것이 무조건 좋을까요?**
  ⇒ 아닙니다. 이전의 props과 현재 props를 비교하기 위해 이전 props 값을 저장할 공간과 비교하는 연산이 필요하므로 성능 비용의 이슈가 있기 때문입니다. 작성된 props의 수, 컴포넌트의 복잡성, 컴포넌트의 자식 컴포넌트의 수의 따라 최적화를 했어도 props의 비교 연산에 의해 효율적이지 않을 수도 있습니다. 따라서 부모 컴포넌트를 재평가할 때마다 자식 컴포넌트의 props가 변하는 경우라면 해당 자식 컴포넌트에 React.memo를 사용하지 않는 것이 좋습니다.

- **꼬리 질문 4: React.memo를 적용해도 동작하지 않는 경우가 있을까요?**
  => React.memo가 동작하지 않는 경우도 있습니다. React.memo는 이전 props와 현재 props값을 비교할 때 얕은 비교를 하기 때문에 props로 객체를 넘긴 경우에 최적화가 일어나지 않을 수 있습니다.
  이 때, React.memo의 두 번째 매개변수로 비교 함수를 제공하면 props의 비교를 커스터마이징할 수 있습니다.
  => 상태 라이브러리, 예를 들어 redux와 같은 상태 라이브러리는 contextAPI로 구현되어있고 컴포넌트 내부에서 useSelector를 사용할 경우 React.memo로 래핑했더라도 리렌더링이 발생할 수 있다.

- **꼬리 질문 5: 일반적으로 일부 상태 업데이트가 느릴 때 우리는 어떻게 성능을 최적화 할 수 있을 까요?**
  => production build 중인지를 확인한다. (develop 서버는 극단적인 경우에는 의도적으로 수십배까지 느리게 작동하기 때문) - state를 tree에서 불필요하게 높은곳에 두지 않았는가를 확인한다. - React DevTools Profiler를 실행하여 리렌더링되는 부분을 확인하고 가장 비싼 하위 트리를 `memo()`로 감쌉니다.

- **꼬리 질문 6: 또 다른 방법으로는 무엇이 있을까요? (memo 전에 실행해볼 방법)**
  => 상태가 관련있는 것들만(변경되는 것들을) 컴포넌트로 나누는 방법, 관련있는 상태를 부모 컴포넌트가 사용하고 있는 경우

[before you memo](https://overreacted.io/before-you-memo/)
[useMemo & useCallback](https://medium.com/@yujso66/%EB%B2%88%EC%97%AD-usememo-%EA%B7%B8%EB%A6%AC%EA%B3%A0-usecallback-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-844620cd41a1)
