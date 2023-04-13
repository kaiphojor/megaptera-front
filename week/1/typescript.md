# TypeScript

## Interface vs Type

### type

* 프로퍼티 추가 안됨

확장

```javascript
type Animal = {
  name: string
}

type Bear = Animal & {
  honey: Boolean
}

const bear = getBear();
bear.name;
bear.honey;        
```

### interface

확장

```javascript
interface Animal {
  name: string
}

interface Bear extends Animal {
  honey: boolean
}

const bear = getBear()
bear.name
bear.honey        
```

필드 추가(가능)

```javascript
interface Window {
  title: string
}

interface Window {
  ts: TypeScriptAPI
}

const src = 'const a = "Hello World"';
window.ts.transpileModule(src, {});
```

## 타입 추론

javascript 특정 값을 넣을 때 그 값의 타입을 변수의 타입으로 여기고 사용하는 것.

* "hello" -> string
* 3 -> number

## Union Type vs Intersection Type

### Union Type

`type var = 'a' | 'b' | 'c';`

타입의 입력 값을 지정한 것만 받아들인다. any를 추가해서 지정한 것 이외도 받아들일 수도 있다.

취약점 진단 항목 중에 open redirectiond이 있다. 해당 취약점은 url을 매개변수로 받을 경우 위험한 url로 지정될 수도 있는 문제가 있는데, 조치 방법 중에 switch case, if else 같이 지정한 url만 받아들이는 방법이 있다. 뒷단에서도 url 검사를 하는데, 만약에 앞단에서 typescript를 쓸 경우에 union을 활용해서 정해진 url만 화이트리스트로 받는다면 더 안전하게 어플리케이션을 구성할 수 있을 것 같다.

```javascript
function start(
  arg: string | string[] | (() => string) | { s: string }
): string {
  // this is super common in JavaScript
  if (typeof arg === "string") {
    return commonCase(arg);
  } else if (Array.isArray(arg)) {
    return arg.map(commonCase).join(",");
  } else if (typeof arg === "function") {
    return commonCase(arg());
  } else {
    return commonCase(arg.s);
  }
 
  function commonCase(s: string): string {
    // finally, just convert a string to another string
    return s;
  }
}
```

### intersections

교집합은 두개 다 만족하는 것인데, `&` 를 쓰면 아래 a, b 둘을 모두 포함하는 Combined type이 생성된다.

```javascript
type Combined = { a: number } & { b: string };
type Conflicting = { a: number } & { a: string };
```

## Optional Parameter

함수의 매개변수를 0 개 혹은 1개 두개 다 받고 싶으면 `?:` 엘비스 연산자를 이용해서 받는다.

```javascript
function f(x?: number) {
  // ...
}
f(); // OK
f(10); // OK
```

## reference

* [type vs interface](https://www.typescriptlang.org/ko/docs/handbook/typescript-in-5-minutes.html#%ED%83%80%EC%9E%85-%EC%B6%94%EB%A1%A0-types-by-inference)
* [타입 추론](https://www.typescriptlang.org/ko/docs/handbook/typescript-in-5-minutes.html#%ED%83%80%EC%9E%85-%EC%B6%94%EB%A1%A0-types-by-inference)
* [union](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-func.html#unions)
* [Optional parameters](https://www.typescriptlang.org/docs/handbook/2/functions.html#optional-parameters)
