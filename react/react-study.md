## useNavigate()

useNavigate()로 뒤로가기 구현

```jsx
const navigate = useNavigate();
```

```jsx
onClick = {() => navigate(-1)}
```

버튼을 클릭하면 Route를 이용해서 이동을 할 수도 있지만 뒤로가기만 구현하면 되는 상황에서는 usenavigate()를 사용하면 된다.
