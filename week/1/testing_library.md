# Testing Library

## Jest

단순함에 집중한 JS testing framework. describe context it 지원, 단언(assrtion) expect 지원. Mocking 도 가능

mock - 가짜 객체를 만들어 테스트시에 의존성 문제를 해결

Rspec은 원조이다. 하지만 컨셉 정도만 참고할 것.

### 사용

* 파일 작성 : abc.ts -> abc.test.ts
* 작성 시 마다 테스트 : `jest --watch-all`

TDD ?
테스트를 먼저 작성하고 테스트를 통과하는 코드를 구현

## Describe-Context-It 패턴

RSpec describe it 참고

* Describe - 무엇이
  * Context - 어떤 조건에서
    * It - 어떻게 될 것인가?

```javascript

describe('add 함수', ()=>{
  context('두 양수가 주어지면',()=>{
    it('합을 반환한다',()=>{
        expect(add(1,2)).toBe(3);
    });
  });  
});
```

구어체 처럼 표현할 수 있다 보니 보다 표현력이 풍성해진다.

## React Testing Library

React Component를 가지고 테스트 하는 UI 테스트 라이브러리이다.

`toBeVisible` 같이 보이는지 여부, `toBeEmptyDOMElement` 처럼 DomElement가 어떤 상태인지 체크하는 함수를 사용한다

주의 - react component test만 하는 것은 지양해야 한다. 화면 감시하는 건 너무 방대해지고, UI가 조금만 달라져도 테스트를 다 수정해야하는 상황이 발생할 수 있다.

tip

* `Screen.getByText`는 없으면 에러가 나지만 `Screen.queryByText`는 없어도 에러가 안난다.

## Reference

* [jest docs](https://jestjs.io/)
* [react testing library docs](https://testing-library.com/docs/react-testing-library/intro/)
* [react testing library git - matcher 목록들](https://github.com/testing-library/jest-dom)
