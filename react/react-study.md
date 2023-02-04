## React

- CRA(Create React App)

한 줄의 명령어 입력으로 React 프로젝트 개발에 필요한 필수요소를 자동으로 구성하는 방법이다. React 프로젝트를 쉽고 빠르게 만들 수 있도록 도와준다.

- 상대경로 import → 절대경로 지정
    - root경로에 json파일 생성 후 아래 코드 작성
    
    ```json
    {
        "compilerOptions": {
            "baseUrl": "src"
        },
        "include": ["src"]
    }
    ```
    

### React component

컴포넌트를 사용하면 UI를 재사용이 가능한 개별적인 여러 조각으로 나눌 수 있다. “props”라고 하는 임의의 입력을 받은 후 화면에 어떻게 표시되는지를 기술하는 react element를 반환한다.

1. 함수형 컴포넌트
    
    ```jsx
    function hello(props){
    	return <h1>hello, {props.name}</h1>
    }
    ```
    
2. 클래스형 컴포넌트
    
    ```jsx
    class hello extends React.component {
     render() {
    		return <h1>hello, {props.name}</h1>
    	}
    }
    		
    ```
    

 두 가지 모두 기능상으로 동일하지만 공식 홈페이지에서는 **함수형 컴포넌트**를 사용하기를 권장하고 있다. 

- 함수, 화살표함수 사용해보기

```jsx
import 'App.css';

function App() {
  function onClickButtonHandler1() {
    alert('hello');
  }
  const onClickButtonHandler2 = () => {
    alert('hello');
  }
  return (
    <div
      style={{
        height: "100vh",
        display: "flex",
        flexDirection: "column",
        justifyContent: "center",
        alignItems:"center",
      }}
    >
      Hello
      <button onClick={onClickButtonHandler1()}>클릭1</button>
			<button onClick={onClickButtonHandler2}>클릭2</button>
    </div>
    
  );
}

export default App;
```

- 부모, 자식 컴포넌트
    
    ```jsx
    // src/App.js
    import React from "react";
    
    function Child() {
    	return <div>child component</div>
    }
    
    function App() {
    	return (
    		<child />
    		<child />
    		<child />
    	);
    }
    // 여러 줄로 입력하려면 괄호 필요
    export default App;
    ```
    
    `App.js` 파일 안에서 `Child` 라는 새로운 컴포넌트를 만들고 Child 컴포넌트를 App 컴포너트에서 마치 HTML 태그를 쓰듯이 넣었다. 컴포넌트 안에 다른 컴포넌트를 넣을 수 있다.
    

---

### JXS(JavaScript + XML)

```jsx
// 자바스크립트 안에서 html 태그 같은 마크업을 넣어 UI작업을 편하게 할 수 있다.
const hello = <div>
		<h1>안녕</h1>
		<p>반가워</p>
	</div>;
```

<aside>
💡 리액트 돔을 구성하는 건 리액트 요소, 돔을 구성하는 건 돔 요소

</aside>

react snippet extension 설치

→ rfc 또는 rfce 입력 후 tab

```jsx
// rfc
import React from 'react'

export default function App() {
  return (
    <div>App</div>
  )
}
```

```jsx
// rfce
import React from 'react'

function App() {
  return (
    <div>App</div>
  )
}

export default App
```

전체를 감싸주는 최상위 태그는 하나만 있어야 한다.

```jsx
import React from "react";

export default function App() {
	const number = 10;
	
	const pTagStyle = {
		color: "red",
	};
	return (
		<div className="test">
			<p style={pTagStyle}>
				{number > 9 ? number + "은 9보다 크다" : number + "은 9보다 작다"}
			</p>
		</div>
	);
}
```

---

### props - properties

컴포넌트끼리의 정보교환 방식

props를 통해 부모에서 자식으로 값을 내려줄 수 있다. (단방향)

자식 컴포넌트에서 부모로부터 받은 값을 렌더링하는 방법을 알 수 있다.

```jsx
import React from "react";

function Son(props) {
	console.log(props); // motherName: "엄마" 
	console.log(props.motherName); // 엄마
	return <div>나는 {props.motherNmae}의 아들이에요</div>;  // 화면에 렌더링
}

function Mother() {
	const name = '엄마';  // name을 자식 컴포넌트인 Son은 props를 통해 물려받을 수 있다.
	return <Son motherName={name}/>;  // 부모 컴포넌트에서 자식 컴포넌트로 데이터를 전달
}

function GrandFather() {
	return <Mother />;
}

function App() {
	return <GrandFather />;
}
```

불필요한 props drilling이 생길 수 있다.

**children props**

```jsx
import React from "react";

function App() {
	return <User> 
		안녕하세요
		</User>  // 하위 컴포넌트인 User 컴포넌트 호출, '안녕하세요'가 props.children
}
function User(props) {
	console.log(props); // {children: '안녕하세요'}
	return <div></div>;
}

export default App;
```

여는 태그, 닫는 태그 사이에 값을 써주면 자동으로 children이라는 props를 갖게 된다.

- children을 사용하는 이유?
    
    컴포넌트를 재사용하기 편리하다. 똑같은 형식의 페이지를 쉽게 만들 수 있다.
    
     
    

- props 추출
    
    **구조 분해 할당**
    
    ```jsx
    function App() {
    	const obj = {
    		name: 'zzanggu',
    		age: 5,
    		height: 120,
    	};
    	const { name, age, height } = obj;
    	
    	console.log(name); // zzanggu
    	console.log(age); // 5
    	console.log(height); // 120
    ```
    
     1. App.js
    
    ```jsx
    import React from "react";
    import Child from "Child";
    
    export default function App() {
      const age = 5;
    	return (
        <>
        <Child age={age} name={'zzanggu'}>
          이름
        </Child>
    
        </>
      );
    }
    ```
    

1. Child.js

```jsx
import React from 'react'

function Child({name, age, children}) {
    console.log(name); // zzanggu
    console.log(age); // 5
    console.log(children); // 이름
  return (
    <div>Child</div>
  )
}

export default Child
```

```jsx
Child.defaultProps={
	name: '이름'
};
// default값을 설정할 수 있다.
```

---

### state

UI를 바꾸기 위해서 state를 사용한다. 즉, 렌더링을 다시 하기 위해서 사용한다.

```jsx
import {useState} from "react";

function App() {
	const [count, setCount] = useState('initial Value');
	return <duv></div>
}
// setCount : count를 변경할 수 있는 메서드
```

**useState사용해보기**

```jsx
import {useState} from "react";
import "App.css";

export default function App() {
	const [name, setName] = useState('김천재');
	return (
    <div>
      {name}
      <button onClick={() => setName('김만재')}>
        btn
      </button>
    </div>
  );
}
```

**onChange**

```jsx
import {useState} from "react";
import "App.css";

export default function App() {
  const [fruit, setFruit] = useState('');
	return (
    <div>
      과일 : <input
        value={fruit}  // 이 값도 setFruit에 따라 변경? 초기 인풋값이여서 상관없나?
        onChange={function(event){
          console.log(event.target.value); // 우리가 입력하는 값들이 출력된다.
          setFruit(event.target.value);
        }}
      />
      <br />
      {fruit}
    </div>
  );
}
```

state사용해보기

```jsx
import {useState} from "react";
import "App.css";

export default function App() {
  const [id, setId] = useState('');
  const [pw, setPw] = useState('');

  function clickhandler() {
    alert(`아이디는 ${id} 이고 비밀번호는 ${pw},입니다.`);
    setId('');
    setPw('');
  }

	return (
    <div>
      아이디 : <input
        type="text"
        value={id}
        onChange={function(event){
          setId(event.target.value);
        }}
      />
      <br />
      비밀번호 : <input
        type="password"
        value={pw}
        onChange={function(event){
          setPw(event.target.value);
        }}
      />
      <br />
      <button onClick={clickhandler}>
        로그인
      </button>
    </div>
  );
}
```

---

### 불변성

컴포넌트의 생명주기. 갱신된다는 것은 렌더된다는 뜻이다. state와 불변성의 관계?

불변성이란 메모리에 있는 값을 변경할 수 없는 것이다.

- 원시 타입 : 숫자, 문자, 불리언 … → 불변성이 있다.
- 참조 타입 : 배열, 객체, 함수 …  → 불변성이 없다.

 - 데이터 할당 과정

```jsx
let obj1 = {
	name: 'kim',
};
let obj2 = {
	name: 'kim',
};
console.log(obj1 === obj2); // false
```

**React에서 렌더링이 되는 조건**

 - **state의 변화에 따라 결정된다.** 

 - state가 변했으면 리렌더링을 하고, 변하지 않았으면 리렌더링을 하지 않는다.

 - 단순 변수는 무시한다.

```jsx
const [obj, setObj] = useState({
	name: "wonjang",
	age: 21,
});
```

```jsx
obj.name = "twojang";
setObj(obj); // 콘솔창에는 값이 바뀌어 나오지만 렌더링되지 않는다. 
```

```jsx
obj.name = "twojang";
const obj2 = {...obj};
setObj(obj2);
```

---

### 실습

```jsx
import React, {useState} from "react";
import "App.css";

export default function App() {
  const [count, setCount] = useState(0);
  const minus = function() {
    setCount(count - 1);
  }
  function func() {
      setCount(count - 2);
  }
  return (
    <div>
      <div>{count}</div>
      <button
        onClick={ () =>{
          const plus = count + 1;
          setCount(plus);
        }}
      > +1 </button>
      <button onClick={minus}> -1 </button>
      <button onClick={func}> -2 </button>
			// 또는 <button onClick={()=>func()}> -2 </button>
    </div>
  );
}
```
