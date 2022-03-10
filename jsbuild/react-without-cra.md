# webpack 으로 CRA 없이 리액트 빌드 설정하기
- electron 빌드 설정 중 CRA 만으로는 부족함을 느끼고 webpack을 공부해 보기로 했다.
- [참고 블로그](https://velog.io/@jeff0720/React-%EA%B0%9C%EB%B0%9C-%ED%99%98%EA%B2%BD%EC%9D%84-%EA%B5%AC%EC%B6%95%ED%95%98%EB%A9%B4%EC%84%9C-%EB%B0%B0%EC%9A%B0%EB%8A%94-Webpack-%EA%B8%B0%EC%B4%88)


## 기본 개념
### Webpack
- 자바스크립트 앱을 위한 static module bundler이다.
- 여러 개로 흩어진 에셋을 모아 하나의 파일로 묶어준다.
- 기본적으로 json과 js 파일만을 읽지만, loader를 추가하여 html 등 다른 종류의 파일 또한 읽어올 수 있다.
- plugin을 이용해 최적화, 환경 변수 주입 등의 변경 작업을 추가할 수 있다.
- development 모드와 production 모드를 지원한다.
- [공식 문서](https://webpack.js.org/concepts/)

### Babel
- ES6+ 문법으로 쓰여진 자바스크립트를 하위 호환되는 코드로 변환하기 위한 컴파일러이다.
- 문법 변환, polyfill, 코드 변환 등을 지원한다.
- JSX 등의 문법 또한 일반 자바스크립트 문법으로 변환해준다.
- annotation 이나 typescript 등도 처리한다.
- [공식 문서](https://babeljs.io/docs/en/)


## 일렉트론 빌드 설정파일
```javascript
// webpack.config.js
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
    entry: "./src/index.js",
    output: {
        filename: "bundle.js",
        path: path.resolve(__dirname, "./react_build"),
    },
    mode: "production",
    module: {
        rules: [
            {
                test: /.\html$/,
                use: [
                    {
                        loader: "html-loader",
                        options: {minimize: true}
                    }
                ]
            }
        ]
    },
    plugins: [
        new HtmlWebpackPlugin({
            template: "./public/index.html",
            filename: "index.html"
        })
    ]
};
```
