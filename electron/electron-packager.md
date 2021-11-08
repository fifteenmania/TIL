# electronPackager를 이용한 일렉트론 앱 빌드
- 공식 문서에서 추천하는 electron-forge는 .deb 등 패키징까지 자동화하긴 하나 크로스 플랫폼 빌드에 오류가 있다. 참고: [이슈: electronForge의 windows 빌드 실패 문제](./issue-electron-forge-build-fail.md)
- electron-packager를 사용하면 소스코드를 자동으로 받아 패키징하는 원리인 것 같다.
- 아이콘 부분은 추후에 추가 예정.
##  빌드 스크립트
```json
"scripts": {
    "start": "electron .",
    "package-linux": "electron-packager ./ App --out ./out/ --overwrite --asar --platform linux --arch x64",
    "package-win": "electron-packager ./ App --out ./out/ --overwrite --asar --platform win32 --arch x64",
    "package-darwin": "electron-packager ./ App --out ./out/ --overwrite --asar --platform darwin --arch x64"
  }
```
- 위와 같이 사용하면 asar 패키징까지 자동으로 이루어진다.
- asar는 작성된 소스 코드를 하나의 파일로 압축하여 로딩 속도를 높이고 소스코드 노출을 방지해준다.
