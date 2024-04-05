## Operators
JS는 이항 연산자와 단항 연산자 모두를 포함하여 삼항 연산자도 가지고 있습니다. 
- Assignment operators
- Comparison operators
- Arithmetic operators
- Bitwise operators
- Logical operators
- BigInt operators
- String operators
- Conditional (ternary) operator
- Comma operator
- Unary operators
- Relational operators
### Assignment operators
rhs의 값을 lhs에 할당하는 연산자. 기본적으로 `=`을 이용해 대입을 수행하지만, 연산과 할당을 동시에 수행하는 것도 가능합니다. 반환 값은 lhs에 할당된 결과 값입니다. 

```javascript
let x;
const y = (x = f()); // Or equivalently: const y = x = f();
console.log(y); // Logs the return value of the assignment x = f().

console.log(x = f()); // Logs the return value directly.

// An assignment expression can be nested in any place
// where expressions are generally allowed,
// such as array literals' elements or as function calls' arguments.
console.log([0, x = f(), 0]);
console.log(f(0, x = f(), 0));
```

변수 chaing을 하는 경우 우결합을 수행하지만, 평가는 좌측부터 수행됩니다.
### Comparison operators
피연산자들을 서로 비교하고, 비교 결과가 참인지에 따라 논리 값을 반환합니다. 일반적으로 JS는 두 피연산자의 타입이 다르면 비교하기에 적합한 타입으로 변환해 비교를 수행합니다. `===`와 `!==`는 엄격한 일치와 불일치를 수행해 타입 변환을 수행하지 않고 비교를 수행합니다.
### Arithmetic operators
두 개의 숫자 값을 피연산자로 받아서 하나의 수를 반환합니다. 표준 산술 연산자는 `+`, `-`, `*`, `/`입니다. 다른 프로그래밍 언어에서 부동소수점 값을 연산할 때와 동일하게 동작합니다. (0으로 나누는 경우 `Infinity`를 반환합니다) 추가적으로 나머지(`%`), 증가/감소(`++/--`), 단항 부정/긍정(`-/+`), 거듭제곱(`**`)을 지원합니다.
### Bitwise operators
피연산자를 특정 진수의 수로 취급하지 않고 32개의 bit집합으로 취급해 연산합니다. 이진법 표현에 대한 연산을 수행하지만, 반환할 때는 JS 표준 숫자로 반환합니다.
+ `&`, `|`, `^`, `~`: 비트 AND, OR, XOR, NOT
+ `<<`, `>>`, `>>>`: 왼쪽, 오른쪽 시프트, 부호 없는 오른쪽 시트트
### Logical operators
boolean 값과 함께 사용해서 boolean 값을 반환합니다. 사실 `&&`와 `||` 연산자는 두 피연산자 중 하나를 반환하는 것으로, 둘 중 하나가 boolean 값이 아니라면 논리연산자의 반환 값도 boolean 값이 아닐 수 있습니다. 
+ `&&`: 논리 AND, lhs를 `false`로 변환할 수 있으면 lhs를 반환하고, 그 외에는 rhs를 반환합니다. 
+ `||`: 논리 OR, lhs를 `true`로 변환할 수 있으면 lhs를 반환하고, 그 외에는 rhs를 반환합니다. 
+ `!`: 논리 NOT, 단일 피연산자를 `true`로 변환할 수 있으면 `false`를 반환하고 그 외에는 `true`를 반환합니다.

`false`로 변환할 수 있는 표현식은 평가 결과가 `null`, `0`, `NaN`, 빈 문자열, `undefined`인 경우입니다. 

```javascript
const a1 = true && true; // t && t returns true
const a2 = true && false; // t && f returns false
const a3 = false && true; // f && t returns false
const a4 = false && 3 === 4; // f && f returns false
const a5 = "Cat" && "Dog"; // t && t returns Dog
const a6 = false && "Cat"; // f && t returns false
const a7 = "Cat" && false; // t && f returns false
const o1 = true || true; // t || t returns true
const o2 = false || true; // f || t returns true
const o3 = true || false; // t || f returns true
const o4 = false || 3 === 4; // f || f returns false
const o5 = "Cat" || "Dog"; // t || t returns Cat
const o6 = false || "Cat"; // f || t returns Cat
const o7 = "Cat" || false; // t || f returns Cat
const n1 = !true; // !t returns false
const n2 = !false; // !f returns true
const n3 = !"Cat"; // !t returns false
```
### BigInt operators
`Number` 사이에 사용할 수 있는 대부분의 연산자는 `BigInt` 값 사이에서도 사용할 수 있습니다. 그러나 `>>>`는 정의되지 않습니다. 이는 `BigInt`에 고정된 너비가 없기 때문에 기술적으로 가장 높은 비트가 없기 때문입니다. 

`BigInt`와 `Number`는 서로 대체할 수 없고, 혼합해서 사용할 수 없습니다. 이는 `BigInt`가 `Number`의 하위 집합도, 상위 집합도 아니기 때문입니다. `BigInt`는 큰 정수를 나타낼 때 `Number`보다 정밀도가 높지만 실수를 나타낼 수 없기 때문에 암시적 변환에서 정밀도가 떨어질 수 있습니다. 명시적 변환을 사용해 연산을 수행할 수 있습니다.

```javascript
const a = Number(1n) + 2; // 3
const b = 1n + BigInt(2); // 3n
```

두 값의 비교는 변환 없이도 수행 가능합니다.
```javascript
const a = 1n > 2; // false
const b = 3 > 2n; // true
```
### String operators
문자열에는 비교 연산자들 외에도 `+`를 통해 두 문자열을 연결할 수 있습니다. 
### Conditional (ternary) operator
조건 연산자는 JS에서 유일한 3항 연산자로, 주어진 조건에 따라 두 값 중 하나를 반환합니다. 
### Comma operator
두 피연산자를 모두 평가한 후 오른쪽 피연산자의 값을 반환합니다. 주로 `for` 반복문 안에서 사용하여 한 번의 반복으로 여러 변수를 변경할 때 사용합니다. 

```javascript
var x = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
var a = [x, x, x, x, x];

for (var i = 0, j = 9; i <= j; i++, j--);
//                                  ^
console.log(`a[${i}][${j}]= ${a[i][j]}`);
```
### Unary operators
오직 하나의 피연산자만 사용하는 연산입니다.
#### `delete`
객체의 속성을 삭제합니다. 다음과 같이 사용될 수 있습니다. 
```javascript
delete object.property;
delete object[propertyKey];
delete objectName[index];
```
`delete` 연산자가 속성을 성공적으로 삭제한 이유 해당 속성에 접근하려고 하면 `undefined`가 반환됩니다. `delete`는 속성을 제거할 수 있는 경우에는 `true`를 반환하고 제거할 수 없을 땐 `false`를 반환합니다. 

배열에서도 `delete`를 사용해 원소를 제거할 수 있지만, 배열 길이 속성은 영향에 받지 않으며 다른 요소의 인덱스도 그대로 남아있습니다. 이런 동작을 원한다면 그 값을 단순히 `undefined`로 바꾸는 것이 낫습니다. 
#### `typeof`
```javascript
typeof operand;
typeof (operand);
```
평가 전의 피연산자 타입을 나타내는 문자열을 반환합니다. 

```javascript
typeof true; // returns "boolean"
typeof null; // returns "object"
typeof 62; // returns "number"
typeof "Hello world"; // returns "string"
typeof document.lastModified; // returns "string"
typeof window.length; // returns "number"
typeof Math.LN2; // returns "number"
typeof blur; // returns "function"
typeof eval; // returns "function"
typeof parseInt; // returns "function"
typeof shape.split; // returns "function"
typeof Date; // returns "function"
typeof Function; // returns "function"
typeof Math; // returns "object"
typeof Option; // returns "function"
typeof String; // returns "function"
```
#### `void
```javascript
void (expression);
void expression;
```
표현식을 평가할 때 값을 반환하지 않도록 지정합니다. `expression`은 평가할 JS의 표현식입니다.
### Relational operators
피연산자를 서로 비교하고, 비교 결과가 참인지에 따라 `boolean` 값을 반환합니다.
#### `in`
```javascript
propNameOrNumber in objectName;
```
지정한 속성이 지정한 객체에 존재하는 경우 `true`를 반환합니다. 
#### `instanceof`
```javascript
objectName instanceof objectType;
```
지정한 객체가 지정한 객체 타입에 속하면 `true`를 반환합니다
### 연산자 우선순위
높은 순서에서 낮은 순서로 나열되어 있습니

|     유형     | 개별 연산자                                                                                    |
| :--------: | ----------------------------------------------------------------------------------------- |
|   멤버 접근    | `.` `[]`                                                                                  |
| 인스턴스 호출/생성 | `()` `new`                                                                                |
|     증감     | `!` `~` `-` `+` `++` `--` `typeof` `void` `delete`                                        |
|    거듭제곱    | `**`                                                                                      |
|  곱하기/나누기   | `*` `/` `%`                                                                               |
|   더하기/빼기   | `+` `-`                                                                                   |
|   비트 시프트   | `<<` `>>` `>>>`                                                                           |
|     관계     | `<` `<=` `>` `>=` `in` `instanceof`                                                       |
|   동등/일치    | `==` `!=` `===` `!==`                                                                     |
|   비트 AND   | `&`                                                                                       |
|   비트 XOR   | `^`                                                                                       |
|   비트 OR    | `\|`                                                                                      |
|   논리 AND   | `&&`                                                                                      |
|   논리 OR    | `\|\|`                                                                                    |
|     조건     | `?:`                                                                                      |
|     할당     | `=` `+=` `-=` `**=` `*=` `/=` `%=` `<<=` `>>=` `>>>=` `&=` `^=` `\|=` `&&=` `\|\|=` `??=` |
|     쉼표     | `,`                                                                                       |
## Expression
표현식이란 어떤 값으로 이행하는 임의의 유효한 코드 단위를 말합니다. 

모든 표현식은 구문이 유효하다면 어떤 값으로 이행하지만, 개념적으로는 두 가지 범주로 나뉩니다.
+ 부수 효과가 있는 표현식(변수에 값을 할당)
+ 평가하면 어떤 값으로 이행하는 표현식
### `this`
현재 객체를 참조하려면 `this`를 사용하면 됩니다. 일반적으로 `this`는 method의 호출 객체를 참조합니다.
### Grouping operator
`()`는 표현식 평가의 우선순위를 조절합니다.
### `new`
사용자 정의 객체 타입이나 내장 객체 타입의 인스턴스를 생성할 수 있습니다
### `super`
객체의 부모가 가진 함수를 호출할 때 사용합니다. 

## 출처
+ https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_operators#assignment_operators