---
description: Node Package Manager
---

# NPM

`NPM(Node Package Manager)` 는 javascript 패키지 저장소이다. 모듈(프레임워크나 라이브러리)은 JS 패키지를 모아 놓은 DB인 npm registry에서 받으며 npm 명령어를 쓰기위해서 필요한 것도 npm을 통해 받는다.

* package

package는 `NPM registry` 에 등록가능한 대상이고 node 모듈이거나 node 모듈을 포함한다. `package.json`이 꼭 있어야 한다.

* module

`/node_modules` 안에 담기고 Node `require()`로 호출 가능한 파일/디렉토리이다. `package.json`은 선택 사항이다.

module ⊂ package

## package.json

`package.json`은 package의 metadata이고, `npm init`을 했을 때 생성되는 파일이다. 안드로이드에서의 매니페스트 파일과 비슷한 위치이다.

`dependencies` 와 `devDependencies` 가 있는데, dev의 경우엔 개발할 때만 쓰이는 종속성 모듈을 넣는다. 개발은 typescript로 하지만 배포는 typescript로 운영시에 일일이 변환해서 실행하는게 아니라 변환한 것을 배포하는 것이므로 필요없다.

개발용 설치시에는 `--save-dev` / `-D` 옵션을 넣어준다.

* version

0.0.0 (major / minor / patch) 로 나누어서 설정 한다. semantic versioning 참고.

* scripts

실행 할 스크립트를 미리 설정해 놓는다. `npm <스크립트 이름>` 으로 실행 가능하다

## package-lock.json

`/node_modules` 나 `package.json`을 건들면 자동으로 생성되는 파일이다. `package-lock.json`으로 설치하면 파일 생성시와 똑같은 종속성 트리 정보의 `/node_modules`를 받을 수 있다.

모듈 별로 버전 업데이트가 된다 해도 해당 패키지 개발 당시의 버전으로 잠금(lock)이 되기 때문에 종속성이 충돌하지 않는다.

만약 협업할 때 이 파일이 없으면 심히 곤란해질 것 같다. 그리고 프론트엔드 쪽이 정말 빠르게 바뀌는 편인데 옛날 프로젝트를 돌린다 치면 충돌없이 돌리려면 필수로 보인다.

## node\_modules

npm을 통해 설치된 모듈은 node\_modules란 폴더에 담기게 되는데, 모듈 용량이 꽤 되기 때문에 git에 올릴 때는 .gitignore로 해당 경로를 제외 시켜줘야 한다. 이전에 git으로 올릴 때 신경 안쓰고 올렸다가 용량제한에 걸린적이 있었으니 더더욱 주의해야 한다. 처음 프로젝트 설정시 미리미리 .gitignore을 설정하는 것이 좋은 습관이다.

* .gitignore 만들때 유용한 사이트
  * [.gitignore 쉽게 만들어주는 사이트](https://www.toptal.com/developers/gitignore)
  * [github gitignore 양식](https://github.com/github/gitignore)

그리고 `/node_modules`는 해당 프로젝트에만(local install) 설치한 모듈을 담기 때문에 global install한 패키지는 다른 곳에 담긴다. 전역 설치는 `-g` 옵션으로 가능하고 `/usr/local`/Node 설치 폴더에 담긴다.

## npx

설치안한 npm package를 사용가능한 커맨드이다. 물론 설치한 것도 가능하다. 설치한 것을 쓸 때는 `/node_modules/.bin` 에 있는 것을 실행한다.

```bash
npx -- <pkg>[@<version>] [args...]
npx --package=<pkg>[@<version>] -- <cmd> [args...]
npx -c '<cmd> [args...]'
npx --package=foo -c '<cmd> [args...]'
```

## reference

* [about npm](https://docs.npmjs.com/about-npm)
* [package와 모듈](https://docs.npmjs.com/about-packages-and-modules)
* [package.json 상세](https://docs.npmjs.com/cli/v9/configuring-npm/package-json)
* [semantic versioning](https://docs.npmjs.com/about-semantic-versioning)
* [package-lock.json](https://docs.npmjs.com/cli/v9/configuring-npm/package-lock-json)
* [node\_modules 관련](https://docs.npmjs.com/cli/v9/configuring-npm/folders)
* [npx](https://docs.npmjs.com/cli/v9/commands/npx)
* [MD040 지원 언어](https://www.rubycoloredglasses.com/2013/04/languages-supported-by-github-flavored-markdown/)
