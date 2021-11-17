# 효율적 resizable sidebar 구현하기
- 놀랍게도 리액트에서 resizable sidebar 구현체가 생각보다 별로 없다는 것을 알았다.
- vscode와 같이 파일 탐색기의 창 크기 조절을 지원해주고 싶어 만들어보았다.
## 구현
```js
// Resizer.js
function Resizer({setWidth}) {
    const resizerRef = useRef(null);

    const resize = (event) => {
        const newSize = event.clientX - sidebarRef.current.getBoundingClientRect().left;
        setWidth(newSize);
    }
    
    useEffect(() => {
        const resizeHandler = () => {
            document.addEventListener("mousemove", resize, false);
            const handleMouseup = () => {
                document.removeEventListener("mousemove", resize, false);
                document.removeEventListener("mouseup", handleMouseup);
            }
            document.addEventListener("mouseup", handleMouseup, false);
        };
        resizerRef.current.addEventListener("mousedown", resizeHandler);
        return () => resizerRef.current.removeEventListener("mousedown", resizeHandler);
    }, [])
    return <div className="component-resizer" ref={resizerRef}></div>
}
```
```css
/* style.css */
.component-resizer {
    z-index: 2;
    cursor: col-resize;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    border: 3px solid rgba(255, 255, 255, 0.05);
}

.component-resizer:hover {
    border: 3px solid rgba(0, 0, 255, 1);    
}

.file-tree-wrapper {
    display: flex;
    flex-grow: 0;
    flex-shrink: 0;
    flex-direction: row;
}

```
```js
//FileTree.js
function FileTreeWrapper() {
    const [width, setWidth] = useState(100);
    return <section className="file-tree-wrapper" style={{width:width}}>
        <FileTree />
        <Resizer sidebarRef={fileTreeContainerRef} setWidth={setWidth}/>
    </section>
}
```
- Resizer 컴포넌트에서 클릭 이벤트를 받을 경우 마우스 움직임을 감지하는 리스너를 부착한다.
- 마우스 움직임에 따라 width state를 업데이트하며, 마우스를 놓는 순간 리스너를 해제한다.
