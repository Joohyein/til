**charCodeAt, fromCharCode**

- charCodeAt : 문자열을 아스키코드로 변환
    
    ```jsx
    // 예제
    let str = 'abc'
    // c를 아스키코드로 변환
    let ascii = str.charCodeAt(2); // 99
    ```
    
- fromCahrCode : 아스키코드를 문자열로 변환
    
    ```jsx
    let ascii = 99;
    let str = String.fromCharCode(ascii); // 'c'
    ```
    

**Array.from**

```jsx
let arr = ['1', '2', '3', '4', '5'];
answer = Array.from(arr, (v) => Number(v));
```

- 숫자를 문자열로 바꾸기
    
    ```jsx
    let num = 123;
    let str = '' + num;
    ```
    

**최빈값 구하기**

```jsx
function solution(array) {
    let a = array.filter((num, index) => array.indexOf(num) == index); 
    if(a.length === 1) return array[0];
    let arr = {};

    for(let i = 0; i < array.length; i++){
        if(arr[array[i]]) arr[array[i]]++;
        else arr[array[i]] = 1;
    }
    
    let tmp = [];
    for(let value in arr){
        tmp.push([value, arr[value]]);
    }
    
    tmp.sort(function(a, b) {
        return b[1] - a[1];
    });
    
    if(tmp[0][1] === tmp[1][1]) return -1;
    return +tmp[0][0];
}
```

```jsx
let a = array.filter((num, index) => array.indexOf(num) == index); 
```

배열에 같은 값만 여러 개 있을 때 런타임 에러가 생겨서 filter함수를 사용해서 길이가 1이면 배열 안의 값을 리턴하도록 최상단에 넣어주었다.
