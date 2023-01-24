- 문자열 뒤집기 - split(), reverse(), join()
    - split() : 문자열을 부분 문자열로 구분해 문자열 객체를 여러 개의 문자열로 이루어진 배열로 분할한다.
    - reverse() : 배열을 반전한다.
    - join() : 배열의 모든 요소를 문자열로 결합한다.
    
    ```jsx
    function reverse(str) {
    	let splitStr = str.split(""); // ["h", "e", "l", "l", "o"]
    	let reverseArr = splitStr.reverse(); // ["o", "l", "l", "e", "h"]
    	let joinArr = reverseArr.join(""); // "olleh"
    	return joinArr;
    }
    reverse("hello");
    ```
    
    한 줄에 작성 가능
    
    ```jsx
    function reverse(str) {
    	return str.split("").reverse().join("");
    }
    reverse("hello");
    ```
    
- concat()
    
    두 개의 문자열을 하나의 문자열로 만들어준다. 입력값을 문자열 대신 배열을 사용하여 두 개의 배열을 하나의 배열로 만들어줄 수도 있다. **기존 배열을 변경하지 않으며 추가된 새로운 배열을 반환한다.**
    
    ```jsx
    let str1 = "hello";
    let str2 = "world";
    console.log(str1.concat(str2));
    // "hello world"
    
    let arr1 = new Array("1", "2");
    let arr2 = new Array("3", "4");
    console.log(arr1.concat(arr2));
    // ["1", "2", "3", "4"]
    ```
    
- Number.isInteger()
    
    인수의 값이 정수인지 아닌지를 반환해준다. 전달된 값이 정수이면 `true` 를 반환하고 정수가 아니라면 `false` 를 반환한다. (String, true, NaN, Infinity와 같은 값도 false를 반환)
    
    ```jsx
    Number.isInteger(0); // true;
    Number.isInteger(-10); // true;
    Number.isInteger(0.1); // false
    ```
    
- 배열값 초기화하는 방법
    - fill()
    
    ```jsx
    let arr = [1,2,5,10,30];
    console.log(arr.fill(0)); // [0,0,0,0,0]
    ```
    
    - 일정 길이의 배열을 0으로 초기화하기
    
    ```jsx
    arr = function(len) {
    	return new Array(len).fill(0);
    }
    ```
