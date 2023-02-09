***React.memo***
- 리렌더링의 발생 조건
    - 컴포넌트에서 state가 바뀌었을 때
    - 컴포넌트가 내려받은 props가 변경되었을 때
    - 부모 컴포넌트가 리렌더링 된 경우 자식 컴포넌트는 모두 리렌더링 된다.
- 최적화(Optimization)
    
    리액트에서 불필요한 렌더링이 발생하지 않도록 최적화 하는 대효적인 방법
    
    - memo(React.memo) : 컴포넌트를 캐싱
        - 부모 컴포넌트가 리렌더링 된 경우 자식 컴포넌트는 모두 리렌더링 되는걸 방지
        - `React.memo` 를 이용해서 컴포넌트를 **메모리**에 저장해두고 필요할 때 가져다 쓴다. 임시로 메모리에 저장해두는 것을 캐싱이라고 말한다. 이렇게 하면 부모 컴포넌트의 `state` 의 변경으로 인해 `props` 가 변경이 일어나지 않는 한 컴포넌트는 리렌더링 되지 않는다.
            
            ```jsx
            export default React.memo(Box1);
            ```
            
    - useCallback : 함수를 캐싱
    - useMemo : 값을 캐싱


React.memo는 컴포넌트를 메모이제이션 했다면, useCallback은 인자로 들어오는 함수 자체를 기억(메모이제이션)한다.

- Box1에서 ‘초기화’버튼을 클릭하면 함수가 실행되도록 만드는데 그 함수는 App.js에서 만들고 props로 내려준다. 이렇게 하면 App.js와 Box1.js가 리렌더링되는데 이는 함수형 컴포넌트를 사용했기 때문이다.
    
    App.jsx에 작성한 ‘초기화’하는 함수가 별도의 공간을 바라보고 있는 것인 주솟값을 저장한다. 초기화하는 함수가 실행되지 않아도(state가 변하지 x) 리렌더링이 되는 이유는 초기화하는 함수가 새로운 주솟값을 갖게 되기 때문이다.
    
    이런 상황들 때문에 useCallback을 통해서 함수 자체를 메모이제이션 하는 방법을 사용한다.
    
- App.jsx가 처음 렌더링 될 때 initCount 함수를 메모리 공간에 그대로 저장한다.

```jsx
const initCount = useCallback(() => {
  setCount(0);
}, [count]);
```

dependency array → count가 변경될 때만큼은 useCallback으로 인해서 다시 저장된다.

### useMemo

- React.memo : 컴포넌트의 메모이제이션
- useCallback : 함수
- useMemo : value → 함수가 리턴하는 값 자체

```jsx
const value = 반환할_함수();

const value = useMemo(()=>{
	return 반환할_함수()
}, [dependencyArray]);
```

dependencyArray의 값이 변경될 때만 `반환할_함수()` 가 호출된다. 

그 외의 경우에는 memoization 해놨던 값을 가져오기만 한다.

- 무거운 컴포넌트

```jsx
import React, { useState } from 'react'

function HeavyComponent() {
    const [count, setCount] = useState(0);

    const heavyWork = () => {
        for(let i = 0; i < 100000000; i++){}
        return 100;
    }
    const value = heavyWork();
  return (
    <div>
        <p>나는 무거운 컴포넌트야</p>
        <button onClick={()=>{
            setCount(count + 1);
        }}>클릭하면 아래 count가 증가해요</button> <br />
        {count}<br />
        {value}
    </div>
  )
}

export default HeavyComponent
```

count가 증가하는 버튼을 누르면 함수 전체가 리렌더링 되어서 count가 증가하는 속도가 느려진다. heavyWork() 때문에 다른 작업도 함께 느려진다. 이를 해결하기 위해서 heavyWork에서 리턴하는 값(100)을 메모리에 저장해두자.

<aside>
💡 `useMemo` 의 첫 번째 파라미터에는 어떻게 연산할지 정의하는 함수를 넣어주고 두 번째 파라미터에는 deps 배열을 넣어주면 되는데, 이 배열 안에 넣은 내용이 바뀌면, 우리가 등록한 함수를 호출해서 값을 연산해주고, 만약에 내용이 바뀌지 않았다면 이전에 연산한 값을 재사용하게 된다.

</aside>

- 객체를 useMemo로 감싸기

```jsx
const me = useMemo(()=>{
	return {
		name: 'hyein',
		age: 27,
		isAlive: isAlive ? "생존" : "사망",
	};
}, [isAlive]);
```

isAlive가 바뀌면 리렌더링된다.

- 주의사항

메모리에 저장되게 되는데 메모리를 많이 사용하면 성능이 안좋아져서 반드시 필요할 때에만 사용하자.
   
   
