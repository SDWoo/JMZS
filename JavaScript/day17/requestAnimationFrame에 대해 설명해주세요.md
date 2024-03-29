# requestAnimationFrame에 대해 설명해주세요.

<br />

> 목차

> [동우](#동우)

> [은지](#은지)

> [지연](#지연)

> [규란](#규란)

<br />

## 동우

- 백그라운드 동작 및 비활성화시 중지(성능 최적화) 합니다.
- 최대 1ms(1/1000s)로 제한되며 1초에 60번 동작한다.
- 다수의 애니메이션에도 각각 타이머 값을 생성 및 참조하지 않고 내부의 동일한 타이머 참조하게 됩니다.
- AnimationFrameQueue에 쌓인다.

<br />

## 은지

자바스크립트에서 애니메이션을 구현하는 방법으로 브라우저에게 수행하기를 원하는 애니메이션을 알리고 다음 리페인트가 진행되기 전에 해당 애니메이션을 업데이트하는 함수를 호출하게 합니다. 이 메소드는 리페인트 이전에 실행할 콜백을 인자로 받습니다.

<br />

## 지연

- 브라우저에게 수행하기를 원하는 애니메이션을 알리고 다음 리페인트가 진행되기 전에 해당 애니메이션을 업데이트하는 함수를 호출하게 한다.

<br />

## 규란

자바스크립트로 복잡한 애니메이션처리를 처리해야 할 때 사용할 수 있습니다.
setTimeout, setInterval은 animation을 위한 최적화된 기능이 아니라서 animation 주기를 16.6 미만으로 하는 경우 불필요한 frame 생성이 되는 등의 문제가 생깁니다.
requestAnimationFrame함수를 통해서 원하는 함수를 인자로 넣어주면, 브라우저는 인자로 받은 그 비동기 함수가 실행될 가장 적절한 타이밍에 실행시켜줍니다. 특정 조건이 될 때까지(함수의 탈출 조건) 계속 함수를 연속적으로 호출합니다.

<br />
