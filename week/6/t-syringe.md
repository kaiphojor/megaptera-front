# TSyringe

## TSyringe란?

[TSyringe](https://github.com/microsoft/tsyringe). 주사기, 주입기

MS에서 만듬(Typescript도). JS/TS를 위한 경량 의존성 주입 컨테이너.

TSyringe(ts와 관련있다는 것을 보여주기 위해 노림 ). props drilling을 해결하는 괜찮은 방법이다.(useContext도 가능).

전역으로 취급되며 Context 자체를 변경하면 전체를 forceupdate 하는데 그렇게 하지 않고 선택적으로 우아하게 처리하기 위해 tsyringe로 처리한다.

tsyringe도 내부적으로는 context를 사용한다.

IOC container DI conteainre 해서 container라 한다 .

## Dependency Injection

의존성 주입은 클래스간의 의존관계를 느슨하게 결합하는 디자인 패턴

객체간의 의존성을 명시적으로 정의하고, 객체 생성/관리를 자동화해서 더 유연하게 프로그램을 만들 수 있다.

이점

* 코드 재사용성
* 테스트 용의성 - Mocking을 또는 가짜 객체 주입이 용이. 테스트중 다른 구현체로 교체도 가능
* 느슨한 결합/ 확장성 - 변경의 영향 최소화 (OCP - 변경에는 닫혀있고 확장에는 열려있음). 기존 코드 수정없이 새로운 의존성 주입 및 확장 가능

요소

### Dependency

클래스/모듈이 다른 클래스/모듈에 의존하는 상황.

> A가 B를 사용 => A는 B에 의존성을 가짐

### Dependency Provider

의존성이 필요한 클래스에 의존성을 제공.

의존성을 생성하거나, 외부에서 주입받은 의존성을 전달하는 식으로 전달

### DI Container

의존성 주입을 관리하고, 의존성을 필요로 하는 클래스에 의존성을 주입하는 역할

의존성을 자동으로 생성하거나, 외부에서 주입받은 의존성을 관리하고, 필요한 곳에 주입

## reflect-metadata

[relect-metadata - NPM](https://www.npmjs.com/package/reflect-metadata)
Reflect API의 polyfill 중 일부

java의 annotation과 비슷한 decorator를 통해 class와 그 휘하 member를 조작 가능(reflection). 선언적 문법을 이용.

tsyringe에 사용될 때는 의존성주입을 위해 reflect-metadata를 사용해 클래스의 생성자에 주입할 의존성을 지정하고 컨테이너에서 자동으로 의존성을 해결.

### reflection

프로그램 실행중(runtime)에 코드 자체를 검사/조작할 수 있는 기능

프로그램이 자기 구조와 특성을 알고 동적으로 변경하는 메타프로그래밍 기능을 제공

기능

1. 클래스 정보 검사 - class 정보(이름,상위클래스,인터페이스,필드타입등)를 동적으로 알수 있다
2. 동적인 인스턴스 생성 및 생성된 인스턴스의 메서드 호출
3. 클래스의 필드값 동적 변경 가능 (접근지시자를 무시)
4. 어노테이션(decorator) / 메타데이터 활용 - reflection을 통한 프로그램의 동작 제어.

## Singleton Pattern

생성자가 여러개 호출되어도 실제 생성은 한번만되고 최초 생성된 객체만 계속 사용하는 디자인 패턴

DB Connection pool 같은 경우에 pool 자체는 인스턴스 하나를 계속 써도 상관이 없으므로 싱글턴으로 쓴다.

이유

* 공유 리소스 - 동일한 리소스를 공유해서 쓰는 경우
* 상태 유지 - 객체 상태가 유지되어야 하는 경우.
* 제한된 인스턴스 생성 - 리소스를 절약하기 위해 인스턴스 생성 수를 제한한다.
* 전역 접근 - 어디서든 접근가능하도록 하는 경우

전역에서 하나. DI container(IOC container)가 new 해준적 없는데도 객체생성을 알아서 해주고 다른 것을 의존하면 의존성도 알아서 해결해준다.

사용


하나의 객체만을 쓰는 패턴. 객체가 없으면 하나만 만들어서 쓰고 다시 쓸때는 이전에 만든것을 가져와서 재활용한다.


spring 사용에서 하듯 annotation을 - decorator를 적용한다.(tsConfig.json에서 decorator 관련설정을 해준다.)

container.resolve(Store)

stores/soter.ts 생성

store.ts의 forceupdate에 등록한다. store에서는 update를 통해 forceupdate한다.

store는 들고 있는 것은 없고, 각 component쪽에서 store를 구독한다.

## 학습 키워드

- TSyringe
- 의존성 주입(Dependency Injection)
- reflect-metadata

tsyringe 사용을 위해 import 하는 것들. jest.config.js 에서 setupFilesAfterEnv(환경 설정 이후 setup해주는 file들 )에서 import 문을 추가해준다.