# State

## State 란?

한 화면 UI를 나눈 조각이 Component라면, Component는 특정 상태에 따라 표시하는 부분이 달라질 수 있다. 변하는 component를 결정하는 가변적인 상태를 React의 State이다.

### step by step

* UI 간단하게 component로 나눠보기
* component hierarchy 정하기 
* 정적인 버전 제작하기(노가다) . 간단한 프로젝트 top down 대규모 프로젝트 bottom up


### SSOT가 나온 이유는? state와의 관계는 ?

데이터는 딱 한곳에서 제어, 조작하는 정보모델이 SSOT(Single Source of Truth) 이다. 현실세계에서 국민의 의료정보를 한곳에서 통합관리하고 각 병원에서 이걸 참조하는 사례도 이 모델에 해당한다.

State도 마찬가지다. 같은 state를 여러 군데에서 독자적으로 중구난방 사용하면 관리가 제대로 안된다. 만약 독자적인 state가 있고 이것을 모두 동기화 해준다면 일일이 업데이트를 해줘야 하니 state를 이용하는 과정보다 state 동기화 하는 과정이 더 많이 걸리게 될 수도 있다. 그렇게 보면 하나로 정해서 관리하는 것이 효율적인 방식이다.

## 기타

* golden record - 정리 필요

## reference

1. [jsx 공식문서](https://facebook.github.io/jsx/)
