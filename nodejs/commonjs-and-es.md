# 자바스크립트의 모듈 시스템

## CommonJS (CJS)
```
// A.js
let x = 10
let mod = require("./B").x;
console.log(mod) // 30

//B.js
let x = 20
exports.x = 30
```
- 웹 브라우저 이외의 환경에서 모듈 관리를 위해 만든 규격이다.
- 주로 nodejs 환경에서 사용된다.
- `require()`, `module.exports` 의 구문을 사용한다.
- 동기적으로 모듈을 불러와서 로드 중 주 스레드가 차단된다.
- export 객체에 값이 복사된다.
- CJS 모듈에서는 ESM 모듈을 불러올 수 없다. 
    - ESM은 모듈 최상부에서 비동기 실행을 지원해야 하기 때문이다. 
    - 반면 CJS는 모든 모듈을 동기로 불러오기 때문에 모듈 최상부의 비동기 실행을 허용할 수 없다.
- 주로 사용되는 환경이기 때문에 노드 모듈을 빌드할 때 CJS 또한 지원하는 것이 좋다.
- 브라우저용 배포를 위해서는 주로 번들러(rollup, webpack, esbuild 등)를 사용해 파일을 변환시키고 묶어 준다.
### 파생 규격
- 웹 브라우저 환경에서는 오랫동안 모듈 시스템이 존재하지 않았기 때문에 CJS에서 여러 파생 규격이 등장하였다.
- 비동기 실행을 지원하기 위해 AMD (Asynchronous Module Definition) 표준안이 탄생했다. AMD는 define 구문을 사용한다.
- AMD 기반의 모듈 로더로 RequireJS 가 주로 사용되었다.
- AMD와 CJS의 호환을 위한 UMD (Universial Module Definition) 패턴이 등장했다.

## ES Module (ESM)
```
import {a} from 'a.js'
import {fn} from 'fn.js'
import {Class} from 'class.js'

export const a = 1
export function fn(){}
export class Class{}
```
- 브라우저와 브라우저 외 환경에서 일관된 모듈 시스템을 지원하기 위해 만들어졌다.
- ES6 규격이며, node 14 부터 지원되었다. 
- 브라우저 환경에서는 `type="module"` 로 설정하여 활성화한다.
- `import`, `export` 구문을 사용한다.
- 의존 파일 분석에 따라 구문 분석이 실행된다.
- 비동기적으로 로드된다. 
- export 객체에 참조를 반환하는 함수가 정의된다.
- CJS 또는 브라우저 환경에서 ESM 을 사용하고 싶다면 .mjs 파일로 저장해야 한다.
- 보일러플레이트를 작성하거나 번들러를 이용하면 CJS 모듈을 불러올 순 있으나 효율적이진 않다.

## IIFE
```
(function () {
    var aName = "Barry";
})();
```

-   CommonJs 와는 반대로, 웹 브라우저에서 모듈 시스템과 유사한 환경을 지원하기 위한 기법이다.
-   자바스크립트의 closure를 이용해 전역 스코프를 오염시키지 않고 해당 모듈의 값들을 호출할 수 있게 지원한다.