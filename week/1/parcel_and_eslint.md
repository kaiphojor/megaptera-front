# Parcel & ESLint

## Bundler(번들러)

번들링 - 파일들을 둘둘 묶어서 하나로 만들어내는 과정

번들러 - 번들링을 해주는 도구

바벨 - 최신버전 자바스크립트를 옛날 버전 브라우저를 지원하도록 구버전으로 변환 시켜주는 도구

### Parcel

빌드 툴
npx parcel index.html --port 8080
(package.json에 source: 파일을 추가해서 index.html을 안넣어도 된다)

정적 파일을 빌드에 포함 시킬 경우 - reference의 parcel-reporter-static-files 참고. static/images 에서 이미지 파일을 불러온다.

빌드 명령어

`npm parcel build`
`npx servor ./dist` - 현재 배포되는 환경을 확인할 때

tip

* 빌드 새로 했을 때는 캐시를 날려버리고 다시 불러오기 한다.

## Lint(린트)

소스 코드 정적 분석 도구

* 스타일을 일관적으로 유지
* 잠재적인 문제 탐색
* 좋은 사례 추천 -> 최신 스타일 학습 가능

보안 관련 정적 분석 도구가 있는데, 쓰임만 다르지 분석하는 것은 똑같다. 동적 분석 도구는 정적 분석 도구보다 시간이 확실히 오래걸린다.

### ESLint

더글러스 크록포드가 저자이고, ESlint를 만들었다. typescript 또한 지원한다.

linter는 코딩 컨벤션을 지키게 만들어서 여러명이 함께 일할 때 일관성 있는 코드를 짤 수 있게 도와준다.

#### es lint 저장 시 자동 수정 설정

`.vscode/settings.json` 에 추가

```json
{
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    }
}
```

other tip

* 80 줄 마다 줄 그어 주기 - `.vscode/settings.json` : `"editor.rulers": [ 80 ],`
* 맨 끝 빈 줄 지워주기 - [링크 참고](https://marketplace.visualstudio.com/items?itemName=shardulm94.trailing-spaces)

## Reference

[parcel-reporter-static-files](https://github.com/elwin013/parcel-reporter-static-files-copy)
[servor](https://www.npmjs.com/package/servor)
