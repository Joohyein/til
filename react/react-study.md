## Styled components

- 2.2 Adapthing and Extending
    
    css를 재사용하는 방법 → props로 다른 부분만 바꿔준다
    
    ```jsx
    import styled from "styled-components";
    
    function App() {
      return (
       <Father>
        <Box bgColor="green">
          <Text>Hyein zzang</Text>
        </Box>
        <Box bgColor="yellowgreen"></Box>
       </Father>
      );
    }
    
    export default App;
    
    const Father = styled.div`
      display: flex;
    `;
    const Box = styled.div`
      background-color: ${(props) => props.bgColor};
      width:100px;
      height:100px;
    `
    
    const Text = styled.span`
      color: white;
    `
    ```
    
    - 컴포넌트 확장하기
    
    ```jsx
    import styled from "styled-components";
    
    function App() {
      return (
       <Father>
        <Circle bgColor="green"></Circle>
        <Box bgColor="yellowgreen"></Box>
       </Father>
      );
    }
    
    export default App;
    
    const Father = styled.div`
      display: flex;
    `;
    const Box = styled.div`
      background-color: ${(props) => props.bgColor};
      width:100px;
      height:100px;
    `
    const Circle = styled(Box)`
      border-radius: 50px;
    `
    // Box의 모든 속을 가져오고 거기에 Circle을 추가
    ```
    
- 2.3 ‘As’ and Attrs
    
    여러 개의 컴포넌트를 다룰 때 도움이 될 만한 몇 가지 트릭
    
    ```jsx
    <Btn as="a" href="/"></Btn>
    ```
    
    이 prop은 button styled component인 Btn을 사용할 건데 HTML부분을 바꿔서 a를 전달했다.
    
    - styled components가 컴포넌트를 생성할 때, 속성값을 설정할 수 있게 해준다.
    
    ```jsx
    import styled from "styled-components";
    
    function App() {
      return (
       <Father as="header">
          <Input />
          <Input />
          <Input />
          <Input />
          <Input />
          <Input />
       </Father>
      );
    }
    
    export default App;
    
    const Father = styled.div`
      display: flex;
    `;
    const Input = styled.input.attrs({required:true, minLength:10})`
      background-color: yellow;
    `
    ```
    
    attrs에는 input으로 전달된 모든 속성을 가진 오브젝트를 담을 수 있다.
    
    input이 여러 개 있을 때 같은 속성을 주고싶을 때 사용한다.
    
- Animations and Pseudo Selectors
    - keyframe
    
    ```jsx
    const rotateAnimation = keyframes`
      0% {
        transform:ratate(0deg);
        border-radius: 0px;
      }
      50% {
        border-radius: 100px;
      }
      100% {
        transform:rotate(360deg);
        border-radius: 0px;
      }
    `;
    
    const Box = styled.div`
      height: 100px;
      width:100px;
      display: flex;
      justify-content: center;
      align-items: center;
      background-color: green;
      animation: ${rotateAnimation} 3s linear infinite;
    `
    ```
    
    - 컴포넌트 안에 있는 <span> 태그에 style주기
    
    꼭 모든 component에 styled component 처리를 해 줄 필요 없다.
    
    ```jsx
    const Box = styled.div`
    	width:100px;
    	height:100px;
    	span {
    		font-size:36px;
    	}
    `
    ```
    
    - Pseudo Selectors
    
    선택한 요소의 특수한 상태를 지정
    
    ```jsx
    const Box = styled.div`
    	span {
      font-size: 36px;
      &:hover {
        font-size: 40px;
      }
      &:active {
        opacity: 0;
      }
    }
    `
    ```
