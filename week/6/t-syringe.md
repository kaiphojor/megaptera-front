# TSyringe

MS에서 만듬(Typescript도). JS/TS를 위한 경량 의존성 주입 컨테이너.

TSyringe(ts와 관련있다는 것을 보여주기 위해 노림 ). props drilling을 해결하는 괜찮은 방법(useContext도 가능). 전역으로 취급됨. Context 자체를 변경하면 전체를 forceupdate 하는데 그렇게 하지 않고 선택적으로 우아하게 처리하기 위해 tsyringe를 처리한다. tsyringe도 내부적으로는 context를 사용한다.

IOC container DI conteainre 해서 container라 한다 .

## 학습 키워드

- TSyringe
- 의존성 주입(Dependency Injection)
- reflect-metadata

tsyringe 사용을 위해 import 하는 것들. jest.config.js 에서 setupFilesAfterEnv(환경 설정 이후 setup해주는 file들 )에서 import 문을 추가해준다. 

- sington (싱글톤)

하나의 객체만을 쓰는 패턴. 객체가 없으면 하나만 만들어서 쓰고 다시 쓸때는 이전에 만든것을 가져와서 재활용한다. 

전역에서 하나. DI container(IOC container)가 new 해준적 없는데도 객체생성을 알아서 해주고 다른 것을 의존하면 의존성도 알아서 해결해준다. 

사용

spring 사용에서 하듯 annotation을 - decorator를 적용한다.(tsConfig.json에서 decorator 관련설정을 해준다.)

container.resolve(Store) 

stores/soter.ts 생성 

store.ts의 forceupdate에 등록한다. store에서는 update를 통해 forceupdate한다. 

store는 들고 있는 것은 없고, 각 component쪽에서 store를 구독한다. 