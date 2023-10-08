# 생성자 함수에 의한 객체 생성

## Object 생성자 함수

> 💡 `new 연산자`와 함께 `Object 생성자 함수를 호출`하면 빈 객체를 생성하여 반환

- `생성자 함수`란 `new 연산자`와 함께 호출하여 `객체(인스턴스)`를 생성하는 함수
- 생성자 함수에 의해 생성된 객체를 `인스턴스(instance)`라 함
- 자바스크립트는 Object 생성자 함수 이외에도 `String, Number, Boolean, Function, Array, Date, RegExp, Promise` 등의 `빌트인(built-in)` 생성자 함수 제공

```javascript
// 빈 객체 생성
const person = new Object();

// 프로퍼티 추가
person.name = 'Lee';
person.sayHello = function() {
  console.log('hi' + this.name);
}

console.log(person); // {name: 'Lee', sayHello: f}

// String 생성자 함수에 의한 String 객체 생성
const strObj = new String('Lee');
console.log(tupeof strObj);   // object
console.log(strObj);          // String {"Lee"}

// Number 생성자 함수에 의한 Number 객체 생성
const numObj = new Number(123);
console.log(tupeof numObj);   // object
console.log(numObj);          // Number {123}

// Boolean 생성자 함수에 의한 Boolean 객체 생성
const boolObj = new Boolean(true);
console.log(typeof boolObj);  // object
console.log(boolObj);         // Boolean {true}

// Function 생성자 함수에 의한 Function 객체(함수) 생성
const func = new Function('x', 'return x * x');
console.log(typeof func);     // function
console.log(func);            // f anonymous(x)

// Array 생성자 함수에 의한 Array 객체(배열) 생성
const arr = new Array(1, 2, 3);
console.log(typeof arr);      // object
console.log(arr);             // [1, 2, 3]

// RegExp 생성자 함수에 의한 RegExp 객체(정규 표현식)생성
const regExp = new RegExp(/ab+c/i);
console.log(typeof regExp);   // object
console.log(regExp);          // /ab+c/i

const date = new Date();
console.log(typeof date);     // object
console.log(date);            // Sun Oct 08 2023 15:23:00 GMT+0900 (GMT+09:00)
```

<br />

## 생성자 함수

### 객체 리터럴에 의한 객체 생성 방식의 문제점

> 💡 `객체 리터럴`에 의한 객체 생성 방식은 직관적이고 간편하나 `단 하나의 객체만 생성`

```javascript
// 프로퍼티 구조가 동일함에도 불구하고 매번 같은 프로퍼티와 메서드를 기술해야 함
const circle1 = {
  radius: 5,
  getDiamter() {
    return 2 * this.radius;
  }
}
console.log(circle.getDiamter());  // 10

const circle2 = {
  radius: 10,
  getDiamter() {
    return 2 * this.radius;
  }
}
console.log(circle.getDiamter());  // 20
```

### 생성자 함수에 의한 객체 생성 방식의 장점

> 💡 `객체(인스턴스)`를 생성하기 위한 `템플릿(클래스)`처럼 `생성자 함수`를 사용하여 `프로퍼티 구조가 동일한 객체 여러 개`를 간편하게 `생성`

```javascript
// 생성자 함수
function Circle(radius) {
  // 생성자 함수 내부의 this는 생성자 함수가 생성할 인스턴스를 가리킴
  this.radius = radius;
  this.getDiamter = function() {
    return 2 * this.radius;
  };
}

// 인스턴스의 생성
const circle1 = new Circle(5);      // 반지름이 5인 Circle 객체 생성  
const circle2 = new Circle(10);     // 반지름이 10인 Circle 객체 생성

console.log(circle1.getDiamter());  // 10
console.log(circle2.getDiamter());  // 20
```

> 💡 `this`는 객체 자신의 프로퍼티나 메서드를 참조하기 위한 `자기 참조 변수(self-referencing variable)`

- this가 가리키는 값, 즉 this 바인딩은 함수 호출 방식에 따라 동적으로 결정

| 함수 호출 방식 | this가 가리키는 값(this 바인딩) |
| --- | --- |
| 일반 함수로서 호출 | 전역 객체 |
| 메서드로서 호출 | 메서드를 호출한 객체(마침표 앞의 객체) |
| 생성자 함수로서 호출 | 생성자 함수가 (미래에) 생성할 인스턴스 |

```javascript
// 함수는 다양한 방식으로 호출될 수 있음
function foo() {
  console.log(this);
}

// 일반적인 함수로서 호출
// 전역 객체는 브라우저 환경에서 window, Node.js 환경에서 global
foo(); // window;

const obj = { foo }; // ES6 프로퍼티 축약 표현
// 메서드로서 호출
obj.foo(); // obj

// 생성자 함수로서 호출
const inst = new foo(); // inst
```

- 클래스 기반 객체지향 언어의 생성자와 다르게 형식이 정해져 있지 않음
- 일반 함수와 동일한 방법으로 생성자 함수를 정의하고 `new 연산자`와 함께 호출하면 해당 함수는 `생성자 함수로 동작`

```javascript
// new 연산자와 함께 호출하지 않으면 생성자 함수로 동작하지 않음
// 즉, 일반 함수로 호출
const circle3 = Circle(15);

// 일반 함수로서 호출된 Circle은 반환문이 없으므로 암묵적으로 undefined 반환
console.log(circle3);  // undefined

// 일반 함수로서 호출된 Circle 내의 this는 전역 객체를 가리킴
console.log(radius);   // 15
``` 

### 생성자 함수의 인스턴스 생성 과정

- 생성자 함수의 역할은 프로퍼티 구조가 동일한 인스턴스를 생성하기 윈한 템플릿(클래스)으로서 동작
- 인스턴스를 생성하는 것과 생성된 인스턴스를 초기화(인스턴스 프로퍼티 추가 및 초기값 할당)하는 것
- 생성자 함수 내부에서 명시적으로 반환하는 것은 생성자 함수의 기본 동작 훼손
- ⭐️ `생성자 함수 내부`에서 `return 문은 반드시 생략`

```javascript
// 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩
console.log(this); // Circle {}

function Circle(radius) {
  // 2. 인스턴스 초기화
  // this에 바인딩 되어 있는 인스턴스 초기화
  this.radius = radius;
  this.getDiamter = function() {
    return 2 * this.radius;
  };

  // 3. 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환
  // 명시적으로 원시 값을 반환하면 원시 값 반환은 무시되고 암묵적으로 this 반환
  return 100;
}

// 인스턴스 생성
// Circle 생성자 함수는 암묵적으로 this 반환
const circle = new Circle(5);
console.log(circle); // Circle {radius: 1, getDiamter: f}
```
  

### 내부 메서드 [[Call]]과 [[Construct]]

> 💡 모든 함수 객체는 `호출`할 수 있지만 모든 함수 객체를 `생성자 함수로서 호출할 수 있는 것은 아님`

- 함수는 객체이므로 일반 객체가 가지고 있는 내부 슬롯과 내부 메서드를 모두 가지고 있음
- 함수로서 동작하기 위해 함수 객체만을 위한 `내부 슬롯`과 `내부 메서드`를 추가로 가짐

```javascript
// 함수는 객체
function foo() {}

// 함수는 객체이므로 프로퍼티를 소유할 수 있음
foo.prop = 10;

// 함수는 객체이므로 메서드를 소유할 수 있음
foo.method = function() {
  console.log(this.prop);
};

foo.method(); // 10
```

- 함수로서 동작하기 위해 함수 객체만을 위한 `[[Environment]], [[FormalParameters]]` 등의 `내부 슬롯`과 `[[Call]], [[Construct]]` 와 같은 `내부 메서드`를 추가로 가짐
- 함수가 `일반 함수`로서 호출되면 객체의 내부 메서드 `[[Call]]` 호출
- 함수가 new 연산자와 함께 `생성자 함수`로서 호출되면 내부 메서드 `[[Construct]]` 호출

```javascript
function foo() {}

// 일반적인 함수로서 호출: [[call]] 호출
// 모든 함수 객체는 [[Call]]이 구현되어 있음
foo();

// 생성자 함수로서 호출: [[Construct]] 호출
// [[Construct]]를 갖지 않는다면 에러 발생
new foo();
```

- `callable`: 내부 메서드 [[Call]]을 갖는 함수 객체, 호출할 수 있는 객체, 즉 `함수`
- `constructor`: 내부 메서드 [[Construct]]를 갖는 함수 객체, `생성자 함수로서 호출할 수 있는 함수`
- `non-constructor`: 내부 메서드 [[Construct]]를 갖지 않는 함수 객체, `생성자 함수로서 호출할 수 없는 함수`
- ⭐️ 함수 객체는 `callable`이면서 `constructor이거나 non-constructor`
  - 모든 함수 객체는 호출할 수 있지만 모든 함수 객체를 생성자 함수로서 호출할 수 있는 것은 아님

### constructor와 non-constructor의 구분

> 💡 자바스크립트 엔진은 함수 객체를 생성할 때 `함수 정의 방식`에 따라 함수를 `constructor`와 `non-constructor`로 구분

- `constructor`: 함수 선언문, 함수 표현식, 클래스(클래스도 함수)
- `non-constructor`: 메서드(ES6 메서드 축약 표현), 화살표 함수

```javascript
// 일반 함수 정의: 함수 선언문, 함수 표현식
function foo() {}
const bar = function() {};
// 프로퍼티 x의 값으로 할당된 것은 일반 함수로 정의된 함수. 이는 메서드로 인정하지 않음
const baz = {
  x: function() {}
};

// 일반 함수로 정의된 함수만이 constructor
new foo();     // -> foo {}
new bar();     // -> bar {}
new baz.x();   // x {}

// 화살표 함수 정의
const arrow = () => {};

new arrow();   // TypeError: arrow is not a constructor

// 메서드 정의: ES6의 메서드 축약 표현만 메서드로 인정
const obj = {
  x() {}
};

new obj.x();   // TypeError: obj.x is not a constructor
```

### new 연산자

> 💡 `new 연산자와 함께 호출하는 함수`는 `constructor`이어야 함

```javascript
// 생성자 함수로서 정의하지 않은 일반 함수
function add(x, y) {
  return x + y;
}

// 생성자 함수로서 정의하지 않은 일반 함수를 new 연산자와 함께 호출
let inst = new add();

// 함수가 객체를 반환하지 않았으므로 반환문이 무시
// 따라서, 빈 객체가 생성되어 반환
console.log(inst);  // {}

// 객체를 반환하는 일반 함수
function createUser(name, role) {
  return {name, role};
}

// 일반 함수를 new 연산자와 함께 호출
inst = new createUser('Lee', 'admin');
// 함수가 생성한 객체를 반환
console.log(inst); // {name: 'Lee', role: 'admin'};
```

- new 연산자 없이 생성자 함수를 호출하면 일반 함수로 호출
- 함수 객체의 내부 메서드 [[Construct]]가 호출되는 것이 아니라 [[Call]] 호출

```javascript
// 생성자 함수
function Circle(radius) {
  this.radius = radius;
  this.getDiameter = function() {
    return 2 * this.radius;
  }
}

// new 연산자 없이 생성자 함수 호출하면 일반 함수로서 호출
const circle = Circle(5);
console.log(circle); // undefined

// Circle 함수는 일반 함수로서 호출되어 
// 일반 함수 내부의 this는 전역 객체 window를 가리킴
// radius 프로퍼티와 getDiameter 메서드는 전역 객체의 프로퍼티와 메서드
console.log(radius);       // 5
console.log(getDiameter()); // 10

circle.getDiameter(); // TypeError: Cannot read property 'getDiameter' of undefined
```

### new.target

> 💡 `생성자 함수`가 `new 연산자 없이 호출`되는 것을 `방지`하기 위해 ES6에서 `new.target` 지원

- new.target을 사용하면 new 연산자와 함께 생성자 함수로서 호출되었는 지확인 가능
- new 연산자와 함께 `생성자 함수`로서 호출되면 함수 내부의 `new.target`은 `함수 자신`을 가리킴
- new 연산자 없이 `일반 함수`로서 호출되면 함수 내부의 `new.target`은 `undefined`

```javascript
// 생성자 함수
function Circle(radius) {
  // 이 함수가 new 연산자와 함께 호출되지 않았다면 new.target은 undefined
  if(!new.target) {
    // new 연산자와 함께 생성자 함수를 재귀 호출하여 생성된 인스턴스 반환
    return new Circle(radius);
  }

  this.radius = radius;
  this.getDiameter = function() {
    return 2 * this.radius;
  };
}

// new 연산자 없이 생성자 함수를 호출하여도 new.target을 통해 생성자 함수로서 호출
const circle = Circle(5);
console.log(circle.getDiameter());
```

- 대부분의 `빌트인 생성자 함수`는 new 연산자와 함께 호출되었는지 확인 후 `적절한 값 반환`
- 예를 들어, `Object`와 `Function` 생성자 함수는 new 연산자 없이 호출해도 `new 연산자와 함께 호출했을 때와 동일하게 동작`

```javascript
let obj = new Object();
console.log(obj); // {}

obj = Object();
console.log(Obj); // {}

let f = new Function('x', 'return x ** x');
console.log(f); // f anonymous(x) { return x ** x}

f = Function('x', 'return x ** x');
console.log(f); // f anonymous(x) { return x ** x}
```

- `String, Number, Boolean` 생성자 함수는 `new 연산자와 함께 호출`했을 때 String, Number, Boolean `객체를 생성하여 반환`
- `new 연산자 없이 호출`하면` 문자열, 숫자, 불리언 값 반환`

```javascript
const str = String(123);
console.log(str, typeof str);   // 123 string

const num = Number('123');
console.log(num, typeof num);   // 123 number

const bool = Boolean('true');
console.log(bool, typeof bool); // true boolean
```
