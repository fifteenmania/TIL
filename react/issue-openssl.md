# 이슈: node 최신 버전 사용시 openssl 오류
- nodejs 최신 버전을 사용했을 경우, cra로 리액트 앱 생성 후 npm start 했을 때 openssl 관련 오류가 생기며 실행되지 않는다.
- 

## 에러 전문
```console
$ npm run start

> react-scripts start
```
```console
Starting the development server...

Error: error:0308010C:digital envelope routines::unsupported
    at new Hash (node:internal/crypto/hash:67:19)
    at Object.createHash (node:crypto:130:10)
    at module.exports (/home/fifteenmania/workspace/file-explorer/node_modules/webpack/lib/util/createHash.js:135:53)
    at NormalModule._initBuildHash (/home/fifteenmania/workspace/file-explorer/node_modules/webpack/lib/NormalModule.js:417:16)
    at handleParseError (/home/fifteenmania/workspace/file-explorer/node_modules/webpack/lib/NormalModule.js:471:10)
    at /home/fifteenmania/workspace/file-explorer/node_modules/webpack/lib/NormalModule.js:503:5
    at /home/fifteenmania/workspace/file-explorer/node_modules/webpack/lib/NormalModule.js:358:12
    at /home/fifteenmania/workspace/file-explorer/node_modules/loader-runner/lib/LoaderRunner.js:373:3
    at iterateNormalLoaders (/home/fifteenmania/workspace/file-explorer/node_modules/loader-runner/lib/LoaderRunner.js:214:10)
    at iterateNormalLoaders (/home/fifteenmania/workspace/file-explorer/node_modules/loader-runner/lib/LoaderRunner.js:221:10)
/home/fifteenmania/workspace/file-explorer/node_modules/react-scripts/scripts/start.js:19
  throw err;
  ^

Error: error:0308010C:digital envelope routines::unsupported
    at new Hash (node:internal/crypto/hash:67:19)
    at Object.createHash (node:crypto:130:10)
    at module.exports (/home/fifteenmania/workspace/file-explorer/node_modules/webpack/lib/util/createHash.js:135:53)
    at NormalModule._initBuildHash (/home/fifteenmania/workspace/file-explorer/node_modules/webpack/lib/NormalModule.js:417:16)
    at /home/fifteenmania/workspace/file-explorer/node_modules/webpack/lib/NormalModule.js:452:10
    at /home/fifteenmania/workspace/file-explorer/node_modules/webpack/lib/NormalModule.js:323:13
    at /home/fifteenmania/workspace/file-explorer/node_modules/loader-runner/lib/LoaderRunner.js:367:11
    at /home/fifteenmania/workspace/file-explorer/node_modules/loader-runner/lib/LoaderRunner.js:233:18
    at context.callback (/home/fifteenmania/workspace/file-explorer/node_modules/loader-runner/lib/LoaderRunner.js:111:13)
    at /home/fifteenmania/workspace/file-explorer/node_modules/babel-loader/lib/index.js:59:103 {
  opensslErrorStack: [ 'error:03000086:digital envelope routines::initialization error' ],
  library: 'digital envelope routines',
  reason: 'unsupported',
  code: 'ERR_OSSL_EVP_UNSUPPORTED'
}

Node.js v17.0.1
```

## 해결책
```console
nvm install --lts
nvm use --lts
```
- 위와 같은 방법으로 nvm을 이용해 LTS(v16.13.0)으로 변경하면 정상적으로 실행된다.