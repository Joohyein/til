- splice - **배열에서 특정 값 삭제, 추가**

```jsx
arr.splice(1, 2, optional)
```

```jsx
let arr = [1, 2, 3, 4];
arr.splice(1, 2);
return arr; // [1, 4]
```

```jsx
// 삭제하고 원하는 값 추가
let arr = [1, 2, 3, 4];
arr.splice(1, 2, 100, 200);
return arr; // [1, 100, 200, 4]
```

```jsx
// 삭제 없이 원하는 값 추가
let arr = [1, 2, 3, 4];
arr.splice(1, 0, 100, 200);
return arr; // [1, 100, 200, 2, 3, 4]
```

- slice - **배열 얕은 복사본을 새로운 배열 객체로 반환. 원본 배열은 바뀌지 않는다.**

```jsx
let arr = [1, 2, 3, 4];
return arr.slice(1, 2);  // [2]
```

- 배열을 원하는 길이, 원하는 값으로 초기화

```jsx
const arr = Array.from({length: 5}, () => 0);
```

- n.toString(3) : n을 3진수로 변환
- parseInt(’0021’, 3) : 문자열 ‘0021’을 3진수로 변환
