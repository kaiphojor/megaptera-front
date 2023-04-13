# React

## React란?

JS 기반의 UI 라이브러리. 선언형이라서 간단하게 뷰를 만들고, 코드별 역할을 쉽게 파악할 수 있다.

## React 컴포넌트

재사용 가능한 UI 조각. props를 매개변수처럼 입력 받고, React 엘리먼트를 반환

* 함수 컴포넌트

```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

* ES6 class 컴포넌트

```javascript
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

render() - Class component의 필수 구현 메서드

react element(JSX) / 배열/ fragemnt / Portal / 문자열 / 숫자를 반환

## React 리렌더링

리렌더링은 이미지를 업데이트하는 과정이다. 이미지를 업데이트 할 때는 컴포넌트의 상태 변경과 관련이 있다. 상태변경은 react DOM(VDOM) 에서 DOM으로 이어지고, DOM 에서 UI를 변경 한다. `setState` 가 실행 될 때 해당 컴포넌트 호출과 동시에 별 상관없어 보이는 모든 하위 컴포넌트들도 리렌더링 당한다.

만약, props의 참조가 변하지 않거나 제대로 업데이트가 안되었을 때에는 리렌더링이 발생하지 않는다.

수동으로 강제 리렌더링을 할 때에는 `forceUpdate`를 이용한다. hooks 에서는 `React.useState`를 사용해서 강제 리렌더링을 시켜버린다.

## IoC(Inversion of Control)

```javascript
function Page(props) {
  const user = props.user;
  const userLink = (
    <Link href={user.permalink}>
      <Avatar user={user} size={props.avatarSize} />
    </Link>
  );
  return <PageLayout userLink={userLink} />;
}

// 이제 이렇게 쓸 수 있습니다.
<Page user={user} avatarSize={avatarSize} />
// ... 그 아래에 ...
<PageLayout userLink={...} />
// ... 그 아래에 ...
<NavigationBar userLink={...} />
// ... 그 아래에 ...
{props.userLink}
```

제어의 역전. user, avatarSize에 대한 제어를 최상위 컴포넌트에 넘겨준다. 그렇게 하면 해당 정보를 Page가 Avatar 컴포넌트에 직접 넣어준다. props와 상관없는 컴포넌트가 props를 전달받지 않는다. Page의 제어권은 더 커지고 코드는 더 깔끔해진다.

만약 Component가 중첩되어서 깊이가 더더욱 깊어진다면, 설계자체에 문제가 있을 가능성도 있겠지만 그 상황에서 제어의 역전을 적용하면 중간 과정이 생략되어 힘들게 전달을 안해도 된다.

## Library vs Framework

[react 개발자 답변](https://twitter.com/trueadm/status/1194567962784653312) - 둘 다 해당 된다.

[InversionOfControl - 리팩터링 저자](https://martinfowler.com/bliki/InversionOfControl.html) - 내가 프레임워크를 부르는 것이 아니라 프레임워크가 나를 부른다. 이러한 제어의 역전이 프레임워크와 라이브러리를 구분하는 핵심 요소

IoC를 통해 상태/ 업데이트를 선언형으로 비교적 간단하고 가독성있게 구성한다.

프레임워크이고, 라이브러리이나, 면접 시에는 출제자의 의도를 잘 유추하여 유연하게 답변하도록 하자.

## reference

* [react 문서](https://ko.reactjs.org/)
* [component](https://ko.reactjs.org/docs/components-and-props.html)
* [엘리먼트 렌더링](https://ko.reactjs.org/docs/rendering-elements.html#rendering-an-element-into-the-dom)
* [컨텍스트](https://ko.reactjs.org/docs/context.html#before-you-use-context)
