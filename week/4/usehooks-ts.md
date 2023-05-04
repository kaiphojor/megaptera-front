# usehooks-ts

## usehooks-ts란?

[usehooks-ts](https://usehooks-ts.com/) 는 typescript로 쓰인 react custom hook library 이다.

설치

```bash
npm i usehooks-ts
```

usehooks-ts 의 특징은 hook 별로 구현 코드, 예제가 다 있어서 쓰기도 쉬울 뿐더러 custom hook 설계에도 도움을 얻을 수 있다.

### useBoolean

hook의 setter가 여러개이고 toggle도 `useToggle()`로 지정을 해서 !isXXX 을 쓰는것보다 훨씬 직관적이다. 문서, 함수 사용에서 직관적이면 이해도 한번에 되고, 사용시에도 빠르게 쓸 수 있다.

아래 코드 처럼 한눈에 알기 쉬운 함수를 여러개 반환하니, 쓸것만 뽑아서 쓰면 된다. 구현 코드에서는 사용시 return 함수 정도를 체크해서 빠르게 사용해도 될 것 같다.

```typescript
  return { value, setValue, setTrue, setFalse, toggle }
```

### useEffectOnce

간단해서 구현 부분까지 모두 가져왔다. 구현 자체는 빈 의존성 배열을 넣었기에 간단하지만, 해당 hook의 효용은 끝의 빈 배열을 찾는 수고 없이 useEffectOnce 라는 함수이름을 읽을때 내용의 파악이 끝난다는 점이다.

```typescript
import { EffectCallback, useEffect } from 'react'

function useEffectOnce(effect: EffectCallback) {
  // eslint-disable-next-line react-hooks/exhaustive-deps
  useEffect(effect, [])
}

export default useEffectOnce

```

### useFetch

`fetch` 함수를 쓸 때 async await를 쓰거나 chunk를 계속 받아오거나 decode 하는 과정들 없이 url만 입력하면 data를 받아올 수 있다. 귀찮은 과정들을 모두 배제해주므로 실제 사용시에 자주 사용할 것 같다.

```typescript
import { useFetch } from 'usehooks-ts'

const url = `http://jsonplaceholder.typicode.com/posts`

interface Post {
  userId: number
  id: number
  title: string
  body: string
}

export default function Component() {
  const { data, error } = useFetch<Post[]>(url)

  if (error) return <p>There is an error.</p>
  if (!data) return <p>Loading...</p>
  return <p>{data[0].title}</p>
}

```

### useInterval

`setInterval`을 함수 react component로 사용한 것이다. 가장 큰 차이는 arguments 가 동적이다는 것이다.

이것은 진짜 잘 활용할 수 있을 것 같다. 왜냐하면 setInterval은 예상한 대로 잘 동작 안해주기 때문이다. custom hook을 쓰면  `useInterval`을 통해 더이상 안쓰는 `setInterval`에 대한 clear 작업을 해줄 수 있다.

```typescript
 useInterval(() => {
    // ...
  }, 1000);
```

```typescript
  setInterval(() => {
    // ...
  }, 1000);
```

비슷하지만, 만약에 delay arugment를 동적으로 설정하고 싶다? 그때는 wrapping한 useInterval을 쓰면 간단하게 할 수 있다. 하지만 setInterval을 사용하면 해당 작업을 시간을 들여서 더 신중하게 다뤄야 한다. abramov는 글에서 [기존의 명령형 api를 wrapping 해서 선언형 api로 바꾼 것이 더 시의적절하다고 봤다.](https://overreacted.io/making-setinterval-declarative-with-react-hooks/)

 dan abramov 도 그래서 useInterval 과같은 custom hooks로 setInterval을 쓰는 것을 추천하는 것이다.

### useEventListener

addEventListener의 option을 거의 같은 식으로 쓸 수 있다. 사용상에 있어 기존 addEventListener에 대한 이해만 있다면 큰 노력이 필요없을 것 같다. 개발자 아샬님은 특히 dispatchEvent로 전달되는 커스텀 이벤트에 반응하기 좋다며 강력 추천하기까지 했다.

### useLocalStorage

page refresh 이후에도 영속해야할 데이터를 담는다. dark theme 설정값 같은 것을 담을 때 필요 하다. 이벤트를 통해(dispatchEvent + useEventListener) 다른 컴포넌트와 동기화하는 게 매우 중요한 특징이라고 한다.

### useDarkMode

정말 dark 모드에 대해서 제어하고 싶다면 `useDarkMode`를 사용하면 된다. `isDarkMode, toggle, enable, disable ` 같은 세부 함수들이 들어있으니 기호에 따라 사용하면 된다.

## swr

[SWR](https://swr.vercel.app/ko)은 캐시 무효 전략 `stale-while-revalidate` 에서 유래되었으며, 시시각각 바뀌는 데이터의 빠른 최신화를 위해 캐시와 fetch 데이터 간 비교(재검증)을 한뒤 다를 시 갱신을 하는 전략이다. SWR을 사용시 캐시 이슈 해결을 위해 데이터 바뀌었는지 실시간으로 계속 확인을 한다(지속적이고, 자동으로 데이터 업데이트 스트림을 받는다. UI는 항상 빠르고 반응적)

```typescript
import useSWR from 'swr'

function Profile() {
  const { data, error, isLoading } = useSWR('/api/user', fetcher)

  if (error) return <div>failed to load</div>
  if (isLoading) return <div>loading...</div>
  return <div>hello {data.name}!</div>
}
```

역으로 생각하자면, 반대로 말해서 데이터의 변화가 거의 없는 경우에는 SWR을 쓰면 오히려 불필요하게 데이터를 fetch하는 오버헤드가 많이 발생한다고 볼 수 있다.

## react-query

tanstack-query로 바뀜. React Query는 React App에서 데이터 관리/처리를 위한 라이브러리다. 데이터 캐싱, 자동 재요청, 재사용, 비동기 처리, 에러 핸들링 등 다양한 기능을 제공한다.

데이터의 상태는 세가지 이다.

* IDLE: 데이터가 존재하지 않는 상태
* LOADING: 데이터를 요청하는 중인 상태
* SUCCESS: 데이터를 성공적으로 받아온 상태

React Query는 Query와 Mutation 두 가지 유형의 Hook을 제공한다. Query Hook은 데이터를 가져오는 데 사용하고, Mutation Hook은 데이터를 수정하는 데 사용한다.

React Query는 캐시 시스템을 통한 API 요청의 최적화를 꾀한다. 효율적인 데이터 캐싱을 통해 성능향상 및 중복 요청을 배제한다. 또한 새로운 데이터가 서버에서 업데이트되면 자동으로 캐시를 업데이트하여 UI를 즉시 업데이트한다.

React Query는 다른 상태 관리 라이브러리와 함께 사용할 수 있으며, 다른 라이브러리와 결합 사용이 가능하다.