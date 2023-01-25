# Day4 - this, 콜백 함수, 클로저

- Prerequisite
    
    ## this
    
    상황에 따라 그때 그때 달라질 뭔가를 가리키기 위해서 사용한다.
    
    프로퍼티가 메서드가 자기를 참조할 수 있게 인스턴스 생성 이후에 해당 인스턴스를 가리키기 위해서 사용한다. 자바스크립트에서 this는 실행 컨텍스트가 생성될 때 함께 결정된다. 실행 컨텍스트는 함수를 호출할 때 생성되므로, this는 함수를 호출할 때 결정된다고 할 수 있다. 그래서 어떤 방식으로 호출하냐에 따라 값이 달라진다고 한다. 
    
    - 전역 함수(Global function)
        
        전역 함수는 애플리케이션 전역에서 호출할 수 있는 함수로서 전역 객체의 메서드이다.
        
        - parseFloat()
            
            매개변수에 전달된 문자열을 부동소수점 숫자로 변환하여 반환한다. 문자열의 첫 숫자만 반환되며 전후 공백은 무시된다. 첫 문자를 숫자로 변환할 수 없다면 NaN을 반환한다.
            
            ```jsx
            parseFloat('3.14');     // 3.14
            parseFloat('10.00');    // 10
            parseFloat('34 45 66'); // 34
            parseFloat(' 60 ');     // 60
            parseFloat('40 years'); // 40
            parseFloat('He was 40') // NaN
            ```
            
        - parseInt()
            
            매개변수에 전달된 문자열을 정수형 숫자(Integer)로 해석하여 반환한다. 반환값은 언제나 10진수이다.
            
            ```jsx
            parseInt(string, radix);
            // string : 파싱 대상 문자열
            // radix : 진법을 나타내는 기수(2 ~ 36, 기본값 10)
            ```
            
            ```jsx
            parseInt(10); // 10
            parseInt(10.12); // 10
            ```
            
            ```jsx
            parseInt('10', 2);  // 2진수 10 → 10진수 2
            parseInt('10', 8);  // 8진수 10 → 10진수 8
            parseInt('10', 16); // 16진수 10 → 10진수 16
            ```
            
            두번째 매개변수에 진법을 나타내는 기수를 지정하지 않더라도 첫번째 매개변수에 전달된 문자열이 “0x” 또는 “0X”로 시작한다면 16진수로 해석하여 반환한다.
            
            ```jsx
            parseInt('0x10'); // 16진수 10 → 10진수 16
            ```
            
    
    ## 콜백함수
    
    - 자료 영상 - 콜백함수
        
        호이스팅이 된 이후부터 코드가 나타나는 순서대로 자동적으로 실행이 된다.
        
        - setTimeout 콜백함수
        
        ```jsx
        setTimeout(function() {
        	console.log(1);
        }1000);
        
        // arrow function
        setTimeout(() => console.log(1), 1000);
        ```
        
    
    ## 클로저
    
    - DOM API
        1. DOM(Document Object Model)
            
            텍스트 파일로 만들어져 있는 웹 문서를 브라우저에 렌더링 하려면 웹 문서를 브라우저가 이해할 수 있는 구조로 메모리에 올려야 한다. 브라우저의 렌더링 엔진은 웹 문서를 로드한 후, 파싱하여 웹 문서를 브라우저가 이해할 수 있는 구조로 구성하여 메모리에 적제하는데 이를 DOM이라고 한다. 즉 모든 요소와 요소의 어트리뷰트, 텍스트를 각각의 객체로 만들고 이들 객체를 부자 관계를 표현할 수 있는 트리 구조로 구성한 것이 DOM이다. 이 DOM은 자바스크립트를 통해 동적으로 변경할 수 있으며 변경된 DOM은 렌더링에 반영된다.
            
            DOM에서 모든 요소, 어트리뷰트, 텍스트는 하나의 객체이며 Document 객체의 자식이다. 요소의 중첩관계는 객체의 트리로 구조화하여 부자관계를 표현한다. DOM tree의 진입점(Entry point)는 document 객체이며 최종점은 요소의 텍스트를 나타내는 객체이다.
            

### 상황에 따라 달라지는 this

Javascript에서 this는 기본적으로 실행 컨텍스트가 생성될 때 함께 결정된다. 

- this
    
    `this` 키워드는 지금 동작하고 있는 코드를 가지고 있는 객체를 가리킨다. 
    
    - 왜 직접 `person` 객체를 쓰지 않을까?
        
        this 는 객체 멤버의 컨텍스트가 바뀌는 경우에도 언제나 정확한 값을 사용하게 해준다. ex) 두 개의 다른 `person` 객체가 각각 다른 이름으로 인스턴스로 생성된 상태에서 인사말을 출력하기 위해 객체의 name을 참조해야 하는 경우
        
- 전역 공간에서의 this
    - 전역 공간에서의 this
        
        전역 공간에서의 this는 전역 객체를 가리킨다. 브라우저에서는 window, node.js에서는 global이라는 객체이다. 개념상 전역 컨텍스트를 실행하는 주체가 전역객체이기 때문이다. 자바스크립트가 실행되는 환경, 즉 런타임에 따라서 전역객체의 정보가 달라진다.  
        
        자바스크립트의 모든 변수는 실은 특정 객체의 프로퍼티로서 동작한다. 사용자가 var 연산자를 이용해서 변수를 선언하더라도 실제 자바스크립트 엔진은 어떤 특정 객체의 프로퍼티로 인식하는 것이다. 특정 객체란 바로 실행 컨텍스트의 LexicalEnvironment이다. 실행 컨텍스트는 변수를 수집해서 L.E의 프로퍼티로 저장한다. 
        
        전역변수를 선언하면 자바스크립트 엔진은 이를 전역객체의 프로퍼티로 할당한다.
        
        var로 선언한 전역변수와 전역객체의 프로퍼티는 호이스팅 여부 및 configurable(변경 및 삭제 가능성)여부에서 차이를 보인다.
        
- 메서드로서 호출할 때 그 메서드 내부에서의 this
    - 메서드로서 호출할 때 그 메서드 내부에서의 this
        - 함수 vs 메서드
        
        함수와 메서드를 구분하는 유일한 차이는 **독립성**에 있다. 함수는 그 자체로 독립적인 기능을 수행하는 반면, 메서드는 자신을 호출한 대상 객체에 관한 동작을 수행한다. 자바스크립트는 상황별로 this 키워드에 다른 값을 부여하게 함으로써 이를 구현했다.
        
        ```jsx
        var func = function (x) {
        	console.log(this, x);
        };
        func(1); // Window { ... } 1
        
        var obj = {
        	method: func
        };
        obj.method(2); // { method; f } 2
        // 원래는 함수인데 어떤 객체와 '관련된'동작을 하게 되면 obj객체의 메서드로써 method함수를 호출
        ```
        
        원래의 익명함수는 그대로인데 이를 변수에 담아 호출한 경우와 obj 객체의 프로퍼티에 할당해서 호출한 경우에 this가 달라지는 것이다.
        
        ‘함수로서 호출’과 ‘메서드로서 호출’을 어떻게 구분할까? 함수 앞에 점(.)이 있는지 여부만으로 간단하게 구분할 수 있다. 점 표기법이든 대괄호 표기법이든, 어떤 함수를 호출할 때 그 함수 이름(프로퍼티명) 앞에 객체가 명시돼 있는 경우에는 메서드로 호출한 것이고, 그렇지 않은 모든 경우에는 함수로 호출한 것이다.
        
        ```jsx
        var a = 10;
        var obj = {
        	a: 20,
        	b: function() {
        		console.log(this.a);  // 20
        
        		function c() {
        			console.log(this.a);  // 10
        		}
        		c();
        	}
        }
        obj.b();
        ```
        
        - 메서드 내부에서의 this
        
        this에는 호출한 주체에 대한 정보가 담긴다.
        
        ```jsx
        var obj = {
        	methodA: function () {console.log(this);},
        	inner: {
        		methodB: function () {console.log(this);}
        	}
        };
        obj.methodA(); // { methodA: f, inner: {...} } (===obj)
        obj['methodA']();
        
        obj.inner.methodB(); // { methodB: f } ( === obj.inner )
        obj.inner['methodB']();
        obj['inner'].methodB();
        obj['inner']['methodB']();
        ```
        
- 함수로서 호출할 때 그 함수 내부에서의 this
    - 함수로서 호출할 때 그 함수 내부에서의 this
        - 함수 내부에서의 this
        
        어떤 함수를 함수로서 호출할 경우에는 this가 지정되지 않는다. this에는 호출한 주체에 대한 정보가 담기는데 함수로서 호출하는 것은 호출 주체(객체지향 언어에서의 객체)를 명시하지 않고 개발자가 코드에 직접 관여해서 실행한 것이기 때문에 호출 주체의 정보를 알 수 없는 것이다. 함수의 this는 전역 객체를 가리킨다. 
        
        - 메서드의 내부함수에서의 this
        
        ```jsx
        var obj1 = {  // 객체 생성, 객체 내부에는 outer라는 프로퍼티가 있으며, 여기에는 익명함수가 연결된다. 이렇게 생성한 객체를 변수 obj1에 할당한다. 
            outer: function () {   // obj1.outer함수의 실행 컨텍스트가 생성되면서 호이스팅하고, 스코프 체인 정보를 수집하고, this를 바인딩한다. obj1이 바인딩된다.
                console.log(this); // obj1 객체 정보가 출력된다. 
                var innerFunc = function () {  // innerFunc함수의 실행 컨텍스트가 생성되면서 호이스팅, 스코프 체인 수집, this바인딩 등을 수행한다. 함수로서 호출한 것이므로 this가 지정되지 않았고 자동으로 스코프 체인상의 최상위 객체인 전역객체(window)가 바인딩된다
                    console.log(this); // window 객체 정보가 출력된다. 
                }
                innerFunc();
        
                var obj2 = {  // 호이스팅된 변수 obj2 역시 outer 스코프 내에서만 접근할 수 있는 지역변수이다. 여기에는 다시 객체를 할당하는데, 그 객체에는 innerMethod라는 프로퍼티가 있으며, 여기에는 앞서 정의된 변수 innerFunc와 연결된 익명 함수가 연결된다.
                    innerMethod: innerFunc
                };
                obj2.innerMethod();
            }
        };
        obj1.outer(); // obj1.outer를 호출
        ```
        
        함수를 함수로서 호출하느냐 함수를 메서드로서 호출하느냐에 따라 같은 함수임에도 바인딩되는 this의 대상이 서로 달라진다. 
        
        this 바인딩에 관해서는 함수를 실행하는 당시의 주변 환경(메서드 내부인지, 함수 내부인지 등)은 중요하지 않고, 오직 해당 함수를 호출하는 구문 앞에 점 또는 대괄호 표기가 있는지 없는지가 관건이다. 
        
        - 메서드 내부 함수에서의 this를 우회하는 방법
        
        ```jsx
        var obj = {
            outer: function () {
                console.log(this);  // {outer: f}
                var innerFunc1 = function () {
                    console.log(this);  // Window { ... } - 전역객체를 가리킨다. 
                };
                innerFunc1();
        
                var self = this;  // self라는 변수에 this를 저장
                var innerFunc2 = function () {
                    console.log(self); // { outer: f }
                };
                innerFunc2();
            }
        };
        obj.outer();
        ```
        
        상위 스코프의 this를 저장해서 내부함수에서 활용하려는 수단일 뿐이므로 의미만 통한다면 변수명을 무엇으로 정해도 무관하다. 원활한 협업이나 의사소통을 위해서는 널리 쓰이는 단어(self, _this, that, _ 등)를 활용하는 것이 바람직하다.
        
        - this를 바인딩하지 않는 함수
        
        ES6에서는 함수 내부에서 this가 전역객체를 바라보는 문제를 보완하고자, this를 바인딩하지 않는 화살표 함수를 새로 도입했다. 화살표 함수는 실행 컨텍스트를 생성할 때 this 바인팅 과정 자체가 빠지게 되어, 상위 스코프의 this를 그대로 활용할 수 있다. 내부함수를 화살표 함수로 바꾸면 ‘우회법’이 불필요해진다. 
        
        ```jsx
        var obj = {
            outer: function () {
                console.log(this);
                var innerFunc = () => {
                    console.log(this);
                };
                innerFunc();
            }
        };
        obj.outer();
        ```
        
        ```jsx
        // ES6 arrow function
        var a = 10;
        var obj = {
        	a: 20,
        	b: function() {
        		console.log(this.a);  // 20
        	
        		const c = () => {
        			console.log(this.a); // 20
        		}
        		c();
        	}
        }
        obj.b();
        ```
        
        ```jsx
        // ES5 call / apply
        var a = 10;
        var obj = {
        	a: 20,
        	b: function() {
        		console.log(this.a);  // 20
        	
        		function c() {
        			console.log(this.a); // 20
        		}
        		c.call(this);
        	}
        }
        obj.b();
        ```
        
- 콜백 함수 호출 시 그 함수 내부에서의 this
    
    ```jsx
    function a(x, y, z) {
    	console.log(this, x, y, z);
    }
    var b = {
    	bb: 'bbb'
    };
    
    a.call(b, 1, 2, 3); //{ bb: 'bbb' } 1 2 3
    
    a.apply(b, [1, 2, 3]); //{ bb: 'bbb' } 1 2 3
    
    var c = a.bind(b);  // this를 들고 있는 상태
    c(1, 2, 3);  //{ bb: 'bbb' } 1 2 3
    
    var d = a.bind(b, 1, 2);
    d(3);  //{ bb: 'bbb' } 1 2 3
    
    // 모두 똑같이 출력된다.
    ```
    
    - 명시적으로 this를 바인딩하는 방법 세 가지
    
    ```jsx
    func.call(thisArg[, arg1[, arg2[, ...]]])
    func.apply(thisArg, [argsArray])
    func.bind(thisArg[, arg1[, arg2[, ...]]])
    ```
    
    - 콜백함수에서의 this
    
    ```jsx
    var callback = function() {
    	console.dir(this); // 함수로써 호출을 했으니 전역객체가 나온다.
    };
    var obj = {
    	a: 1,
    	b: function(cb) {
    		cb();
    	}
    };
    obj.b(callback);
    ```
    
    ```jsx
    var callback = function() {
    	console.dir(this);  // obj
    };
    var obj = {
    	a: 1,
    	b: function(cb) {
    		cb.call(this);  // thisArg에 this를 넘겼다.
    	}
    };
    obj.b(callback);
    ```
    
    콜백함수에서의 this는 기본적으로는 전역객체를 보는 게 맞지만 obj.b 라는 함수 안에서 콜백을 호출했을 때 this를 가지고 있던 this로 지정을 하면(cb.call(this)) 그 지정한 값으로 바뀐다.
    
    ```jsx
    var callback = function() {
    	console.dir(this);  // 전역객체
    };
    var obj = {
    	a: 1
    };
    setTimeout(callback, 100);  // 0.1초 뒤에 callback함수를 실행
    ```
    
     - bind 메서드 
    
    ```jsx
    var callback = function() {
    	console.dir(this);
    };
    var obj = {
    	a: 1
    };
    setTimeout(callback.bind(obj), 100);  
    ```
    
     - 이벤트리스너
    
    ```jsx
    document.body.innerHTML += '<div id="a">클릭</div>';
    
    document.getElementById('a').addEventListener(
    	'click',
    	function() [
    		console.dir(this);  // html dom element
    	}
    );
    // 콜백함수의 this를 별도로 지정해 놓은 경우이다.
    ```
    
    ```jsx
    // this를 바꾸고 싶은 경우
    document.body.innerHTML += '<div id="a">클릭</div>';
    var obj = { a: 1 };
    
    document.getElementById('a').addEventListener(
    	'click',
    	function() [
    		console.dir(this);  // html dom element
    	}.bind(obj)
    );
    // 콜백함수를 넘겨줄 때 this를 obj로 하도록 명시적으로 바인딩
    ```
    
    **정리**
    
     - 콜백함수는 기본적으로는 함수의 this와 같다.
    
     - 제어권을 가진 함수가 콜백의 this를 지정해둔 경우도 있다.
    
     - 이 경우에도 개발자가 this를 바인딩해서 콜백을 넘기면 그에 따른다.
    
- 생성자함수 호출 시 그 함수 내부에서의 this
    새로 만들 인스턴트 객체 그 자체가 곧 this가 된다.

```jsx
function Person(n, a) {
	this.name = n;
	this.age = a;
}
var roy = Person('혜인', 20);
console.log(window.name, window.age);  // 혜인 20
```

전역객체의 name프로퍼티와 age프로퍼티에 값이 할당되어서 ‘혜인 20’이 출력된다.

```jsx
function Person(n, a) {
	this.name = n;
	this.age = a;
}
var roy = new Person('혜인', 20);
console.log(roy);  // 혜인 20
```

new를 넣어서 호출을 하면 생성자함수로써 호출되어 roy라고 하는 변수, 즉 새로 생성될 Person의 인스턴스 객체 자신이 곧 this가 되니까 객체가 새로 만들어지면서 그 객체 안에 name프로퍼티, age 프로퍼티가 생성되면서 name프로퍼티에 ‘혜인’, age 프로퍼티에 20이 들어간 채로 그 객체가 다시 roy라고 하는 변수에 담기게 된다.

- 콜백 함수
    - 제어권 위임
        - 실행 시점
        
        ```jsx
        // 주기함수 호출, 인자1 : 콜백함수, 인자2 : 주기(ms)
        setInterval(function () {
        	console.log('1초마다 실행');
        }, 1000);
        ```
        
        ```jsx
        var cb = function() {
        	console.log('1초마다 실행');
        };
        setInterval(cb, 1000);
        // setInterval에게 함수를 넘겨주기 -> 제어권을 setInterval에게 넘긴다.
        ```
        
        `setInterval` 은 일정 시간 간격으로 한 번씩 함수를 실행해주는 함수이다.
        
        내가 제어권을 넘겨주고자 하는 대상의 규칙에 따라야만 동작을 제대로 할 수 있다.
        
        - 매개변수
        
        ```jsx
        // ex)
        var arr = [1,2,3,4,5];
        var entries = [];
        // forEach함수 호출, 인자1 : 콜백함수, 인자2 : this로 인식할 대상(생략가능)
        arr.forEach(function(v,i) {
        	entreis.push([i,v,this[i]]);
        }, [10, 20, 30, 40, 50]);
        console.log(entries);
        ```
        
        - this
        
        ```jsx
        document.body.innerHTML = '<div id="a">abc</div>';
        function cbFunc(x){
        	console.log(this, x);
        }
        
        document.getElementById('a').addEventListener('click', cbFunc);
        ```
        
    - 콜백함수의 특징
        - 다른 함수(A)의 인자로 콜백함수(B)를 전달하면, A가 B의 제어권을 갖게 된다.
        - 특별한 요청(bind)이 없는 한 A에 미리 정해놓은 방식에 따라 B를 호출한다.
        - 미리 정해놓은 방식이란 어떤 시점에 콜백을 호출할지, 인자에는 어떤 값들을 지정할지, this에 무엇을 바인딩할지 등이다.
        - 콜백으로 넘기는 것은 메서드가 아니라 함수이다.
- 클로저
    
    A의 LexicalEnvironment와 내부함수B의 조합에서 나타나는 특별한 현상
    
    → 컨텍스트A에서 선언한 변수를 내부함수B에서 참조할 경우에 발생하는 특별한 현상
    
    → 컨텍스트A에서 선언한 변수a를 참조하는 내부함수B를 A의 외부로 전달할 경우, A가 종료된 이후에도 a가 사라지지 않는 현상
    
    → 함수 종료 후에도 사라지지 않는 지역변수를 만들 수 있다
    
    ```jsx
    var outer = function() {
    	var a = 1;
    	var inner = function() {
    		console.log(++a);
    	};
    	inner();
    }
    outer();
    ```
    
    - outer : LexicalEnvironment, environmentRecord : {a: 1, inner: f}, outerEnvironmentReference: { outer: f }
    - inner : LexicalEnvironment, environmentRecord : { }, outerEnvironmentReference: { a: 1 → 2, inner: f }
    
    ```jsx
    var outer = function() {
    	var a = 1;
    	var inner = function() {
    		return ++a;
    	};
    	return inner();
    }
    var outer2() = outer();
    console.log(outer2());  // 2
    console.log(outer2());  // 3
    ```
    
    inner에 대한 참조 카운트가 0이 아니어서 계속 연결되어 있다. (outer에 있는 a가 사라지지 않음)
