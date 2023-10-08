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

### __proto__ 접근자 프로퍼티
### prototype 프로퍼티