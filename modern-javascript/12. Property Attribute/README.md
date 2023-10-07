# 프로퍼티 어트리뷰트

## 내부 슬롯과 내부 메서드

> 💡 자바스크립트 엔진의 `구현 알고리즘`을 설명하기 위해 ECMAScript 사양에서 사용하는 `의사 프로퍼티(pseudo property)`와 `의사 메서드(pseudo method)`

- `[[...]]`와 같은 `이중 대괄호`로 감싼 이름들이 `내부 슬롯`과 `내부 메서드`
- 자바스크립트 엔진의 내부 로직이므로 원칙적으로 직접적으로 접근하거나 호출할 수 있는 방법을 제공하지 않음
- 단, 일부 내부 슬롯과 내부 메서드에 한해 `간접적으로 접근`할 수 있는 수단 제공
  - 예를 들어 `모든 객체`는 `[[Prototype]]` 내부 슬롯을 가지며 `__proto__`를 통해 간접 접근 가능

```javascript
const o = {};

// 내부 슬롯은 자바스크립트 엔진의 내부 로직이므로 직접 접근할 수 없음
o.[[Prototype]]; // Uncaught SyntaxError: Unexpected token '['

// 단, 일부 내부 슬롯과 내부 메서드에 한하여 간적접으로 접근할 수 있는 수단 제공
o.__proto__; // -> Object.prototype
```

<br />

## 프로퍼티 어트리뷰트와 프로퍼티 디스크립터 객체

> 💡 자바스크립트 엔진은 프로퍼티를 `생성`할 때 `프로퍼티의 상태`를 나타내는 `프로퍼티 어트리뷰트`를 `기본값`으로 `자동 정의`

- `프로퍼티 상태` : 프로퍼티의 값, 값의 갱신 가능여부, 열거 가능 여부, 재정의 가능 여부
- `내부 슬롯`: [[Value]], [[Writable]], [[Enumerable]], [[Configurable]]
- Object.getOwnPropertyDescriptor 메서드를 사용하여 간적접으로 확인

```javascript
const person = {
  name: 'Lee';
}

// 프로퍼티 어트리뷰트 정보를 제공하는 프로퍼티 디스크립터 객체 반환
console.log(Object.getOwnPropertyDescriptor(Person, 'name'));
// {value: "Lee", writable: true, enumerable: true, configurable: true}

// 프로퍼티 동적 생성
person.age = 20;
console.log(Object.getOwnPropertyDescriptor(Person));
// name : {value: "Lee", writable: true, enumerable: true, configurable: true},
// age : {value: 20, writable: true, enumerable: true, configurable: true},
```

<br />

## 데이터 프로퍼티와 접근자 프로퍼티

> 💡 프로퍼티는 `데이터 프로퍼티`와 `접근자 프로퍼티`로 구분

- `데이터 프로퍼티(data property)` : `키와 값으로 구성`된 일반적인 프로퍼티
- `접근자 프로퍼티(accessor property)` : 자체적으로는 값을 갖지 않고 `다른 데이터 프로퍼티의 값을 읽거나 저장할 때 호출되는 접근자 함수로 구성`된 프로퍼티

### 데이터 프로퍼티

- [[Value]]
  - 프로퍼티 키를 통해 프로퍼티 `값`에 접근하면 반환되는 값
  - 프로퍼티 키를 통해 프로퍼티 값을 변경하면 [[Value]]의 값을 재할당
- [[Writable]]
  - 프로퍼티 `값의 변경 가능` 여부
  - 값이 false인 경우 해당 프로퍼티의 [[Value]] 값을 변경할 수 없는 읽기 전용 프로퍼티가 됨
- [[Enumerable]]
  - 프로퍼티의 `열거 가능` 여부
  - 값이 false인 경우 해당 프로퍼티는 for...in 문, Object.keys 메서드 등으로 열거할 수 없음
- [[configurable]]
  - 프로퍼티의 `재정의 가능` 여부
  - 값이 false인 경우 해당 프로퍼티의 삭제, 프로퍼티 어트리뷰트 값의 변경 금지
  - 단, [[Writable]]이 ture인 경우 [[Value]]와 [[Writable]]을 false로 변경하는 것은 허용

### 접근자 프로퍼티

- [[Get]]
  - 접근자 프로퍼티를 통해 데이터 프로퍼티의 값을 읽을 때 호출되는 접근자 함수
  - getter 함수가 호출되고 그 결과가 프로퍼티 값으로 반환
- [[Set]]
  - 접근자 프로퍼티를 통해 데이터 프로퍼티의 값을 저장할 때 호출되는 접근자 함수
  - setter 함수가 호출되고 그 결과가 프로퍼티의 값으로 저장
- [[Enumerable]], [[configurable]]
  - 데이터 프로퍼티와 동일

<br />

## 프로퍼티 정의

> 💡 Object.defineProperty 메서드를 사용하여 프로퍼티 어트리뷰트 정의

```javascript
// Object.defineProperty 메서드
// 인수 -> 객체의 참조, 데이터 프로퍼티 키 문자열, 프로퍼티 디스크립터 객체 전달

const person = {};

// 데이터 프로퍼티 정의
Object.defineProperty(person, 'firstName', {
  value: 'gahee',
  writable: true,
  enumerable: true,
  configurable: true
})

Object.defineProperty(person, 'lastName', {
  value: 'Lee',
})

let descriptor = Object.getOwnPropertyDescriptor(person, 'firstName');
console.log('firstName', descriptor);
// firstName {value: 'Gahee', writable: true, enumerable: true, configurable: true};

// 디스크립터 객체의 프로퍼티를 누락시키면 undefined, false가 기본값
descriptor = Object.getOwnPropertyDescriptor(person, 'lastName');
console.log('lastName', descriptor);
// lastName {value: 'Lee', writable: false, enumerable: false, configurable: false}

// 접근자 프로퍼티 정의
Object.defineProperty(person, 'fullName', {
  // getter 함수
  get() {
    return `${this.firstName} ${this.lastName}`;
  },
  set(name) {
    [this.firstName, this.lastName] = name.split(' ');
  },
  enumerable: true,
  configurable: true
});

descriptor = Object.getOwnPropertyDescriptor(person, 'fullName');
console.log('fullName', descriptor);
// fullName {get: f, set: f, enumerable: true, configurable: true}

person.fullName = 'Gahee Lee';
console.log(person); // {firstName: "Gahee", "Lee"};

// Object.defineProperties 메서드를 사용하면 여러 개의 프로퍼티 한 번에 정의
```

<br />

## 객체 변경 방지

> 💡 객체는 변경 가능한 값이므로 재할당 없이 직접 변경할 수 있음. 자바스크립트는 객체의 변경을 방지하는 다양한 메서드 제공

| 구분 | 메서드 | 프로퍼티 추가 | 프로퍼티 삭제 | 프로퍼티 값 읽기 | 프로퍼티 값 쓰기 | 프로퍼티 어트리뷰트 재정의 |
| --- | --- | --- | --- | --- | --- | --- | 
| 객체 확장 금지 | Object.preventExtensions | X | O | O | O | O |
| 객체 밀봉 | Object.seal | X | X | O | O | X |
| 객체 동결 | Object.freeze | X | X | O | X | X |


- `객체 확장 금지`
  - `객체 확장 금지`(프로퍼티 추가가 금지)
  - `Object.isExtensible` 메서드로 확인
- `객체 밀봉`
  - 프로퍼티 추가 및 삭제와 프로퍼티 어트리뷰트 재정의 금지(`읽기`와 `쓰기`만 가능)
  - `Object.isSealed` 메서드로 확인
- `객체 동결`
  - 프로퍼티 추가 및 삭제와 프로퍼티 어트리뷰트 재정의 금지, 프로퍼티 값 갱신 금지(`읽기`만 가능)
  - `Object.isFrozen` 메서드로 확인