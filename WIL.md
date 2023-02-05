## 콜백함수

- 콜백함수의 특징
    - 다른 함수(A)의 인자로 콜백함수(B)를 전달하면, A가 B의 제어권을 갖게 된다.
    - 특별한 요청(bind)이 없는 한 A에 미리 정해놓은 방식에 따라 B를 호출한다.
    - 미리 정해놓은 방식이란 어떤 시점에 콜백을 호출할지, 인자에는 어떤 값들을 지정할지, this에 무엇을 바인딩할지 등이다.
    - 콜백으로 넘기는 것은 메서드가 아니라 함수이다.

---

## HTTP

- 평문 통신이기 때문에 도청이 가능하다.

**TCP/IP** 구조의 통신은 전부 통신 경로 상에서 엿볼 수 있다. 패킷을 수집하는 것만으로 도청할 수 있다. 평문으로 통신을 할 경우 메세지의 의미를 파악할 수 있기 때문에 암호화하여 통신해야 한다.

**보완**

1. 통신 자체를 암호화 -  `SSL(Secure Socket Layer)` 또는 `TLS(Transport Layer Security)` 라는 다른 프로토콜을 조합함으로써 HTTP의 통신 내용을 암호화할 수 있다. SSL을 조합한 HTTP를 `HTTPS(HTTP Secure)` 또는 `HTTP over SSL` 이라고 부른다.
2. 콘텐트를 암호화 - HTTP메세지에 포함되는 콘텐츠만 암호화하는 것이다. 암호화해서 전송하면 받은 측에서는 그 암호를 해독하여 출력하는 처리가 필요하다.

- 통신 상대를 확인하지 않기 때문에 위장이 가능하다.

HTTP에 의한 통신에는 상대가 누구인지 확인하는 처리는 없기 때문에 누구든지 요청을 보낼 수 있다. IP주소나 포트 등에서 그 웹 서버에 액세스 제한이 없는 경우 요청이 오면 상대가 누구든지 무언가의 리스폰스를 반환한다. 

1. 요청을 보낸 곳의 웹 서버가 원래 의도한 리스폰스를 보내야 하는 웹 서버인지 알 수 없다.
2. 리스폰스를 반환한 곳의 클라이언트가 원래 의도한 리퀘스트를 보낸 클라이언트인지 알 수 없다.
3. 통신하고 있는 상대가 접근이 허가된 상대인지 알 수 없다.
4. 어디에서 누가 요청을 보냈는지 알 수 없다.
5. 의미없는 요청도 수신한다.(DDoS 공격을 방지할 수 없다)

**보완**

 `SSL` 은 상대를 확인하는 수단으로 **증명서**를 제공하고 있다. 증명서는 신뢰할 수 있는 제 3자 기관에 의해 발행되는 것이기 때문에 서버나 클라이언트가 실재하는 사실을 증명한다. 이 증명서를 이용함으로써 통신 상대가 내가 통신하고자 하는 서버임을 알 수 있고 이용자는 개인 정보 누설 등의 위험성이 줄어들게 된다. 클라이언트는 이 증명서로 본인 확인을 하고 웹 사이트 인증에서도 이용할 수 있다.

- 완전성을 증명할 수 없기 때문에 변조가 가능하다.

여기서 완전성이란 정보의 정확성을 의미한다. 서버 또는 클라이언트에서 수신한 내용이 송신측에서 보낸 내용과 일치한다라는 것을 보장할 수 없는 것이다. 요청이나 리스폰스가 발신된 후에 상대가 수신하는 사이에 누군가에 의해 변조되더라도 이 사실을 알 수 없다. 공격자가 도중에 요청이나 리스폰스를 빼앗아 변조하는 공격을 중간자 공격(Man-in-the-Middle)이라고 부른다.

**보완**

`MD5` , `SHA-1` 등의 해시값을 확인하는 방법과 파일의 디지털 서명을 확인하는 방법이 존재하지만 확실히 확인할 수 있는 것은 아니다. 확실히 방지하기에는 `HTTPS` 를 사용해야 한다. SSL에는 인증이나 암호화, 그리고 다이제스트 기능을 제공하고 있다.

## HTTPS

HTTPS는 SSL의 껍질을 덮어쓴 HTTP라고 할 수 있다. 즉, 새로운 애플리케이션 계층의 프로토콜이 아니라는 것이다. HTTP 통신하는 소켓 부분을 `SSL` 또는 `TLS` 라는 프로토콜로 대체하는 것 뿐이다. HTTP는 TCP와 직접 통신했지만, HTTPS에서 HTTP는 SSL과 통신하고 SSL이 TCP와 통신하게 된다. SSL을 사용한 HTTPS는 암호화와 증명서, 안정성 보호를 이용할 수 있게 된다.

HTTPS의 SSL에서는 공통키 암호화 방식과 공개키 암호화 방식을 혼합한 하이브리드 암호 시스템을 사용한다. 공통키를 공개키 암호화 방식으로 교환한 다음에 다음부터의 통신은 공통키 암호를 사용하는 방식이다.

---

### Styling

1. App.js

```jsx
import React, {useState} from "react";
import "App.css";

export default function App() {
  const arr = ['오이', '당근', '피망', '가지', '메론'];
  return (
    <div className="content">
      
      {
        arr.filter((item)=>{
          return item !== '피망';
        }).map((item)=>{
          return <div className="box">{item}</div>;
        })
      }
    </div>
  );
}
```

1. App.css

```css

.content{
  padding:20px;
  display: flex;
  gap:12px;
}

.box {
  width: 100px;
  height:100px;
  border: solid 1px yellowgreen;
  border-radius: 5px;
  display: flex;
  justify-content: center;
  align-items: center;
}
```

---

### 반복되는 컴포넌트 처리하기

- 객체

```css

import React, {useState} from "react";
import "App.css";

export default function App() {
  const obj = [
    {id:1, age:21, name:'짱구'}, 
    {id:2, age:23, name:'훈이'}, 
    {id:3, age:22, name:'철수'},
    {id:4, age:20, name:'유리'}, 
    {id:5, age:22, name:'맹구'}];
  return (
    <div className="content">     
      {
        obj.map((item)=>{
          return <div key={item.id} className="box">{item.age}, {item.name}</div>
        })
      }
    </div>
  );
}
```

map함수를 사용할 때는 key가 반드시 있어야 한다.

- 값을 추가하고 삭제하면 렌더링이 되어야 하니까 state로 작성해야 한다.

```css
import React, {useState} from "react";
import "App.css";

export default function App() {
  const [obj, setObj] = useState([
    {id:1, age:21, name:'짱구'}, 
    {id:2, age:23, name:'훈이'}, 
    {id:3, age:22, name:'철수'},
    {id:4, age:20, name:'유리'}, 
    {id:5, age:22, name:'맹구'}
	]);
  return (
    <div className="content">     
      {
        obj.map((item)=>{
          return <div key={item.id} className="box">{item.name}, {item.age}</div>
        })
      }
    </div>
  );
}
```

- 삭제기능

각 item마다 기능이 들어가야 한다.

```jsx
import React, {useState} from "react";
import "App.css";

export default function App() {
  const [obj, setObj] = useState([
    {id:1, age:21, name:'짱구'}, 
    {id:2, age:23, name:'훈이'}, 
    {id:3, age:22, name:'철수'},
    {id:4, age:20, name:'유리'}, 
    {id:5, age:22, name:'맹구'}
	]);

  const [name, setName] = useState('');
  const [age, setAge] = useState('');

  const nameChangeHandler = (event) => {
    setName(event.target.value);
  }
  const ageChangeHandler = (event) => {
    setAge(event.target.value);
  }
  const btnClickHandler = () => {
    const info = {
      id: obj.length + 1,
      age,
      name,
    }
    setObj([...obj, info])
    // 불변성유지
  }
  
  return (
    <div>
      <div>
        이름 :&nbsp;<input 
        value={name}
        onChange={nameChangeHandler} 
        /><br />
        나이 : <input 
        value={age}
        onChange={ageChangeHandler}
        /><br />
        <button
        onClick={btnClickHandler}
        >button</button>
      </div>
      <div className="content">     
        {
          obj.map((item)=>{
            return (<Obj item={item} obj={obj} setObj={setObj} />); // props로 필요한 것들을 내려주기
          })
        }
      </div>
    </div>
    
  );
};
// 컴포넌트 분리
const Obj = (item, obj, setObj) => {
  const clickremovebtnhandler = (id) => {
    const newObj = obj.filter((item)=> item.id !== id);
    setObj(newObj);
  }
  <div className="box">
    {item.age}, {item.name}
    <button onClick={()=>clickremovebtnhandler(item.id)}> x </button>
  </div>
};
```

- 컴포넌트 분리하기
1. 삭제버튼 분리

```jsx
import React, {useState} from "react";
import "App.css";

export default function App() {
  const [obj, setObj] = useState([
    {id:1, age:21, name:'짱구'}, 
    {id:2, age:23, name:'훈이'}, 
    {id:3, age:22, name:'철수'},
    {id:4, age:20, name:'유리'}, 
    {id:5, age:22, name:'맹구'}
	]);

  const [name, setName] = useState('');
  const [age, setAge] = useState('');

  const nameChangeHandler = (event) => {
    setName(event.target.value);
  }
  const ageChangeHandler = (event) => {
    setAge(event.target.value);
  }
  const btnClickHandler = () => {
    const info = {
      id: (obj.length + 1),
      age,
      name,
    };
    setObj([...obj, info]);
    // 불변성유지
  };
  const clickremovebtnhandler = (id) => {
    const newObj = obj.filter((item)=> item.id !== id);
    setObj(newObj);
  }
  
  return (
    <div>
      <div>
        이름 :&nbsp;<input 
        value={name}
        onChange={nameChangeHandler} 
        /><br />
        나이 : <input 
        value={age}
        onChange={ageChangeHandler}
        /><br />
        <button
        onClick={btnClickHandler}
        >button</button>
      </div>
      <div className="content">     
        {
          obj.map((item)=>{
            return (
              <div>
                <Obj 
                  key={item.id}
                  item={item}
                  clickremovebtnhandler={clickremovebtnhandler}
                />
               </div>
          )})
        }
      </div>
    </div>
    
  );
};
// 컴포넌트 분리
const Obj = ({item, clickremovebtnhandler}) => {
  return(
    <div className="box">
      {item.age}, {item.name}
      <button onClick={()=>clickremovebtnhandler(item.id)}> x </button>
    </div>
  )
};
```

1. 추가버튼 분리

```jsx
import React, {useState} from "react";
import "App.css";

export default function App() {
  const [obj, setObj] = useState([
    {id:1, age:21, name:'짱구'}, 
    {id:2, age:23, name:'훈이'}, 
    {id:3, age:22, name:'철수'},
    {id:4, age:20, name:'유리'}, 
    {id:5, age:22, name:'맹구'}
	]);

  const [name, setName] = useState('');
  const [age, setAge] = useState('');

  const nameChangeHandler = (event) => {
    setName(event.target.value);
  }
  const ageChangeHandler = (event) => {
    setAge(event.target.value);
  }
  const btnClickHandler = () => {
    const info = {
      id: (obj.length + 1),
      age,
      name,
    };
    setObj([...obj, info]);
    // 불변성유지
  };
  const clickremovebtnhandler = (id) => {
    const newObj = obj.filter((item)=> item.id !== id);
    setObj(newObj);
  }
  
  return (
    <div>
      <div>
        이름 :&nbsp;<input 
        value={name}
        onChange={nameChangeHandler} 
        /><br />
        나이 : <input 
        value={age}
        onChange={ageChangeHandler}
        /><br />
        <Addbtn btnClickHandler={btnClickHandler}> add </Addbtn>
      </div>
      <div className="content">     
        {
          obj.map((item)=>{
            return (
              <div>
                <Obj 
                  key={item.id}
                  item={item}
                  clickremovebtnhandler={clickremovebtnhandler}
                />
               </div>
          )})
        }
      </div>
    </div>
    
  );
};
// 컴포넌트 분리
const Addbtn = ({btnClickHandler, children}) => {
  return (
    <button onClick={btnClickHandler}> {children} </button>
  );
};
const Obj = ({item, clickremovebtnhandler}) => {
  return(
    <div className="box">
      {item.age}, {item.name}
      <button onClick={()=>clickremovebtnhandler(item.id)}> x </button>
    </div>
  )
};
```

→ 분리한 컴포넌트는 파일을 만들어서 분리하자. (import, export)

```jsx
import Obj from "component/Obj";
import Button from "component/Button";
```

---

`&nbsp;` : 띄어쓰기


---
**Reference**
https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Network
