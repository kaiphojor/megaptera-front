# Routing

## HTML DOM API

[HTML DOM API](https://developer.mozilla.org/en-US/docs/Web/API/HTML_DOM_API)

html의 요소(elements)를 [DOM](https://developer.mozilla.org/ko/docs/Web/API/Document_Object_Model)을 통해 접근 조작이 가능한 인터페이스

Location 객체를 사용하기 위한 기반이다. Routing 기능을 사용하기 위해서는 URL을 접근,조작해야 하고, 그러기 위해 HTML DOM API 속 `Location.pathname`에 접근해야 한다.

### Location

[Location](https://developer.mozilla.org/ko/docs/Web/API/Location)

URL을 표현하는 interface. Document와 Window 모두 가지고 있다.

[Window.location](https://developer.mozilla.org/ko/docs/Web/API/Window/location)은  Window 객체의 Prop이다. document.location은 read only라는 점이 다르다.

#### Window

[Window](https://developer.mozilla.org/ko/docs/Web/API/Window)

DOM 문서를 담은 창 객체 / 인터페이스. [document](https://developer.mozilla.org/ko/docs/Web/API/Document)가 브라우저에 로드된 웹페이지를 표현하는 것과는 달리 브라우저 창을 표현하는 전역 객체다.

브라우저의 탭, 창을 조작가능하며 URL, 쿠키, 창 조절 또한 가능하다.

### pathname

[Location.pathname](https://developer.mozilla.org/en-US/docs/Web/API/Location/pathname)

`/` 으로 시작되는 URL의 path 정보

query 나 fragment는 포함하지 않는다

예시

```text
element : <a id="myAnchor" href="/en-US/docs/Location.pathname">
access : document.getElementById("myAnchor").pathname
result : '/en-US/docs/Location.pathname'
```
