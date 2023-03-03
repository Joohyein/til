## error

웹소켓을 사용하지 않는데 아래 에러메시지가 떠서 확인했더니 웹팩은 파일이 변경될 때 다시 로드하기 위해 WebSocket을 사용한다고 한다. CRA를 할 때 패키지 설치가 덜 되어서 생긴 오류인 것 같다.

error message

```jsx
WebSocket connection to 'wss:/서버주소:3000/ws' failed: WebSocketClient.js:16
```

```jsx
**yarn add webpack webpack-cli**
```

webpack, webpack-cli를 설치해서 해결되었다.
