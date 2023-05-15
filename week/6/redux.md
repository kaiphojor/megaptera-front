# Redux 

- Redux
- Reflect

useDispatch 사용한다.

따라하기 

baseStore

store는 필요없다 (원래 redux 쓸때는) . 실제 redux 쓸 때는 초기값만 지정해준다. 


const initialState = this.state = {
      count: 0;
}
@singleton()
export deafult class Store extends BaseStore{

  state : Satate;
  reducer: (state: state, action : Action) => State;

  listeners = new Set<Listener>();
  constructor(initalState: State, reducer: Reducer) {
    this.state = initialState;
  }
    super();


  }

}
store {
  
}
reducer = (state, action ) =>{
  switch ( action.type) {
    case 'increase' : 
    return {
      ...statet,
      count: state.count  + 1
    };
    default : 
    return state; 
  }
  console.log( )
  return { ...state};
}

reducer = 

listener s = new Set<Listerner>(0; 

dispatch(action) {
  this.statet = this.reducter(this.state, action) ;
  this.publish();
})


hooks - useStore

export default function useStore(){
  const store = useStore();

  const dispatch = (action) => {
    store.dispatch({type: 'increase'})
  }
}

function useDispoatch() {
  const soter = useStore();
  return 
}

useDispatch 및 useStore를 쓴다. 

type Selector<T> = (state:State) => T;

payload? 