# 일렉트론 프로세스와 ipc

## 일렉트론의 프로세스 모델
- 일렉트론은 크로뮴의 멀티 프로세스 모델을 차용하여 메인 프로세스(main)와 각 렌더러 프로세스(renderer)가 독립적으로 작동한다.
- 메인 프로세스의 생명주기는 app 모듈에서 관리된다.
- 메인 프로세스는 네이티브 OS의 기능을 직접 지원하는 API에 접근 가능하다. 즉, nodejs의 모듈을 직접 사용할 수 있다.
- 렌더러 프로세스는 개별 BrowserWindow에 붙어서 작동한다.
- 렌더러 프로세스는 웹 브라우저의 렌더러와 매우 유사하게 작동한다.
- https://www.electronjs.org/docs/latest/tutorial/process-model

## preload script
- contextIsolation: true 로 렌더러 프로세스를 실행하면 메인 프로세스로의 모든 직접 접근이 차단된다. 
- preload srcipt에서 conetextBridge.exposeMainWorld를 통해 렌더러 프로세스에서 접근 가능한 메인 프로세스의 API를 제공할 수 있다.

## ipcMain
- 메인 프로세스에서 렌더러 프로세스와의 통신을 위한 모듈이다.
- 일반적으로 렌더러 프로세스의 요청에 대한 응답만을 정의한다. 메인 프로세스에서 먼저 요청을 보낼 때는 다른 모듈을 사용한다.
- https://www.electronjs.org/docs/latest/api/ipc-main
### ipcMain.handle(channel, listener) 
- 리턴 값이 요청에 대한 응답값으로 사용된다. 
- promise를 리턴할 경우, 프로미스 결과 값이 요청에 대한 응답값으로 사용된다.
- ipcRenderer.invoke 에 대한 응답을 정의하기 위해 사용한다.
- 렌더러 프로세스에서 일반 함수처럼 처리할 수 있어 코드가 한결 이해하기 쉽다.
### ipcMain.on(channel, listener) 
- 특정 채널 요청에 대한 응답을 정의한다.
- 동기나 비동기 요청을 모두 처리할 수 있으나 비동기 요청의 경우 응답 채널을 따로 정의해야 해서 가독성이 더 떨어진다.

## ipcRenderer
- 렌더러 프로세스에서 메인 프로세스로의 통신을 위한 모듈이다.
- 자바스크립트의 event hander 등에 붙여서 사용한다.
- https://www.electronjs.org/docs/latest/api/ipc-renderer
### ipcRenderer.on(channel, listener)
- ipcMain의 비동기 응답에 대응하기 위한 함수이다.
- 보통 ipcRenderer.send -> ipcMain.on -> ipcRenderer.on 의 형태가 된다.
### ipcRenderer.send(channel, listener)
- 특정 채널에 응답을 요청한다.
- 동기나 비동기 요청을 모두 보낼 수 있다.
- 입력 인자들은 직렬화된다.
- DOM element는 전송할 수 없다. POJO 만을 지원한다.
- structured clone algorithm을 사용한다고 하는데 뭔지 더 봐야 할 것 같다.
### ipcRenderer.invoke(channel, listener)
- promise를 반환하는 간편한 요청 함수이다.
- 세부 사항은 ipcRenderer.send와 유사하나 코드가 간결하다.

## 이 장에 대한 고민
- string을 채널명으로 쓰는데 코드 여러 부분에 채널명이 흩어져 있으면 유지보수가 어렵지 않나? 한 곳에서 정리할 방법은 없을까?
- 일반적으로 event handler는 가볍게 유지하라는 말이 있는데, 그러면 무거운 로직을 어디서 처리하는 게 좋을까?
