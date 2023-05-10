# TDD

## TDD란

[Test Driven Development](http://wiki.c2.com/?TestDrivenDevelopment)
[XP - TDD](https://web.archive.org/web/20070628064054/http://xper.org/wiki/xp/TestDrivenDevelopment)

구현 전에 테스트코드를 작성해서 먼저 인터페이스와 스펙을 정의하는 개발 방식.

code, deploy, release 각 과정을 진행 하기 이전에 테스트를 빠르게 반복해서 코드 이해도,유지보수성을 향상시킨다.

deployment : 프로그램을 특정 환경에 배포(QA, staging, production)
release :  새로운 기능추가 / 버그 수정 버전이 사용자 실제 사용 환경에 배포되는 것 [참고](https://www.bmc.com/blogs/software-deployment-vs-release/)

* <span style="background-color:red;">RED</span> : 구상한 API에 맞지만 테스트 실패하는 코드를 짠다.
* <span style="background-color:green;">GREEN</span> : 어떻게 만들던 테스트를 통과하는 코드를 짠다.
* <span style="background-color:blue;">REFACTORING</span> : 리팩토링 해서 중복을 제거하고 가독성을 높여준다. 의존성을 줄이고 응집도를 늘리는 과정도 포함된다.

TDD를 하면 운영상에 발생할 수 있는 문제들을 TDD를 진행하는 과정에서 미리 파악할 수 있어서 안정적이다.

다만, TDD를 시간낭비라고 생각하지 않는 분위기가 형성이 되어야 적용이 가능할 듯하다.


## Jest

페이스북(메타)에서 만든 [테스팅 프레임워크](https://jestjs.io/)

설정 없이 빠르게 사용할 수 있고, 자동 mocking, 병렬실행으로 시간도 절약할 수 있다.


테스트 케이스 방식

* 통상적인 테스트. test를 열고 함수의 결과와 기대값을 비교한다.

* BDD 스타일로 주체 - 행위 중심 조직화, 구조화

## Describe - Context - It 패턴

테스트 대상을 주체로 삼아서,

```text
해당 주체가 (Describe)

특정상황에서 (Context)

특정 행동을 했을 때 (It)

어떤 결과가 나오는지 테스트 한다.(Expect Value toBe Result)
```

```javascript
const context = describe;

describe('add', () => {
	context('with no argument', () => {
		it('returns zero', () => {
			expect(add()).toBe(0);
		});
	});

	context('with only one number', () => {
		it('returns the same number', () => {
			expect(add(1)).toBe(1);
		});
	});

});
```

대상과 처한 상황, 행위를 나눠서 기술하면 가독성이 좋고 일반 글처럼 서술해서 친숙하다.

상황을 여러개로 나누어서 구조화가 가능하고,

상황에 대한 여러 행동을 기술할 때 중복제거 또한 자연스럽게 된다.

```javascript
module.exports = {
	testEnvironment: 'jsdom',
	setupFilesAfterEnv: [
		'@testing-library/jest-dom/extend-expect',
	],
	transform: {
		'^.+\\.(t|j)sx?$': ['@swc/jest', {
			jsc: {
				parser: {
					syntax: 'typescript',
					jsx: true,
					decorators: true,
				},
				transform: {
					react: {
						runtime: 'automatic',
					},
				},
			},
		}],
	},
};
```

## 단위테스트란

Unit Test 단위 테스트는 프로그램 요소(function, class 등)를 단위로 격리/수행하는 테스트

단위 테스트는 해당 단위가 원래 의도한 대로 잘 작동하는 것인지 확인하는 것이 목적이다.
따라서 단위 테스트를 통해 수정을 계속하며 코드의 신뢰성/ 유지보수 용이성을 보장할 수 있다.

단위 테스트는 작은 범위를 정해서 쪼갠다. 쪼개는 이유는

* 격리성 : 작게 쪼개서 다른 코드 영향을 최소화하도록 격리
* 명확성 : 크면 의미가 모호해진다. 작게 쪼개야 해당 단위의 기능,동작,목적이 잘 보인다.
* 테스트 커버리지 : 작으면 분기별로 쪼개지는 작은 경우에 대해서도 모두 커버가 가능하다.
* 리팩토링 & 유지보수성 향상 : 코드 변경시 단위가 작을 수록 영향을 덜 받아서 다른 테스트가 실패하는 일이 적어진다.
