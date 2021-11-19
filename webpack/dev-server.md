# 개발용 dev-server 설정
- CRA 쓰면서 제일 좋았던 기능이 devserver 기능이었다.
- 파일 하나 수정할 때마다 일일히 빌드 안 해줘도 서버에서 자동으로 업데이트되고 새로고침까지 해 준다.
- 컨텍스트를 완전히 새로 로드하는 게 아니라서 부작용이 있을 수 있다고 하는데, 아직 찌꺼기가 남는 경험은 없었다.

## 설정
```js
// webpack.dev.js
module.exports = merge(common, {
    mode: "development",
    devtool: "inline-source-map",
    devServer: {
        static: "./temp",
        port: "3000",
        hot: true
    }
});
```
```json
// package.json
{
  "scripts": {
    "start:dev": "webpack serve --config webpack.dev.js",
    "start": "npm run start:dev"
  },
}
```
- 생각보다 매우 간단하다. 이래서 다들 웹팩 쓰나 보다.