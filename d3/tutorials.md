# d3 기초
- data driven documents 의 약자이다.
- 웹 문서에서 html, css, svg 등을 조작하기 위한 라이브러리이다.
- 웹 표준을 준수하여 어느 환경에서나 사용할 수 있으며 외부 설정과도 그대로 호환된다.
- 공식 사이트에서 다양한 예제를 지원하지만 양이 너무 방대해서 오히려 공부하기 힘들었다. [d3 공식 사이트](https://d3js.org)
- 기본적으로 그래픽 생성이 svg 조작을 통해 이뤄지기 때문에 svg 규격을 먼저 이해해야 한다. [w3c의 svg 규격 문서](https://www.w3.org/TR/SVG/struct.html#NewDocument)
- 개인적으론 이쪽 튜토리얼이 더 이해하기 쉬운 것 같다. [rip tutorial](https://riptutorial.com/d3-js)

## 선택자와 바인딩
```js
var p = d3.select("body")
  .selectAll("p")
  .data([4, 8, 15, 16, 23, 42])
    .text(function(d) { return d; });

// Enter…
p.enter().append("p")
    .text(function(d) { return d; });

// Exit…
p.exit().remove();
```
- .select 함수 등으로 요소를 선택한다.
- 선택자로 선택된 요소에 .data 로 배열 요소를 바인딩하면 선택된 요소와 배열 요소가 하나씩 쌍을 이루게 된다.
- 선택된 요소의 수보다 배열 요소가 더 많다면, 남는 요소는 .enter 로 바인딩할 수 있다.
- 선택된 요소의 수가 배열 요소보다 더 많다면, 남는 요소는 .exit 함수로 바인딩할 수 있다.
- 위 예제와 같이 순서대로 조작/생성/삭제를 실행하면 정확히 배열 요소만큼 원하는 요소를 만들 수 있다. 

## 조작자
- .style 함수로 html 요소의 css를 조작한다.
- .attr 함수로 요소의 어트리뷰트를 조작한다.
- .append 함수로 새로운 요소를 하위 요소로 삽입한다.
- .on 함수로 이벤트 리스너를 삽입한다.
- .transition 함수로 interpolation을 사용하여 점진적인 스타일 변화를 지원한다. 

## d3 좌표 시스템
- 왼쪽 위에서부터 페이지의 폭 방향이 x, 높이 방향이 y이다.
- 상위 요소를 기준으로 상대 좌표를 사용한다.
