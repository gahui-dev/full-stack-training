# 객체 리터럴

## 객체란

> 💡 자바스크립트는 `객체기반의 프로그래밍 언어`이며, `원시 값을 제외한 나머지 값(함수, 배열, 정규 표현식 등)`은 모두 `객체`

- 원시 타입 : 단 하나의 값만 나타내고 변경 불가능한 값
- `객체 타입` : 다양한 타입의 값을 하나의 단위로 구성한 복합적인 `자료구조`이며 `객체`는 `변경 가능한 값`

```javascript
// 객체는 0개 이상의 프로퍼티로 구성된 집합이며, 프로퍼티는 키(Key)와 값(Value)으로 구성
var person = {
  // 프로퍼티 키 : name, age
  // 프로퍼티 값 : 'Lee', 20
  name: 'Lee', // 프로퍼티
  age: 20      // 프로퍼티
}
```

- 객체는 `프로퍼티`와 `메서드`로 구성된 집합체(`상태와 동작을 하나의 단위로 구조화`)
  - `프로퍼티` : 객체의 상태를 나타내는 값(data)
  - `메서드` : 프로퍼티(상태 데이터)를 참조하고 조작할 수 있는 동작
- 자바스크립트에서 사용할 수 있는 모든 값은 프로퍼티 값이 될 수 있음
  - 자바스크립트의 함수는 `일급 객체`이므로 `값으로 취급`할 수 있음
  - 따라서 함수도 프로퍼티 값이며, `프로퍼티 값이 함수`일 경우 일반 함수와 구분하기 위해 `메서드`라 부름


```javascript
var counter = {
  num: 0,                // 프로퍼티
  increase: function() { // 메서드
    this.num++;
  }
}
```

<br />

## 객체 생성

> 💡 자바스크립트는 `프로토타입 기반`의 `객체 지향 언어`

- 자바스크립트는 클래스 기반 객체지향 언어와는 달리 `다양한 객체 생성 방법` 지원
  1. `객체 리터럴`
  2. Object 생성자 함수
  3. 생성자 함수
  4. Object.create 메서드
  5. 클래스(ES6)

### 객체 리터럴을 사용한 객체 생성

- 객체 리터럴은 `중괄호({...})` 내에 `0개 이상의 프로퍼티 정의`
- `변수에 할당되는 시점`에 자바스크립트 엔진은 `객체 리터럴을 해석해 객체 생성`
- 객체 리터럴의 중괄호는 코드 블록이 아니므로 `세미콜론`을 붙임

```javascript
var person = {
  name: 'Lee',
  sayHello: function() {
    conosle.log(`hello~ My name is ${this.name}`);
  }
}
console.log(typeof person); // object
console.log(person); // {name: "Lee", sayhellof: f}

var empty = {}; // 빈 객체
console.log(empty); // object
```

<br />

## 프로퍼티

> 💡 `객체`는 `프로퍼티의 집합`, 프로퍼티는 `키`와 `값`으로 구성

- `프로퍼티 키(key)` : 빈 문자열을 포함하는 `모든 문자열` 또는 `심벌 값`
- `프로퍼티 값(value)` : 자바스크립트에서 사용할 수 있는 모든 값 
- 프로퍼티 키는 프로퍼티 값에 접근할 수 있는 이름으로서 `식별자 역할`
- `식별자 네이밍 규칙`을 준수하는 프로퍼티 키 사용 권장
  ```javascript
  // 식별자 네이밍 규칙을 따르지 않는 이름에는 반드시 따옴표 사용
  var person = {
    firstName: 'Ga-hee', // 식별자 네이밍 규칙을 준수하는 프로퍼티 키
    'last-name': 'Lee'   // 식별자 네이밍 규칙을 준수하지 않은 프로퍼티 키
  }
  ```
- 문자열 또는 문자열로 평가할 수 있는 `표현식`을 사용해 `프로퍼티 키를 동적으로 생성`할 수 있음
  ```javascript
  var obj = {};
  var key = 'hello';

  // ES5: 프로퍼티 키 동적 생성
  obj[key] = 'world';
  // ES6: 계산된 프로퍼티 이름
  var obj = { [key] : 'world' };
  console.log(obj); // {hello: "world"}
  ```
- 프로퍼티 키에 `숫자 리터럴`을 사용하면 따옴표는 붙지 않지만 `내부적으로 문자열`로 반환
  ```javascript
  var foo = {
    0: 1,
    1: 2,
    2: 3
  }
  console.log(foo); // {0: 1, 1: 2, 2: 3}
  ```
- 이미 존재하는 프로퍼티 키를 `중복 선언`하면 `나중에 선언한 프로퍼티`가 먼저 선언한 프로퍼티를 덮어씀
  ```javascript
  var foo = {
    name: 'Lee',
    name: 'Kim'
  }
  console.log(foo); // {name: "Kim"}
  ```
- 빈 문자열을 프로퍼티 키로 사용해도 에러가 발생하지 않지만 의미를 갖지 못하므로 권장하지 않음
- var, function과 같은 예약어를 프로퍼티 키로 사용해도 에러가 발생하지 않지만 예상치 못한 에러가 발생할 여지가 있으므로 권장하지 않음

<br />

## 메서드

> 💡 프로퍼티 값이 함수일 경우 일반 함수와 구분하기 위해 `메서드(객체에 묶여있는 함수 의미)`라 부름

```javascript
var circle = {
  reaiuds: 5, // 프로퍼티
  getDiamter: function () { // 메서드
    return 2 * this.radius; // this는 circle을 가리킴
  }
  console.log(circle.getDiamter()); // 10
}
```

<br />

## 프로퍼티 접근

> 💡 `마침표 표기법(dot notation)`과 `대괄호 표기법(bracket notation)`이 있음

- `마침표 표기법` : 마침표 프로퍼티 접근 연산자(.) 사용
- `대괄호 표기법` : 대괄호 프로퍼티 접근 연산자([...]) 사용
  - 대괄호 프로퍼티 접근 연산자 내부에 지정하는 프로퍼티 키는 반드시 `따옴표로 감싼 문자열`
  - 따옴표로 감싸지 않은 이름을 프로퍼티 키로 사용하면 자바스크립트 엔진은 `식별자`로 해석
  - 프로퍼티 키가 `식별자 네이밍 규칙을 준수하지 않는 이름`이라면 반드시 대괄호 표기법 사용
- 객체에 존재하지 않는 프로퍼티에 접근하면 `undfined 반환`
  - ⭐ ReferenceError가 발생하지 않는 것에 주의

```javascript
var person = {
  name: 'Lee'
};

console.log(person.name);     // 마침표 표기법에 의한 프로퍼티 접근
console.log(person['name']);  // 대괄호 표기법에 의한 프로퍼티 접근
console.log(person[name]);    // ReferenceError: name is not defined
console.log(person.age);      // undefined
```

<br />

## 프로퍼티 값 갱신, 동적 생성, 삭제

- `프로퍼티 값 갱신` : 이미 존재하는 프로퍼티에 값을 할당하면 프로퍼티 값 갱신
- `프로퍼티 동적 생성` : 존재하지 않는 프로퍼티에 값을 할당하면 동적으로 생성되어 추가되고 값이 할당됨
- `프로퍼티 삭제` : `delete 연산자`는 객체의 프로퍼티를 삭제

```javascript
var person = {
  name: 'Lee'
}

// 프로퍼티 값 갱신
person.name = 'Kim'
console.log(person); // {name: "Kim"}

// 프로퍼티 동적 생성
person.age = 20;
console.log(person); // {name: "Kim", age: 20}

// 프로퍼티 삭제
// 존재하지 않는 프로퍼티를 삭제해도 에러 없이 무시됨
delete person.age;
delete person.address;
conosle.log(person); // {name: "Kim"}
```

<br />

## ES6에서 추가된 객체 리터럴의 확장 기능

### 프로퍼티 축약 표현

> 💡 프로퍼티 값으로 변수를 사용하는 경우 `변수 이름`과 `프로퍼티 키`가 `동일한 이름`일 때 `프로퍼티 키 생략 가능`

```javascript
let x = 1, y =2;

const obj = {x, y};
console.log(obj); // {x: 1, y: 2}
```

### 계산된 프로퍼티 이름

> 💡 `객체 리터럴 내부`에서도 계산된 `프로퍼티 이름`으로 프로퍼티 키를 `동적 생성` 가능

```javascript
const prefix = "prop";
let i = 0;
var obj ={};

// ES5 객체 리터럴 외부에서 대괄호 표기법을 사용해야 했음
// ES6 객체 리터럴 내부에서 계산된 프로퍼티 이름으로 프로퍼티 키를 동적 생성
const obj = {
  [`${prefix}-${++i}`]: i,
  [`${prefix}-${++i}`]: i,
  [`${prefix}-${++i}`]: i,
};

console.log(obj); // {prop-1: 1, prop-2: 2, prop-3: 3 }
```

### 메서드 축약 표현

> 💡 메서드를 정의할 때 `function 키워드 생략 가능`

```javascript
const obj = {
  name: 'Lee',
  sayHi() {
    console.log('Hi ' + this.name);
  }
};

obj.sayHi(); // Hi! Lee
```
