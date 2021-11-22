# SVG 요소 기초
- Scaleable Vector Graphics 의 약자로, 2차원 벡터 그래픽을 XML로 표현하기 위한 마크업 언이이다.
- 웹 표준으로 다른 형식과 잘 호환되도록 설계되었다.
- 검색, 색인, 스크립트 적용, 압축 등이 가능하며 텍스트 편집기로 생성 가능하다.
- 크기에 따른 화질 저하 등이 없어 편리하다.
- W3C에서 1999년부터 개발 관리하고 있다.
- [모질라 참고 문서](https://developer.mozilla.org/ko/docs/Web/SVG)
## svg
- 새 좌표계와 뷰포트를 정의한다. 
- 보통 svg 요소의 가장 바깥에서 사용되지만 안쪽에서 사용할 수도 있다.

## g
- 여러 svg 요소를 그룹핑할 때 사용한다.
- 그룹에 사용한 변형은 하위 요소들에 상속된다.
- use 요소를 그룹 요소들을 한 번에 재사용할 수 있다.

## text
```svg
<svg viewBox="0 0 240 80" xmlns="http://www.w3.org/2000/svg">
  <style>
    .small { font: italic 13px sans-serif; }
    .heavy { font: bold 30px sans-serif; }

    /* Note that the color of the text is set with the    *
     * fill property, the color property is for HTML only */
    .Rrrrr { font: italic 40px serif; fill: red; }
  </style>

  <text x="20" y="35" class="small">My</text>
  <text x="40" y="35" class="heavy">cat</text>
  <text x="55" y="55" class="small">is</text>
  <text x="65" y="55" class="Rrrrr">Grumpy!</text>
</svg>
```
- 텍스트로 구성된 요소이다.
- ```<text>```태그로 둘러싸이지 않은 텍스트는 렌더링되지 않는다.
- 다른 요소와 같이 그라디언트, 패턴, 클리핑 패스, 마스크, 필터 등 변형을 적용할 수 있다. 

## use
```svg
<svg viewBox="0 0 30 10" xmlns="http://www.w3.org/2000/svg">
  <circle id="myCircle" cx="5" cy="5" r="4" stroke="blue"/>
  <use href="#myCircle" x="10" fill="blue"/>
  <use href="#myCircle" x="20" fill="white" stroke="red"/>
</svg>
```
- 이미 정의된 요소를 재사용할 때 사용한다.
- id를 레퍼런스해서 사용하며, 속성을 오버라이드할 수 있다.

## path
```svg
<svg viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
  <path d="M 10,30
           A 20,20 0,0,1 50,30
           A 20,20 0,0,1 90,30
           Q 90,60 50,90
           Q 10,60 10,30 z"/>
</svg>
```
- 불특정한 형태를 그리기 위한 요소이다.
- d 속성에 경로 커맨드를 적어서 정의한다.
- 다른 모든 요소는 path 요소를 통해 정의할 수도 있다.

## filter
```svg
<svg width="230" height="120" xmlns="http://www.w3.org/2000/svg">
  <filter id="blurMe">
    <feGaussianBlur stdDeviation="5"/>
  </filter>
  
  <circle cx="60" cy="60" r="50" fill="green"/>
  
  <circle cx="170" cy="60" r="50" fill="green" filter="url(#blurMe)"/>
</svg>
```
- 직접 렌더링될 수 없고 다른 요소의 filter 속성에서 참조되기만 하는 요소이다.
- 가우시안 블러, 요소 중첩, 광원효과 등 이미지 효과를 주기 위해 사용된다.

## mask
```svg
<mask id="myMask">
<!-- Everything under a white pixel will be visible -->
    <rect x="0" y="0" width="100" height="100" fill="white" />

    <!-- Everything under a black pixel will be invisible -->
    <path d="M10,35 A20,20,0,0,1,50,35 A20,20,0,0,1,90,35 Q90,65,50,95 Q10,65,10,35 Z" fill="black" />
</mask>
```
- 사용하면 마스크의 모양만큼 다른 요소가 제거된다. 
- 다른 요소에서 뚫기 위한 펀치카드 모양으로 생각하면 된다.
