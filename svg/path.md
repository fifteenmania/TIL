# SVG path
- 일반적인 형태를 그리기 위한 요소이다.
- d 속성에 경로 커맨드를 적어 만든다.
- stroke 속성에 색 등을 넣는다.
- 경로 커맨드 약어는 다음과 같다.
- MoveTo: M, m
- LineTo: L, l, H, h, V, v
- Cubic Bezier Curve: C, c, S, s
- Quadratic Bezier Curve: Q, q, T, t
- Elliptical Arc Curve: A, a
- ClosePath: Z, z

## 전체적인 특징
- 각각의 커맨드는 절대 좌표를 기준으로 하는 대문자 커맨드, 상대 좌표를 기준으로 하는 소문자 커맨드로 구성된다.
- 이후의 좌표에 명령을 지정하지 않으면 적절한 커맨드가 암묵적으로 선택된다. 예를 들어, 커서 이동 다음에서는 경로 커맨드가 선택된다. 절대 좌표 다음엔 절대 좌표가, 상대 좌표 다음엔 상대 좌표가 선택된다.
- 유선형 경로를 그리기 위해 기준점 사이를 보간하는 베지에 곡선이 사용된다.
- 유선형 폐곡선을 그리기 위해 타원 곡선이 사용된다.
- 끝에 z 커맨드를 붙여 폐곡선으로 만들 수 있다.


## MoveTo
- 단순히 커서를 옮기는 명령어이다.
- 해당 위치에서부터 다음 커맨드를 실행한다.

| Command | Parameter | Notes |
|---|---|---|
| M | (x, y)+ | 옮길 절대 좌표를 지정한다.  |
| m | (dx, dy)+ | 옮길 상대 좌표를 지정한다. |

## LineTo
- 직선 경로를 잇기 위해 사용된다.
- 2차원 좌표를 이동하는 L 계열 명령어와, 수평축만 이동하는 H 계열 명령어, 수직축만 이동하는 V 계열 명령어가 있다.
- L 계열 명령어는 x, y 좌표 한 개씩을 인자로 받으며 H, V 계열은 하나의 값을 인자로 받는다.

## Cubic Bezier Curve
- 두 개의 컨트롤 포인트와 두 개의 끝점이 필요하다.
- 시작점은 현재 커서 위치를 기준으로 하므로 두 개의 컨트롤 포인트와 끝점만 정해주면 된다.
- 컨트롤 포인트를 직접 지정하는 C 계열 명령어와 끝쪽 컨트롤 포인트를 대칭으로 사용하는 S 계열 명령어가 있다.

## Quadratic Bezier Curve
- 베지에 커브를 연속적으로 잇기 위해 사용된다.
- 시작점, 끝점, 컨트롤 포인트의 세 점이 필요하지만 시작점은 현재 커서 위치를 기준으로 하여 두 점만 정해주면 된다.
- 컨트롤 포인트를 직접 지정하는 Q 계열 명령어와 이전 컨트롤 포인트를 대칭으로 사용하는 T 계열 명령어가 있다.
- T 계열 명령어를 사용할 때 이전 커브가 4차 베지에 커브가 아니라면 컨트롤 포인트는 시작점과 같게 선택된다.

