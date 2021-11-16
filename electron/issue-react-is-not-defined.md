# 이슈: react is not defined 문제
- 리액트 앱 빌드 결과물이 웹에서는 정상적으로 실햄됨에도 불구하고, renderer process 에서 불러오면 오류를 뱉는 경우가 있었다.
- 빌드 설정 잘못인 줄 알고 하루종일 헤맸는데, import React 를 모든 파일에서 해 주지 않아 생긴 문제였다.
- 근데 결론적으로는 빌드 설정에서 webpack의 ProvidePlugin으로 해결할 수 있으니, 빌드 문제라고 할 수 있을지도 모르겠다. 
- CRA를 쓰면 자동으로 설정돼 있는 부분이라 모르고 지나갔던 것 같다.

## 오류 전문
```console
bundle.js:2 ReferenceError: React is not defined
    at n (bundle.js:2)
    at oo (bundle.js:2)
    at Qu (bundle.js:2)
    at Ni (bundle.js:2)
    at Ci (bundle.js:2)
    at _i (bundle.js:2)
    at gi (bundle.js:2)
    at di (bundle.js:2)
    at Zi (bundle.js:2)
    at bundle.js:2
```
- production 모드로 빌드하면 위와 같은 에러가 뜨며 리액트 앱이 실행되지 않는다.

## 해결책
```javascript
// webpack.config.js
module.exports = {
    entry: "./src/index.js",
    output: {
        filename: "bundle.js",
        path: path.resolve(__dirname, "main", "compile")
    },
    mode: "production",
    plugins: [
        new webpack.ProvidePlugin({
            React: 'react'
        })
    ]
};
```
- 위와 같이 웹팩에서 ProvidePlugin을 이용해 자동 임포트 설정해 주면 의존성 오류가 발생하지 않는다.
- 위 설정을 하지 않으면 모든 모듈에서 `import React from 'react'`를 붙여주어야 한다.
