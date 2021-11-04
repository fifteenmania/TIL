# 예제: contextIsolation 모드의 렌더러 프로세스로 메인 이벤트 전송
- browserWindow.webContents.send를 사용하면 별 거 아니라고 생각할 수 있지만, renderer 쪽에서 이벤트 핸들러 붙이는 게 생각보다 까다롭다.
- 주요 함수의 정의는 renderer.js 에 있는데, 이벤트 핸들러를 preload.js 에서 작성하여야 하기 때문이다. 공식 문서조차 업데이트가 안 된 건지 렌더러 스크립트 내에서 require문을 사용한다.
- 사실 서드파티 엑세스가 없으면 contextIsolation 안 해도 된다고는 하는데, 그래도 언젠간 필요할 수 있으니 규정을 준수해보고자 한다.
- [공식 문서](https://www.electronjs.org/docs/latest/api/web-contents)


## 메인 메뉴에서 파일 불러왔을 때 활성 창에 이벤트 전송 코드
```javascript
// main.js
const focusedWindow = BrowserWindow.getFocusedWindow()
loadTextFile(focusedWindow).then((result)=>
    focusedWindow.webContents.send('file-render:opened', result))
```

```javascript
// preload.js
function dispatchMainEvent(eventName, payload) {
    const mainHandler = document.getElementById('main-event-receiver');
    const openedEvent = new CustomEvent(eventName, {
        detail: payload,
    })
    mainHandler.dispatchEvent(openedEvent);
}

ipcRenderer.on('file-render:opened', (event, result) => {
    dispatchMainEvent('file-render:opened', result);
})
```

```javascript
// renderer.js
const mainEventReceiver = document.getElementById('main-event-receiver');
mainEventReceiver.addEventListener('file-render:opened', (event) => {
    const result = event.detail;
    handleFileLoad(result);
})
```

```html
<!-- index.html -->
<body>
    <input type="hidden" id="main-event-receiver">
</body>
```

- 아이디어는 preload.js에서 ipcRenderer로 이벤트를 받고, 자바스크립트 customEvent객체로 한 번 변환해 주는 것이다. 
- 위 코드에서 preload.js의 dispatchMainEvent가 해당 역할을 한다.
- html에서 메인 이벤트 수신용의 hidden input을 하나 추가하여, cutomEvent를 여기로 전송시켰다.
- 레이어가 하나 추가되어 이벤트를 두 곳에서나 처리해야 하는 번거로움이 있지만, main과 renderer간 종속성 없이 이벤트를 처리할 수 있게 되었다.
