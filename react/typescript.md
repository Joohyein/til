## Typescript

- Optional Props

props를 필수(required)가 아닌 선택적(optional)이 되도록 만들기

```jsx
interface CircleProps {
    bgColor: string;
    borderColor?:string;
}

function Circle({bgColor, borderColor}:CircleProps) {
    return <Container bgColor={bgColor} borderColor={borderColor}/>;
}
// borderColor은 optional
// 그냥 borderColor를 Container에 넣어주면 Container는 borderColor가 뭔지 모른다.
```

 

- Container에서는 borderColor가 required이지만 Circle 안에서는 borderColor가 required 상태가 아니다.

```tsx
import styled from "styled-components";

// typescript가 봤을 때는 Containger가 div여서 component는 어떤 props도 받고 있지 않는다.
// typescript에게 bgColor를 styled-component(Container?)에게도 보내고 싶다고 말하자.
interface ContainerProps {
    bgColor:string;
    borderColor:string;
}

// typescipt에게 Container가 bgColor를 받을거라고 얘기하려면 <ContainerProps>를 붙여주면 된다.
const Container = styled.div<ContainerProps>`
    width: 200px;
    height: 200px;
    background-color: ${props => props.bgColor};
    border-radius: 50%;
		bordr: 2px solid ${props => props.borderColor};   
`

interface CircleProps {
    bgColor: string;
    borderColor?:string;
}
// 

function Circle({bgColor, borderColor}:CircleProps) {
    return <Container bgColor={bgColor} borderColor={borderColor} />;
}

export default Circle;
```

 - **borderColor가 있으면 쓰고 아니면 아무 색상을 지정해주면 된다.**

```tsx
borderColor={borderColor ?? bgColor}
// default값을 설정해줘야 한다. optional이기 때문에
```

- default value 주는 두 가지 방법
1. typescript

```tsx
function Circle({bgColor, borderColor, text}:CircleProps) {
    return <Container bgColor={bgColor} borderColor={borderColor ?? bgColor} >
        {text ?? "default value"}
    </Container>;
}
```

1. js

```tsx
function Circle({bgColor, borderColor, text="default value"}:CircleProps) {
    return <Container bgColor={bgColor} borderColor={borderColor ?? bgColor} >
        {text}
    </Container>;
}
```
