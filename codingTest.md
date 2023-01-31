**startwith**

**`startsWith()`**메서드는 어떤 문자열이 특정 문자로 시작하는지 확인하여 결과를 `true`혹은 `false`로 반환한다.

```jsx
const str1 = 'Saturday night plans';

console.log(str1.startsWith('Sat'));
// Expected output: true

console.log(str1.startsWith('Sat', 3));
// Expected output: false
```

**정규표현식**

```jsx
let regex = /\d{3}-\d{4}-\d{4}/;
regex.test('010-0101-0101'); // true
regex.test('01-0000-111'); // false
```

```jsx
let str = "내 전화번호는 010-1111-0000 이야. 저장해.";
str.match(/\d{3}-\d{4}-\d{4}/); //010-1111-0000
```
