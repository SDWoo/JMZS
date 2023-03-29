# React-Query에 대해 설명해주세요.

<br />

> 목차

> [동우](#동우)

> [은지](#은지)

> [지연](#지연)

> [규란](규란)

<br />

### 동우

- 비동기 API 통신을 사용하면서, 서버 상태 관리 및 비동기 로직을 쉽게 사용할 수 있게 하는 라이브러리입니다. 크게 get 요청을 위한 useQuery와 post, update요청을 위한 useMutation 두가지 경우로 사용하는 hook 함수가 나뉩니다. hook 함수들의 반환 객체의 isLoading, error, isSuccess 등을 통해 로딩, 에러, 성공했을때의 처리를 따로따로 해줄 수 있습니다. (useQueries, useInfiniteQuery 같은 Hook들도 제공합니다.)

<br />

### 은지

- 리액트 쿼리는 클라이언트에서 서버 상태를 관리하기 위한 라이브러리이다.
- 기본적으로 React Query는 데이터를 가능한 한 빨리 사용자에게 보여주는 동시에 새로운 데이터로 유지하도록 동작합니다. 따라서 거의 즉각적으로 느껴지는 훌륭한 UX를 제공할 수 있죠.

- 💫 어떤 상황에서 react-query를 사용하면 좋을까요?

  - 클라이언트 사이드 데이터보다 서버 사이드 데이터 관리가 더 많을 때 사용하면 좋을 것 같습니다. 예를 들어 refetch 옵션을 통해 서버 데이터와 쉽게 동기화할 수 있기 때문이다.

- 💫 staleTime vs. cacheTime
  - `staleTime` : 데이터가 **fresh → stale** 상태로 변경되는데 걸리는 시간, 기본값은 0
  - `cacheTime` : 데이터가 inactive 상태일 때, **캐싱된 상태로 남아있는 시간**, 기본값은 5분, cacheTime이 지나면 가비지 콜렉터로 수집된다. cacheTime 이 지나기 전에 쿼리 인스턴스가 다시 마운트 되면, 데이터를 fetch 하는 동안 캐시 데이터를 보여준다.

<br />

### 지연

- React application에서 서버 상태를 불러오고, 캐싱하며, 지속적으로 동기화하고 업데이트하는 작업을 도와주는 라이브러리
- React component 내부에서 간단하고 직관적으로 API를 사용할 수 있다.
- 서버의 값을 클라이언트에 가져오거나, 캐싱, 값 업데이트, 에러 핸들링 등 **비동기 과정**을 더욱 편하게 하는 데 사용

<br />

### 규란

- react query는 서버의 상태를 관리하기 위한 라이브러리이고, react query를 사용하면 서버의 데이터를 클라이언트에 가져오거나 캐싱, 값 업데이트, 에러 핸들링 등 비동기 과정을 쉽게 처리할 수 있습니다.

---

<br />

### 꼬리 질문 모음

- **꼬리질문 1 : useQuery와 useMutation의 차이점은 무엇인가요?**

  => useQuery는 get 요청을 위한 hook 함수입니다. queryKey와 해당 Query 요청을 위한 Promise를 반환하는 API 요청 함수, Options 객체를 인자로 받아, UniqueKey인 queryKey 값으로 서버 상태를 로컬에 캐시하고 관리합니다.  
  => useMutation은 post, update, delete등 서버의 사이드 이펙트를 발생시키는 요청을 위한 hook 함수입니다. q해당 Query 요청을 위한 Promise 를 반환하는 API 요청 함수와, Options 객체를 인자로 받아 사용합니다. 반환 객체의 mutate 함수를 호출하여 서버에 side effect를 발생시킨다.

- **꼬리질문 2 : options 객체엔 어떤 것이 있고 어떨 때 사용하는가?**

  => 대표적으로, 쿼리 함수 자동 실행을 조절하는 enabled, 재시도를 설정할 수 있는 retry, 상태를 변경하는 staleTime, cacheTime 등이 있다. 이외에도 onSuccess, onError 와 같이 데이터 Fetching 이후의 동작을 쓸 수 있는 함수들이 있고, refetch가 접두사인 함수를 사용하여 특정 상황때마다 refetch를 할수도 있다.

- **꼬리 질문 3 : 어떤 상황에서 react query를 사용하는 것이 좋은 지 설명해주세요.**

  ⇒ 클라이언트 사이드보다 **서버 사이드** 데이터 관리가 더 많을 때 유리하다.

- **꼬리 질문 4 : 캐싱은 무엇을 이용하여 일어나는 지 설명해주세요.**

  ⇒ 유니크한 쿼리 키, staleTime과 cacheTime을 적절히 사용해야 한다.
