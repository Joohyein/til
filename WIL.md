## ES(ECMA Script)

자바스크립트의 표준, 규격을 나타내는 용어이다. ES5는 2009년 출시, ES6은 2015년에 출시되었다. 

**ES5**

배열에 forEach, map, filter, reduce, some, every와 같은 메소드들이 지원되었다. 

**ES6에 추가된 기능**

- let, const
    
    ES6 이전 var키워드는 함수 레벨 스코프를 가지며 암묵적 재할당이 가능하였다. 단점을 보완하기 위해 블록 레벨 스코프를 가지며 재할당이 가능한 let, const키워드가 추가되었다.
    
- Arrow function
    
    ```jsx
    // ES5
    function func(a, b){
    	return a + b;
    }
    
    // ES6
    const func = (a, b) => a + b;
    ```
    
    가독성 및 유지 보수성이 좋아졌다. 화살표 함수는 lexical this를 따르기 때문에 기존 함수와 this 바인딩이 다르다.
    

- Default parameter
    
    ES6 이전에는 함수의 매개변수에 초기값을 주기 위해서 함수 내부에서 로직이 필요했다. 
    
    ```jsx
    // ES5
    var tmp = function(a, b){
    	var a = a || 100;
    	var b = b || 200;
    	return a + b;
    
    // ES6
    const tmp = function(a = 100, b = 200) {
    	return a + b;
    }
    ```
    

- Template literal
    
    ```jsx
    // ES5
    var firstname = 'hyein'
    var lastname = 'Joo'
    var name = 'My name is ' + lastname + firstname + '.'
    // My name is Joohyein.
    
    // ES6
    const name = `My name is ${lastname}${firstname}.`
    // My name is Joohyein.
    ```
    

- Multi-line string
    
    ES6이전에는 줄바꿈을 하기 위해서 ‘\n’과 덧셈 연산자를 사용했는데 백틱을 사용하여 줄바꿈을 할 수 있다.
    
    ```jsx
    // ES5
    var str = 'My name is hyein. \n' +
    'hello' + 'hahaha'
    
    // ES6
    const str = `My name is hyein.
    hello hahaha`
    ```
    

- class
    
    객체 생성 방식 중 하나이다.
    
- module
    
    재사용하기 위한 코드 조각을 뜻하며, 세부사항은 캡슐화시키고 API부분만 외부에 노출시킨 코드이다.
    
    ```jsx
    <script type="module" src="app.mjs"></script>
    // type에 module을 추가하고 파일 확장자를 mjs로 변경
    ```
    
    모듈은 모듈 스코프를 가지며 export, import키워드로 사용한다.
    

- destructuring
    
    ```jsx
    // ES5
    var arr = [1, 2, 3]
    
    var a = arr[0]
    var b = arr[1]
    var c = arr[2]
    
    console.log(a, b, c);  // 1 2 3
    ```
    
    ```jsx
    // ES6
    const arr = [1, 2, 3];
    const [a, b, c] = arr;
    console.log(a, b, c);  // 1 2 3
    ```
    

## this

상황에 따라 그때 그때 달라질 뭔가를 가리키기 위해서 사용한다. 프로퍼티가 메서드가 자기를 참조할 수 있게 인스턴스 생성 이후에 해당 인스턴스를 가리키기 위해서 사용한다. 자바스크립트에서 this는 실행 컨텍스트가 생성될 때 함께 결정된다. 실행 컨텍스트는 함수를 호출할 때 생성되므로, this는 함수를 호출할 때 결정된다고 할 수 있다. 그래서 어떤 방식으로 호출하냐에 따라 값이 달라진다고 한다.

`this`키워드는 지금 동작하고 있는 코드를 가지고 있는 객체를 가리킨다. this 는 객체 멤버의 컨텍스트가 바뀌는 경우에도 언제나 정확한 값을 사용하게 해준다. ex) 두 개의 다른 `person`객체가 각각 다른 이름으로 인스턴스로 생성된 상태에서 인사말을 출력하기 위해 객체의 name을 참조해야 하는 경우

- 전역 공간에서의 this
    
    전역 공간에서의 this는 전역 객체를 가리킨다. 브라우저에서는 window, node.js에서는 global이라는 객체이다. 개념상 전역 컨텍스트를 실행하는 주체가 전역객체이기 때문이다. 자바스크립트가 실행되는 환경, 즉 런타임에 따라서 전역객체의 정보가 달라진다.
    
    자바스크립트의 모든 변수는 실은 특정 객체의 프로퍼티로서 동작한다. 사용자가 var 연산자를 이용해서 변수를 선언하더라도 실제 자바스크립트 엔진은 어떤 특정 객체의 프로퍼티로 인식하는 것이다. 특정 객체란 바로 실행 컨텍스트의 LexicalEnvironment이다. 실행 컨텍스트는 변수를 수집해서 L.E의 프로퍼티로 저장한다.
    
    전역변수를 선언하면 자바스크립트 엔진은 이를 전역객체의 프로퍼티로 할당한다.
    
    var로 선언한 전역변수와 전역객체의 프로퍼티는 호이스팅 여부 및 configurable(변경 및 삭제 가능성)여부에서 차이를 보인다.
    

## 동기, 비동기

**async와 await**

promise를 좀 더 편하게 사용할 수 있는 문법이다.

- async

function 앞에 `async` 를 붙이면 해당 함수는 항상 프라미스를 반환한다. 프라미스가 아닌 값을 반환하더라도 이행 상태의 프라미스(resolved promise)로 값을 감싸 이행된 프라미스가 반환되도록 한다.

- await

자바스크립트는 `await` 키워드를 만나면 프라미스가 처리될 때까지 기다린다. 결과는 그 이후 반환된다.

프라미스가 처리되길 기다리는 동안엔 엔진이 다른 일(다른 스크립트를 실행, 이벤트 처리 등)을 할 수 있기 때문에, CPU 리소스가 낭비되지 않는다.

`await` 는 `promise.then` 보다 좀 더 세련되게 프라미스의 `result` 값을 얻을 수 있도록 해주는 문법이다. 가독성도 좋고 쓰기도 쉽다.
