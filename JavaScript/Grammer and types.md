## Basic
JS는 문법의 대부분을 Java와 C, C++로부터 차용하고 있으며, Awk, Perl, Python의 영향도 받았습니다. 

*대소문자*를 구별하며 *Unicode* 문자셋을 사용합니다. 
### 명령문(statement)
JS에서는 구문을 명령문이라고 정의합니다. 이 명령문은 세미클론(;)에 의해 구분됩니다. 

만약 명령문이 한 줄 단위로 작성되면 세미클론은  필요하지 않습니다. 하지만 한 줄에 하나 이상의 명령문이 존재하는 경우 이를 구분하기 위해 세미클론이 필요합니다. 

그러나 명령문 뒤에 항상 세미클론을 사용해 코드에 버그가 들어갈 가능성을 줄일 수 있습니다.  
## 주석(Comment)
주석은 C++ 및 기타 언어의 구문과 동일합니다. 
```javascript
// a one line comment
/* this is a longer,
 * multi-line comment
 */
```

블록 주석 구문은 중첩되어 사용될 수 없습니다. 

```ad-tip
일분 JS 파일의 시작부분에 `#!/usr/bin/env/node`와 같은 주석이 있는 경우가 있습니다.

이러한 주석을 hashbang commnet 구문이라고 하며, 스크립트를 실행해야 하는 특정 JS 엔진에 대한 경로를 지정하는 데 사용되는 특수 주석입니다. 
```
## 선언(Declarations)
JS에서는 세 가지 방식의 변수 선언이 존재합니다.
+ `var`: 변수를 선언하고, 선택적으로 초기화할 수 있습니다
+ `let`: block scoped 지역 변수를 선언할 수 있습니다. 선택적으로 초기화할 수 있습니다
+ `const`: block scoped 변경 불가능한 상수를 선언합니다
### 변수
변수명은 식별자라고 하며 다음과 같은 규칙을 따릅니다.
+ 문자, 밑줄(_) 혹은 달러 기호($)로 시작해야 합니다.
+ 대소문자를 구분하기 때문에 문자는 A-Z, a-z를 포함합니다. 
+ 숫자와 유니코드 문자도 사용할 수 있습니다.
+ 유니코드 escape sequence도 문자로 사용할 수 있습니다
### 변수 선언
아래 3가지 방법으로 가능합니다.
+ `var x = 42`와 같이 `var` 키워드로 변수를 선언할 수 있습니다. 지역 및 전역 변수를 선언하는데 모두 사용할 수 있습니다.
+ `let y = 13`와 같이 `const` 혹은 `let` 키워드로 변수를 선언할 수 있습니다. 이 구문은 block scoped 지역 변수를 선언하는데 사용됩니다. 

[[구조 분해 할당]] 구문을 사용해 변수를 선언할 수 있습니다. (`const { bar } = foo`)

간단히 변수에 값을 할당할 수도 있습니다. 예를 들어 `x = 42`와 같은 구문은 선언되지 않은 전역변수를 만듭니다. `strict mode`에서는 오류가 발생하기 때문에 사용을 피하는 것이 좋습니다.

### 변수 선언과 초기화 
선언되지 않은 변수에 접근을 시도하는 경우 `ReferenceError` 예외가 발생합니다. 

지정된 초기 값 없이 `var` 혹은 `let`을 사용해 선언된 변수는 `undefied` 값을 갖습니다. 
### Varaible scope
변수는 아래 중 하나의 scope에 속하게 됩니다.
+ Global scope: default scope for all code running in script mode. 
+ Module scope: for code running in module mode.
+ Function scope: created with a function

추가적으로 변수가 `let` 혹은 `const`로 선언된 경우 추가적인 scope에 속할 수 있습니다. 
+ Block scope: created with a pair of curly braces (a block)

변수를 함수 밖에 선언하는 경우 전역변수(Global scope)가 됩니다. 같은 문서 내의 어떤 다른 코드에서도 접근이 가능하기 때문입니다. 함수 안에 선언하는 경우 지역변수(Function scope)가 됩니다. 오직 함수 내에서만 접근 가능하기 때문입니다.

`let`과 `const`로 선언된 변수는 선언된 블록 내부에서만 사용 가능합니다. `var`로 선언된 변수는 블록이 속한 범위에서 사용 가능합니다. 
### Variable hoisting
`var`로 선언된 변수는 선언된 범위의 맨 위로 끌어 올려지게 됩니다. 즉, `var` 선언 위에서 해당 변수를 사용하더라도 변수를 참조할 수 있습니다. 그러나 변수가 선언되기 전에 변수에 접근하는 경우 *선언*만 hoisting되고 *초기화*는 아니기 때문에 값은 항상 `undefined`입니다. 

```javascript
console.log(x === undefined); // true
var x = 3;

(function () {
  console.log(x); // undefined
  var x = "local value";
})();
```

`let`과 `const`도 hoisting이 발생하지만 TDZ(Temporal Dead Zone) 때문에 초기화 전에 해당 변수를 사용하려고 하면 `ReferenceError`가 발생합니다. TDZ는 `let` 및 `const` 키워드로 선언된 변수가 선언된 이후에 해당 변수에 접근하기 전까지 영역을 가리킵니다. 이 영역에서는 변수가 존재하지만 값을 할당받지 않은 상태입니다.

```javascript
console.log(x); // ReferenceError
const x = 3;

console.log(y); // ReferenceError
let y = 3;
```

함수 선언은 항상 함수 전체의 scope가 hoisting되므로 언제나 사용할 수 있습니다.
### Global variables
전역 변수는 실제로 전역 객체의 속성입니다. 

웹 페이지에서 전역 객체는 `window`이므로 `window.variable`을 사용하여 전역 변수를 읽고 설정할 수 있습니다. 모든 환경에서 `globalThis` 변수를 사용해 전역 변수를 읽고 설정할 수 있습니다. 
### Constants
변경 불가능한 상수는 `const` 키워드를 통해 생성합니다. 사용되는 식별자는 변수 식별자와 규칙이 동일합니다. 

기본적으로 `const`는 재할당을 방지하는 것이지, 변형을 방지하지는 않습니다. 그래서 객체를 `const`로 선언하는 경우 객체 속성을 변경할 수 있습니다.
```javascript
const MY_OBJECT = { key: "value" };
MY_OBJECT.key = "otherValue";
```

또한, 배열의 경우에도 변형이 가능합니다.
```javascript
const MY_ARRAY = ["HTML", "CSS"];
MY_ARRAY.push("JAVASCRIPT");
console.log(MY_ARRAY); // ['HTML', 'CSS', 'JAVASCRIPT'];
```
## Data structures and types
### Data types
+ `Boolean`: `true` or `false`
+ `null`: null 값을 나타내는 키워드. `Null`, `NULL`과 다릅니다.
+ `undefined`: 변수가 선언되지 않은 경우 최상위 속
+ `Number`: 정수 혹은 부동소수점 숫자
+ `BigInt`: 임의의 정밀도를 가지는 정수. `9007199254740992n`
+ `String`: 텍스트 값을 표현하는 문자 순열
+ `Symbol`: 인스턴스가 고유하고 불변인 데이터
+ `Object`
### 데이터 타입 변환
JS는 동적으로 데이터 타입이 지정되는 언어입니다. 실행 중에 필요에 따라 데이터 타입이 자동으로 변환되고 결정됩니다. 
#### 숫자와 '+'
숫자 및 문자열 값을 포함하는 표현식에서 `+`는 숫자를 문자열로 변환합니다.
```javascript
x = "The answer is " + 42; // "The answer is 42"
y = 42 + " is the answer"; // "42 is the answer"
z = "37" + 7; // "377"
```
#### 문자열을 숫자로
숫자를 나타내는 값이 문자열로 있는 경우 변환하는 방법은 다음과 같습니다.
+ `parseInt()`: 정수만 반환
+ `parseFloat()`: 실수로 반환
`parseInt()`를 사용할 때 두 번째 인자를 넣게 되면 해당 값을 기수로 하여 반환할 수 있다.
```Javascript
parseInt("101", 2); // 5
```
다른 방법으로는 다음과 같이 `+`를 이용할 수 있습니다. 
```Javascript
"1.1" + "1.1" // '1.11.1'
(+"1.1") + (+"1.1"); // 2.2
// Note: the parentheses are added for clarity, not required.
```
## Literals
JS의 값을 나타냅니다. 문자 그대로 스크립트에 제공하는 변수가 아닌 고정된 값입니다. 
### Array Literals
0개 이상의 표현식 목록으로, 각 표현식은 대괄호(`[]`)로 묶인 배열 요소를 나타냅니다. 

배열 리터럴은 평가될 때마다 *새 배열 개체*를 만듭니다.

```javascript
const coffees = ["French Roast", "Colombian", "Kona"];
let fish = ["Lion", , "Angel"];
var myList = ["home", , "school", ];
```
### Boolean Literals
`true`와 `false` 두 개의 값을 가진다.
### Numeric Literals
JS 숫자 리터럴은 여러 진법의 정수 리터럴과 10진수의 부동 소수점 리터럴을 포함합니다.
#### Interger literals
`int`와 `BigInt` 리터럴은 10, 16, 8, 2진수로 표현될 수 있습니다.
+ 10진수: `0`으로 시작하지 않는 숫자열
+ 8진수: `0`으로 시작하거나 `0o(0O)`으로 시작하는 숫자열
+ 16진수: `0x(0X)`로 시작하는 숫자열 (대소문자 구분x)
+ 2진수: `0b(0B)`로 시작하는 숫자열
+ `BigInt`: `n`으로 끝나는 숫자열. 위 모든 진수 표현이 가능하지만 `0`으로 시작하는 8진수 구문은 허용되지 않습니다
```Javascript
0, 117, 123456789123456789n             (decimal, base 10)
015, 0001, 0o777777777777n              (octal, base 8)
0x1123, 0x00111, 0x123456789ABCDEFn     (hexadecimal, "hex" or base 16)
0b11, 0b0011, 0b11101001010101010101n   (binary, base 2)
```
### Floating-point Literals
다음과 같은 요소로 구성될 수 있습니다.
+ 부호 없는 10진수,
+ 소수점(`.`)
+ 분수
+ 지수

지수부는 `e`나 `E` 다음에 오며 부호가 있는 정수입니다. 부동소수점 리터럴은 적어도 숫자 하나와 소수점 혹은 `e(E)`가 있어야 합니다
```
[digits].[digits][(E|e)[(+|-)]digits]
```
### Object literals
객체 리터럴은 중괄호(`{}`)로 묶인 0개 이상의 객체의 속성 명과 관련 값 쌍 목록입니다.
```ad-caution
명령문 시작에 객체 리터럴을 사용하는 경우 `{`가 블록의 시작으로 해석되기 때문에 오류를 유발하거나 의도한 대로 동작하지 않을 수 있습니다.
```

```javascript
var car = { manyCars: { a: "Saab", b: "Jeep" }, 7: "Mazda" };

console.log(car.manyCars.b); // Jeep
console.log(car[7]); // Mazda
```
#### Enhanced Object Literals
ES2015에서 객체 리터럴은 구성에서 프로토타입 설정, `foo: foo` 할당을 위한 단축 표기, 메서드 정의, `super` 클래스 호출 및 식으로 동적인 속성명 계산을 지원하기 위해 확장되었습니다

이에 따라 객체 리터럴이 클래스 선언에 더 가까워지고, 객체 기반 설계가 편해졌습니다.
```Javascript
var obj = {
  // __proto__
  __proto__: theProtoObj,
  // ‘handler: handler’의 단축 표기
  handler,
  // Methods
  toString() {
    // Super calls
    return "d " + super.toString();
  },
  // Computed (dynamic) property names
  ["prop_" + (() => 42)()]: 42,
};
```
### RegExp Literals
`/` 사이에 감싸인 패턴입니다.
```Javascript
var re = /ab+c/;
```
### String Literals
큰 따음표(`"`) 혹은 작은 따음표(`'`)로 묶인 0개 이상의 문자입니다. 
꼭 `String` 객체를 사용할 필요가 없는 경우 문자열 리터럴을 사용해야 합니다.

문자열 리터럴은 `String` 객체의 모든 메서드를 호출할 수 있습니다. JS는 자동으로 문자열 리터럴을 임시 문자열 객체로 변환, 메서드를 호출하고 나서 임시 문자열 객체를 폐기합니다. 

템플릿 리터럴도 사용할 수 있습니다. 템플릿 리터럴은 `(``)`를 이용해 감싸서 사용합니다. 문자열 구성을 위한 구문으로, 다음과 같이 사용할 수 있습니다.
```javascript
// 기본적인 문자열 리터럴 생성
`In JavaScript '\n' is a line-feed.`;

// 여러 줄 문자열
`In JavaScript, template strings can run
 over multiple lines, but double and single
 quoted strings cannot.`;

// 문자열 삽입
var name = "Bob",
  time = "today";
`Hello ${name}, how are you ${time}?`;
```

## 출처
+ https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types