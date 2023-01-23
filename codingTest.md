## sort()

- 숫자 기준

```jsx
const a = [100, 3, 20];
a.sort((a, b) => a - b);
// [3, 20, 100]
```

`sort()` 함수 안에 있는 람다 함수(익명 함수)는 a, b 중에 더 큰 값을 식별하기 위한 함수이다.

- 음수가 리턴된다면 `a < b` 를 의미
- 양수가 리턴된다면 `a > b` 를 의미
- 0이 리턴된다면 `a == b` 를 의미한다.

정렬을 위해 두 값을 비교하는 기준을 정의하여 `sort()` 함수의 매개변수로 넘겨주는 것이다.

- 숫자와 문자열을 함께 sort()

```jsx
let sortedArray = array.sort((a, b) => {
  if(a < b) return -1;
  if(a > b) return 1;
  if(a === b) return 0;
  else return -1;
})
```

else일 경우는 문자열과 숫자를 비교할 때이다.

---

## 객체를 배열로 변환하는 방법

- for in
    
    ```jsx
    let objstr = {
        a : 'a string',
        b : 'b string',
        c : 'c string'
    };
    
    let arr = [];
    
    for(let objkey in objstr){
        if(objstr.hasOwnProperty(objkey)){
    			arr.push(objkey);
    		}
    }
    console.log(arr); // ['a', 'b', 'c']
    ```
    
- Object.keys()함수
    
    객체에서 key를 문자열 배열로 반환한다.
    
     
    
    ```jsx
    let objstr = {
        a : 'a string',
        b : 'b string',
        c : 'c string'
    };
    
    let arr = Object.keys(objstr);
    
    console.log(arr); // ['a', 'b', 'c']
    ```
    
    Object.keys()함수와 map()함수를 결합하여 객체의 값을 배열로 변환할 수 있다.
    
    ```jsx
    let objstr = {
        a : 'a string',
        b : 'b string',
        c : 'c string'
    };
    
    let arr = Object.keys(objstr).map(item => objstr[item]);
    
    console.log(arr); // ['a string', 'b string', 'c string']
    ```
    
- Object.values()함수
    
    객체에서 값을 문자열 배열로 반환한다.
    
    ```jsx
    let objstr = {
        a : 'a string',
        b : 'b string',
        c : 'c string'
    };
    
    let arr = Object.values(objstr);
    
    console.log(arr); // ['a string', 'b string', 'c string']
    ```
    
- Object.entries() 함수
    
    객체에서 [key, value]형식의 값을 배열로 반환한다.
    
    ```jsx
    let objstr = {
        a : 'a string',
        b : 'b string',
        c : 'c string'
    };
    
    let arr = Object.entries(objstr);
    
    console.log(arr); // [['a','a string'], ['b','b string'], ['c','c string']]
    ```
    

---

## 귤 모으기

- forEach 사용

`tangerine.forEach((el) => (tangMap[el] = (tangMap[el] || 0) + 1));`

이해하고 넘어가기
