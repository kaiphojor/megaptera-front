# Node.js

Node.js 는 크롬 v8 JS엔진으로 만들어진 javascript 실행환경이다. 싱글 스레드로 여러 작업을 동시에 처리하기 위해 논 블로킹, 이벤트 루프를 활용한다.

## 특성

* single thread

Node.js는 싱글스레드로 돌아간다. 작업을 동시에 처리하기 위해 추가적으로 스레드를 만들지 않는다. 여러 작업은 시스템 커널의 멀티스레드가 처리하도록 던져버리고 이벤트 루프의 콜백으로 관리한다.

* non-blocking(비동기)

블로킹 - 다른 JS 작업이 있을 때, 이전 작업의 I/O 작업들이 마무리 될 때까지 실행하지 못하고 막혀(block) 있는것이다

논 블로킹은 JavaScript가 아닌 작업을 기다리지 않는다. I/O 같은 다른 작업은 시스템 커널에 넘긴 뒤 콜백으로 올 때 처리한다. 기다리지 않고 추가 Javascript 작업을 실행하기 때문에 더 많은 작업을 빠르게 처리할 수 있다.

* event loop

이벤트 루프는 Node.js 가 싱글 스레드로 여러 작업을 동시처리 하기위한 구조이다. 시스템 커널에 여러 작업을 떠맡겨서 node 자체는 계속 돌아갈 수 있다. poll 단계에서 새로운 입출력 작업을 추가하고, 각 단계를 돌며 단계 별 queue 에서 콜백을 실행 한다. 대기 작업이 없으면 종료한다.

구조

```text
   ┌───────────────────────────┐
┌─>│           timers          │
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │     pending callbacks     │
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │       idle, prepare       │
│  └─────────────┬─────────────┘      ┌───────────────┐
│  ┌─────────────┴─────────────┐      │   incoming:   │
│  │           poll            │<─────┤  connections, │
│  └─────────────┬─────────────┘      │   data, etc.  │
│  ┌─────────────┴─────────────┐      └───────────────┘
│  │           check           │
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
└──┤      close callbacks      │
   └───────────────────────────┘
```

1. timers : setTimeout() / setInterval() 콜백 실행
2. pending callbacks : 연기된 I/O 콜백
3. idle, prepare : 내부용 콜백
4. poll : 새 I/O 이벤트 가져옴, I/O 콜백 대부분 수행.
5. check : setImmediate() 콜백
6. close callbacks : 일부 close 콜백

## 경쟁자(Deno)

요즘은 Deno(디노) 라고 해서 Node 개발자(ryan dahl)가 만든 런타임이 따로 있고, 많이 쓰인다고 한다. 더 쉽고 간결하며, 초당 response 수(rps)도 많다. 심지어 의심스러운 코드에 대해 미리 감시하는 기능도 있다.

### 그럼에도 Node로 배우는 이유

Deno를 쓰면 더 편할 것이나, 처음에는 어렵게 배우는 것이 낫다. 어렵게 배우면 쉽게/ 어렵게 쓸 수 있으나, 쉽게 배우면 쉽게 밖에 못쓰기에 Node로 배우는 것이 더 낫다. 그리고 아직 Job description에 Node가 많이 올라오기 때문에 더더욱 Node로 배워야 한다.

## Reference

* [Node.JS](https://nodejs.org/ko/about)
* [논블로킹](https://nodejs.org/ko/docs/guides/blocking-vs-non-blocking)
* [이벤트 루프](https://nodejs.org/ko/docs/guides/event-loop-timers-and-nexttick)
