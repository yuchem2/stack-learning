## Conditional statements
### if...else statement
논리 조건이 `true`이면 `if` 구문을 실행하고, `false`이면 `else` 구문을 실행합니다.
```javascript
if (condition) {
  statement1;
} else {
  statement2;
}
```
`else if`를 통해 복합적인 조건을 추가할 수 있습니다.
```javascript
if (condition1) {
  statement1;
} else if (condition2) {
  statement2;
} else if (conditionN) {
  statementN;
} else {
  statementLast;
}
```
#### false value
+ `false`
+ `undefined`
+ `null`
+ `0`
+ `NaN`
+ `""`
### switch statement
```javascript
switch (expression) {
  case label1:
    statements1;
    break;
  case label2:
    statements2;
    break;
  // …
  default:
    statementsDefault;
}
```
JS에서는 위의 `switch` 구문을 다음과 같이 평가합니다.
+ 프로그램은 먼저 표현식 값과 일치하는 레이블이 있는 `case`를 찾은 다음 해당 절로 제어를 전송하여 명령문을 실행합니다
+ 일치하는 레이블이 없으면 프로그램은 선택적 `default` 구문을 찾습니다.
	+ `default` 절이 발견되지 않으면 `switch`문의 끝 다음에 오는 명령문을 실행합니다
+ `break`이 없다면 `switch` 구문에서는 찾은 레이블부터 순차적으로 계속 실행합니다
## Exception handling statements
### Exception types
JS에서는 거의 모든 객체를 `throw`를 이용해 에러로 던질 수 있습니다. 그럼에도 숫자나 문자열보다 예외를 나타내기 위해 사전에 정의된 예외 유형을 쓰는 것이 좋습니다.
+ ECMAScript Exception
+ `DOMException`, `DOMError`
### throw statement
예외를 발생시킬 때 `throw`를 이용해 발생시킬 수 있습니다. 
```javascript
throw "Error2"; // String
throw 42; // Number
throw true; // Boolean
throw {
  toString: function () {
    return "저는 객체예요";
  },
};
```
### try...catch statement
실행을 시도할 블록을 표시하고, 그 안에서 예외가 발생한 경우 처리를 맡을 문을 `catch`를 통해 잡아내 실행합니다.

```javascript
function getMonthName(mo) {
  mo = mo - 1; // 배열 인덱스에 맞춰 월 조절 (1 = Jan, 12 = Dec)
  let months = [
    "Jan",
    "Feb",
    "Mar",
    "Apr",
    "May",
    "Jun",
    "Jul",
    "Aug",
    "Sep",
    "Oct",
    "Nov",
    "Dec",
  ];
  if (months[mo]) {
    return months[mo];
  } else {
    throw "InvalidMonthNo"; // 여기서 throw 키워드 사용
  }
}

try {
  // 시도할 명령문
  monthName = getMonthName(myMonth); // 예외가 발생할 수 있는 함수
} catch (e) {
  monthName = "unknown";
  logMyErrors(e); // 오류 처리기에 예외 객체 전달
}
```
#### finally block
`finally`는 `try`와 `catch` 블록 실행이 끝난 후 이어서 실행되는 블럭 구문입니다. 예외 발생 여부에 없이 항상 실행됩니다.

## 출처
+ https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Control_flow_and_error_handling
