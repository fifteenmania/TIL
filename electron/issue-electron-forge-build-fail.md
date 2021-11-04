# 이슈: electronForge의 windows 빌드 실패 문제
- 크로스 플랫폼이라면서...! 개발용으로 우분투 20 LTS 를 사용하고 있는데, 타 플랫폼 빌드가 되지 않는다.
- 집컴 사면 꼭 윈도우도 같이 설치할거다. 억울해서 못살겠다.

## 실행한 스크립트
```console
$ electron-forge make --platform win32 --targets @electron-forge/maker-squirrel
```
```
> text-editor@0.1.0 make-windows
> electron-forge make --platform win32 --targets @electron-forge/maker-squirrel

✔ Checking your system
✔ Resolving Forge Config
We need to package your application before we can make it
✔ Preparing to Package Application for arch: x64
✔ Preparing native dependencies
✔ Packaging Application
Making for the following targets: squirrel
✖ Making for target: squirrel - On platform: win32 - For arch: x64

An unhandled error has occurred inside Forge:
An error occured while making for target: squirrel
spawn mono ENOENT
Error: spawn mono ENOENT
    at Process.ChildProcess._handle.onexit (node:internal/child_process:282:19)
    at onErrorNT (node:internal/child_process:475:16)
    at processTicksAndRejections (node:internal/process/task_queues:83:21)
```
- win32용 squirrel 빌드 스크립트를 실행했을 때, mono 관련 오류가 뜨면서 빌드가 되지 않는다.

## 시도 사항
- wine64와 mono를 설치하였다.
- mono-runtime 도 설치 시도하였으나 리포지터리를 찾지 못한다.
- stackoverflow 에 검색해봤을 때 squirrel 자체에 오류가 있다고 한다. 

## 향후 시도해볼 방법들
- 빌드 도구를 electron-packager로 바꾸면 어떨까? 같은 오류를 겪은 사람이 있다고 한다. [참고](https://stevenklambert.com/writing/comprehensive-guide-building-packaging-electron-app/)
- 소스 코드를 직접 받아서 빌드하는 게 가능하다고 한다. electron-forge 문제라면 이것도 시도해 볼 만해 보인다. [참고](https://www.electronjs.org/docs/latest/tutorial/application-distribution)