# chai의 should/expect/assert 비교

- assert와 expect는 둘 다 Object.prototype을 변화시키지 않는다. 따라서 불변성을 유지하고 싶면 should를 사용하지 않는 게 좋다.
- assert와 expect는 커스텀 메세지를 어디서든 출력시킬 수 있는 반면, should는 그런 기능이 없다.
- expect가 가독성이 더 좋다. assert는 메세지 없이는 무얼 테스트하는지 알기 힘들다.
- 따라서 expect 인터페이스를 사용하는 게 제일 나을 듯 하다.
- [스택오버플로우 글 참고](https://stackoverflow.com/questions/21396524/what-is-the-difference-between-assert-expect-and-should-in-chai)