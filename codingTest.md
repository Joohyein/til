**문자열 내림차순 정렬 - sort()**

```jsx
let str = ['a', 'h', 'i', 'b'];

str.sort((a, b) => {
	if(a > b) return -1;
	else if(a < b) return 1;
	else return 0;
});
```

**localeCompare**

메서드는 참조 문자열이 정렬 순으로 지정된 문자열 앞 혹은 뒤에 오는지 또는 동일한 문자열인지 나타내는 수치를 반환한다.

```jsx
function solution(strings, n) {
    return strings.sort((a, b) => {
			if (a[n] === b[n]) {				
				a.localeCompare(b) // a가 b보다 전에 위치하므로 음수
			} else {
				a[n].localeCompare(b[n])
		}
    });
}
```

**프로그래머스 - 행렬의 덧셈**

```jsx
function solution(arr1, arr2) {
  var answer = [[]];
	for(let i = 0; i < arr1.length; i++){
		const arr = [];
		for(let j = 0; j < arr1[i].length; j++){
				arr.push(arr1[i][j] + arr2[i][j]);
		}
		answer.push(arr);
	}
  return answer;
}
```

```jsx
// map
function solution2(arr1, arr2) {
  return arr1.map((row, i) => {
    return row.map((element, j) => {
      console.log(element);
      return element + arr2[i][j];
    });
  });
}
```


---

**참고문헌**

localecompare - 

[String.prototype.localeCompare() - JavaScript | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare)
