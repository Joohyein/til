## 한 줄 글자 자르기

```jsx
h3 {
	display: inline-block: // or block
	width: 200px;
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis; // 넘치는 text를 숨긴 후 ...으로 처리
}
```

## qeury string url

두 가지 방법

```
const getPrevChat = async (dmId) => {
  const response = await instance.get(`/api/dm`, {param:{id:dmId}});
  console.log("response", response);
  return response.data;
}
```

```
const getPrevChat = async (dmId) => {
  const response = await instance.get(`/api/dm?=id${dmId}`);
  console.log("response", response);
  return response.data;
}
```

- reference

[https://axios-http.com/kr/docs/req_config](https://axios-http.com/kr/docs/req_config)

## useQuery

```jsx
const {isLoading, isError, data} = useQuery('blog', getBlogs);
```

```jsx
const {isLoading: loadingData, isError: errorData, data: blogData} = useQuery('blog', getBlogs);
```

이렇게 이름을 지정해서 사용하면 useQuery를 여러 개 사용할 수 있고 지정된 이름(isLoading, isError, data)말고 다른 이름으로 사용할 수 있다.
