# push-dir을 이용해 gh-pages없이 배포하기

- 개인 플젝에서 깃 페이지로 배포할 때 gh-pages를 즐겨 사용하고 있었다.
- 그런데 요새 무슨 버그가 있는지, npm run deploy로 잘 배포가 되지 않는다.
- 같은 시도를 꼭 두세 번 해야 배포에 성공했다. 
- 답답해서 gh-pages를 버리고 손수 배포하기로 했다. push-dir 모듈을 이용하면 된다.

## 준비사항
- `.env.local`파일에 `PUBLIC_URL=/memopad`(리포지터리 이름)를 추가해 준다. 이게 없으면 깃페이지에서 404 오류가 뜬다.
- `package.json`파일에 `"deploy": "push-dir --dir=build --branch=gh-pages"` 커맨드를 추가한다. 
- 변경사항 커밋 후 `npm run deploy`를 입력하면 빌드 폴더를 바라보고 gh-pages-[hash] 이름의 브랜치가 생성되며 푸시된다.

## 브랜치 삭제 팁
- 배포할 때마다 새로운 이름의 로컬 브랜치가 생겨서 귀찮을 때가 있다.
- 한 번에 지우려면 `git branch | grep gh-pages-* | xargs git branch -D` 커맨드를 사용하자.
