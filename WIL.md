## axios

- 문법 구성

```jsx
axios({
	url: "https://blog/api/login",  // 통신할 웹문서
	method: 'post',  // 통신 방식
	data: {
		id: '1'
	}
});
```

withCredentials : cross-site access-control 요청의 허용 유무. true로 하면 cross-origin으로 쿠키값을 전달할 수 있다.

axios를 통해 요청을 서버에게 보내면, 서버에서 처리를 하고 다시 데이터를 클라이언트에 응답한다. `.then` 함수인자(response)로 받아 객체에 담긴 데이터가 응답 데이터이다.

```jsx
response.data: {}, // 서버가 제공한 은답(데이터)
response.status: 200, // 'status'는 서버 응답의 http 상태 코드
response.statusText: 'OK', // 'statusText'는 서버 응답으로부터의 http 상태 메시지
response.headers: {}, // 'headers' 서버가 응답한 헤더는 모든 헤더 이름이 소문자로 제공
response.config: {}, // 'config'는 요청에 대해 'axios'에 설정된 구성(config)
response.request: {} // 'request'는 응답을 생성한 요청
```

### axios GET

1. 단순 데이터(페이지 요청, 지정된 요청) 요청을 수행할 경우
2. 파라미터 데이터를 포함시키는 경우(사용자 번호에 따른 조회)

```jsx
axios.get('/user', {
	params: {
			ID: 123
		}
	})
	.then((response) => {
		console.log(response);
	})
	.catch((error) => {
		console.log(error);
	})
}

// async / await
async getUser() => {
	try{
		const reponse = await axios.get('/user?ID=123');
		console.log(reponse);
	} catch(error) {
		console.error(error);
	}
}
```

### axios POST

일반적으로 데이터를 message body에 포함시켜 보낸다. 

get 메서드에서 params를 사용한 경우와 비슷하게 수행된다.

```jsx
axios.post('url', {
		id: 1,
		userName: 'name'
	})
	.then((response) => {
		console.log(response)
	})
	.catch((error) => {
		// 오류 발생시 실행
	})
```

### axios DELETE

delete네서드에는 일반적을 body가 비어있다. REST기반 api프로그램에서 데이터베이스에 저장되어 있는 내요을 삭제하는 목적으로 사용한다.

```jsx
axios.delete('/user?ID=12345')
  .then(function (response) {
    // handle success
    console.log(response);
  })
  .catch(function (error) {
    // handle error
    console.log(error);
  })
```

하지만 query나 params가 많아져서 헤더에 많은 정보를 담을 수 없을 때는 다음과 같이 두 번째 인자에 data를 추가해줄 수 있다.

```jsx
axios.delete('/user?ID=12345',{
    data: {
      post_id: 1,
      comment_id: 13,
      username: "foo"
    }
  })
  .then(function (response) {
    // handle success
    console.log(response);
  })
  .catch(function (error) {
    // handle error
    console.log(error);
  })
```

### axios PUT

REST 기반 API프로그램에서 디이터베이스에 저장되어 있는 내용을 갱신(수정)하는 목적으로 사용된다. 서버에 있는 데이터베이스의 내용을 변경하는 것이 주목적이다. 서버 내부적으로 get → post 과정을 거치기 때문에 post메서드와 형태가 비슷하다.

```jsx
axios.put("url", {
      username: "",
      password: ""
  })
  .then(function (response) {
       // response  
  }).catch(function (error) {
      // 오류발생시 실행
  })
```

### try catch, .then.catch

try catch는 Promise가 아닌 것에 대한 에러처리 및 진해응ㄹ 다루기 위한 것이고 then catch는 Promise에 대한 에러처리 및 진행을 다루기 위한것이다.

try catch와 .then.catch가 같은 결과를 만들 수 있는데 그러기 위해서는 try catch는 async await으로 묶어서 사용하면 된다.

## error

토이프로젝트를 하면서 여러 번 봤던 오류였지만 협업프로젝트를 오랜만에 해서 어떻게 해결했는지 생각이 나지 않아서 다시 구글링을 하면서 해결했다. 

- 에러 코드

```jsx
hyein@juhyein-ui-noteubug nyangdang % git pull upstream dev
From https://github.com/NyangDang/frontend
 * branch              dev        -> FETCH_HEAD
hint: You have divergent branches and need to specify how to reconcile them.
hint: You can do so by running one of the following commands sometime before
hint: your next pull:
hint: 
hint:   git config pull.rebase false  # merge
hint:   git config pull.rebase true   # rebase
hint:   git config pull.ff only       # fast-forward only
hint: 
hint: You can replace "git config" with "git config --global" to set a default
hint: preference for all repositories. You can also pass --rebase, --no-rebase,
hint: or --ff-only on the command line to override the configured default per
hint: invocation.
```

```jsx
hyein@juhyein-ui-noteubug nyangdang % git config pull.rebase false
hyein@juhyein-ui-noteubug nyangdang % git pull upstream dev
From https://github.com/NyangDang/frontend
 * branch              dev        -> FETCH_HEAD
error: The following untracked working tree files would be overwritten by merge:
	node_modules/.yarn-integrity
Please move or remove them before you merge.
Aborting
```

```jsx
hyein@juhyein-ui-noteubug nyangdang % git add .
hyein@juhyein-ui-noteubug nyangdang % git stash
No local changes to save
hyein@juhyein-ui-noteubug nyangdang % git stash --all
Saved working directory and index state WIP on hyein: 4814e61a setCookis
hyein@juhyein-ui-noteubug nyangdang % git pull upstream dev
```

untracked 파일들이어서 먼저 add 후 stash를 했고 git stash —all는 untracked 파일까지 모두 stash해주는 명령어이다.

stash 기능은 **git add 로 특정 파일을 수정해서 staging area에 올려놓은 버전을 큐 와 비슷한 방식으로 돌아가는 자료구조에 백업해놓는다.**

   
   ## react image upload

input type=’file’

```jsx
<input 
	type='file'
	accept='image/jpg,image/png, image/gif'
	name='img'
	onChange={onChange}
/>
	
```

`accept` : 업로드할 수 있는 파일 확장자

---

reference

[https://inpa.tistory.com/entry/AXIOS-📚-설치-사용](https://inpa.tistory.com/entry/AXIOS-%F0%9F%93%9A-%EC%84%A4%EC%B9%98-%EC%82%AC%EC%9A%A9)
