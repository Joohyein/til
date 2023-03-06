## stomp

- Simple/Stream Text Oriented Message Protocal의 약자로 메시지 브로커의 역할을 한다.
- Websocket 기반으로 동작하며 pub/sub 구조로 되어 있다.
    - publishoer : 편지를 쓰는 사람
    - subscriber : 편지를 받고 읽는 사람
- 대표적인 예
    - 채팅방 생성 : pub/sub 구현을 위한 Topic 생성
    - 채팅방 입장 : Topic 구독
    - 채팅방에서 메시지를 송수신 : 해당 Topic으로 메시지를 송신(pub), 수신(sub)
- send, subscribe 같은 명령을 사용하려면 destination이라는 header를 필요로 하는데 이 헤더는 어디에 메시지를 전송할지, 어디에서 메시지를 구독할지를 알려주는 헤더이다.

## sockjs

- WebSocket은 upgrade header를 이용하여 Socket연결을 하고, 통신을 한다. 이 과정에서 여러가지 이유로 소켓 연결이 불가능하게 될 경우가 있는데 이 경우에는 http기반의 다른 기술로 전환하여 다시 연결을 시도해야 할 필요가 있다. 이때 사용하는 것이 ‘WebSocket Emulation’이다. Spring에서는 Emulation을 위해 ‘SockJS’라이브러리를 지원한다.

아래 코드에서 SockJS에 들어갈 url에서 프로토콜을 ws로 프록시설정을 해줘야한다고 생각했는데 바로 서버 url을 넣어줘도 되었다. 

```jsx
useEffect(()=>{
  const socket = new SockJS('http://3.36.51.159:8080/ws/chat');
  const stompClient = Stomp.over(socket);

  stompClient.connect({}, () => {
    console.log("connected");
    stompClient.subscribe(`/topic/chat/room/1`, (data) => {

      const msgData = JSON.parse(data.body);
      console.log("msgData: ", msgData);

      setMessages((prev) => [...prev, msgData]);
    });
    setStompClient(stompClient);
  });
  return () => {
    // stompClient.disconnect();
  }
}, []);
```

```jsx
Stomp.over(socket)
// stomp 프로토콜 위에 sockJS가 돌아가도록 Stomp.over()의 인자로 
// socket이라는 변수를 넣어준다.
```

서버와 연결이 되었고 메시지도 주고 받았지만 아직 stomp에 대해서 더 공부가 필요한 것 같다. 데이터가 많아질수록 같은 메시지가 여러번 찍히는데 원인을 찾아서 해결해야한다.
