# git-page에 빌드 결과물만 배포하기
- webpack을 사용해 번들링할 경우, git-page에서 index.html을 찾지 못하는 문제가 생긴다.
- 이를 해결하기 위해 git worktree를 활용, 빌드 결과물 폴더만 다른 브랜치로 관리하여 git-page에서 호스팅시켜 준다.
- [참고 블로그](https://velog.io/@bigsaigon333/gh-pages-dist-%EB%94%94%EB%A0%89%ED%86%A0%EB%A6%AC%EB%A7%8C-deploy-%ED%95%98%EA%B8%B0)
