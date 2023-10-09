# 프로토타입

> 💡 자바스크립트는 명령형, 함수형, `프로토타입 기반 객체지향 프로그래밍`을 지원하는 `멀티 패러다임 프로그래밍 언어`

- 원시 타입의 값을 제외한 나머지 값들`(함수, 배열, 정규 표현식)`은 모두 객체

## 객체지향 프로그래밍

> 💡 여러 개의 독립적 단위, 즉 `객체의 집합`으로 프로그램을 표현하려는 프로그래밍 패러다임

- 실체는 `특성이나 성질`을 나타내는 `속성(attribute/property)`을 가지며 이를 통해 실체를 인식하거나 구별
- `추상화(abstraction)` : 객체의 다양한 속성 중에서 `프로그램에 필요한 것`만 간추려 내어 표현하는 것
- 객체는 `상태 데이터`와 `동작`을` 하나의 논리적인 단위`로 묶은 `복합적인 자료구조`
  - 프로퍼티(property) : 상태 데이터
  - 메서드(method) : 동작

```javascript
// 이름과 주소 속성을 갖는 객체
const person = {
  name: 'Lee',
  address: 'Busan'
}

const circle = {
  // 원의 상태를 나타내는 데이터 -> 프로퍼티
  radius: 5,

// 원의 지름, 둘레, 넓이를 구하는 것은 동작 -> 메서드
  getDiamter() {
    return 2 * this.radius;
  }

  getPerimeter() {
    return 2 * Math.PI * this.radius;
  }

  getArea() {
    return Math.PI * this.radius ** 2;
  }
}
```

<br />

## 상속과 프로토타입

> 💡 상속은 `어떤 객체의 프로퍼티 또는 메서드를 다른 객체가 상속받`아 `그대로 사용`할 수 있는 것

- 자바스크립트는` 프로토타입을 기반`으로 `상속을 구현`하여 불필요한 중복 제거
- 예시)
  - '원'이란 객체에 대해, 각각의 원은 다른 반지름을 가질 수 있음
  - 원의 반지름이 달라도 원의 지름, 원주율, 원의 넓이를 구하는 방법은 동일
  - 따라서, `자신의 상태`은 `개별적으로 소유`하고, 내용이 `동일한 메서드`는 `상속을 통해 공유`하여 사용

```javascript
// 생성자 함수
function Circle(radius) {
  this.radius = radius;
}

// Circle 생성자 함수가 생성한 모든 인스턴스가 getArea 메서드를 공유해서 사용할 수 있도록 프로토타입에 추가
// 프로토타입은 Circle 생성자 함수의 prototype 프로퍼티에 바인딩 되어 있음
Circle.prototype.getArea = function() {
  return Math.PI * this.radius ** 2;
};

// 인스턴스 생성
// Circle 생성자 함수가 생성한 모든 인스턴스는 자신의 프로토타입,
// 즉 상위(부모)객체 역할을 하는 Circle.prototype의 모든 프로퍼티와 메서드 상속
const circle1 = new Circle(1);
const circle2 = new Circle(2);

console.log(circle1.getArea === circle2.getArea()); // true;
console.log(circle1.getArea());  // 3.141592653589793 
console.log(circle2.getArea());  // 12.566370614359172
```

<br />

## 프로토타입 객체

> 💡 `프로토타입 객체`란 객체지향 프로그래밍의 근간을 이루는 객체 간 `상속을 구현하기 위해 사용`

- `프로토타입`은 어떤 객체의 상위(부모) 객체의 역할을 하는 객체로서 `다른 객체에 공유 프로퍼티(메서드 포함)를 제공`
- 프로토타입을 `상속받은 하위(자식) 객체`는 상위 객체의 프로퍼티를 `자신의 프로퍼티`처럼 `자유롭게 사용`
- 모든 객체는 `[[Prototype]] 내부 슬롯`을 가지며 이 내부 슬롯의 값은 `프로토타입의 참조`
  - 객체가 생성될 때 객체 생성 방식에 따라 프로토타입이 결정되고 [[Prototype]]에 저장
  - 모든 객체는 `하나의 프로토타입`을 가지며 `모든 프로토타입은 생성자 함수와 연결`

### \_\_proto\_\_ 접근자 프로퍼티

> 💡 모든 객체는 `__proto__` 접근자 프로퍼티를 통해 자신의 프로토타입, 즉 [[Prototype]] 내부 슬롯에 간적접으로 접근할 수 있음

<b>`__proto__`는 접근자 프로퍼티</b>

- 내부 슬롯은 프로퍼티가 아니므로 자바스크립트는 직접적으로 접근하거나 호출할 수 있는 방법을 제공하지 않음
- 단, 일부 내부 슬롯과 내부 메서드에 한하여 간접적으로 접근할 수 있는 수단을 제공

```javascript  
const obj = {};
const aprent = { x: 1 };

// getter 함수인 get __proto__가 호출되어 obj 객체의 프로토타입 취득
obj.__proto__;

// setter 함수인 set __proto__가 호출되어 obj 객체의 프로토타입을 교체
obj.__proto__ = parent;  // 1

console.log(obj.x);
```

<b>`__proto__` 접근자 프로퍼티는 상속을 통해 사용</b>

- `__proto__` 접근자 프로퍼티는 객체가 직접 소유하는 프로퍼티가 아니라 Object.prototype의 프로퍼티
- 모든 객체는 상속을 통해 `Object.__proto__` 접근자프로퍼티를 사용할 수 있음

```javascript
const person = { name: 'Lee'};

// person 객체는 __proto__ 프로퍼티를 소유하지 않음
console.log(person.hasOwnProperty('__proto__')); // false

// __proto__ 프로퍼티는 모든 객체의 프로토타입 객체인 Object.prototype의 접근자 프로퍼티
console.log(Object.getOwnPropertyDescriptor(Object.prototype, '__proto__'));
// {enumerable: false, configurable: true, get: ƒ, set: ƒ}

// 모든 객체는 Object.prototype의 접근자 프로퍼티 __proto__를 상속받아 사용할 수 있음
console.log({}.__proto__ === Object.prototype); // true
```

<b>`__proto__` 접근자 프로퍼티를 통해 프로토타입에 접근하는 이유</b>

- `상호 참조`에 의해 `프로토타입 체인이 생성되는 것을 방지`하기 위해서임
- 아무런 체크없이 무조건적으로 프로토타입을 교체할 수 없도록 `__proto__` 접근자 프로퍼티를 통해 접근하고 교체하도록 구현
  - 프로토타입 체인은 `단방향 링크드 리스트`로 구현되어야 함(프로퍼티 검색 방향이 한쪽 방향으로만 흘러가야 함)
  - `순환 참조`하는 프로토타입 체인이 만들어지면 체인 종점이 존재하지 않기 때문에 프로토타입 체인에서 프로퍼티를 검색할 때 `무한 루프`에 빠짐

```javascript
const parent = {};
const child = {};

// child의 프로토타입을 parent로 설정
child.__proto__ = parent;
// parent의 프로토타입을 child로 설정
parent.__proto__ = child; // TypeError: Cyclic __proto__ value
```

<b>`__proto__` 접근자 프로퍼티를 코드 내에서 직접 사용하는 것은 권장하지 않음</b>

- 모든 객체가 `__proto__` 접근자 프로퍼티를 사용할 수 있는 것은 아님
- 직접 상속을 통해 다음과 같이 Object.prototype을 상속받지 않는 객체를 생성할 수도 있기 때문

```javascript
// obj.는 프로토타입 체인의 종점. 따라서 Object.__proto__를 상속받을 수 없음
const obj = Object.create(null);

// obj는 Object.__proto__를 상속받을 수 없음
console.log(obj.__proto__);  // undefiend

// 따라서 __proto__보다 Object.getPrototypeOf 메서드를 사용하는 편이 좋음
console.log(Object.getPrototypeOf(obj));
```

- `프로토타입의 참조`를 취득하고 싶은 경우 : `Object.getPrototypeOf` 메서드(= get Object.prototype.\_\_proto\_\_)
- `프로토타입을 교체`하고 싶은 경우 : `Object.setPrototypeOf` 메서드(= set Object.prototype.\_\_proto\_\_)

```javascript
const obj = {};
const parent = { x: 1};

// obj 객체의 프로토타입을 취득
Object.getPrototypeOf(obj);  // obj.__proto__;
// obj 객체의 프로토타입을 교체
Object.setPrototypeOf(obj, parent);  // obj.__proto__ = parent;

console.log(obj.x);  // 1
```

### 함수 객체의 prototype 프로퍼티

> 💡 함수 객체만이 소유하는 `prototype 프로퍼티`는 `생성자 함수가 생성할 인스턴스`의 `프로토타입`을 가리킴

- 생성자 함수로서 호출할 수 없는 함수`(non-constructor)`인 `화살표 함수`와 `ES6 메서드 축약 표현으로 정의한 메서드`는 `prototype 프로퍼티를 소유하지 않으며 프로토타입도 생성하지 않음`

```javascript
// 함수 객체는 prototype 프로퍼티를 소유
(function() {}).hasOwnProperty('prototype'); // -> true

// 일반 객체는 prototype 프로퍼티를 소유하지 않음
({}).hasOwnProperty('prototype'); // -> false

// 화살표 함수는 non-constructor
const Person = name => {
  this.name = name;
}

// non-constructor는 prototype 프로퍼티를 소유하지 않음
console.log(Person.hasOwnProperty('prototype')); // false

// non-constructor는 프로토타입을 생성하지 않음
console.log(Person.prototype); // undefiend

// ES6의 메서드 축약 표현으로 정의한 메서드는 non-constructor
const obj = {
  foo() {}
};

// non-constructor는 prototype 프로퍼티를 소유하지 않음
console.log(obj.hasOwnProperty('prototype')); // false

// non-constructor는 프로토타입을 생성하지 않음
console.log(obj.foo.prototype); // undefiend
```

- 생성자 함수로 호출하기 위해 정의하지 않은 `일반 함수(함수 선언문, 함수 표현식)`도 `prototype 프로퍼티를 소유`하지만 `객체를 생성하지 않는 일반 함수`의 `prototype은 아무런 의미가 없음`
- ⭐️ 모든 객체가 가지고 있는(Object.prototype으로부터 상속받은) `__proto__ 접근자 프로퍼티`와 `함수 객체`만이 가지고 있는 `prototype 프로퍼티`는 결국 `동일한 프로토타입`을 가리킴

| 구분 | 소유 | 값 | 사용 주체 | 사용 목적 |
| -- | -- | -- | -- | -- |
| `__proto__ 접근자 프로퍼티` | 모든 객체 | 프로토타입의 참조 | 모든 객체 | 객체가 자신의 프로토타입에 접근 또는 교체하기 위해 사용 |
| `prototype 프로퍼티` | constructor | 프로토타입의 참조 | 생성자 함수 | 생성자 함수가 자신이 생성할 객체(인스턴스)의 프로토타입을 할당하기 위해 사용 |

```javascript
// 생성자 함수
function Person(name) {
  this.name = name;
}

const me = new Person('Lee');

// 결국 Person.prototype과 me.__proto__는 결국 동일한 프로토타입을 가리킴
console.log(Person.prototype === me.__proto__); // ture
```

### 프로토타입의 constructor 프로퍼티와 생성자 함수

> 💡 `모든 프로토타입`은 `constructor 프로퍼티`를 가지며 prototype 프로퍼티로 `자신을 참조`하고 있는 `생성자 함수`를 가리킴

```javascript
function Person(name) {
  this.name = name;
}

const me = new Person('Lee');

// me 객체의 생성자 함수는 Person
console.log(me.constructor === Person);
```