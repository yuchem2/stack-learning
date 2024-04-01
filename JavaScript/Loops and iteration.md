## for statement
JS의 `for`문은 C의 반복문과 유사합니다.
```javascript
for (initialization; condition; afterthought)
  statement
```
## do...while statement
`do...while`은 특정한 조건이 `false`가 될 때까지 반복합니다. 조건을 확인하기 전까지 명령문은 최소 한번 실행됩니다.
```javascript
do
  statement
while (condition);
```
## while statement
조건이 `true`인 경우 명령문을 속해서 수행합니다.
```javascript
while(condition) 
	statement
```
## labeled statement
레이블은 프로그램에서 다른 곳으로 참조할 수 있도록 하는 식별자를 제공합니다. 제어는 `break`와 `continue`를 통해 수행할 수 있습니다.
```javascript
label:
	statement
```
## break statement
반복문, `switch`문, 레이블 문과 같은 명령문을 빠져나올 때 사용합니다.
+ 레이블 없이 사용하는 경우: 가장 가까운 `while`, `do...while`, `for` 또는 `switch`문을 종료하고 다음 명령문으로 넘어갑니다.
+ 레이블 문을 쓰는 경우: 특정 레이블 문에서 끝납니다.

```javascript
var x = 0;
var z = 0;
labelCancelLoops: while (true) {
  console.log("Outer loops: " + x);
  x += 1;
  z = 1;
  while (true) {
    console.log("Inner loops: " + z);
    z += 1;
    if (z === 10 && x === 10) {
      break labelCancelLoops;
    } else if (z === 10) {
      break;
    }
  }
}
```
## continue statement
`while`, `do-while`, `for`, 레이블 문을 다시 시작하기 위해 사용할 수 있습니다.
+ 레이블 없이 사용하는 경우: 가장 가까운 `while`, `do...while`, `for` 또는 `switch`문을 둘러싼 현재 반복을 종료하고, 다음 반복으로 루프의 실행을 계속합니다. 
+ 레이블 문을 쓰는 경우: `continue`가 그 레이블로 식별되는 반복문에 적용됩니다.
## for...in statement
iterates를 이용해 특정 변수나 객체의 특성을 분해해 반복을 수행할 수 있습니다. 이때 순서 없이 단순히 반복하게 됩니다.
```javascript
for (variable in object)
  statement
```
배열의 경우 `for..in` 구문을 사용하지 않는 것이 권장됩니다. (항상 인덱스 순서대로 실행된다는 보장이 없기 때문입니다.)
## for...of statement
반복 가능한 객체(`Array`, `Map`, `Set`, `arguments`)를 이용해 반복 객체를 만들어 낼 수 있습니다. 
```javascript
const arr = [3, 5, 7];
arr.foo = "hello";

for (const i in arr) {
  console.log(i);
}
// "0" "1" "2" "foo"

for (const i of arr) {
  console.log(i);
}
// Logs: 3 5 7
```

## 출처
+ https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Loops_and_iteration