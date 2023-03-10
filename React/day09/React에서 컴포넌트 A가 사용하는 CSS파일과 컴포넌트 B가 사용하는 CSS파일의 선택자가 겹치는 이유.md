# React에서 컴포넌트 A가 사용하는 CSS파일과 컴포넌트 B가 사용하는 CSS파일의 선택자가 겹치는 이유가 뭘까요?

<br />

> 목차

> [동우](#동우)

> [은지](#은지)

> [지연](#지연)

> [규란](규란)

<br />

### 동우

- SPA 환경에서는 모든 페이지 컴포넌트가 Router.js로 모이고 index.js를 거쳐 index.html에 모이기 때문에 겹치는 선택자가 있다면, 스타일이 깨 질 수 밖에 없다.
- CSS에서 모든 것은 글로벌 네임스페이스에 선언되기 때문에 명명 규칙 등으로 분할할 필요가 있습니다.
- 방법으로는 css in js를 사용하거나, className, nesting문법을 사용하여

<br />

### 은지

css는 기본적으로 global namespace를 가진다는 특징이 있기 때문에 한 파일에 특정 선택자를 선언했더라도 다른 파일에 같은 선택자가 사용되었다면 그 요소에 영향을 줄 수 있다.

<br />

### 지연

컴포넌트를 구성하는 태그의 양이 많아지면, 선택자 네이밍에 있어 중복이 발생할 수 있기 때문이다.

<br />

### 규란

React와 같은 SPA 환경에서는 기본적으로 글로벌 네임 스페이스를 사용한다. 따라서 외부 css의 파일을 각 컴포넌트에서 따로 import 했더라도 전체 모듈에 사용된다. 이렇게 css 선택자가 중첩 혹은 충돌하는 것을 방지하고 싶다면, 모두 고유한 className을 설정하거나 css module과 같은 기술을 사용하면 된다.
css module을 사용하면 클래스명에 고유한 hash 값이 적용되어 모듈별로 css를 적용할 수 있다.

- 참고 [https://www.daleseo.com/react-styling/](https://www.daleseo.com/react-styling/)

<br />

### 꼬리 질문 모음

- **꼬리 질문 1 : 선택자의 중복을 방지하는 방법을 설명해주세요.**
  ⇒ **css module**을 사용해, 클래스 이름이 중첩되는 것을 방지하고, 사용 범위를 제한해 스타일링 하고자 하는 컴포넌트가 다른 컴포넌트와 중복되는 것을 막는다.
  이외에도 **css in js 방식**을 이용해 컴포넌트 별로 스타일링해 중복 적용되는 것을 방지할 수 있다.
