# 함수와 일급 객체

## 일급 객체

> 💡 다음 조건을 만족하는 객체를 `일급 객체`라 함

1. 무명의 리터럴로 생성할 수 있다. 즉, 런타임에 생성이 가능
2. 변수나 자료구조(객체, 배열)등에 저장할 수 있음
3. 함수의 매개변수에 전달할 수 있음 
4. 함수의 반환값으로 사용할 수 있음

```javascript
// 자바스크립트의 함수는 조건을 모두 만족하므로 일급 객체
// 1. 함수는 무명의 리터럴로 생성할 수 있다.
// 2. 함수는 변수에 저장할 수 있다.
// 런타임(할당 단계)에 함수 리터럴이 평가되어 함수 객체가 생성되고 변수에 할당된다.
const increase = function(num) {
  return ++num;
}

const decrease = function(num) {
  return --num;
}

// 2. 함수는 객체에 저장할 수 있다.
const auxs = {increase, decrease};
// 3. 함수의 매개변수에 전달할 수 있다.
// 4. 함수의 반환값으로 사용할 수 있다.
function makeCounter(aux) {
  let num = 0;

  return function() {
    num = aux(num);
    return num;
  };
}

// 3. 함수는 매개변수에 함수를 전달할 수 있다.
const increaser = makeCounter(auxs.increase);
console.log(increase());  // 1
console.log(increase());  // 2

// 3. 함수는 매개변수에 함수를 전달할 수 있다.
const decrease = makeCounter(auxs.decrease);
console.log(decrease());  // -1
console.log(decrease());  // -2
```

- 함수가 일급 객체라는 것은 함수를 객체와 동일하게 사용할 수 있다는 의미
- `함수`는 값을 사용할 수 있는 곳`(변수 할당문, 객체의 프로퍼티 값, 배열의 요소, 함수 호출의 인수, 함수 반환문)`이라면 어디서든지 `리터럴로 정의`할 수 있으며 `런타임에 함수 객체로 평가`

<br />

## 함수 객체의 프로퍼티

> 💡 함수는 객체이며 따라서 함수도 프로퍼티를 가질 수 있음

- arguments, caller, length, name, prototype 프로퍼티는 모두 함수 객체의 데이터 프로퍼티
- `__proto__`는 `접근자 프로퍼티`이며, 함수 객체 고유의 프로퍼티가 아니라 `Object.prototype 객체의 프로퍼티`를 상속받은 것
-- Object.prototype 객체의 `__proto__ 접근자 프로퍼티`는 `모든 객체가 사용`할 수 있음

```javascript
function square(number) {
  return number * number;
}

console.dir(square);
console.log(Object.getOwnPropertyDescriptors(square));
// arguments: {value: null, writable: false, enumerable: false, configurable: false}
// caller: {value: null, writable: false, enumerable: false, configurable: false}
// length: {value: 1, writable: false, enumerable: false, configurable: true}
// name: {value: 'square', writable: false, enumerable: false, configurable: true}
// prototype: {value: {…}, writable: true, enumerable: false, configurable: false}

// __proto__는 square함수의 프로퍼티가 아님
console.log(Object.getOwnPropertyDescriptor(square, '__proto__')); // undefiend

// __proto__는 Object.prototype 객체의 접근자 프로퍼티
// square 함수는 Object.prototype 객체로부터 __proto__ 접근자 프로퍼티를 상속받음
console.log(Object.getOwnPropertyDescriptor(Object.prototype, '__proto__'));
// {enumerable: false, configurable: true, get: ƒ, set: ƒ}
```

### arguments 프로퍼티

> 💡 함수 호출 시 전달된 `인수들의 정보`를 담고 있는 순회 가능한 유사 배열 객체

- 함수 내부에서 지역 변수처럼 사용되며 함수 외부에서는 참조할 수 없음
- `arguments 객체`는 `인수`를 프로퍼티 값으로 소유하며 프로퍼티 키는 인수의 순서를 나타냄
  - `callee 프로퍼티` : 호출되어 arguments 객체를 생성한 함수, 즉 `함수 자신`
  - `length 프로퍼티` : `인수의 개수`

```javascript
function multiply(x, y) {
  console.log(arguments);
  return x * y;
}

console.log(multiply());
console.log(multiply(1));        // NaN
console.log(multiply(1, 2));     // 2 
console.log(multiply(1, 2, 3));  // 2
```

- 선언된 매개변수의 개수와 함수를 호출할 때 전달하는 인수의 개수를 확인하지 않는 자바스크립트의 특성 때문에 함수가 호출되면 `인수 개수를 확인하고 이에 따라 함수의 동작을 달리 정의할 필요`가 있을 때 유용하게 사용
  - 매개변수 개수를 확정할 수 없는 `가변 인자 함수`를 구현할 때 유용

```javascript
function sum() {
  let res = 0;

  // arguments 객체는 length 프로퍼티가 있는 유사 배열 객체이므로 for문으로 순회할 수 있음
  // 유사 배열 객체는 배열이 아니므로 배열 메서드를 사용하면 에러 발생
  for(let i = 0; i < arguments.length; i++) {
    res += arguemnts[i];
  }

  return res;
}

console.log(sum());           // 0
console.log(sum(1, 2));       // 3
console.log(sum(1, 2, 3));    // 6
```

### caller 프로퍼티

> 💡 함수 자신을 호출한 함수를 가리킴

```javascript
function foo(func) {
  return func();
}

function bar() {
  return 'caller : ' + bar.caller;
}

// 브라우저에서 실행 결과
console.log(foo(bar));  // caller : function foo(func) { return func(); }
console.log(bar());     // caller : null
```

### length 프로퍼티

> 💡 함수를 정의할 때 선언한 매개변수의 개수를 가리킴

- arguments 객체의 length 프로퍼티와 함수 객체의 length 프로퍼티의 값은 다를 수 있으므로 주의
- `arguments 객체`의 `length 프로퍼티` : `인자의 개수`
- `함수 객체`의 `length 프로퍼티`: `매개변수의 개수`

```javascript
function foo {}
console.log(foo.length);  // 0

function bar(x) {
  return x;
}
console.log(bar.length);  // 1

function baz(x, y) {
  return x * y;
}
console.log(baz.length);  // 2
```

### name 프로퍼티

> 💡 함수 이름을 나타냄

- ES5와 ES6에서 동작을 달리함
- 익명 함수 표현식의 경우, `ES5`에서는 name 프로퍼티는 `빈 문자열을 값`으로 가짐
- 익명 함수 표현식의 경우, `ES6`에서는 함수 객체를 가리키는 `식별자를 값`으로 가짐

```javascript
// 기명 함수 표현식
var namedFunc = function foo() {};
console.log(namedFunc.name); // foo

// 익명 함수 표현식 
var anonymousFunc = function() {};
// ES5: 빈 문자열을 값으로 가짐
// ES6: 함수 객체를 가리키는 변수 이름을 값으로 가짐
console.log(anonymousFunc.name); // anonymousFunc

// 함수 선언문
function bar() {}
console.log(bar.name);  // bar
```

### __proto__ 접근자 프로퍼티

> 💡 `[[Prototype]]` 내부 슬롯이 가리키는 `프로토타입 객체에 접근`하기 위해 사용하는 `접근자 프로퍼티`

- `모든 객체`는 `[[Prototype]]` 내부 슬롯을 가지며` 객체지향 프로그래밍의 상속을 구현하는 프로토타입 객체`를 가리킴
- 내부 슬롯에는 직접 접근할 수 없고 간접적인 접근 방법을 제공하는 경우에 한해 접근 가능

```javascript
const obj = { a : 1 };

// 객체 리터럴 방식으로 생성한 객체의 프로토타입 객체는 Object.prototype
console.log(obj.__proto__ === Object.prototype);  // true

// 객체 리터럴 방식으로 생성한 객체는 프로토타입 객체인 Object.prototype의 프로퍼티를 상속 받음
console.log(obj.hasOwnProperty('a'));         // true
console.log(obj.hasOwnProperty('__proto__'))  // false
```

### prototype 프로퍼티

> 💡 생성자 함수로 호출할 수 있는 객체, 즉 `constructor 소유하는 프로퍼티`

- portotype 프로퍼티는 함수가 객체를 생성하는 `생성자 함수로 호출될 때` 생성자 함수가 생성할 `인스턴스의 프로토타입 객체`를 가리킴
- 일반 객체와 생성자 함수로 호출할 수 없는 non-constructor prototype 프로퍼티가 없음

```javascript
// 함수 객체는 prototype 프로퍼티를 소유
(function () {}).hasOwnProperty('prototype'); // true

// 일반 객체는 prototype 프로퍼티를 소유하지 않음
({}).hawOwnProperty('prototype');             // false
```