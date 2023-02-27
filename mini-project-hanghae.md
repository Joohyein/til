## error

upstream dev브랜치에서 pull을 할 때 아래와 같은 오류가 계속 떴다.

```jsx
hyein@juhyein-ui-noteubug nyangdang % git pull upstream dev
From https://github.com/NyangDang/frontend
 * branch              dev        -> FETCH_HEAD
error: Your local changes to the following files would be overwritten by merge:
        nyangdang/node_modules/.cache/.eslintcache
Please commit your changes or stash them before you merge.
Aborting
```

현재 디렉토리의 파일을 임시로 백업하고 깨끗한 상태로 돌린다.

```jsx
% git stash // 현재 Staging 영역에 있는 파일의 변경사항을 스택에 넣어 둔다
% git pull upstream dev // 원격 저장소에서 내 로컬 브랜치로 변경사항을 적용한다
% git stash pop // 변경사항을 적용하고, 스택에서 제거
```
