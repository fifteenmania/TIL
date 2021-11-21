# git-page에 빌드 결과물만 배포하기
- webpack을 사용해 번들링할 경우, git-page에서 index.html을 찾지 못하는 문제가 생긴다.
- 이를 해결하기 위해 git worktree를 활용, 빌드 결과물 폴더만 다른 브랜치로 관리하여 git-page에서 호스팅시켜 준다.
- [참고 블로그](https://velog.io/@bigsaigon333/gh-pages-dist-%EB%94%94%EB%A0%89%ED%86%A0%EB%A6%AC%EB%A7%8C-deploy-%ED%95%98%EA%B8%B0)
## 새 배포 브랜치 생성
```console
git switch --orphan gh-pages
git commit --allow-empty -m "init"
git push origin gh-pages
git switch develop
rm -rf dist
git worktree add dist gh-pages
cd dist
npm run build
cd dist
git add .
git commit -m "build 0"
git push origin gh-pages
```
- npm run build를 실행하면 dist 폴더에 빌드 결과물이 저장될 경우이다.
- 기존 dist 폴더에 내용물이 있으면 워크트리가 생성되지 않기 때문에 지워주어야 한다.

## 기존 배포 브랜치 연결
```console
git worktree prune
git worktree add dist origin/gh-pages
npm run build
```
- 잘못해서 .git 파일째로 폴더를 날려버렸을 경우 prune 명령어로 워크트리를 정리해 준다.
- 리모트의 gh-pages 브랜치와 연결하여 배포 브랜치를 다시 설정한다.

## 웹팩 설정 수정
```js
// webpack.config.js
module.exports{
    output: {
        clean: {
            keep: ".git"
        },
    }
}
```
- 웹팩이 빌드할 때 .git 파일을 지워버리면 안 되기 때문에 keep 설정해 준다. 