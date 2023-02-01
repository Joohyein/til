**padStart**

문자열의 시작을 다른 문자열로 채워,주어진 길이를 만족하는 새로운 문자열을 반환한다. 문자열의 시작부터 적용된다.

```jsx
let str = '1';
console.log(str.padStart(2, '0')); // '01'
// 길이가 2가 되도록 문자열 앞에 0을 추가
```

```jsx
function solution(left, right) {
    var answer = 0;
    
    for(let i=left; i<=right; i++){
        Math.sqrt(i)%1===0 ? answer-=i : answer+=i;
    }
    
    return answer;
}
// 약수의 개수가 홀수 : 제곱수가 정수임
```

match()

문자열이 정규식과 매치되는 부분을 검색한다.

```jsx
let str = "hello world";
console.log(str.match('world'); // world
```

자연수 n이 매개변수로 주어질 때, 연속된 자연수들로 n을 표현하는 방법의 수를 return.

```jsx
// 점화식 사용
function solution(n) {
    let result = 0;
    for (let i = 1; i <= n; i++) {
        if (n % i == 0 && i % 2 == 1) {
            result++;
        }
    }
    return result;
}
```
