## useMutaion

데이터 조회를 할 때는 useQuery를 사용하고 

```jsx
const {isLoading, isError, data} = useQuery("books", getBooks); // 쿼리의 이름, api(조회를 해오는 비동기 함수)
```

useMutation은 React Query를 이용해 서버에 데이터 변경 작업을 요청할 때 사용한다.

```jsx
const queryClient = useQueryClient();
const mutation = useMutation(addBooks, {
  onSuccess: () => {
    queryClient.invalidateQueries("books"); // "books"로 읽어온 데이터를 무효화시키고 다시 불러옴
    console.log("성공")
  }
});
```

- mutationFn(mutation function)
    - promise 처리가 이루어지는 함수(axios를 이용해 서버에 API를 요청하는 부분)
- mutate
    - useMutation을 이용해 작성한 내용들이 실행될 수 있도록 도화주는 trigger 역할을 한다.
    - useMutation을 정의해둔 뒤 이벤트가 발생되었을 때 mutate를 사용한다.
    
    ```jsx
    mutation.mutate(newBook); // 데이터 저장
    ```
