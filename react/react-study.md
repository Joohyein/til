### typescript styled-components

```jsx
<StButton padding="20px" > Medium </StButton>
<StButton padding="10px"> Small </StButton>

const StButton = styled.button<{padding:string}>`
  padding: ${(props)=>props.size};
`;
```

```jsx
// optional
<StButton > Medium </StButton>
<StButton padding="10px"> Small </StButton>

const StButton = styled.button<{padding?:string}>`
  padding: ${(props)=>props.size};
`;
```

```tsx
import { useState } from "react";
import React from "react";

type InputProps = [string, (e: React.ChangeEvent<HTMLInputElement>) => void];

const useInput = ():InputProps => {
    const [value, setValue] = useState<string>("");
    const changeHandler = (e:React.ChangeEvent<HTMLInputElement>) => {
        setValue(e.target.value);
    };
    return [value, changeHandler];
};

export default useInput;
```

- vertical-align → text와 icon 정렬

```tsx
vertical-align: middle;
```

- 인증/인가 (쿠키)
    - 인증(Authentication) : 서비스를 이용하는 유저가 등록된 회원인지 확인하는 절차
    - 인가(Authorization) : 유저에게 특정 리소스에 대한 접근할 수 있는 권한이 있는지 확인하는 절차
    
    - http 프로토콜 통신의 특징 두 가지
        1. 무상태(Stateless) : 서버는 클라이언트의 상태를 기억하지 않는다. 따라서 각 요청마다 서버에서 요구하는 모든 상태 정보를 담아서 요청해야 한다.
            - 상태값은 매 요청마다 클라이언트가 가지고 오기 때문에, 서버는 클라이언트의 상태를 별도로 기억할 필요 없이 주문받은 대로 응답해준다.
            - 무상태라는 특성 덕분에 동일한 서버를 여러 개로 확장시킬 수 있다.(Scale-Out)
        2. 비연결성(Connectionless) : 서버와 클라이언트는 연결되어 있지 않다. 서버 입장에서는 매번 새로운 요청이다. (반대로 채팅같은 경우는 연결성이다)
            - 비연결성으로 인해 최소한의 서버 자원으로 서버를 유지할 수 있게 해준다.
            - 그러나, 각 사용자별 요청이 잦은 서비스의 경우 이러한 비연결성은 오히려 비효율적일 수 있다.
        
    
    ## 쿠키
    
    - 브라우저가 주머니에 갖고 있는 과자
    - 무상태와 비연결성이라는 http통신의 특징에도 불구하고 마치 서버가 클라이언트의 인증 상태를 기억하는 것처럼 구현할 수 있는 수단으로 사용할 수 있다.
    - 쿠키란 브라우저에 저장되는 텍스트 파일이며, key-value 형태로 저장된다.
    - 쿠키는 별도로 삭제하거나 유효기간이 만료되지 않는 이상 서버와 통신을 할 때 자동으로 주고받게 된다.
    - 서버에 특정 API 요청을 했을 때 서버가 응답 시 header 안에 set-cookie 속성으로 쿠키 정보를 담아주면 응답을 받은 브라우저는 쿠키를 브라우저에 자동으로 저장한다. (저장된 쿠키 정보는 개발자도구 → 애플리케이션 → 저장용량(Storage) → 쿠키 에서 확인가능)
    - 서버에 http 요청을 할 때마다 브라우저에 저장되어 있는 쿠키는 자동으로 서버에 보내진다. (단, 동일한 Origin 또는 CORS를 허용하는 Origin에만 쿠키를 보낸다. ex. 유튜브 서버에서 받은 쿠키는 유튜브 이용 시에만 주고 받을 수 있다)
        - Origin : 출처를 의미한다. protocol + host + port → http://localhost:3000
        - CORS
            - Cross Origin Resource Sharing(CORS)는 다른 출처에 리소스 요청하는 것을 허용하는 정책이다.
            - 브라우저는 보안상의 이유로 기본적으로 Same Origin Policy(SOP)를 원칙으로 하고 있지만, 서버와 클라이언트 각각 CORS 설정을 통해 상호 합의 된 웹사이트는 예외적으로 서로 다른 출처(Cross Origin)임에도 API요청이 가능하다.
    - 쿠키는 클라이언트에서 직접 추가/삭제/수정 할 수 있다.
    

## 세션

- 세션이란 클라이언트와 서버 간의 연결이 활성화된 상태를 의미한다. (또는 인증이 유지되고 있는 상태)
- 로그인 성공 → 서버에서 세션 생성 및 저장(key-value 형식) → key(sessionID)를 브라우저에 응답 ~ 계속해서 연결이 되어 있는 것처럼 작동 → 브라우저에 있는 key를 서버에 자동으로 요청

 

```jsx
const getData = async() => {
	const response = await axios.get("url", {
		withCredentials: true,
	})
	setData(response.data.data);
};
```

→ 분리된 다른 서버끼리 정보 교환을 할 수 있다. withCredentials의 기본값은 false이다. false이면 (클라이언트 쪽에 없으면?) 서버에서 sessionId를 담아서 주더라도 브라우저에서는 쿠키에 자동으로 담을 수 없다.

- 서버쪽에서 CORS옵션을 주는 방법

```jsx
const corsOption = {
	origin: true,
	//credentials: true,
};
```

→ credentials: true 를 꺼주게 되면 통신이 안된다.

정리) post요청으로 response를 받아 오면 그 response 안에는 서버에서 자동으로 세팅해주는 것들이 있다. 그 중에서 sessionId도 들어있고 sessionId는 쿠키에 자동으로 저장된다.

## 토큰

- 클라이언트에서 보관하는 암호화된 인증 정보
- 세션처럼 서버에서 사용자의 인증 정보를 보관 할 필요가 없기 때문에 서버 부담을 줄여주는 인증 수단이라고 할 수 있다.
- 웹에서 인증 수단으로 사용되는 토큰은 주로 JWT(Json Web Token)을 이용한다.
- JWT의 특징
    - **header, payload, signature** 형식으로 3가지 데이터로 구성되어 있다.
    - 국제 인터넷 표준 인증 규격 중 하나이다.
    - 암호화된 토큰을 누구나 복호화하여 payload를 볼 수 있다 → 토큰의 용도는 인증정보(payload)에 대한 보호가 아니라 위조방지를 하는 것이다.
    - 정보(payload)를 토큰화 할 때 signmature에 secret key가 필요하고, secret key는 복호화가 아니라 토큰이 유효한지 검증하는 데 사용된다.
    
    ```jsx
    const getData = async() => {
    	const accessToken = cookies.get("accessToken");
    	const response = await axios.get(`${BASE_URL}/product-list`, {
    		headers: {
    			"Content-Type": "application/json",
    			Authorization: `Bearer ${accessToken}`,
    		}
    	})
    	setData(response.data.data);
    };
    ```
    
- Refresh Token 으로 보안 강화
    
    리소스 접근 인가를 받기 위해 사용되는 토큰을 Access Token이라고 부른다.
    
    Access Token의 만료기간을 길게 잡고 인증 상태를 오래 가져갈 경우 서버 부담은 줄어드나 보안성(탈취 당할 경우)에 허점이 있다.
    
    인증 보안이 중요한 서비스의 경우 인증 시 두 개의 토믄(Access Token, Refresh Token)을 발급하고 Access Token의 기간은 30분 정도로 짧게 가져가고, Refresh Token은 1~2주 정도로 길게 잡는 경우가 많다.
    
    이 경우 서버에서는 Access Token이 만료되었을 때 Refresh Token이 유효한 상태면 새로운 Access Token을 클라이언트에 발급해주고 인증 상태를 유지할 수 있도록 하고, Refresh Token 만료 시 다시 로그인하라는 메세지를 응답한다.
    

### 세션 인증 vs 토큰 인증

|  | 세션 인증 | 토큰 인증 |
| --- | --- | --- |
| 인증 정보 저장 위치 | 서버 | 클라이언트 |
| 확장성(Scale-out) | Bad | Good |
| 보안성(상대적) | Good | Bad |
| 비용(상대적) | 비싸다 | 저렴하다 |
