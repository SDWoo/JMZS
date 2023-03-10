# CSS in JS를 사용해 본 적이 있나요? 있다면 소감을 말해주세요.

<br />

> 목차

> [동우](#동우)

> [은지](#은지)

> [지연](#지연)

<br />

### 동우

- 써보았다. 상당히 편했습니다. 컴포넌트마다 스타일을 적용시켜서 제가 느끼기엔 좀 더 직관적으로 보이고 고칠 수 있어서 좋았다. 하지만 재사용성인 측면에서는 좀 더 신경써야되어서 불편한 점도 있었다.

<br />

### 은지

- styled-components와 emotion 라이브러리를 이용해 본 경험이 있습니다. css의 특성상 global한 namespace를 가져서 selector가 중복될 위험성이 존재할 수 있는데 css in js 라이브러리는 고유한 이름을 생성하므로 편리했던 경험이 있습니다.

<br />

### 지연

- 개발할 때 주로 emotion을 이용함.
- 컴포넌트 레벨로 작성하기 때문에 컴팩트하게 작성하고 관리할 수 있다는 점이 가장 마음에 들었지만, 테스트를 하거나 개발자 도구를 이용해 확인할 때 새로운 이름이 입혀진 객체로 확인되어 구분이 조금 힘들었던 것 같다.

<br />

### 꼬리 질문 모음

- **꼬리 질문 1 : emotion과 styled component의 차이에 대해 설명해주세요.**
  ⇒ emotion의 경우, 번들 사이즈가 확실히 적고, 서버 사이드 렌더링에 따로 서버쪽 설정을 하지 않아도 된다는 장점이 있다. 사실 두 라이브러리 모두 큰 차이점은 없기 때문에 개발 환경에 따라 유연하게 선택하면 될 것 같다.
- **꼬리 질문 2 : CSS in JS의 장단점**
  ⇒ 장점 - css 모델을 문서 레벨이 아닌 컴포넌트 레벨로 추상화, 단점 - 별도의 라이브러리 설치로 인한 번들 크기 이슈에 의해 느린 속도
- **꼬리 질문 3 : 대표적으로 styled-component가 있는데, 요즘은 emotions가 많이 쓰인다. 그 이유는 무엇일까?**

- styled-componets
  - 번들 용량이 가장 크다 ⇒ 컨텐츠 제공에 큰 영향을 끼쳐 중요한 문제다!
- EmotionJS
  - 번들 용량이 다른 라이브러리에 비해 압도적으로 작다.
  - styled-components의 기능을 거의 동일하게 사용, 라이브리러 설치를 통한 손쉬운 기능 확장
