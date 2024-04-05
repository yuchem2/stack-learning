일련의 명령문인 프로시저와 유사하지만, 함수로 자격을 얻으려면 입력을 받아서 출력 사이에 명확한 관계가 있는 반환을 해야 합니다. 
## Defining functions
### Function declarations
함수 선언은 다음과 같은 `function` 키워드로 구성되어 있습니다.
+ 함수의 이름
+ 함수의 매개변수를 `()`를 통해 묶고 `,`로 구분
+ 함수를 정의하는 명령문을 `{}`로 묶습니다

```javascript
function square(number) {
	return number * number;
}
```

기본적으로 `number`와 같은 매개변수는 값으로 함수에 전달됩니다. 따라서 함수 내의 코드가 전달된 매개변수에 완전히 새로운 값을 할당하는 경우에도 변경사항은 전역적으로 또는 해당 함수를 호출한 코드에 반영되지 않습니다.

객체, 배열을 매개 변수로 전달한 후 내부 요소를 변경하면 변경사항이 적용됩니다. (주소를 통한 전달)
### Function expression
위 함수 선언은 구문론적이지만 표현식으로 생성될 수 있습니다. 이러한 함수는 이름이 없어도 선언 가능합니다.

```javascript
const square = function (number) {
	return number * number;
};
const x = square(4);
```

함수 표현식으로 선언하는 경우에도 함수의 이름을 지정할 수 있습니다. 함수가 자신을 참조할 수 있고, 디버거의 스택 추적에서 함수를 보다 쉽게 식별할 수 있습니다.
```javascript
const factorial = function fac(n) {
	return n < 2 ? 1 : n * fac(n - 1);
};

console.log(factorial(3));
```
## Calling functions
함수는 호출될 때 스코프 내에 있어야 합니다. 함수의 선언 또한 hoisting될 수 있습니다. 

함수는 자기 자신을 호출할 수도 있고, 동적 호출하거나 매개변수의 수를 다르게 하거나 호출의 맥락이 런타임에 결정되는 등의 조작을 할 수 있습니다.

함수는 객체로써 다뤄져 자체적으로 method를 가지고 있습니다. `call()`과 `apply()` method를 호출함으로써 위에 언급한 작업을 수행할 수 있습니다.
### Function hoisting
```javascript
console.log(square(5));

function square(n) {
	return n * n;
}
```
위 예시는 오류 없이 실행됩니다. JavaScript 인터프리터가 전체 함수 선언을 현재 scope의 맨 위로 끌어올리기 때문입니다.

function hoisting은 함수 선언에서만 작동하며 함수 표현식에는 작동하지 않습니다. (변수 hoisting은 해당 선언만 hoisting하기 때문)
### Function scope
함수 내부에 정의된 변수는 함수 범위 내에서만 정의됩니다. 하지만 함수는 자신이 정의된 범위 내에 정의된 모든 변수와 함수에 접근 가능합니다.
## Scope and the function stack
### Recursion
함수는 자신을 참조하고 호출할 수 있습니다. 자신을 참조하는 방법은 다음과 같습니다.
+ 함수 이름
+ `arguments.callee`
+ 함수를 참조하는 범위 내 변수

```javascript
const foo = function bar() {
	// statements 
};
```
위와 같은 예시의 함수에서 자신을 참조하는 방법은 다음과 같습니다.
+ `bar()`
+ `arguments.callee()`
+ `foo()`
### Nested functions and closures
다른 함수 내에 함수를 중첩할 수 있습니다. 내부 함수는 외부 함수에서만 사용할 수 있습니다.

중첩은 `closure`를 생성합니다. `closure`은 변수를 바인딩하는 환경과 함께 자유 변수를 가질 수 있는 표현입니다. 이렇게 정의된 내부 함수는 다음과 같은 특징을 가집니다.
+ 내부 함수는 외부 함수의 명령문에서만 액세스할 수 있습니다. 
+ 내부 함수는 `closure`를 형성합니다. 내부 함수만이 외부 함수의 인수와 변수를 사용할 수 있습니다
#### Preservation of variables
```javascript
function outside(x) {
  function inside(y) {
    return x + y;
  }
  return inside;
}

fn_inside = outside(3);
result = fn_inside(5); // 8

result1 = outside(3)(5); // 8
```

`inside`가 반환될 때 외부 함수의 인수 `x`가 보존된다는 점을 알 수 있습니다. `closuer`는 그것을 참조하는 모든 스코프에서 인수와 변수를 보존해야 합니다. 

각 호출은 다른 인수를 제공할 수 있기 때문에 `closure`는 `outside`에 대하여 매번 새롭게 생성됩니다. 

변수의 보존은 일반 객체에서 참조를 저장하는 것과 차이점이 없지만, 직접 참조를 설정하고 검사하는 게 아니기 때문에 명확하지 않는 경우가 있습니다
#### Multiply-nested functions
중첩은 중복으로도 수행할 수 있습니다. 이로 인해 `closure`는 여러 scope가 포함될 수 있으며, 함수의 scope를 재귀적으로 포함합니다. 이러한 것을 scope chaining이라고 합니다. 
#### Name conflicts
`closure`의 scope에서 두 개의 인수 혹은 변수의 이름이 같은 경우 name conflicts가 발생합니다. 이 경우 더 안쪽 scope가 우선순위를 갖습니다. 이러한 방식을 scope chain이라고 합니다
## Closures
JS의 강력한 기능 중 하나로, JS는 함수의 중첩을 허용하고, 내부 함수가 외부 함수 안에서 정의된 모든 변수와 함수에 대해 전체 접근 권한을 부여합니다.

하지만 외부 함수는 내부 함수에 정의된 변수와 함수에 접근할 수 없습니다. 일종의 캡슐화를 제공합니다.

또한, 내부함수는 외부 함수의 scope에 접근할 수 있기 때문에, 내부 함수가 외부 함수보다 오래 생존하는 경우 외부 함수에서 선언된 변수와 함수는 외부함수의 실행기간보다 오래 유지됩니다. 
## Using the arguments object
함수의 인수들은 배열과 유사한 객체로서 처리됩니다. 함수 내에서 전달된 인수를 다음과 같이 다룰 수 있습니다. 
```javascript
arguments[i];
```
총 인수의 개수는 `arguments.length`에서 얻을 수 있습니다. `arguments` 객체를 이용하면 보통 함수에 정의된 개수보다 많은 인수를 넘겨주면서 함수를 호출할 수 있습니다.

```javascript
function myConcat(separator) {
  let result = "";
  for (let i = 1; i < arguments.length; i++) {
    result += arguments[i] + separator;
  }
  return result;
}

console.log(myConcat(", ", "red", "orange", "blue"));
// "red, orange, blue, "

console.log(myConcat("; ", "elephant", "giraffe", "lion", "cheetah"));
// "elephant; giraffe; lion; cheetah; "

console.log(myConcat(". ", "sage", "basil", "oregano", "pepper", "parsley"));
// "sage. basil. oregano. pepper. parsley. "
```
## Function parameters
ECMAScript 2015에서 추가된 매개변수 구문에는 기본 매개변수와 나머지 매개변수라는 두 가지 유형이 존재합니다.
### Default parameters
JS에서 함수의 매개변수는 기본적으로 `undefined`으로 설정됩니다. 경우에 따라 다른 기본값을 설정할 수 있습니다.
### Rest parameters
배열로 임의 개수의 인수를 나타낼 수 있습니다.

```javascript
function multiply(multiplier, ...theArgs) {
  return theArgs.map((x) => multiplier * x);
}

var arr = multiply(2, 1, 2, 3);
console.log(arr); // [2, 4, 6]
```
## Arrow functions
화살표 함수 표현은 함수 표현식에 비해 짧은 문법을 가지고 있고 사전적으로 `this` 값을 묶습니다. 화살표 함수는 언제나 이름이 없는 함수로서 선언됩니다. 

이 함수의 장점은 더 짧은 함수와 바인딩 되지 않은 `this`가 있습니다.
### Shorter functions
```javascript
var a = ["Hydrogen", "Helium", "Lithium", "Beryllium"];

var a2 = a.map(function (s) {
  return s.length;
});
console.log(a2); // logs [8, 6, 7, 9]

// Arrow function
var a3 = a.map((s) => s.length);
console.log(a3); // logs [8, 6, 7, 9]
```
### No separate this
화살표 함수 이전까지 모든 `new` 함수는 고유한 `this` 값을 정의했습니다. 이러한 방향석은 객체 지향 프로그래밍 스타일과 잘 맞지 않습니다.

화살표 함수에는 `this`가 없기 때문에 화살표 함수를 포함하는 객체 값이 사용되게 됩니다. 

```javascript
function Person() {
  this.age = 0;

  setInterval(() => {
    // `this`는 person 객체를 가리킵니다.
    this.age++;
  }, 1000);
}

var p = new Person();
```
## 출처
+ https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions
