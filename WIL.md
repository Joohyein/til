한 주 동안 자바스크립트에 대해서 이론공부를 한 것 중에 중요하다고 생각되는 것과 헷갈리는 것들을 다시 모아서 정리해보았다. 

## 함수와 객체

- 매개변수 기본값을 설정할 수 있는 방법
    
    함수 선언 후에 매개변수 기본값을 설정하는 것이 적절한 경우도 있다. 이런 경우에는 함수를 호출할 때 매개변수를 undefined와 비교하여 매개변수가 전달되었는지 확인한다.
    
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
    
    - if문 대신 논리연산자 `||` 사용
    
    ```jsx
    function showMessage(text) {
      text = text || '빈 문자열';
      ...
    }
    ```
    
    - nullish 병합 연산자 `??` 를 사용하면 `0` 처럼 falsy로 평가되는 값들을 일반 값처럼 처리할 수 있다.
    
    ```jsx
    // 매개변수 'count'가 `undefined` 또는 `null`이면 'unknown'을 출력해주는 함수
    function showCount(count) {
      alert(count ?? "unknown");
    }
    
    showCount(0); // 0
    showCount(null); // unknown
    showCount(); // unknown
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
    
    EX) 매개변수가 3개 있는 함수
    
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
    
    함수 `ask`의 인수, `showOk`와 `showCancel`은 콜백함수 또는 콜백이라고 불린다.
    
    - 함수 표현식 vs 함수 선언문
        - 함수 선언문 : 함수는 주요 코드 흐름 중간에 독자적인 구문 형태로 존재한다.
        - 함수 표현식 : 함수는 표현식이나 구문 구성(syntax construct)내부에 생성된다.
        
        자바스크립트는 스크립트를 실행하기 전, 준비단계에서 전역에 선언된 함수 선언문을 찾고, 해당 함수를 생성한다. 스크립트가 진짜 실행되기 전 “초기화 단계”에서 함수 선언 방식으로 정의한 함수가 생성되는 것이다.
        
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
    
- 메서드
    
    객체 프로퍼티에 할당된 함수
    
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
    
    ```jsx
    let user = {
      name: "John",
      age: 30,
    
      sayHi() {
        alert(user.name); // 'this' 대신 'user'를 이용함
      }
    
    };
    ```
    
    → user.sayHi()가 실행되는 동안에 this는 user를 나타낸다.
    
- 배열
    - forEach(func)와 map(func)의 차이
        - forEach(func) : 모든 요소에 func을 호출하고 결과는 반환하지 않는다.
        - map(func) : 모든 요소에 func을 호출하고 반환된 결과를 가지고 새로운 배열을 만든다.
        

- Object.keys, values, entries
    - [Object.keys(obj)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/keys) – 객체의 키만 담은 배열을 반환
    - [Object.values(obj)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/values) – 객체의 값만 담은 배열을 반환
    - [Object.entries(obj)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/entries) – `[키, 값]` 쌍을 담은 배열을 반환
    
- 메모리 구조
    
    프로그램이 실행되기 위해서는 먼저 프로그램이 메모리에 로드되어야 한다. 또한, 프로그램에서 사용되는 변수들을 저장할 메모리도 필요하다. 따라서 컴퓨터 운영체제는 프로그램의 실행을 위해 다양한 메모리 공간을 제공하고 있다. 
    
    - 프로그램이 운영체제로부터 할당받는 대표적인 메모리 공간은 4가지다.
        1. **코드(code)영역**
            
            실행할 프로그램의 코드가 저장되는 영역으로 텍스트영역이라고도 부른다. CPU는 코드 영역에 저장된 명령어를 하나씩 가져가서 처리하게 된다.
            
        2. **데이터(data)영역**
            
            프로그램의 전역변수와 정적변수가 저장되는 영역이다. 데이터영역은 프로그램의 시작과 함께 할당되며, 프로그램이 종료되면 소멸한다.
            
        3. **스택(stack)영역**
            
            함수의 호출과 관계되는 지역 변수와 매개변수가 저장되는 영역이다. 스택 영역은 함수의 호출과 함께 할당되며, 함수의 호출이 완료되면 소멸한다. 스택 영역에 저장되는 함수의 호출 정보를 스택 프레임(stack frame)이라고 한다. 스택은 후입선출 방식에 따라 동작한다. 스택 영역은 메모리의 높은 주소에서 낮은 주소의 방향으로 할당된다.
            
        4. **힙(heap)영역**
            
            메모리의 힙(heap) 영역은 사용자가 직접 관리할 수 있는 ‘그리고 해야만 하는’ 메모리 영역이다. 힙 영역은 사용자에 의해 메모리 공간이 동적으로 할당되고 해제된다. 메모리의 낮은 주소에서 높은 주소의 방향으로 할당된다.
            
    
- 실행 컨텍스트
    
    함수를 실행하는 데에 필요한 배경이 되는 조건 / 환경
    
    어떤 코드를 봤을 때 그 코드가 이 자리에서 어떤 역할을 수행하는 지를이해하기 위해서는 그 코드에 영향을 주는 주변 코드나 변수들을 파악해야한다. 그렇게 영향을 주는 환경을 일컬어서 context라고 한다.
    
    - Variable Environment
    - Lexical Environment : 어휘적 / 사전적 환경
    - environmentRecord : 현재문맥의 식별자(hoisting)
    - outerEnvironmentReference : 외부 식별자(scope chain)
    - this
    
    - 스코프(scope)
        
        스코프는 참조 대상 식별자(identifier, 변수, 함수의 이름과 같이 어떤 대상을 다른 대상과 구분하여 식별할 수 있는 유일한 이름)를 찾아내기 위한 규칙이다. 자바스크립트는 이 규칙대로 식별자를 찾는다.
        
        전역에 선언된 변수는 어디에든 참조할 수 있다. 하지만 함수 내에서 선언된 변수는 함수 외부에서는 참조할 수 없다. 이러한 규칙을 스코프라고 한다.
        
    - 실행 컨텍스트(Execution Context)
        
        자바스크립트 코드가 실행되고 연산되는 범위를 나타내는 추상적인 개념우리가 코드를 작성하고 실행한다면 실행 컨텍스트 내부에서 실행되고 있는 것이다. 코드들이 실행되기 위한 환경이자 하나의 박스이자 컨테이너라 볼 수 있다.
        
    - 코드의 실행 순서를 관리하는 **콜스택**
        
        코드의 실행에 필요한 환경 정보를 “컨텍스트”라고 이름 지어서 객체로 만들어 두고 실행 순서에 따라 콜스택에 쌓았다가, 가장 이에 쌓여있는 컨텍스트와 관련 있는 코드를 실행하는 순서로 이루어진다.
        
    - 실행 컨텍스트는 어떻게 구성되어 있는가?
        
        실행 컨텍스트는 생성단계와 실행단계로 이루어져 있다. 그리고 두 가지로 이루어져 있는데, 해당 스코프 안에 어떤 변수 등이 있는지 적혀있는 객체와 지금 스코프(함수) 바로 바깥이 어디인지 알려주는 참조로 이해하면 된다.
