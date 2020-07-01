# var vs let

## 1. 선언 전 사용 가능 여부
### var
- 선언하기 전에 사용 가능
````javascript
a;
console.log(a);  // undefined
var a = 5;
````

### let
- 선언하기 전에는 존재하지 않음
````javascript
a;  // Uncaught SyntaxError: Identifier 'a' has already been declared
console.log(a);
let a = 5;
````

## 2. 재선언 가능 여부
### var
- 재선언 가능
````javascript
var a = 5;
var a = 10;
console.log(a);  // 10
````

### let
- 재선언 불가능
````javascript
let a = 5;
let a = 10;  // Uncaught SyntaxError: Identifier 'a' has already been declared
console.log(a);
````

## 3. scope
### var
- function scope
````javascript
for(var i = 0; i < 5; i++) {
    console.log("i : " + i);
}
console.log(i);  // 5
````
````javascript
function f() {
    for(var i = 0; i < 5; i++) {
        console.log("i : " + i);
    }
}
f();
console.log(i);  // ReferenceError: i is not defined
````

### let
- block scope
````javascript
for(let i = 0; i < 5; i++) {
    console.log("i : " + i);
}
console.log(i);  // ReferenceError: i is not defined
````

# Temporal dead zone(사각지대)
- var와 let 둘 다 hoisting
- 그러나
````javascript
// 에러 발생하지 않음
a = 5;
var a;
````
````javascript
a = 5;  // ReferenceError
let a;
````
- temporal dead zone 때문.
- 스코프 안에서 변수의 사각지대는 변수가 선언되기 전의 코드다. 

# const
- `let`은 변수에 재할당이 가능하지만 `const`는 불가능
````javascript
// 에러 발생하지 않음
let b = 1;
b = 2;
````
````javascript
const b = 1;
b = 2;  // Uncaught TypeError: Assignment to constant variable.
````

### 언제 let을 쓰고 언제 const를 쓰는가?
- 기본적으로 const 사용 권장
    - 의도치 않은 재할당 방지
- 재할당이 필요한 경우 let 사용