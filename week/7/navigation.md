# Navigation

웹 애플리케이션 내에서 다른 페이지 또는 뷰로 이동하는 기능. 브라우저 주소를 변경, 변경한 주소에 따라 다른 컴포넌트/라우트를 렌더링해서 다양한 화면을 보여줌.

navigation과 그냥 창 이동과의 차이는 전체를 렌더링하느냐 여부이다. navigation 시 공통 부분은 rendering 할 필요가 없어 효율적이다.

React 에서는 React Router를 통해 제공한다.

## Web APIs - History

[History API](https://developer.mozilla.org/ko/docs/Web/API/History_API)

history 객체를 통해 브라우저의 방문기록의 앞/뒤로 가거나 세션기록, history 스택을 접근, 조작이 가능하다.

```javascript
history.back(); // 뒤로 가기
history.forward(); // 방문기록 앞으로 가기
history.go(1); // 현재 페이지 기준 한페이지 앞으로 가기
history.go(0); // 또는 인자 없이.
history.go(-1); // 현재 페이지 기준 한페이지 뒤로 가기

```

## React Router - NavLink, Link, Navigate, useNavigate

[NavLink](https://reactrouter.com/en/main/components/nav-link)

다른 링크 하곤 달리 active / pending 여부를 알 수 있는 링크. navigation menu를 만들 때 어떤 것이 현재 선택 된 것인지 구분할 때 유용하다.

접근성 관련 유용한 정보도 제공

[Link](https://reactrouter.com/en/main/components/link)

클릭시 다른 페이지로 갈수 있게 해주는 element. `<a>` 속 `href` 속성을 통해 어느 자원으로 연결할지 정한다.

[Navigate](https://reactrouter.com/en/main/components/navigate)

element가 render 되고 나서 현재 위치를 바꾼다.

[useNavigate](https://reactrouter.com/en/main/hooks/use-navigate)

Navigate를 선언적이 아닌 명령적 프로그래밍 식으로 수행할 때 사용하는 함수다.