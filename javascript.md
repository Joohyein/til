- 함수와 객체
    - 함수
        
        유사한 동작을 하는 코드가 여러 곳에서 필요할 때 사용 ex) 사용자가 로그인이나 로그아웃을 했을 때 안내 메세지를 보여주는 동작
        
        - 함수 선언
            
            ```jsx
            function name(parameter1, parameter2, ... parameterN) {
            	// ...
            }
            
            name(...);
            ```
            
        
        - 지역 변수
            
            함수 내에서 선언한 변수인 지역 변수는 함수 안에서만 접근할 수 있다.
            
        - 외부 변수
            
            함수 내부에서 함수 외부의 변수인 외부 변수에 접근하거나 수정할 수 있다.
            
        - 전역 변수
            
            함수 외부에 선언된 변수이다. 변수는 연관되는 함수 내에 선언하고, 전역변수는 되도록 사용하지 않는 것이 좋다. 비교적 근래에 작성된 코드들은 대부분 전역변수를 사용하지 않거나 최소한으로만 사용한다. 다만 프로젝트 전반에서 사용되는 데이터는 전역 변수에 저장하는 것이 유용한 경우도 있다.
            
        - 매개변수(parameter)
            
            매개변수를 이용하면 임의의 데이터를 함수 안에 전달할 수 있다. 매개변수는 인자(parameter)라고 불리기도 한다.
            
        - 기본값
            
            함수 호출 시 매개변수에 인수를 전달하지 않으면 그 값은 `undefined`가 된다.
            
            매개변수에 값을 전달하지 않아도 그 값이 `undefind` 가 되지 않게 하려면 함수를 선언할 때 `=` 를 사용해 ‘기본값(default value)’을 설정해주면 된다.
            
            ```jsx
            function showMessage(from, text = "no text given") {
              alert( from + ": " + text );
            }
            
            showMessage("Ann"); // Ann: no text given
            ```
            
            text가 값을 전달받지 못해도 undefined대신 기본값 “no text given”이 할당된다.
            
            - 매개변수 기본값 평가 시점
            
            ```jsx
            function showMessage(from, text = anotherFunction()) {
              // anotherFunction()은 text값이 없을 때만 호출됨
              // anotherFunction()의 반환 값이 text의 값이 됨
            }
            ```
            
            - 매개변수 기본값을 설정할 수 있는 방법
            
            함수 선언 후에 매개변수 기본값을 설정하는 것이 적절한 경우도 있다. 이런 경우엔 함수를 호출할 때 매개변수를 undefined와 비교하여 매개변수가 전달되었는지 확인한다.
            
            ```jsx
            function showMessage(text) {
              // ...
            
              if (text === undefined) { // 매개변수가 생략되었다면
                text = '빈 문자열';
              }
            
              alert(text);
            }
            
            showMessage(); // 빈 문자열
            ```
            
            - if문 대신 논리연산자 `||` 를 사용할 수도 있다.
            
            ```jsx
            // 매개변수가 생략되었거나 빈 문자열("")이 넘어오면 변수에 '빈 문자열'이 할당됩니다.
            function showMessage(text) {
              text = text || '빈 문자열';
              ...
            }
            ```
            
            - nullish 병합 연산자 `??` 를 사용하면 `0` 처럼 falsy로 평가되는 값들을 일반 값처럼 처리할 수 있어서 좋다.
            
            ```jsx
            // 매개변수 'count'가 `undefined` 또는 `null`이면 'unknown'을 출력해주는 함수
            function showCount(count) {
              alert(count ?? "unknown");
            }
            
            showCount(0); // 0
            showCount(null); // unknown
            showCount(); // unknown
            ```
            
        - 반환값 return
            
            return; 만 명시하면 즉시 함수가 종료된다. return문이 없거나 return지시자만 있는 함수는 undefined를 반환한다.
            
            **return과 값 사이에 절대 줄을 삽입하지 않는다**
            
            표현식을 여러 줄에 걸쳐 작성하고 싶다면 return지시자가 있는 줄에서 시작하도록 작성해야 한다.
            
            ```jsx
            // 안되는 예
            return;
             (some + long + expression + or + whatever * f(a) + f(b))
            ```
            
            ```jsx
            // 가능한 예
            return (
              some + long + expression
              + or +
              whatever * f(a) + f(b)
              )
            ```
            
        - 함수 이름짓기
            
            함수 이름은 가능한 한 간결하고 명확해야 하고 어떤 동작을 하는지 설명할 수 있어야 한다.
            
            - show… : 대개 무언가를 보여주는 함수
            - get… : 값을 반환함
            - calc : 무언가를 계산함
            - create… : 무언가를 생성함
            - check… : 무언가를 확인하고 불린값을 반환함
            
            ```jsx
            showMessage(..)     // 메시지를 보여줌
            getAge(..)          // 나이를 나타내는 값을 얻고 그 값을 반환함
            calcSum(..)         // 합계를 계산하고 그 결과를 반환함
            createForm(..)      // form을 생성하고 만들어진 form을 반환함
            checkPermission(..) // 승인 여부를 확인하고 true나 false를 반환함
            ```
            
- 함수 표현식
    
    자바스크립트에서 함수는 값이다. 따라서 함수를 값처럼 취급할 수 있다. 
    
    - 함수 복사
        
        ```jsx
        function sayHi() {   // (1) 함수 생성
          alert( "Hello" );
        }
        
        let func = sayHi;    // (2) 함수 복사
        
        func(); // Hello     // (3) 복사한 함수를 실행(정상적으로 실행됩니다)!
        sayHi(); // Hello    //     본래 함수도 정상적으로 실행됩니다.
        ```
        
    - 콜백 함수
        
        ex) 매개변수가 3개 있는 함수, `ask(question, yes, no)` 
        
        ```jsx
        function ask(question, yes, no) {
          if (confirm(question)) yes()
          else no();
        }
        
        function showOk() {
          alert( "동의하셨습니다." );
        }
        
        function showCancel() {
          alert( "취소 버튼을 누르셨습니다." );
        }
        
        // 사용법: 함수 showOk와 showCancel가 ask 함수의 인수로 전달됨
        ask("동의하십니까?", showOk, showCancel);
        ```
        
        함수는 반드시 질문(question)을 해야 하고, 사용자의 답변에 따라 yes()나 no()를 호출한다.
        
        함수 `ask` 의 인수, `showOk` 와 `showCancel` 은 콜백함수 또는 콜백이라고 불린다.
        
        함수를 함수의 인수로 전달하고, 필요하다면 인수로 전달한 그 함수를 “나중에 호출(called back)” 하는 것이 콜백 함수의 개념이다. 위의 예시에선 사용자가 “yes”라고 대답한 경우 showOk가 콜백이 되고, “no”라고 대답한 경우 showCancelrk 콜백이 된다.
        
        ```jsx
        function ask(question, yes, no) {
          if (confirm(question)) yes()
          else no();
        }
        
        ask(
          "동의하십니까?",
          function() { alert("동의하셨습니다."); },
          function() { alert("취소 버튼을 누르셨습니다."); }
        );
        ```
        
        위의 코드를 보면 ask(…) 안에 함수가 선언 되었다. 이름 없이 선언한 함수는 익명 함수라고 부른다. 익명 함수는 (변수에 할당된 게 아니기 때문에) ask 바깥에선 접근할 수 없다. 위 예시는 의도를 갖고 구현했기 때문에 바깥에서 접근할 수 없어도 문제가 없다. 
        
    - 함수 표현식 vs 함수 선언문
        - 함수 선언문 : 함수는 주요 코드 흐름 중간에 독자적인 구문 형태로 존재한다.
            
            ```jsx
            // 함수 선언문
            function sum(a, b) {
              return a + b;
            }
            ```
            
        - 함수 표현식 : 함수는 표현식이나 구문 구성(syntax construct)내부에 생성된다.
            
            ```jsx
            // 함수 표현식
            let sum = function(a, b) {
              return a + b;
            };
            ```
            
        
        자바스크립트는 스크립트를 실행하기 전, 준비단계에서 전역에 선언된 함수 선언문을 찾고, 해당 함수를 생성한다. 스크립트가 진짜 실행되기 전 “초기화 단계”에서 함수 선언 방식으로 정의한 함수가 생성되는 것이다.
        
        스크립트는 함수 선언문이 모두 처리된 이후에서야 실행된다. 따라서 스크립트 어디서든 함수 선언문으로 선언한 함수에 접근할 수 있는 것이다.
        
        예시를 보면,
        
        ```jsx
        sayHi("John"); // Hello, John
        
        function sayHi(name) {
          alert( `Hello, ${name}` );
        }
        ```
        
        함수 선언문 `sayHi` 는 스크립트 실행 준비 단계에서 생성되기 때문에 스크립트 내 어디에서든 접근할 수 있다. 
        
        그러나 함수 표현식으로 정의한 함수는 함수가 선언되기 전에 접근하는 게 불가능하다.
        
        ```jsx
        sayHi("John"); // error!
        
        let sayHi = function(name) {  // (*) 마술은 일어나지 않습니다.
          alert( `Hello, ${name}` );
        };
        ```
        
        if문 밖에 선언한 변수에 함수 표현식으로 만든 함수를 할당하면 if문 밖에서도 함수를 호출할 수 있다.
        
        ```jsx
        let age = prompt("나이를 알려주세요.", 18);
        
        let welcome;
        
        if (age < 18) {
        
          welcome = function() {
            alert("안녕!");
          };
        
        } else {
        
          welcome = function() {
            alert("안녕하세요!");
          };
        
        }
        
        welcome(); // 제대로 동작합니다.
        ```
        
        물음표 연산자 `?` 를 사용하면 좀 더 단순화할 수 있다.
        
        ```jsx
        let age = prompt("나이를 알려주세요.", 18);
        
        let welcome = (age < 18) ?
          function() { alert("안녕!"); } :
          function() { alert("안녕하세요!"); };
        
        welcome(); // 제대로 동작합니다.
        ```
        
    
    <aside>
    💡 **함수 선언문과 함수 표현식 중 무엇을 선택해야 하나요?**
    
    함수 선언문을 이용해 함수를 선언하는 걸 먼저 고려하는 게 좋다. 함수 선언문으로 함수를 정의하면, 함수가 선언되기 전에 호출할 수 있어서 코드 구성을 좀 더 자유롭게 할 수 있습니다.
    
    함수 선언문을 사용하면 가독성도 좋아진다. 코드에서 `let f = function(…) {…}`보다 `function f(…) {…}` 을 찾는 게 더 쉽다. 함수 선언 방식이 더 “눈길을 사로잡는다”.
    
    그러나 어떤 이유로 함수 선언 방식이 적합하지 않거나, (위 예제와 같이) 조건에 따라 함수를 선언해야 한다면 함수 표현식을 사용해야 한다.
    
    </aside>
    
- 화살표 함수
    
    함수 표현식보다 단순하고 간결한 문법으로 함수를 만들 수 있는 방법이다.
    
    ```jsx
    let func = (arg1, arg2, ... argN) => expresstion
    // 화살표는 우측의 표현식(expresstion)을 평가하고, 평과 결과를 반환한다.
    ```
    
    아래 함수의 축약버전이다.
    
    ```jsx
    let func = function(arg1, arg2, ... argN) {
    	return expression;
    };
    ```
    
    - 인수가 하나밖에 없다면 인수를 감싸는 괄호를 생략할 수 있다.
    
    ```jsx
    let double = n => n * 2;
    // let double = function(n) {return n * 2 } 와 거의 동일
    alert(double(3)); // 6
    ```
    
    - 인수가 하나도 없을 땐 괄호를 비워놓는다. 괄호 생략 x
    
    ```jsx
    let sayHi = () => alert("안녕하세요!");
    
    sayHi();
    ```
    
    화살표함수는 함수 표현식과 같은 방법으로 사용할 수 있다. 아래 예시와 같이 함수를 동적으로 만들 수 있다.
    
    ```jsx
    let age = prompt("나이를 알려주세요.", 18);
    
    let welcome = (age < 18) ?
      () => alert('안녕') :
      () => alert("안녕하세요!");
    
    welcome();
    ```
    
    본문이 여러줄로 구성되었다면 중괄호를 사용해야 하고 반드시 `return` 지시자를 사용해 반환 값을 명기해 주어야 한다.
    
    - 문제
    
    ```jsx
    // 함수 표현식
    function ask(question, yes, no) {
        if (confirm(question)) yes()
        else no();
      }
      
      ask(
        "동의하십니까?",
        function() { alert("동의하셨습니다."); },
        function() { alert("취소 버튼을 누르셨습니다."); }
      );
    ```
    
    ```jsx
    // 화살표 함수
    ask(
      "동의하십니까?",
      () => { alert("동의하셨습니다."); },
      () => { alert("취소 버튼을 누르셨습니다."); }
    );
    ```
    
- 나머지 매개변수와 스프레드 문법
    
    임의의 수의 인수를 받는 방법과 함수의 매개변수에 배열을 전달하는 방법에 대해서 알아보자.
    
    - 나머지 매개변수 `...`
        
        함수 정의 방법과 상관없이 함수에 넘겨주는 인수의 개수엔 제약이 없다.
        
        ```jsx
        function sum(a, b) {
        	return a + b;
        }
        alert(sum(1,2,3,4,5));
        ```
        
        → 에러가 발생하지 않고 처음 두 개의 인수만을 사용해 계산된다.
        
        `...` : 남아있는 매개변수들을 한데 모아 배열에 집어넣어라
        
        ```jsx
        function sumAll(...args) { // args는 배열의 이름입니다.
          let sum = 0;
        
          for (let arg of args) sum += arg;
        
          return sum;
        }
        
        alert( sumAll(1) ); // 1
        alert( sumAll(1, 2) ); // 3
        alert( sumAll(1, 2, 3) ); // 6
        ```
        
        아래 예시에선 처음 두 인수는 변수에, 나머지 인수들은 `titles`라는 배열에 할당된다.
        
        ```jsx
        function showName(firstName, lastName, ...titles) {
          alert( firstName + ' ' + lastName ); // Bora Lee
        
          // 나머지 인수들은 배열 titles의 요소가 됩니다.
          // titles = ["Software Engineer", "Researcher"]
          alert( titles[0] ); // Software Engineer
          alert( titles[1] ); // Researcher
          alert( titles.length ); // 2
        }
        
        showName("Bora", "Lee", "Software Engineer", "Researcher");
        ```
        
        <aside>
        💡 나머지 매개변수는 항상 마지막에 있어야 한다.
        
        </aside>
        
    - 스프레드 문법(spread syntax, 전개 문법)
        
        ```jsx
        let arr = [3, 5, 1];
        
        alert( Math.max(arr) ); // NaN
        // 배열을 있는 그대로 넘기면 원하는 대로 동작하지 않는다.
        ```
        
        ```jsx
        let arr = [3, 5, 1];
        
        alert( Math.max(...arr) ); // 5
        ```
        
        아래와 같이 이터러블 객체 여러 개를 전달하는 것도 가능
        
        ```jsx
        let arr1 = [1, -2, 3, 4];
        let arr2 = [8, 3, -8, 1];
        
        alert( Math.max(...arr1, ...arr2) ); // 8
        ```
        
        - Array.from은 이터러블 객체인 문자열을 배열로 바꿔주기 때문에 동일한 작업을 할 수 있다.
        
        ```jsx
        let str = "Hello";
        
        // Array.from은 이터러블을 배열로 바꿔줍니다.
        alert( Array.from(str) ); // H,e,l,l,o
        ```
        
        프로토타입 : 객체 만들 때 가져오는 값 중 하나
        
        프로토타입 > symbol.iterator 
        
- 참조에 의한 객체 복사
    
    ```jsx
    let message = "Hello!";
    let phrase = message;
    ```
    
    **변수엔 객체가 그대로 저장되는 것이 아니라, 객체가 저장되어있는 '메모리 주소’인 객체에 대한 '참조 값’이 저장된다.**
    
    복사된 참조를 이용한 모든 작업(프로퍼티 추가, 삭제 등)은 동일한 객체를 대상으로 이뤄진다. 
    
    객체의 ‘진짜 복사본’을 만들려면 ‘얕은 복사(shallow copy)’를 가능하게 해주는 `Object.assign` 이나 ‘깊은 복사’를 가능하게 해주는 _.cloneDeep(obj)를 사용하면 된다. 이때 얕은 복사본은 중첩 객체를 처리하지 못한다.
    
- 메서드와 this
    - 메서드
        - 객체 프로퍼티에 할당된 함수
    - 메서드 단축 구문
        
        ```jsx
        // 아래 두 객체는 동일하게 동작합니다.
        
        user = {
          sayHi: function() {
            alert("Hello");
          }
        };
        
        // 단축 구문을 사용하니 더 깔끔해 보이네요.
        user = {
          sayHi() { // "sayHi: function()"과 동일합니다.
            alert("Hello");
          }
        };
        ```
        
    - 메서드와 this
        
        ```jsx
        let user = {
          name: "John",
          age: 30,
        
          sayHi() {
            // 'this'는 '현재 객체'를 나타냅니다.
            alert(this.name);
          }
        
        };
        
        user.sayHi(); // John
        ```
        
        user.sayHi()가 실행되는 동안에 this는 user를 나타낸다.
        
        ```jsx
        let user = {
          name: "John",
          age: 30,
        
          sayHi() {
            alert(user.name); // 'this' 대신 'user'를 이용함
          }
        
        };
        ```
        
        this를 사용하지 않고 외부 변수를 참조해 객체에 접근하는 것도 가능하다.
        
    - 자유로운 this
        
        동일한 값이라도 다른 객체에서 호출했다면 ‘this’가 참조하는 값이 달라진다.
        
        this값은 런타임에 결정된다.
        
        - 함수를 선언할 때 `this`를 사용할 수 있습니다. 다만, 함수가 호출되기 전까지 `this`엔 값이 할당되지 않습니다.
        - 함수를 복사해 객체 간 전달할 수 있습니다.
        - 함수를 객체 프로퍼티에 저장해 `object.method()`같이 ‘메서드’ 형태로 호출하면 `this`는 `object`를 참조합니다.
        
- 생성자 함수
    - 생성자 함수(짧게 줄여서 생성자)는 일반 함수이다. 다만, 일반 함수와 구분하기 위해 함수 이름 첫 글자를 대문자로 쓴다.
    - 생성자 함수는 반드시 `new`연산자와 함께 호출해야 합니다. `new`와 함께 호출하면 내부에서 `this`가 암시적으로 만들어지고, 마지막엔 `this`가 반환됩니다.
    - 유사한 객체를 여러 개 만들 때 유용하다.
- 배열
    - fruits.shift(); → 배열의 맨 앞의 요소를 빼준다.
    - 배열을 deque처럼 사용할 수 있다
        - `push(...items)` – `items`를 배열 끝에 더해줍니다.
        - `pop()` – 배열 끝 요소를 제거하고, 제거한 요소를 반환합니다.
        - `shift()` – 배열 처음 요소를 제거하고, 제거한 요소를 반환합니다.
        - `unshift(...items)` – `items`를 배열 처음에 더해줍니다.
    - 모든 요소를 대상으로 반복 작업을 할 수 있다
        - `for (let i=0; i<arr.length; i++)` – 가장 빠른 방법이고 오래된 브라우저와도 호환됩니다.
        - `for (let item of arr)` – 배열 요소에만 사용되는 모던한 문법입니다.
        - `for (let i in arr)` – 배열엔 절대 사용하지 마세요.
- 배열과 메서드
    - 요소를 더하거나 지우기
        - `push(...items)` – 맨 끝에 요소 추가하기
        - `pop()` – 맨 끝 요소 추출하기
        - `shift()` – 첫 요소 추출하기
        - `unshift(...items)` – 맨 앞에 요소 추가하기
        - `splice(pos, deleteCount, ...items)` – `pos`부터 `deleteCount`개의 요소를 지우고, `items` 추가하기
        - `slice(start, end)` – `start`부터 `end` 바로 앞까지의 요소를 복사해 새로운 배열을 만듦
        - `concat(...items)` – 배열의 모든 요소를 복사하고 `items`를 추가해 새로운 배열을 만든 후 이를 반환함. `items`가 배열이면 이 배열의 인수를 기존 배열에 더해줌
    - 원하는 요소 찾기
        - `indexOf/lastIndexOf(item, pos)` – `pos`부터 원하는 `item`을 찾음. 찾게 되면 해당 요소의 인덱스를, 아니면 `1`을 반환함
        - `includes(value)` – 배열에 `value`가 있으면 `true`를, 그렇지 않으면 `false`를 반환함
        - `find/filter(func)` – `func`의 반환 값을 `true`로 만드는 첫 번째/전체 요소를 반환함
        - `findIndex`는 `find`와 유사함. 다만 요소 대신 인덱스를 반환함
    - 배열 전체 순회하기
        - `forEach(func)` – 모든 요소에 `func`을 호출함. 결과는 반환되지 않음
    - 배열 변형하기
        - `map(func)` – 모든 요소에 `func`을 호출하고, 반환된 결과를 가지고 새로운 배열을 만듦
        - `sort(func)` – 배열을 정렬하고 정렬된 배열을 반환함
        - `reverse()` – 배열을 뒤집어 반환함
        - `split/join` – 문자열을 배열로, 배열을 문자열로 변환함
        - `reduce(func, initial)` – 요소를 차례로 돌면서 `func`을 호출함. 반환값은 다음 함수 호출에 전달함. 최종적으로 하나의 값이 도출됨
        
    
    <aside>
    💡 `sort`, `reverse`, `splice`는 기존 배열을 변형시킨다
    
    </aside>
    
- Object.keys, values, entries
    - [Object.keys(obj)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/keys) – 객체의 키만 담은 배열을 반환합니다.
    - [Object.values(obj)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/values) – 객체의 값만 담은 배열을 반환합니다.
    - [Object.entries(obj)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/entries) – `[키, 값]` 쌍을 담은 배열을 반환합니다
    
    ```jsx
    let user = {
      name: "John",
      age: 30
    };
    ```
    
    - `Object.keys(user) = ["name", "age"]`
    - `Object.values(user) = ["John", 30]`
    - `Object.entries(user) = [ ["name","John"], ["age",30] ]`
- 구조 분해 할당
 - 구조 분해 할당을 사용하면 객체나 배열을 변수로 연결할 수 있다.
- 객체 분해하기
    
    ```jsx
    let {prop : varName = default, ...rest} = object
    ```
    

object의 프로퍼티 `prop`의 값은 변수 `varName`에 할당되는데, object에 prop이 없으면 `default`가 `varName`에 할당된다.

연결할 변수가 없는 나머지 프로퍼티들은 객체 `rest`에 복사된다.

- 배열 분해하기
    
    ```jsx
    let [item1 = default, item2, ...rest] = array
    ```
    
    - array의 첫 번째 요소는 `item1`에, 두 번째 요소는 변수 `item2`에 할당되고, 이어지는 나머지 요소들은 배열 `rest` 저장된다.
    - 할당 연산자 좌측의 패턴과 우측의 구조가 같으면 중첩 배열이나 객체가 있는 복잡한 구조에서도 원하는 데이터를 뽑아낼 수 있다.
