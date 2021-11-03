# 예제: contextIsolation 모드의 렌더러 프로세스에서 노드 모듈 사용하기
- contextIsolation을 사용할 경우 렌더러 프로세스에서는 노드 모듈을 직접 가져올 수 없다.
- preload 스크립트에서는 사용 가능하기 때문에 여기서 모듈을 임포트하여 api에 붙여 준다.

## markdown to HTML 렌더링을 위한 marked 적용 코드
```javascript
// preload.js
const marked = require('marked');
contextBridge.exposeInMainWorld('markdown', {
    render: (markdown) => marked.parse(markdown)
})
```

```javascript
// renderer.js
function renderMarkDownToHtml(markdown) {
    return window.markdown.render(markdown);
}
```


## 이 장에 대한 고민
- 해당 api가 렌더러 프로세스에서 실행되는 게 확실한지 확인이 필요할 것 같다.
- 커널 권한 사용하는 노드 모듈도 이렇게 사용 가능할까? 오류가 날까?