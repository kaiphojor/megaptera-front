
# External Store

- 관심사의 분리

하나의 시스템을 여러 작은 부품 단위로 나눈다. 각각 맡고 있는 기능이 있고 관심사가 다르다. 기능하는데 필요한 정보만 있으면 된다. 


기능 구분 / 설계 구분 layered architecture에서는 사용자에 가까운정도(UI/business logic/데이터). 사람으로 치면 기능구분이 밥먹는 기능 / 똥싸는 기능이 기능 구분이다. 
자기 관심사에만 집중하면 다른것에 신경쓸 필요가 없어서 복잡도가 낮아진다. 

프로세스 구분 - 입력 -> 처리 -> 출력
Model -> Process, View -> Output, Controller -> Input

자기가 하는 일에 대한 신경만 쓰는 것 

App
- header main greeting 

- Layered Architecture

- Flux Architecture

mvc architecture에 대한 대안. MVC 가 가지고 있는 MODEL - VIEW 가 많아져서 생기는 복잡성을 해결하기 위해 single directional data flow 
action : 시스템에 들어오는 작업 
dispatcher : 작업을 교통정리해준다
store : 작업이 들어오면 상태를 변경해준다 
view : 상태가 변하면 그에 따라 보이는 것들을 변경해준다. 

2-way binding model view의 복잡한 관계를 단방향 data flow로 개선한다.

action - 일종의 이벤트/메시지(broker) 비슷한 객체
dispatcher - action을 (여러)store에 전달 메시지 브로커와 유사. 작업 하나 완료 될때까지 돌리지 않는ㄷ 
store(여러개) -> 받은 action에 따라 상태 변경. 상태 변경 알림
view - 구독중인 store 상태 변경 반영

redux는 단일 store를 사용한다 

Flux architecure


1. action
2. store dispatch 통해 action을 받고  
3. view 

store 하나 입장에서 받고 상태 변을 reducer를 통해 state 변경한다.

- useReducer

const statet = {
  name: 'tester'
}
const nextState = {...state , name: 'new name'}; 
기존 state를 변경 하지 않고 새 state를 만들어낸다. reduce한다는 것이다. 

간단히 정리하면 
input - action + dispactch
process - reducter 
output - view ( react) 

external  store - 외부 저장 소

store가 react 내부에 있지 않음. useState로 관리하지 않음.

왜 react 가 관리하는 state는 (re)rendering에 관여되어 업데이트 하기 때문이다.

react에서의 성능은 rendering을 필요한 부분에서만 하느냐에따라 달라진다. UI framework 니깐. 데이터만 변경이 필요하고 UI 변경 ( rendering)이 필요하지 않은 경우에는...?

외부에서 상태정의를 하면 강제 리렌더링을 해야하는데 지금은 forceUpdate 대신 useReducer를 쓴다. 근데 보면 useState가 useReducer를 쓴다. 

js는 받고 싶지 않은 인자가 있을때 그냥 , 단위로 비워둘 수 이다. 

예제를 보면 component에서 상태 업데이트하는 부분을 정의하지 않고 따로 나눠서 바깥에서 들고온다. 

구조 분해를 통해 새객체를 만들어 주는 식으로만 해도 매번 새롭게 binding이 된다 .

- useCallback

매번 바뀌는 함수가 아닌, 계속 유지되는 함수를 사용할 때 useCallback을 사용한다. 항상 같아야 나중에 처리할 때 변경을 감지하고 useEffect에 걸어줄 수 있다. 

왜 분리하는가? 앞에서 말했듯 UI / 비즈니스간 관심사의 분리를 적용해서 복잡도를 낮추도록 한다. BUSIness logic의 경우 분리가 안되면 UI 변화를 통해 검사해야하지만 분리한다면 신경쓸것 필요없이 test를 적용할 수 있어 테스트 작성시에도 용이하다. 공학적인 접근에는 알빠노주의가 선호된다