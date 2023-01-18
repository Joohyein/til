- Hello world
    - ‘script’태그
        - <script></script> 자바스크립트 프로그램을 html문서 대부분의 위치에 삽입할 수 있다.
    - 외부 스크립트
        - 자바스크립트의 코드의 양이 많을 때, 파일로 소분하여 저장
        - scr속성을 사용해 html에 삽입 ex)src=”path/to/script.js”
        - 스크립트를 별도의 파일에 작성하면 브라우저가 스크립트를 다운받아 캐시(cache)에 저장하기 때문에, 성능상의 이점이 있다.
        - 여러 페이지에서 동일한 스크립트를 사용하는 경우, 브라우저는 페이지가 바뀔 때마다 스크립트를 새로 다운받지 않고 캐시로부터 스크립트를 가져와 사용한다. 스크립트 파일을 한 번만 다운받으면 됨.
        - 이를 통해 트래픽이 절약되고 웹 페이지의 실제 속도가 빨라진다.
        - src속성이 있으면 태그 내부의 코드는 무시되므로 <script src=”..”>로 외부 파일을 연결할지 <script>태그 내에 코드를 작성할지를 선택해야 한다.
- 코드 구조
    - 줄바꿈 : 세미콜론 자동 삽입(automatic semicolon insertion)
        - 대괄호 앞에는 세미콜론이 있다고 가정하지 않는다.
    - 주석
        - // : 한줄짜리 주석
        - /**/ : 여러 줄의 주석
- alert, prompt, confirm을 이용한 상호작용
    
    브라우저 환경에서 사용되는 최소한의 사용자 인터페이스 기능 alert, prompt, confirm
    
    - alert
        - 메세지가 있는 작은 창은 모달 창(modal window)이라고 부른다. ‘모달’이란 단어에는 페이지의 나머지 부분과 상호 작용이 불가능하다는 의미가 내포되어 있다. 확인버튼을 누르기 전까지 모달 창 바깥에 있는 버튼을 누르는 등의 다른 행동을 할 수 없다.
    - prompt
        - 브라우저에서 제공하는 prompt함수는 두 개의 인수를 받는다.
        
        ```python
        result = prompt(title, [default]);
        ```
        
        함수가 실행되면 텍스트 메세지와 입력 필드(input field), 확인(OK) 및 취소(Cancel) 버튼이 있는 모달 창을 띄워준다.
        
        - title : 사용자에게 보여줄 문자열
        - default : 입력 필드의 초깃값(선택값)
        
        ```jsx
        let age = prompt('나이를 입력해주세요.', 100);
        alert(`당신의 나이는 ${age}살 입니다.`);
        // 당신의 나이는 100살입니다.
        ```
        
        ![ ](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4538001a-da60-4b4f-b387-eac88d347b2e/%E1%84%8B%E1%85%B5%E1%84%86%E1%85%B5%E1%84%8C%E1%85%B5_2023._1._18._%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_11.30.jpeg)
        
    
    - 컨펌 대화상자
        
        ```jsx
        //문법:
        result = confirm(question);
        ```
        
        confirm함수는 매개변수로 받은 question(질문)과 확인 및 취소 버튼이 있는 모달 창을 보여준다. 
        
        사용자가 확인 버튼을 누르면 true, 그 외의 경우는 false를 반환
        
        ```jsx
        //예시:
        let isBoss = confirm("당신이 주인인가요?");
        alert(isBoss);
        ```
        
        ![ ](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4bbe081f-3359-420c-9ca5-ffb9a7eb70af/%E1%84%8B%E1%85%B5%E1%84%86%E1%85%B5%E1%84%8C%E1%85%B5_2023._1._18._%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_1.37.jpeg)
        
        ![ ](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8b029f37-93c4-4833-a1a3-a4d0d83c4e06/%E1%84%8B%E1%85%B5%E1%84%86%E1%85%B5%E1%84%8C%E1%85%B5_2023._1._18._%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_1.37_(1).jpeg)
        
- 주석
    
    주석(comment)은 어떻게 코드가 동작하는지, 왜 코드가 동작하는지를 설명
    
    좋은 코드엔 ‘설명이 담긴(explanatory)’주석이 많아선 안된다. 주석 없이 코드 자체만으로도 코드가 무슨 일을 하는지 쉽게 이해할 수 있어야 한다.
    
    - 리팩토링 팁 : 함수 분리하기
    
    ```jsx
    function showPrimes(n) {
    	nextPrime:
    	for(let i = 0; i < n; i++){
    		for(let j = 0; j<i; j++) {
    			if(i % j == 0) continue nextPrime;
    		}
    		alert(i);
    	}
    }
    ```
    
    ```jsx
    //코드 일부를 함수 isPrime으로 옮기기
    function showPrimes(n) {
    	nextPrime:
    	for(let i = 0; i < n; i++){
    		if(!isPrime(i)) continue;
    		alert(i);
    	}
    }
    function isPrime(n) {
    	for(let j = 0; j<i; j++) {
    			if(i % j == 0) continue nextPrime;
    		}
    	return true;
    }
    ```
    
    함수 이름 자체가 주석 역할을 하므로 코드를 쉽게 이해할 수 있다. 이런 코드를 자기 설명적인(self-descriptive) 코드라 부른다.
    
    - 리팩토링 팁 : 함수 만들기
    
     - ‘아래로 죽 늘어져 있는’경우
    
    ```jsx
    // 위스키를 더해줌
    for(let i = 0; i < 10; i++) {
      let drop = getWhiskey();
      smell(drop);
      add(drop, glass);
    }
    
    // 주스를 더해줌
    for(let t = 0; t < 3; t++) {
      let tomato = getTomato();
      examine(tomato);
      let juice = press(tomato);
      add(juice, glass);
    }
    
    // ...
    ```
    
     - 이럴 땐 새로운 함수를 만들고, 코드 일부를 새로 만든 함수에 옮기는 게 좋다.
    
    ```jsx
    addWhiskey(glass);
    addJuice(glass);
    
    function addWhiskey(container) {
      for(let i = 0; i < 10; i++) {
        let drop = getWhiskey();
        //...
      }
    }
    
    function addJuice(container) {
      for(let t = 0; t < 3; t++) {
        let tomato = getTomato();
        //...
      }
    }
    ```
    
    함수는 주석이 없어도 그 존재 자체가 무슨 역할을 하는지 설명할 수 있어야 한다.코드를 분리해 작성하면 더 나은 코드 구조가 된다. 
    
    - 좋은 주석
    
     - 아키텍처를 설명하는 주석
    
    고차원 수준 컴포넌트 개요, 컴포넌트 간 상호작용에 대한 설명, 상황에 따른 제어 흐름 등은 주석에 넣는 게 좋다. 이런 주석은 조감도 역할을 해준다. 
    
    고차원 수준의 아키텍처 다이어그램을 그리는 데 쓰이는 언어 : UML
    
     - 함수 용례와 매개변수 정보를 담고 있는 주석
    
    JSDoc이라는 특별한 문법을 사용하면 함수에 관한 문서를 쉽게 작성할 수 있다. 여기에는 함수 용례, 매개변수, 반환 값 정보가 들어간다.
    
    ```jsx
    /**
     * x를 n번 곱한 수를 반환함
     *
     * @param {number} x 거듭제곱할 숫자
     * @param {number} n 곱할 횟수, 반드시 자연수여야 함
     * @return {number} x의 n 거듭제곱을 반환함
     */
    function pow(x, n) {
      ...
    }
    ```
    
     - 왜 이런 방법으로 문제를 해결했는지를 설명하는 주석
    
     - 미묘한 기능이 있고, 이 기능이 어디에 쓰이는지를 설명하는 주석
    
- 변수와 상수
    - 변수(variable) : 데이터를 저장할 때 쓰이는 ‘이름이 붙은 저장소’이다. 온라인 애플리케이션을 구축하는 경우 상품이나 방문객 등의 정보를 저장할 때 변수를 사용한다.
        - 아래 세 개는 모두 같다.
        
        ```jsx
        let user = 'John';
        let age = 25;
        let message = 'Hello';
        ```
        
        ```jsx
        let user = 'John',
        		age = 25,
        		message = 'Hello';
        ```
        
        ```jsx
        let user = 'John'
        	, age = 25
        	, message = 'Hello';
        ```
        
    - 변수 명명 규칙
        1. 변수명에는 오직 문자와 숫자, 그리고 기호 $와 _만 들어갈 수 있다.
        2. 첫 글자는 숫자가 될 수 없다.
        - 카멜 표기법(camelCase) : 단어를 차례대로 나열하면서 첫 단어를 제외한 각 단어의 첫 글자를 대문자로 작성한다. ex) myVeryLongName
        
         - 예약어(reserved name)목록에 있는 단어는 변수명으로 사용할 수 없다. 예약어 예시 : let, class, return, function
        
    
    - 상수
        
        변화하지 않는 변수를 선언할 땐, let 대신 const를 사용한다.
        
        - 대문자 상수
            
            기억하기 힘든 값을 변수에 할당해 별칭으로 사용하는 관습이다. 이런 상수는 대문자와 밑줄로 구성된 이름으로 명명한다. 
            
            ```jsx
            // 예시 : 웹에서 사용하는 색상 표기법인 16진수 컬러 코드
            const COLOR_RED = "#F00";
            const COLOR_GREEN = "#0F0";
            const COLOR_BLUE = "#00F";
            const COLOR_ORANGE = "#FF7F00";
            
            // 색상을 고르고 싶을 때 별칭을 사용할 수 있게 되었습니다.
            let color = COLOR_ORANGE;
            ```
            
            대문자 상수는 ‘하드 코딩한’값의 별칭을 만들 때 사용하면 된다.
            
    - 바람직한 변수명
        
        **변수명은 간결하고, 명확해야 한다. 변수가 담고있는 것이 무엇인지 잘 설명할 수 있어야 한다.** 
        
        - userName이나 shoppingCart처럼 사람이 읽을 수 있는 이름 사용
        - 무엇을 하고 잇는지 명확히 알고 있지 않을 경우 외에는 줄임말이나 a, b, c와 같은 짧은 이름은 피한다.
        - 최대한 서술적이고 간결하게 명명한다. data와 value는 나쁜 이름의 예시이다. 이런 이름은 아무것도 설명해주지 않는다. 코드 문맥상 변수가 가리키는 데이터나 값이 아주 명확할 대에만 이런 이름을 사용한다.
        - 자신만의 규칙이나 소속된 팀의 규칙을 따른다. 만약 사이트 방문객을 ‘user’라고 부르기로 했다면, 이와 관련된 변수를 currentVisitor 나 newManInTown이 아닌 currentUser나 newUser라는 이름으로 지어야 한다.
- 자료형
    
    자바스크립트에서 값은 항상 문자열이나 숫자형 같은 특정한 자료형에 속한다. 
    
    자바스크립트에는 여덟 가지 기본 자료형이 있다. 
    
    자바스크립트의 변수는 자료형에 관계없이 모든 데이터일 수 있다. 
    
    ```jsx
    //no error
    let message = "hello";
    message = 123;
    ```
    
    위와 같이 자료의 타입은 있지만 변수에 저장되는 값의 타입은 어제든지 바꿀 수 있는 언어를 ‘**동적 타입(dynamically typed)’ 언어**라고 부른다.
    
    - 숫자형
        
        ```jsx
        let n = 123;
        n = 12.345;
        ```
        
        숫자형은 정수 및 부동소수점 숫자(floating point number)를 나타낸다.
        
        숫자형에는 일반적인 숫자 외에 Infinity, -Infinity, NaN같은 ‘특수 숫자 값(special numeric value)’이 포함된다. 
        
        - Infinity는 어떤 숫자보다 더 큰 특수 값, 무한대를 나타낸다.
            
            ```jsx
            alert( 1 / 0 ); 
            alert( Infinity );
            ```
            
        - NaN은 계산 중에 에러가 발생했다는 것을 나타내주는 값이다. 부정확하거나 정의되지 않은 수학 연산을 사용하면 계산 중에 에러가 발생하는데, 이때 NaN이 반환된다.
            
            ```jsx
            alert( "문자" / 2 );
            ```
            
    - BigInt
        
        내부 표현 방식 때문에 자바스크립트에선 (2^53)(9007100254740991)보다 큰 값 혹은 -(2^53-1) 보다 작은 정수는 ‘숫자형’을 사용해 나타낼 수 없다. 
        
        BigInt형은 표준으로 채택된 지 얼마 안 된 자료형으로, 길이에 상관없이 정수를 나타낼 수 있다.
        
        BigInt형 값은 정수 리터럴 끝에 n을 붙이면 만들 수 있다.
        
        ```jsx
        const bigInt = 1234567890123456789012345678901234567890n;
        ```
        
    - 문자형
        1. 큰따옴표 : “hello”
        2. 작은따옴표 : ‘hello’
        3. 역 따옴표(백틱, backtick) : ` hello `
    
    - 불린형
        
        true, false 두 가지 밖에 없는 자료형이다. 긍정이나 부정을 나타내는 값을 저장할 때 사용한다. 
        
    - ‘null’ 값
        
        null값은 오로지 null값만 포함하는 별도의 자료형을 만든다.
        
        자바스크립트의 null은 자바스크립트 이외 언어의 null과 성격이 다르다. 다른 언어에선 null을 ‘존재하지 않는 객체에 대한 참조’나 널 포인터(null pointer)’를 나타낼 때 사용한다.
        
        하지만 자바스크립트에선 null을 ‘**존재하지 않는(nothing)**’값, ‘**비어 있는(empty)’**값, ‘**알 수 없는(unknown)**’값을 나타내는 데 사용한다.
        
        let age = null; 은 나이를 알 수 없거나 그 값이 비어있음을 보여준다.
        
    
    - ‘undefiend’ 값
        
        null 값처럼 자신만의 자료형을 형성한다. ‘값이 할당되지 않은 상태’를 나타낼 때 사용한다. 
        
        ```jsx
        let age;
        alert(age); // 'undefined'
        ```
        
    - 객체와 심볼
        
        객체(object)형은 특수한 자료형이다.
        
        객체형을 제외한 다른 자료형은 문자열이든 숫자든 한 가지만 표현할 수 있기 때문에 원시(primitive)자료형이라 부른다. 반면 객체는 데이터 컬렉션이나 복잡한 개체(entity)를 표현할 수 있다.
        
        심볼(symbol)형은 객체의 고유한 식별자(unique identifier)를 만들 때 사용된다. 
        
    
    - typeof 연산자
        
        인수의 자료형을 반환한다. 
        
        두 가지 형태의 문법을 지원한다.
        
        1. 연산자 : typeof x
        2. 함수 : typeof(x)
        
        괄호가 있든 없든 결과는 동일하다.
        
        ```jsx
        typeof undefined // "undefined"
        
        typeof 0 // "number"
        
        typeof 10n // "bigint"
        
        typeof true // "boolean"
        
        typeof "foo" // "string"
        
        typeof Symbol("id") // "symbol"
        
        typeof Math // "object"  (1)
        
        typeof null // "object"  (2)
        
        typeof alert // "function"  (3)
        ```
        
        (1) : Math는 수학 연산을 제공하는 내장 객체이므로 “object”가 출력된다. 
        
        (2) : null은 별도의 고유한 자료형을 가지는 특수 값으로 객체가 아니지만, 하위 호환성을 유지하기 위해 이런 오류를 수정하지 않고 남겨둔 상황이다. 언어 자체의 오류이므로 null은 객체가 아니다.
        
        (3) : 함수는 객체형에 속한다. 이런 동작 방식이 형식적으론 잘못되긴 했지만, 아주 오래전에 만들어진 규칙이었기 때문에 하위 호환성 유지를 위해 남겨진 상태이다.
        
- 형변환
    
    함수와 연산자에 전달되는 값은 대부분 적절한 자료형으로 자동 변환된다. 이런 과정을 “형 변환(type conversion)”이라고 한다. 
    
    - 문자형으로 변환
        
        `alert`메서드는 매개변수로 문자형을 받기 때문에, `alert(value)`
        에서 value는 문자형이어야 한다. 만약, 다른 형의 값을 전달받으면 이 값은 문자형으로 자동 변환된다. 
        
    - 숫자형으로 변환
        
        수학과 관련된 함수와 표현식에서 자동으로 일어난다. 숫자형이 아닌 값에 나누기를 적용한 경우.
        
        ```jsx
        let str = "123";
        let num = Number(str);
        ```
        
        - 숫자형으로 변환 시 적용되는 규칙
            
            
            | undefined | NaN |
            | --- | --- |
            | null | 0 |
            | true and false | 1 and 0 |
            | string | 문자열의 처음과 끝 공백이 제거된다. 공백 제거 후 남아있는 문자열이 없다면 0, 있다면 문자열에서 숫자를 읽는다. 변환에 실패하면 NaN이 된다. |
    - 불린형으로 변환
        - 숫자 0, 빈 문자열, null, undefined, NaN과 같이 직관적으로도 “비어있다고”느껴지는 값들은 false 가 된다.
        - 그 외의 값들은 true로 변환된다.
        
        ```jsx
        alert(Boolean("0")); // true
        alert(Boolean(" ")); // true
        ```
        
- 기본 연산자와 수학
    - 용어 : ‘단항’, ‘이항’, ‘피연산자’
        - 피연산자(operand)는 연산자가 연산을 수행하는 대상이다. ‘인수(argument)’라는 용어로 불리기도 한다.
        - 피연산자를 하나만 받는 연산자는 단항(unary)연산자라고 부른다. 피연산자의 부호를 뒤집는 단항 마이너스 연산자 -는 단항 연산자의 대표적인 예다.
        - 두 개의 피연산자를 받는 연산자는 이항(binary) 연산자라고 부른다.
    - 수학
        - 거듭제곱 연산자 `**`
    
    - 이항 연산자 ‘+’와 문자열 연결
        
        ```jsx
        let s = "my" + "string";
        alert(s); //mystring
        alert('1'+2); // "12" -> 숫자를 문자열로 변환
        ```
        
    - 단항 덧셈 연산자
        
        Number(…)와 동일한 일을 한다.
        
        ```jsx
        let apples = "2";
        let oranges = "3";
        alert(apples + oranges); // 23
        alert(+apples + +oranges); // 5
        ```
        
        ‘단항 덧셈 연산자’는 우선순위가 ‘(이항) 덧셈 연산자’의 우선순위보다 높다.
        
    - 증감 연산자
        - 후위형(postfix form)
        - 전위형(prefix form)
        
         두 형의 차이는 `++/--` 의 **반환 값을 사용할 때 드러난다**. 전위형은 증가.감소 후의 새로운 값을 반환하는 반면, 후위형은 증가.감소 전의 기존 값을 반환한다.
        
        ```jsx
        let cnt = 1;
        let a = ++cnt;
        alert(a); //2
        ```
        
        ```jsx
        let cnt = 1;
        let a = cnt++;
        alert(a); //1
        //값을 증가시키지만, 증가 전의 기존값을 사용하려면 후위형 사용
        ```
        
    
    - 비트 연산자
        - 비트 AND ( `&` )
        - 비트 OR ( `|` )
        - 비트 XOR ( `^` )
        - 비트 NOT ( `~` )
        - 왼쪽 시프트(LEFT SHIFT) ( `<<` )
        - 오른쪽 시프트(RIGHT SHIFT) ( `>>` )
        - 부호 없는 오른쪽 시프트(ZERO-FILL RIGHT SHIFT) ( `>>>` )
        
    - 쉼표 연산자
        
        ```jsx
        let a = (1 + 2, 3 + 4);
        alert(a); // 7
        ```
        
        3 + 4만 평가되어 a에 할당된다.
        
        쉼표의 우선순위는 매우 낮다. 진짜 필요할 때만 사용하기.
        
- 비교 연산자
    - 일치 연산자
        
        ```jsx
        alert( 0 == false ); // true
        alert( '' == false ); // true
        ```
        
        ```jsx
        alert( 0 === false ); // false
        ```
        
        ```jsx
        alert( null === undefined ); // false
        alert( null == undefined ); // true
        ```
        
        - null vs 0
        
        ```jsx
        alert( null > 0 );  // (1) false
        alert( null == 0 ); // (2) false
        alert( null >= 0 ); // (3) true
        ```
        
        ==와 기타 비교 연산자 <, >, ≤, ≥의 동작 방식이 다르기 때문.
        
        ≥ 은 null을 숫자형으로 반환
        
        - 비교 불가능한 undefined
        
        ```jsx
        alert( undefined > 0 ); // false (1)
        alert( undefined < 0 ); // false (2)
        alert( undefined == 0 ); // false (3)
        ```
        
- if와 '?'를 사용한 조건 처리
    - 조건부 연산자 ’?’
        
        물음표 연산자는 우선순위가 낮다. 조건에 괄호를 표시하지 않아도 된다.
        
    - 다중 ‘?’
        
        ```jsx
        let age = prompt('나이를 입력해주세요.', 18);
        
        let message = (age < 3) ? '아기야 안녕?' :
          (age < 18) ? '안녕!' :
          (age < 100) ? '환영합니다!' :
          '나이가 아주 많으시거나, 나이가 아닌 값을 입력 하셨군요!';
        
        alert( message ); // 환영합니다!
        ```
        
- 논리 연산자
    - ! (NOT)
        
        ```jsx
        alert( !!"non-empty string" ); // true
        alert( !!null ); // false
        ```
        
        ```jsx
        alert( Boolean("non-empty string") ); // true
        alert( Boolean(null) ); // false
        ```
        
- switch문
    
    ```jsx
    switch(x) {
      case 'value1':  // if (x === 'value1')
        ...
        [break]
    
      case 'value2':  // if (x === 'value2')
        ...
        [break]
    
      default:
        ...
        [break]
    }
    ```
    
- for문
