### useEffect

상세페이지에 들어갔을 때 새로고침을 해야 화면에 보여지는 문제가 생겼다.

**에러 메세지(일부)**

<aside>
💡 It looks like you wrote useEffect(async () => ...) or returned a Promise. Instead, write the async function inside your effect and call it immediately:

</aside>

useEffect()에서 getMovie()를 리턴해줘서 오류가 났던 것이었다.

```jsx
const getMovies = async() => {
  const json = await (await fetch("https://yts.mx/api/v2/list_movies.json?minimum_rating=9&sort_by=year")).json();
  setMovies(json.data.movies);
  setLoading(false);
}
```

```jsx
// 잘못 쓴 코드
useEffect(() => getMovie(), []);
```

→ 이렇게 코드를 작성했을 때 unmount가 되었을 때 실행해준다. 

```jsx
useEffect(() => {
    getMovie();
}, []);
```

```jsx
function Hello() {
  useEffect(()=>{
    console.log("hi")
    return () => console.log("bye")
  },[]);
  return <h1>hello</h1>
}
```

---

- 새로고침 시에도 리덕스 내의 데이터를 유지하는 방법
    
    리액트는 기본적으로 SPA라서 페이지를 새로고침하면 값이 휘발된다. 따라서 처리를 해줘야 하는데, 서버에 모든 자료를 저장하게 되면 보안적으로도, 자원적으로도 손해다. 따라서 스토리지를 통해서 해결할 수 있다. 
    
    - 로컬 스토리지
        - 브라우저가 닫혔다가 열려도, OS가 재부팅 되어도 값이 유지가 된다.
    - 세션 스토리지
        - 새로고침에서는 값이 휘발되지 않지만 브라우저를 닫거나 OS를 재부팅하고 탭을 닫는 행위로도 스토리지가 날라간다.

- useRef
    - 값이 변해도 리렌더링을 할 필요가 없는 데이터를 useRef로 관리할 수 있다.
    - ref의 기본 기능처럼 DOM을 직접 조작해야만 할 때(스크롤을 옮기거나 포커스를 줄 때)사용된다.
