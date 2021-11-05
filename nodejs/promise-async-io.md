# promise를 사용한 비동기 파일 입출력
- electron 쓰다 보니 꼭 필요한 부분이었다.
- 사람들이 대부분 fs의 콜백 함수 기준으로 문서를 적어 놓아, 프로미스 기반 api 사용법을 따로 정리해 본다.
- https://nodejs.org/api/fs.html

## 프로미스 기반 api
- nodejs v10.0.0 버전에서 프로미스 기반 입출력 api가 추가되었다.

## 디렉토리 읽기
### fsPromises.openDir(path[, options])
```javascript
try {
  const dir = await opendir('./');
  for await (const dirent of dir)
    console.log(dirent.name);
} catch (err) {
  console.error(err);
}
```
- fs.Dir 객체를 반환한다.
- fs.Dir 객체는 async iterator에서 fs.Dirent 객체를 반환한다.
- fs.Dir 객체는 async iterator가 종료될 때에 자동으로 회수된다.

### fs.Dirent
- ```fs.name```으로 폴더 또는 파일명을 얻을 수 있다. 
- ```fs.isDirectory()```메소드로 폴더인지 여부를 알 수 있다.

### 예제: 디렉토리 트리 재귀 파싱
```javascript
async function getDirectoryTree(dirName) {
    const result = {
        path: dirName,
        name: path.basename(dirName),
        items: []
    }
    const dir = await opendir(dirName, {encoding: 'utf-8'});
    for await (const dirent of dir) {
        const direntPath = path.join(dirName, dirent.name)
        if (dirent.isDirectory()) {
            const subTree = await getDirectoryTree(direntPath)
            result.items.push(subTree);
        } else {
            result.items.push({
                path: direntPath,
                name: dirent.name,
                items: null
            })
        }
    }
    return result;
}
```
- async iterator를 이용하여 간편하게 파싱할 수 있다.

## 파일 한 번에 읽고 쓰기
### fsPromises.readFile(path[, options])
```javascript
const path = './my/app/path';
try{
    const content = await readFile(path, {encoding: 'utf-8'});
} catch (error) {
    // exception
}
```
- FileHandle 오브젝트 또는 url을 인자로 넣어도 된다.
- 성공시 파일 내용을 리턴한다.
- 공식 문서에서는 AbortController() 를 사용하여 입출력을 중간에 취소할 수 있다고 한다.

### fsPromises.write(file, data[, options])
```javascript
const path = './my/app/path';
const content = 'some-interesting-texts';
try{ 
    await writeFile(path, content, {encoding: 'utf-8'});
} catch (error) {
    // excetion
}
```
- read와 마찬가지로 버퍼나 FileHandle, url등을 인자로 넣어도 된다.
- 성공시 undefined를 리턴한다.

## 이 장에 대한 고민
- fileHandler를 메인 프로세스에서 갖고 있어야 할까? 렌더러에서 파일명만 갖고 있어도 충분할까?
- 비동기 스트리밍을 위해서는 fileHandler를 갖고 있어야 하는데, 그럼 결국 메인에서 저장하는 게 맞지 않을까? 
- 열려 있는 파일의 상태 관리를 위한 프로세스를 따로 만드는 게 나으려나?

