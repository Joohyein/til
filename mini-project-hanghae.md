## 비밀번호 확인 구현

비밀번호 확인 입력창을 만들어 보려고 했는데 생각보다 간단했다. 제출버튼을 눌렀을 때 밑에 함수를 넣어주고 true이면 return 하도록 했다. 아이디, 비밀번호 입력창은 useInput 커스텀훅을 사용해서 비밀번호 확인 입력창도 사용해보려고 했는데 따로 함수를 만드는 것이 더 간단해서 커스텀훅은 사용하지 않았다.

```jsx
const pwCheck = () => {
  if(userPw !== pwConfirm){
    alert("비밀번호가 일치하지 않습니다");
    resetPwConfirm();
  } else {
    return true;
  }
}
```

다음에는 커스텀훅에 대해서  더 공부를 한 뒤에 비밀번호 확인 입력창도 커스텀훅을 활용해서 구현해 봐야겠다.

## react 외부 링크 이동

카카오 로그인 연결을 하기 위해서 외부링크를 이미지에 걸어주었다.

```jsx
const url = 'https://kauth.kakao.com/oauth/authorize?client_id=513dbab402347b4ce9abb443337b09a6&redirect_uri=http://localhost:3000/api/user/kakao/callback&response_type=code';
```

```jsx
<StImg src={kakao} id="login-kakao-btn" onClick={()=> window.open(url)}/>
```
