## Redux Toolkit

- 일반 리듀서

```tsx
// <ASIS: 일반 리듀서>
const rootReducer = combineReducers({
    counter: counter,
});
const store: createStore(rootReducer);
```

- 리덕스 툴킷

```tsx
const store = configureStore({
    reducer: {
        counter: counter,
    }
})
export default store;
```

전에는 action value와 reducer를 직접 타이핑해서 만들어 줬다. 리덕스 툴킷에서는 createSlice()를 사용해서 코드를 줄일 수 있다.

## HTTP

### 웹 통신

- 서버와, 클라이언트의 대화 방식은 보통 ‘데이터’로 이루어진다.
- 웹 통신은 약속(=프로토콜)이다.
    - 프로토콜 : 서버와 클라이언트가 대화하는 방식을 정하고 그 방식대로 데이터를 주고 받아야 오류가 생기지 않는다. 그 약속을 프로토콜(protocol)이라고 한다. 특히 웹에서 서버와 클라이언트가 주고 받은 상호간의 약속(프로토콜)을 **HTTP프로토콜**이라고 한다.
- 서버 : 서비스를 제공하는 주체
- HTTP Request를 보내고 HTTP Response를 받는다.

![IMG_200BBBE45BCF-1.jpeg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e33e972e-43b5-44a3-a3c9-594eb752bf55/IMG_200BBBE45BCF-1.jpeg)

### 메서드

약속의 종류라고 생각하면 된다.

GET - 조회

POST - 생성

PUT, PATCH - 수정(변경)

DELETE - 삭제

### 상태코드

오류를 보내는 코드

클라이언트가 서버에 어떤 요청을 하고 나면, 서버는 그에 맞는 응답을 제공한다. 그때, 각 응답은 상태코드를 갖는다.

- 1xx(정보) : 요청을 받았으며 프로세스를 계속 진행
- 2xx(성공) : 요청을 성공적으로 받았으며 인식했고 수용
- 3xx(리다이렉션) : 요청 완료를 위해 추가 작업 조치가 필요
- 4xx(클라이언트 오류) : 요청의 문법이 잘못되었거나 요청을 처리할 수 없다.
- 5xx(서버 오류) : 서버가 명백히 유효한 요청에 대한 충족을 실패

### 미들웨어

리덕스에서 dispatch하면 action 이 리듀서로 전달되고, 리듀서는 새로운 state를 반환한다. 여기에서 미들웨어를 사용하면 이 과정 사이에 우리가 하고 싶은 작업들을 넣을 수 있다.

예를 들어, counter 프로그램에서 ‘더하기’버튼을 클릭했을 때 바로 ‘1’을 더하지 않고 3초를 기다렸다가 더해지도록 구현하려면 미들웨어를 사용하면 된다. dispatch가 되자마자 바로 action이 리듀서로 가서 새로운 state를 반환해버리기 때문이다.

리덕스 미들웨어를 사용하는 이유는 서버와의 통신을 위해서 사용하는 것이 대부분이고, 그 중에서도 많이 사용되고 있는 리덕스 미들웨어는 Redux-thunk라는 것이 있다.

<aside>
💡 dispatch(함수) → 함수 실행 → 함수 안에서 dispatch(객체)

</aside>

- 리덕스 툴킷 구조 준비
    - 구현 순서
        1. thunk 함수 만들기 : createAsyncThunk → reduxToolkit 내장 API
        2.  createSlice 안에 있는 extraReducer를 수정함으로써 thunk 등록
        3. dispatch
        4. 테스트

**counterSlice.js**

thunk 안에 2개의 input

 - 이름 : 의미는 크게 없다.

 - 함수 : 기능. 서버에 요청.

```jsx
// 1. thunk 함수 만들기
export const __addNumber = createAsyncThunk(
	"ADD_NUMBER_WAIT",
	(payload, thunkAPI) => {
		// 수행하고 싶은 동작 : 3초 기다리기
		setTimeout(() => {
			thunkAPI.dispatch(addNumber(payload));
		}, 3000)
	}
);
```

**App.jsx**

```jsx
const onClickAddNumberHandler = () => {
	dispatch(__addNumber(+number));
};
```

→ number값이 counterSlice.js의 payload로 들어간다.

### 정리

- 리덕스 미들웨어를 사용하면 액션이 리듀서로 전달되기 전 중간에 어떤 작업을 할 수 있다.
- Thunk를 사용하면 **객체가 아닌 함수를 dispatch**할 수 있게 해준다.
- 리덕스 툴킷에서 Thunk함수를 생성할 때는 createAsyncThunk를 사용한다.
- createAsyncThunk() 의 첫 번째 자리에는 action value, 두 번째 자리에는 함수가 들어간다.
- 두 번째로 들어가는 함수에서 두 개의 인자를 꺼내어 사용할 수 있는데 첫 번째 인자는 컴포넌트에서 보내준 payload이고, 두 번째 인자는 thunk에서 제공하는 여러가지 기능이다.
