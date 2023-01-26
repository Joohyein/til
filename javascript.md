# Day5 동기, 비동기

- 자바스크립트는 싱글 스레드이다
    
    자바스크립트의 메인 스레드인 이벤트 루프가 싱글 스레드이기 때문에 자바스크립트를 싱글 스레드 언어라고 부른다. 하지만 이벤트 루프만 독립적으로 실행되지 않고 웹 브라우저나 NodeJS같은 멀티 스레드 환경에서 실행된다. 즉, 자바스크립트 자체는 싱글 스레드가 맞지만 자바스크립트 런타임은 싱글 스레드가 아니다. 
    
    **싱글 스레드로 한 번에 여러 요청을 처리하는 방법**
    
    기존 동기식 요청은 코드를 한줄 한줄 차례대로 실행한다. 그래서 하나의 작업에 걸리는 시간에 관계 없이 첫 번째 코드가 실행 된 뒤 다음 코드가 실행된다. 이렇게 되면 앞의 작업시간이 길수록 시간 및 자원의 낭비가 심해진다. 하나의 요청이 완료될 때까지 기다리지 않고 동시에 다른 작업을 실행하는 비동기 호출로 극복할 수 있다. 
    
    - 자바스크립트 비동기 런타임 과정
        
        자바스크립트가 실행될 때 실행을 도와주는 요소
        
        - Call Stack : 자바스크립트에서 수행해야 할 함수들을 순차적으로 스택에 담아 처리
        - Web API : 웹 브라우저에서 제공하는 API로 AJAX나 Timeout등의 비동기 작업을 실행
        - Task Queue : Callback Queue라고도 하며 Web API에서 넘겨받은 Callback함수를 저장
        - Event Loop : Call Stack이 비어있다면 Task Queue의 작업을 Call Stack으로 옮김
    
    멀티 쓰레드로 구현된 서비스에서는 이 동시성 문제에 대해 정말 많은 신경을 쓴다. 하지만 자바스크립트는 단일 쓰레드로 실행되므로 인해 교착 상태와 같은 다중 쓰레드 환경에서 발생할 수 있는 복잡한 시나리오를 신경 쓸 필요가 없으며 비동기 처리를 통해 쉽게 여러 요청을 처리할 수 있다.
    
- 콜백
    
    `src` 에 있는 스크립트를 읽어오는 함수 `loadScript(src)` 를 예시로 비동기 동작 처리가 어떻게 일어나는지 살펴보자
    
    ```jsx
    function loadScript(src) {
    	// <script> 태그를 만들고 페이지에 태그를 추가한다.
    	// 태그가 페이지에 추가되면 src에 있는 스크립트를 로딩하고 실행한다.
    	let script = document.createElement('script');
    	script.src = src;
    	document.head.append(script);
    }
    ```
    
    함수 `loadScript(src)` 는 `<script src="...">` 를 동적으로 만들고 이를 문서에 추가한다. 브라우저는 자동으로 태그에 있는 스크립트를 불러오고, 로딩이 완료되면 스크립트를 실행한다. 
    
    새롭게 불러온 스크립트에 있는 함수를 콜백 함수 안에서 호출하면 원하는 대로 외부 스크립트 안의 함수를 사용할 수 있다. 
    
    **에러 핸들링**
    
    `loadScript` 에서 로딩 에러를 추적할 수 있게 기능을 개선해보자.
    
    ```jsx
    function loadScript(src, callback) {
      let script = document.createElement('script');
      script.src = src;
    
      script.onload = () => callback(null, script);
      script.onerror = () => callback(new Error(`${src}를 불러오는 도중에 에러가 발생했습니다.`));
    
      document.head.append(script);
    }	
    ```
    
    - 오류 우선 콜백
        - `callback` 의 첫 번째 인수는 에러를 위해 남겨둔다. 에러가 발생하면 이 인수를 이용해 `callback(err)` 이 호출된다.
        - 두 번째 인수(필요하면 인수를 더 추가할 수 있음)는 에러가 발생하지 않았을 때를 위해 남겨둔다. 원하는 동작이 성공한 경우엔 `callback(null, result1, result2...)` 이 호출된다.
        - 오류 우선 콜백 스타일을 사용하면, 단일 콜백 함수에서 에러 케이스와 성공 케이스 모두를 처리할 수 있다.
    
    **멸망의 피라미드 혹은 콜백 지옥**
    
    깊은 중첩 코드가 만들어내는 패턴이다. 비동기 동작이 하나씩 추가될 때마다 중첩 호출이 만들어내는 ‘피라미드’는 오른쪽으로 점점 커진다. 멸망의 피라미드를 피할 가장 좋은 방법 중 하나는 ‘프라미스(promise)’를 사용하는 것이다. 
    
    <과제 - 콜백을 이용한 움직이는 원>
    
    ```html
    <!DOCTYPE html>
    <html>
    
    <head>
      <meta charset="utf-8">
      <style>
        .message-ball {
          font-size: 20px;
          line-height: 200px;
          text-align: center;
        }
        .circle {
          transition-property: width, height, margin-left, margin-top;
          transition-duration: 2s;
          position: fixed;
          transform: translateX(-50%) translateY(-50%);
          background-color: red;
          border-radius: 50%;
        }
      </style>
    </head>
    
    <body>
    
    <button onclick="go()">여기를 클릭해 주세요.</button>
    
      <script>
    
      function go() {
        showCircle(150, 150, 100, div => {
          div.classList.add('message-ball');
          div.append("안녕하세요!");
        });
      }
    
      function showCircle(cx, cy, radius, callback) {
        let div = document.createElement('div');
        div.style.width = 0;
        div.style.height = 0;
        div.style.left = cx + 'px';
        div.style.top = cy + 'px';
        div.className = 'circle';
        document.body.append(div);
    
        setTimeout(() => {
          div.style.width = radius * 2 + 'px';
          div.style.height = radius * 2 + 'px';
    
          div.addEventListener('transitionend', function handler() {
            div.removeEventListener('transitionend', handler);
            callback(div);
          });
        }, 0);
      }
      </script>
    
      <!-- <div class="circle message-ball" style="width: 200px; height: 200px; left: 150px; top: 150px;">안녕하세요!</div> -->
    </body>
    </html>
    ```
    
    ### addEventListener 'transitionend'
     setTimeout 안의 함수에 transition-property에 추가 된 요소 중 변화가 있는 값이 변하면서 callback이 그 수만큼 호출되어서 removeEventListener를 해줘야 한다. 
    
    <aside>
    💡 transitionend 이벤트
    transitionend 이벤트는 CSS transition이 완료되면 발생한다. transition 속성이 제거되거나 display가 none으로 설정된 경우와 같이 완료 전에 transition이 제거된 경우에는 이벤트가 생성되지 않는다.
    
    </aside>
    
- Promise
    - ‘제작 코드(producing code)’는 원격에서 스크립트를 불러오는 것 같은 시간이 걸리는 일을 한다.
    - ‘소비 코드(consuming code)’는 ‘제작 코드’의 결과를 기다렸다가 이를 소비한다. 이때 소비 주체(함수)는 여럿이 될 수 있다.
    - 프라미스(promise)는 ‘제작 코드’와 ‘소비 코드’를 연결해 주는 특별한 자바스크립트 객체이다. ‘프라미스’는 시간이 얼마나 걸리든 상관없이 약속한 겨로가를 만들어 내는 ‘제작 코드’가 준비되었을 때, 모든 소비 코드가 결과를 사용할 수 있도록 해준다.
    
    ```jsx
    //promise 객체 문법
    let promise = new Promise(function(resolve, reject) {
    	// executor (제작 코드)
    });
    ```
    
    `new Promise` 에 전달되는 함수는 executor(실행자, 실행 함수)라고 부른다. executor는 `new Promise` 가 만들어질 때 자동으로 실행되는데, 결과를 최종적으로 만들어내는 제작 코드를 포함한다. 
    
    executor의 인수 `resolve` 와 `reject` 는 자바스크립트에서 자체 제동하는 콜백이다. 
    
    executor에선 결과를 즉시 얻든 늦게 얻든 상관없이 상황에 따라 인수로 넘겨준 콜백 중 하나를 반드시 호출해야 한다.
    
    - resolve(value) - 일이 성공적으로 끝난 겨우 그 결과를 나타내는 `value` 와 함께 호출
    - reject(error) - 에러 발생 시 여러 객체를 나타내는 `error` 와 함께 호출
    
    ```jsx
    //promise 생성자와 간단한 executor 함수로 만든 예시
    let promise = new Promise(function(resolve, reject) {
    	// 프라미스가 만들어지면 executor 함수는 자동으로 실행된다.
    	// 1초 뒤에 일이 성공적으로 끝났다는 신호가 전달되면서 result는 '완료'가 된다.
    	setTimeout(() => resolve("완료"), 1000);
    });
    ```
    
    1. executor는 `new Promise` 에 의해 자동으로 그리고 즉각적으로 호출된다.
    2. executor는 인자로 `resolve` 와 `reject` 함수를 받는다. 이 함수들은 자바스크립트 엔진이 미리 정의한 함수이므로 개발자가 따로 만들 필요는 없다. 다만, `resolve` 나 `reject` 중 하나는 반드시 호출해야 한다.
        
        executor ‘처리’가 시작 된 지 1초 후, `resolve("done")` 이 호출되고 결과가 만들어진다. 
        
    - 소비자 : then, catch, finally
    
    프라미스 객체는 executor(’제작 코드’)와 결과나 에러를 받을 소비 함수를 이어주는 역할을 한다. 소비함수는 `.then` , `.catch` , `.finally` 메서드를 사용해 등록된다. 
    
    **then**
    
    가장 중요하고 기본이 되는 메서드이다. 
    
    ```jsx
    promise.then{
    	function(result) { /* 결과(result)를 다룬다 */ },  // 프라미스가 이행되었을 때 실행되는 함수이고, 여기서 실행 결과를 받는다.
    	function(error) { /* 에러(error)를 다룬다 */ }  // 프라미스가 거부되었을 때, 실행되는 함수이고, 여기서 에러를 받는다.
    );
    ```
    
    ```jsx
    // 성공적으로 이행된 프라미스
    let promise = new Promise(function(resolve, reject) {
    	setTimeout(() => resolve("완료"), 1000);
    });
    // resolve함수는 .then의 첫 번째 함수(인수)를 실행한다.
    promise.then(
    	result => alert(result), // 1초 뒤 "완료"를 출력
    	error => alert(error) // 실행되지 않음
    );
    ```
    
    ```jsx
    // 프라미스가 거부된 경우
    let promise = new Promise(function(resolve, reject) {
    	setTimeout(() => reject(new Error("에러 발생")), 1000);
    });
    // resolve함수는 .then의 첫 번째 함수(인수)를 실행한다.
    promise.then(
    	result => alert(result), // 실행되지 않음
    	error => alert(error) // 1초 뒤 "Error: 에러 발생"을 출력
    );
    ```
    
    ```jsx
    // 작업이 성공적으로 처리된 경우만 다루고 싶다면 then에 인수를 하나만 전달하면 된다.
    let promise = new Promise(resolve => {
    	setTimeout(() => resolve("완료"), 1000);
    });
    
    promise.then(alert); 
    ```
    
    **catch**
    
    에러가 발생한 경우만 다루고 싶다면 `.then(null, errorHandlingFunction)` 같이 `null` 을 첫 번째 인수로 전달하면 된다. `.catch(errorHandlingFunction)` 를 써도 되는데, `.catch` 는 `.then` 에 `null` 을 전달하는 것과 동일하게 작동한다. 
    
    ```jsx
    let promise = new Promise((resolve, reject) => {
    	setTimeout(() => reject(new Error("에러 발생")), 1000);
    });
    
    promise.catch(alert); 
    // .catch(f)는 promise.then(null, f)과 동일하게 작동한다.
    ```
    
    **finally**
    
    프라미스가 처리되면 `f` 가 항상 실행된다는 점에서 `.finally(f)` 호출은 `.then(f, f)` 와 유사하다. 쓸모가 없어진 로딩 인디케이터(loading indicator)를 멈추는 경우같이, 결과가 어떻든 마무리가 필요하면 `finally` 가 유용하다. 
    
    ```jsx
    new Promise((resolve, reject) => {
    	/* 시간이 걸리는 어떤 일을 수행, 그 후 resolve, reject를 호출 */
    });
    
    .finally(() => 로딩 인디케이터 중지)
    .then(result => result와 err 보여줌 => error 보여줌)
    ```
    
    finally와 .then(f, f)의 차이점
    
     - `finally` 핸들러에는 인수가 없다. `finally` 에선 프라미스가 이행되었는지, 거부되었는지 알 수 없다. 절차를 마무리하는 ‘보편적’ 동작으로 수행하기 때문에 성공, 실패 여부를 몰라도 된다.
    
     - `finally` 핸들러는 자동으로 다음 핸들러에 결과와 에러를 전달한다. `finally` 는 프라미스 결과를 처리하기 위해 만들어진 게 아니다. 프라미스 결과는 `finally` 를 통과해서 전달된다. 
    
     - `finally(f)` 는 함수 `f` 를 중복해서 쓸 필요가 없기 때문에 `.then(f, f)` 보다 문법 측면에서 더 편리하다. 
    
    ```jsx
    let promise = new Promise(resolve, reject) {
    	resolve(1);
    	
    	setTimeout(() => resolve(2), 1000);
    });
    
    promise.then(alert);
    ```
    
    → 1 이 출력된다. 첫 번째 `reject/resolve` 호출만 고려대상이기 때문에 두 번째 `resolve` 는 무시되기 때문이다. 
    
    ```jsx
    function delay(ms) {
    	return new Promise(resolve => setTimeout(resolve, ms));
    }
    
    delay(3000).then(() => alert('3초 후 실행'));
    ```
    
    → `resolve` 가 인수 없이 호출되었다. 함수 `delay` 는 지연 확인용이기 때문에 반환 값이 필요없다. 
    
    프라미스로 애니메이션이 적용된 원 만들기
    
    ```jsx
    <!DOCTYPE html>
    <html>
    
    <head>
      <meta charset="utf-8">
      <style>
        .message-ball {
          font-size: 20px;
          line-height: 200px;
          text-align: center;
        }
        .circle {
          transition-property: width, height, margin-left, margin-top;
          transition-duration: 2s;
          position: fixed;
          transform: translateX(-50%) translateY(-50%);
          background-color: red;
          border-radius: 50%;
        }
      </style>
    </head>
    
    <body>
    
      <button onclick="go()">Click me</button>
    
      <script>
    
      function go() {
        showCircle(150, 150, 100).then(div => {
          div.classList.add('message-ball');
          div.append("Hello, world!");
        });
      }
    
      function showCircle(cx, cy, radius) {
        let div = document.createElement('div');
        div.style.width = 0;
        div.style.height = 0;
        div.style.left = cx + 'px';
        div.style.top = cy + 'px';
        div.className = 'circle';
        document.body.append(div);
    
        return new Promise(resolve => {
          setTimeout(() => {
            div.style.width = radius * 2 + 'px';
            div.style.height = radius * 2 + 'px';
    
            div.addEventListener('transitionend', function handler() {
              div.removeEventListener('transitionend', handler);
              resolve(div);
            });
          }, 0);
        })
      }
      </script>
    
    </body>
    </html>
    ```
    
- 프라미스 체이닝
    
    프라미스 체이닝(promise chaining)을 이용한 비동기 처리
    
    ```jsx
    new Promise(function(resolve, reject) {
    
      setTimeout(() => resolve(1), 1000); // (*)
    
    }).then(function(result) { // (**)
    
      alert(result); // 1
      return result * 2;
    
    }).then(function(result) { // (***)
    
      alert(result); // 2
      return result * 2;
    
    }).then(function(result) {
    
      alert(result); // 4
      return result * 2;
    
    });
    ```
    
    프라미스 체이닝이 가능한 이유는 `promise.then` 을 호출하면 프라미스가 반환되기 때문이다. 반환된 프라미스에는 당연히 `.then` 을 호출할 수 있다.
    
- async와 await
    
    promise를 좀 더 편하게 사용할 수 있는 문법이다.
    
    - async 함수
    
    function 앞에 `async` 를 붙이면 해당 함수는 항상 프라미스를 반환한다. 프라미스가 아닌 값을 반환하더라도 이행 상태의 프라미스(resolved promise)로 값을 감싸 이행된 프라미스가 반환되도록 한다.
    
    ```jsx
    async function func() {
    	return 1;
    }
    func().then(alert); // 1
    ```
    
    ```jsx
    // 명시적으로 프라미스를 반환하는 것도 가능한데, 결과는 동일하다.
    async function func() {
    	return Promise.resolve(1);
    }
    func().then(alert); // 1
    ```
    
    - await
    
    자바스크립트는 `await` 키워드를 만나면 프라미스가 처리될 때까지 기다린다. 결과는 그 이후 반환된다. 
    
    ```jsx
    // 1초 후 이행되는 프로미스 예시
    async function func() {
    	let promise = new Promise((resolve, reject) => {
    		setTimeout(() => resolve("완료"), 1000)
    });
    
    	let result = await promise; // 프라미스가 이행될 때까지 기다림 
    
    	alert(result); // "완료"
    }
    func();
    ```
    
    프라미스가 처리되길 기다리는 동안엔 엔진이 다른 일(다른 스크립트를 실행, 이벤트 처리 등)을 할 수 있기 때문에, CPU 리소스가 낭비되지 않는다.
    
    `await` 는 `promise.then` 보다 좀 더 세련되게 프라미스의 `result` 값을 얻을 수 있도록 해주는 문법이다. 가독성도 좋고 쓰기도 쉽다. 
    
    - 에러 핸들링
    
    ```jsx
    async function func() {
    	try {
    		let response = await fetch('http://유효하지-않은-주소');
    		let user = await response.json();
    	} catch(err) {
    		alert(err);
    	}
    }
    func();
    ```
    
    → 에러가 발생하면 제어 흐름이 `catch` 블록으로 넘어간다.
