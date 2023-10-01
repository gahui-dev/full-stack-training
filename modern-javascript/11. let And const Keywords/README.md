# let, const 키워드와 블록 레벨 스코프

## var 키워드 문제점

- `변수 중복 선언 허용`
- `함수 레벨 스코프`
  - 오로지 함수의 코드 블록만을 지역 스코프로 인정
  - 코드 블록(if, for문 등) 내에서 선언해도 모두 전역 변수
- `변수 호이스팅`
  - 변수 선언문 이전에 참조할 수 있음
  - `선언 단계`와 `초기화 단계`가 한번에 진행
  - 할당문 이전에 변수를 참조하면 언제나 undefined 반환

## let 키워드

> 💡 `var 키워드의 단점을 보완`한 ES6의 새로운 키워드

### 변수 중복 선언 금지

```javascript
var foo = 123;
// var 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언 허용
// 아래 변수 선언문은 자바스크립트 엔진에 의해 var 키워드가 없는 것처럼 동작
var foo = 456;

let bar = 123;
// let이나 const 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용하지 않음
let bar = 456; // SyntaxError: Identifier 'bar' has already been declared
```

### 블록 레벨 스코프

- `모든 코드 블록`(함수, if, for, while, try/catch문 등)을 `지역 스코프로 인정`하는 블록 레벨 스코프를 따름

```javascript
let foo = 1; // 전역 변수

{
  let foo = 2; // 지역 변수
  let bar = 3; // 지역 변수
}

console.log(foo); // 1
console.log(bar); // ReferenceError: bar is not defined
```

### 변수 호이스팅

- let 키워드로 선언한 변수는 변수 호이스팅이 발생하지 않는 것처럼 동작
- `선언 단계`와 `초기화 단계`가 분리되어 진행
- 스코프의 시작 지점부터 초기화 단계 시작 지점(변수 선언문)까지 변수를 참조할 수 없음
  - `일시적 사각지대` : 스코프의 시작 지점부터 초기화 시작 지점까지 변수를 참조할 수 없는 구간

```javascript
// 런타임 이전에 선언 단계 실행. 아직 변수가 초기화되지 않음
// 초기화 이전의 일시적 사각지대에서는 변수 참조 불가능

console.log(foo); // ReferenceError: foo is not defined

let foo; // 변수 선언문에서 초기화 단계 실행
console.log(foo); // undefinned

foo = 1; // 할당문에서 할당 단계 실행
console.log(foo); // 1
```

### 전역 객체와 let

- var 키워드로 선언한 전역 변수와 전역 함수, 선언하지 않은 변수에 값을 할당한 암묵적 전역은 전역 객체 window의 프로퍼티가 됨
- `let 키워드`로 선언한 전역 변수는 `전역 객체의 프로퍼티가 아님`
- `let 전역 변수`는 `보이지 않는 개념적인 블록`(전역 렉시컬 환경의 선언적 환경 레코드) 내에 `존재`

```javascript
var x = 1;
console.log(window.x); // 1
console.log(x); // 1

// let, const 키워드로 선언한 전역 변수는 전역 객체 window의 프로퍼티가 아님
let y = 1;
console.log(window.y); // undefined
console.log(y); // 1
```

<br />

## const 키워드

> 💡 `상수`를 선언하기 위해 사용

### 선언과 초기화

- const 키워드로 선언한 변수는 `반드시 선언과 동시에 초기화` 해야함
- let 키워드와 마찬가지로 블록 레벨 스코프를 가짐
- 변수 호이스팅이 발생하지 않는 것처럼 동작

```javascript
{
  // 변수 호이스팅이 발생하지 않는 것처럼 동작
  console.log(foo); // ReferenceError: Cannot access 'foo' before initialization
  const foo = 1;
  console.log(foo); // 1
}

// 블록 레벨 스코프를 가짐
console.log(foo); // ReferenceERror: foo is not defined
```

### 재할당 금지

- const 키워드로 선언한 변수는` 재할당이 금지`됨

### 상수

- const 키워드로 선언한 변수에 `원시 값을 할당`한 경우 변수 값을 변경할 수 없음
  - `원시 값`은 `변경 불가능한 값`이므로 재할당 없이 값을 변경할 수 있는 방법이 없기 때문
  - 이러한 특징으로 인해 `const 키워드`를 `상수를 표현`하는데 사용

```javascript
// 세전 가격
let preTaxPrice = 100;

// 세후 가격
// 0.1의 의미를 명확히 알기 어렵기 때문에 가독성이 좋지 않음
let afterTaxPrice = preTaxPrice + preTaxPrice * 0.1;
console.log(afterTaxPrice); // 110
```

- 프로그램 전체에서 공통적으로 사용하므로 유지보수 측면에서도 좋음
- 상수의 이름은 대문자로 선언, 스네이크 케이스 표현

```javascript
// 세율을 의미하는 0.1 은 변경할 수 없는 상수로 사용
// 변수 이름을 대문자로 선언해 상수임을 명확히 표현
const TAX_RATE = 0.1;

// 세전 가격
let preTaxPrice = 100;

// 세후 가격
let afterTaxPrice = preTaxPrice + preTaxPrice * TAX_RATE;
console.log(afterTaxPrice); // 110
```

### const 키워드와 객체

- `const 키워드`로 선언된 변수에 `객체를 할당`한 경우 `값 변경 가능`
- 변경 불가능한 값인 원시 값은 재할당 없이 변경할 수 있는 방법이 없지만 변경 가능한 값인 `객체는 재할당 없이도 직접 변경이 가능`하기 때문
- ⭐ const 키워드는 재할당을 금지할 뿐 `불변`을 의미하는 것이 아님
  - 프로퍼티 동적 생성, 삭제, 프로퍼티 값의 변경을 통해 `객체를 변경하는 것 가능`
  - 객체가 변경되더라도 변수에 할당된 `참조 값은 변경되지 않음`

```javascript
const person = {
  name: 'Lee',
};

person.name = 'Kim';
console.log(person); // {name: "kim"}
```

## var vs let vs const

> 💡 변수 선언에는 `기본적으로 const를 사용`하며 `let은 재할당이 필요한 경우`에 한정해 사용

- ES6를 사용한다면 var 키워드는 사용하지 않음
- `재할당이 필요한 경우`에 한정해 `let 키워드`를 사용
  - 이때 변수의 스코프는 최대한 좁게 만든다.
- 변경이 발생하지 않고 읽기 전용으로 사용하는(재할당이 필요 없는 상수) `원시 값`과 `객체`에는 `const 키워드`를 사용
  - const 키워드는 재할당을 금지하므로 var, let 키워드보다 안전
