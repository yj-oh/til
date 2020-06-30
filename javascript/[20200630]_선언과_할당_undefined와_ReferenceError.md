# 선언과 초기화/할당
### 1. Declaration
````javascript
var a;
````

### 2. Initialisation / Assignment
````javascript
a = 5;
````

### 3. 선언과 동시에 할당할 수 있다
````javascript
var a = 5;
````


# undefined vs ReferenceError
````javascript
console.log(typeof apple);  // undefined
console.log(apple);         // ReferenceError
````
### ReferenceError
- Variable not declared
- Wrong scope

### undefined
- 선언되지 않은 변수
````javascript
console.log(typeof b);  // undefined
console.log(b);         // ReferenceError
````

- 선언했지만 값을 할당하지 않은 변수
````javascript
var a;
console.log(typeof a);  // undefined
console.log(a);         // undefined
````
