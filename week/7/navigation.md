# Navigation

웹 애플리케이션 내에서 다른 페이지 또는 뷰로 이동하는 기능. 브라우저 주소를 변경, 변경한 주소에 따라 다른 컴포넌트/라우트를 렌더링해서 다양한 화면을 보여줌.

React 에서는 React Router를 통해 제공한다.

## Web APIs - History

[History API](https://developer.mozilla.org/ko/docs/Web/API/History_API)

history 객체를 통해 브라우저의 방문기록의 앞/뒤로 가거나 history 스택을 접근, 조작이 가능하다.

```javascript
history.back(); // 뒤로 가기
history.forward(); // 방문기록 앞으로 가기
history.go(1); // 현재 페이지 기준 한페이지 앞으로 가기
history.go(-1); // 현재 페이지 기준 한페이지 뒤로 가기

```

## React Router - NavLink, Link, Navigate, useNavigate