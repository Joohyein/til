## onKeyPress 이벤트 핸들링

input창에 입력을 하고 Enter를 눌렀을 때 함수가 실행되게 할 수 있.

```jsx
const onKeyPress = e => {
  if (e.key === 'Enter') {
    btnClickAddHandler();  // todo박스가 추가되는 함수
  }
};
```

```jsx
<label for="content">
	내용 
	<input 
		type="text" 
		id="content" 
		value={content} 
		onChange={contentChangeHandler} 
		onKeyPress={onKeyPress} 
	/>
</label>
```

## useRef

**DOM 요소에 접근할 수 있도록 하는 React Hook이다.**

- 아이디 입력창에 10자리가 입력되는 순간 비밀번호 입력창으로 focus 이동시키기

```jsx
import React from 'react'
import { useRef, useEffect, useState } from 'react'

function App() {
  const idRef = useRef('');
  const pwRef = useRef('');
  const [id, setId] = useState(''); 

  const idChangeHandler = (e) => {
    setId(e.target.value);
  }

  useEffect(()=> {
    idRef.current.focus();
  }, []);
  useEffect(()=>{
    if(id.length >= 10){
      pwRef.current.focus();
    }
  }, [id]);
  return (
    <div>
      <div>
        아이디 : <input type="text" value={id} onChange={idChangeHandler} ref={idRef}/>
      </div>
      <div>
        비밀번호 : <input type="password" ref={pwRef} />
      </div>
    </div>
  )
}

export default App
```

- useEffect

렌더링 될 때, 특정한 작업을 수행해야할 때 설정하는 훅이다. (ex. console, alert.. ) 어떤 컴포넌트가 화면에 나타나거나 사라질때 실행하고싶다면 사용한다.

위 예제에서는 useRef를 사용했을 때 리렌더링이 되어야 화면에 보이기 때문에 useEffect를 함께 사용해줬다.
1. input에 값을 입력
2. state가 변경
3. state가 바뀌었기 때문에 App 컴포넌트가 리렌더링된다.
4. 리렌더링 → useEffect() 실행
    - 의존성 배열
    
    이 배열에 값을 넣으면, 그 값이 바뀔 때만 useEffect를 실행한다. 
    
    ```jsx
    // useEffect에 빈 배열 추가해보기
    useEffect(()=>{
      console.log("혜인최고");
    }, []);
    ```
    
    의존성 배열을 아무것도 입력을 안해도 동작을 한다. 어떤 값이 변하던 간에 의존성 배열에는 값이 없기 때문에 어떤 state가 변해도 화면이 처음 로딩될 때만 동작한다(console.log()).
    
    ```jsx
    useEffect(() => {
    	console.log(`hello ${value}`);
    }, [value]);
    ```
    
    value값이 바뀔때 console.log가 찍힌다.
    
    → 콘솔창에 값이 두 개가 찍히는데 index.js에서 <React.StrictMode> 때문이다. 주석처리하면 한 번만 출력된다.
    
    화면에서 없어졌을 때 동작하는 useEffect
    
    ```jsx
    useEffect(()=>{
      console.log("혜인최고");
    	return () => {
    		console.log('빠이')
    	};
    }, []);
    ```
