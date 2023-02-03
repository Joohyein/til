
## React

<aside>
💡 ‘React.js’는 **SPA** 기반의 프론트엔드 개발 프레임워크 중 하나이고 **컴포넌트** 단위의 독립적인 블록을 이용한다.

</aside>

- **SPA(Single Page Application) 아키텍쳐**
    
    한 개의 페이지로 이루어진 애플리케이션이다. MPA(Mulit Page Application)과는 상반된 개념이다.
    
     - 한 개의 페이지(Single page)로 구성된 웹 앱이다.
    
     - 서버에 1회 리소스를 요청한다.
    
     - 그 이후에는 필요할 때, 데이터만 받아와서 기존 페이지를 수정해주는 방식이다.
    
     - 자연스러운 UX(User Experience)를 구현할 수 있다.
    
     - 비슷한 기술들 : Angular, Vue
    

- **SPA의 단점**
    
    SEO(Search Engine Optimization)에는 약하다. SEO를 위해서는 HTML 페이지 전체가 필요하다. ex) 구글의 검색 엔진 - 자바스크립트가 로드되지 않은 페이지를 검색엔진으로 스캔해서 결론적으로 아무 페이지도 걸리지 않는다.
    
    이를 보완하기 위해 서버사이드 렌더링 프레임워크 next.js를 사용한다.
    

- **컴포넌트**
    
    리액트가 채택한 개발 방법이다. 프로그램의 한 부분을 의미하며 재사용이 가능한 최소 단위를 말한다. 객체지향언어를 사용할 때 자주 사용되며 재사용이 가능하기 때문에 컴포넌트 단위로 분류하거나 이동 가능하다는 특징이 있다.
    
    컴포넌트는 소프트웨어 시스템에서 독립적인 업무 또는 독립적인 기능을 수행하는 모듈로 시스템을 유지보수하는데 있어서 교체가 가능하다. 
    

- **Object**
    
    **생략해서 표현하는 방법**
    
    ```jsx
    const name = "hyein";
    const obj = {
    	name,   // name: name
    	age: 26,
    	doSomething: () => {}
    };
    ```
    
    **복사**
    
    - 얕은 복사
    
    주솟값을 복사한다.
    
    ```jsx
    const obj1 = {
    	value: 10
    };
    const obj2 = obj1;  // 얕은 복사
    
    obj2.value += 1;
    
    console.log(obj1); // { value: 11 }
    console.log(obj2); // { value: 11 }
    // obj1의 value값도 변경됨
    ```
    
    - 깊은 복사
    
    새로운 주솟값을 반환해준다.
    
    ```jsx
    const obj1 = {
    	value: 10
    };
    const obj2 = JSON.parse(JSON.stringify(obj));
    
    obj2.value += 1;
    
    console.log(obj1); // { value: 10 }
    console.log(obj2); // { value: 11 }
    ```
    

- 배열/객체 비구조화(Array/Object Destructuring)
    
    **객체의 비구조화(구조분해 할당)**
    
    ```jsx
    const person = {
    	name: "짱구",
    	age: "5",
    };
    const { name, age, height } = person;
    
    console.log(name); // 짱구
    console.log(age); // 5
    console.log(height); // undefined
    ```
    
    **배열의 비구조화(구조분해 할당)**
    
    ```jsx
    const arr = [1, 2, 3];
    const [one, two, three] = arr;
    
    console.log(one, two, three); // 1 2 3
    ```
    

- 전개 연산자(Spread Operator)
    
    ```jsx
    let [name, ...rest] = ["짱구", 5, '120'];
    
    console.log(name); // 짱구
    console.log(rest); // [5, '120']
    ```
    
    ```jsx
    let age = [20, 30];
    let people = [25, age, age];
    console.log(people); // [25, [20, 30], [20, 30]]
    
    let people2 = [25, ...age, ...age];
    console.log(people2); // [25, 20, 30, 20, 30]
    // 배열 전체가 아니가 값만 가져오고 싶을 때 사용
    ```
    

## html

<pre>

HTML `<pre>` 요소는 미리 서식을 지정한 텍스트를 나타내며, HTML에 작성한 내용 그대로 표현한다. 텍스트는 보통 고정폭 글꼴을 사용해 렌더링하고, 요소 내 공백문자를 그대로 유지한다.

```jsx
<pre>
  L          TE
    A       A
</pre>
```

- <fieldset>, <legend>, radio

```html
<fieldset>
	<legend>fieldset name</legend>
	<label><input type="radio" name="전달할 값의 이름" value="전달할 값" />value</label>
</fieldset>
```

- defer script

브라우저는 defer script를 ‘백그라운드’에서 다운로드 한다. 지연 스크립트를 다운로드하는 도중에도 HTML 파싱이 멈추지 않고 지연 스크립트 실행은 페이지 구성이 끝날 때까지 지연된다. 

## 문제

정보를 입력하고 제출하는 폼을 만드는 과정에서 폼을 만들고 input창을 빈칸으로 두고 제출 버튼을 눌러도 유효성 검사가 되지 않아서 click이벤트가 발생했다. 

## **해결방법**

기존에 자주 사용하던 ‘onclick’이 아닌 ‘onsubmit’을 폼 태그에 작성해주었다. 

```html
<!-- html -->
<form id="content" onsubmit="alert('제출 완료')">
	...
</form>
```

```jsx
// javascript
const submit = document.getElementById('content');
console.log(submit);
submit.addEventListener('submit', function (){
    alert('제출 완료');
})
```

**정규표현식**

```jsx
let str = "1D10S#10S";
let darts = str.match(/\d\d?.?\D/g);
let darts2 = str.march(/\d.?(S|T|D)(\*|#)?/g);
console.log(darts);  // [ '1D', '10S#', '10S' ]
```
