# 재미있는 브라우저 user-agent 이야기
- 자바스크립트에서 user-agent로 브라우저 정보를 조회하면 항상 혼란스러운 텍스트를 보게 된다.
- 예를 들자면 사파리 브라우저에서 userAgent 를 조회하면 저런 이상한 텍스트를 보게 된다.
```js
navigator.userAgent = "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.0 Safari/605.1.15"
```
- 그냥 사파리라고 하면 안되나? 모질라 5.0 은 왜 있고 웹킷인데 무슨 게코랑 비슷하대?
- 크롬도 마찬가지로 항상 자기가 모질라라느니 게코랑 비슷하다느니 하는 이상한 정보를 뱉어낸다.
- 궁금해져서 찾아보니 이런 글이 있었다. [링크](https://webaim.org/blog/user-agent-string-history/) 

## 대충 번역
- 먼 옛날 윈도우에 mosaic 브라우저가 있었다고 한다.
- 넷스케이프 브라우저는 mosaic killer를 표방하며 자신들을 mozilla라 불렀다고 한다.
- 모질라는 frame 을 지원하지만 mosaic 은 지원하지 않기 때문에 웹마스터들은 모질라 브라우저에만 frame 을 포함해 보냈다.
- 모질라는 이걸 두고 윈도우를 조롱하였다.
- 넷스케이프 죽이기에 나선 윈도우는 새로 개발한 익스플로러의 유저 에이전트를 *Mozilla/1.22 (compatible; MSIE 2.0; Windows 95)* 같이 보내기 시작했다.
- 넷스케이프는 익플에 죽었지만 모질라 재단은 gecko 랜더링 엔진을 개발했다. 게코는 성능이 매우 좋았다.
- 그러곤 스스로를 *Mozilla/5.0 (Windows; U; Windows NT 5.1; sv-SE; rv:1.7.5) Gecko/20041108 Firefox/1.0* 라 불렀다.
- 다른 브라우저들이 게코 엔진을 갖다 쓰며 파폭인 척하기 시작했다. 이때부터 온갖 브라우저에 *Mozilla/5.0 Gecko/~~* 를 붙이는 전통이 시작됐다.
- 웹마스터들은 또 브라우저 스니핑해서 파폭에만 좋은 컨텐츠를 보냈다.
- 리눅스 커뮤니티는 KHTML 엔진을 개발했는데 게코만큼 좋은 페이지를 얻기 위해 *Mozilla/5.0 (compatible; Konqueror/3.2; FreeBSD) (KHTML, like Gecko)* 같은 정보를 보냈다.
- 애플은 KHTML을 포크해서 웹킷을 개발했는데 KHTML용 페이지를 얻기 위해 *Mozilla/5.0 (Macintosh; U; PPC Mac OS X; de-de) AppleWebKit/85.7 (KHTML, like Gecko) Safari/85.5* 같은 정보를 보냈다.
- 크롬은 웹킷을 포크해서 개발했기 때문에 사파리용 페이지를 받고 싶었다. 그래서 나온게 *Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US) AppleWebKit/525.13 (KHTML, like Gecko) Chrome/0.2.149.27 Safari/525.13* ????
- 속이는 사람만 있고 속는 사람은 없다. 개발자만 브라우저 체크하기 힘들어진 것이다.


