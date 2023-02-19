## Modal

외부 영역 클릭하면 모달창이 닫히는 것을 구현

- 이벤트 리스너의 종류
    - `mousedown` : 클릭하는 순간 이벤트가 동작된다.
    - `click` : 클릭이 끝나는 순간 이벤트가 동작한다.

- outside 클릭의 기준이 되는 HTML 요소
    - React ref
- 클릭 이벤트 `mousedown`가 발생하면 `event.target`이 `ref`에 저장된 요소를 포함하는지 확인한다.
- 포함 되지 않는다면, outside 클릭이 되는 것이다.

완성 코드

```tsx
import React, { useState, useRef, useEffect } from 'react'
import styled from 'styled-components';
import Button from './Button';

function Modal() {
  const [modalOpen, setModalOpen] = useState(false);
  const [modalOpenOutside, setModalOpenOutside] = useState(false);
  const modalRef = useRef<HTMLDivElement>(null);

  const showModal = () => {
    setModalOpen(true);
  };
  const showModalOutside = () => {
    setModalOpenOutside(true);
  }

  useEffect(() => {
    // 이벤트 핸들러 함수
    const handler = (event:any) => {
        // mousedown 이벤트가 발생한 영역이 모달창이 아닐 때, 모달창 제거 처리
        if (modalRef.current && !modalRef.current.contains(event.target)) {
            setModalOpenOutside(false);
        }
    };
    // 이벤트 핸들러 등록
    document.addEventListener('mousedown', handler);
    
    return () => {
        // 이벤트 핸들러 해제
        document.removeEventListener('mousedown', handler);
    };
});

  return (
    <div>
      <Button 
        width={"100px"} 
        height={"42px"} 
        bgColor={"green"} 
        border={"none"} 
        textColor={"white"}
        onClick={showModal}
      >modal open</Button>
      {modalOpen ? 
        <StContainer>
          <h3>닫기와 확인 버튼 2개가 있고, 외부 영역을 눌러도 모달이 닫히지 않아요.</h3>
          <StBtnBox>
            <button onClick={()=>setModalOpen(false)}>닫기</button>
            <button onClick={()=>setModalOpen(false)}>확인</button>
          </StBtnBox>
        </StContainer> 
        : null
      }
      <Button 
            width={"200px"} 
            height={"56px"} 
            bgColor={"white"} 
            border={"2px solid pink"} 
            textColor={"brown"}
            onClick={showModalOutside}
      >open modal
      </Button>
      {modalOpenOutside ?
        <StModalOutside ref={modalRef}>
          <h3>닫기 버튼 1개가 있고, 외부 영역을 누르면 모달이 닫혀요.</h3>
          <StBtnClose onClick={()=>setModalOpenOutside(false)}>X</StBtnClose>
        </StModalOutside> 
        : null
      }
    </div>
  )
}

export default Modal;
```

## 라이프 사이클

모든 리액트 컴포넌트에는 라이프사이클(수명 주기)이 존재한다. 컴포넌트의 수명은 페이지에 렌더링이 되기 전인 준비 과정에서 시작하여 페이지에서 사라질 때 끝난다.

리액트 프로젝트를 진행하다 보면 가끔 컴포넌트를 처음으로 렌더링할 때 어떤 작업을 처리해야 하거나 컴포넌트를 업데이트하지 전후로 어떤 작업을 처리해야 할 수도 있고, 또 불필요한 업데이트를 방지해야 할 수 도 있다. 이때는 컴포넌트의 라이프사이클 메서드를 사용하는데 **클래스형 컴포넌트**에서만 사용할 수 있다. 

라이프사이클은 마운트(페이지에 컴포넌트가 나타남), 업데이트(컴포넌트 정보를 업데이트), 언마운트(페이지에서 컴포넌트가 사라짐) 총 세 가지 카테고리로 나눈다. 

---

- 궁금한 것 : custom hook

만약에 모달창을 만들 때 커스텀 훅을 사용하려고 하는데 버튼을 클릭하면 모달창이 뜨고 (여기까지는 동일) 하나는 닫기 버튼을 눌렀을 때만 모달창이 닫히고, 다른 하나는 버튼 또는 모달창 바깥 부분을 클릭했을 때 모달창이 닫히는데 이런 경우에 커스텀훅을 어떻게 작성해야할 지 모르겠다.
