# ES Modules vs CommonJS

모듈 : 따로 떼어내서 필요할 때 가져와서 재사용 가능한 프로그램

## CommonJS

웹 서버, desktop, 브라우저 명령줄에서 동작하는 어플리케이션 생태계를 만들기 위한 모임, 표준, 시스템.
Node JS에서 javascript 코드 패키징하는 기본 방법

* `require` 모듈을 가져온다

```javascript
const circle = require('./circle.js');
console.log(`The area of a circle of radius 4 is ${circle.area(4)}`);
```

* `exports` 모듈을 내보낸다

```javascript
const { PI } = Math;
exports.area = (r) => PI * r ** 2;
exports.circumference = (r) => 2 * PI * r;
```

* `module` 현재 모듈을 보여주는 객체

## ES Modules

* `import` 모듈을 가져온다

`import { name, draw, reportArea, reportPerimeter } from './modules/square.js';`

* `export` 모듈을 내보낸다

`export { name, draw, reportArea, reportPerimeter };`

* `type="module"` 모듈 포함 시키기

`<script type="module" src="main.js"></script>`

## reference

* [es module-node](https://nodejs.org/api/esm.html)
* [모듈](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Modules)
* [common JS](https://wiki.commonjs.org/wiki/Modules/1.1)
* [common js-node](https://nodejs.org/api/modules.html#modules-commonjs-modules)
