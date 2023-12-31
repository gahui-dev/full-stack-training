# 변수(Variable)

## 변수란?

> 💡 `변수(Variable)`란 하나의 값을 저장하기 위해 확보한 메모리 공간 자체 또는 그 `메모리 공간을 식별하기 위해 붙인 이름`

```javascript
// 변수명 = result
// 변수 값 = 30
let result = 10 + 20;
```

- `할당(Assignment), 대입, 저장` = 변수에 값을 저장하는 것
- `참조(Reference)` = 변수에 저장된 값을 읽어 들이는 것

<br />

## 식별자 (Identifier)

> 💡 식별자는 어떤 값을 구별해서 식별할 수 있는 고유한 이름

- 식별자는 값이 저장되어 있는 `메모리 주소와 매핑 관계`를 맺으며, `매핑 정보도 메모리에 저장`되어야 함
- 식별자는 값이 아니라 `메모리 주소를 기억`
- 식별자가 기억하고 있는 `메모리 주소를 통해 메모리 공간에 저장된 값에 접근`할 수 있다는 의미
- 즉, 메모리 주소에 붙인 이름
- 메모리 상에 존재하는 어떤 값을 식별할 수 있는 이름은 모두 식별자라고 함 
  - 변수, 함수, 클래스 등의 이름은 모두 식별자

<br />

## 변수 선언 (Variable Declaration)

> 💡 변수 선언이란, `메모리 공간을 확보(allocate)`하고 `변수 이름`과 확보된 메모리 공간의 `주소를 연결(Name Binding)`해서 값을 저장할 수 있게 준비하는 것

- 변수를 사용하려면 반드시 선언이 필요
- var, let, const 키워드를 사용

```javascript
// 변수 선언(변수 선언문)
// 변수 이름을 등록하고 값을 저장할 메모리 공간을 확보한 후 아직 변수에 값을 할당하지 않음

var score;
```

- 변수 선언으로 확보된 메모리 공간에는 자바스크립트 엔진에 의해 `undefined`라는 값이 암묵적으로 할당되어 초기화됨(자바스크립트의 독특한 특징)
  1. `선언 단계` : 변수 이름을 등록해 자바스크립트 엔진에 변수의 존재를 알림
  2. `초기화 단계` : 값을 저장하기 위한 메모리 공간을 확보하고 암묵적으로 `undefined`를 할당해 초기화
- 변수뿐만 아니라 `모든 식별자`(함수, 클래스 등)를 사용하려면 `반드시 선언`이 필요

<br />

## 변수 선언의 실행 시점과 변수 호이스팅

> 💡 `변수 호이스팅(Variable Hoisting)`이란 변수 선언문이 코드의 선두로 `끌어 올려진 것처럼 동작`하는 특징

```javascript
// undefined
// 변수 선언이 런타임이 아니라 그 이전 단계에서 먼저 실행되기 때문
console.log(score);

// 변수 선언문
var score;
```

1. 자바스크립트 엔진은 소스코드를 순차적으로 실행하기에 앞서 먼저 `소스코드의 평가 과정`을 거치면서 소스코드를 실행하기 위한 준비를 함
2. 소스코드의 평가 과정에서 자바스크립트 엔진은 변수 선언을 포함한 모든 `선언문(변수, 함수 선언문 등)`을 소스코드에서 찾아내 `먼저 실행`
- 즉, 변수 선언이 소스코드의 어디에 있든 상관없이 다른 코드보다 먼저 실행

<br />

## 값의 할당

> 💡 `값의 할당`은 소스코드가 순차적으로 실행되는 시점인 `런타임`에 실행

```javascript
var score;   // 변수 선언
score = 80;  // 값의 할당
```

```javascript
var score = 80;  // 변수 선언과 값의 할당
```

- 두 코드는 정확히 동일하게 동작
- 즉, 자바스크립트 엔진은 변수 선언과 값의 할당을 하나의 문으로 단축 표현해도 `변수 선언`과 `값의 할당`을 2개의 문으로 나누어 `각각 실행`

<br />

```javascript
console.log(score); // undefined

var score;   // 1. 변수 선언
score = 80;  // 2. 값의 할당

console.log(score);  // 80
```

1. 변수 선언 : `런타임 이전에 먼저 실행`
2. 값의 할당 : `런타임에 실행`
- _`score`_ 변수에 값을 할당하는 시점(2)에는 이미 변수 선언이 완료된 상태, `undefined`로 초기화 되어 있음
- 따라서 _`score`_ 변수에 값을 할당하면 _`score`_ 변수의 값은 undefined에서 새롭게 할당한 숫자 값  _`80`_ 으로 변경(재할당)
- ⭐변수에 값을 할당할 때는 이전 값 undefined가 저장되어 있던 메모리 공간을 지우고 그 메모리 공간에 할당 값을 새롭게 저장하는 것이 아니라 `새로운 메모리 공간을 확보`하고 그곳에 할당 값 `80`을 저장

<br />

## 값의 재할당

> 💡 `재할당`이란 이미 값이 할당되어 있는 변수에 `새로운 값을 또다시 할당`하는 것

```javascript
var score = 80;  // 변수 선언과 값의 할당
score = 90;      // 값의 재할당
```

- `var 키워드`로 선언한 변수는 `선언과 동시에 undefined로 초기화`되기 때문에 `엄밀히 말하면` 변수에 처음 값을 할당하는 것도 사실 `재할당`
- 변수에 값을 `재할당`하면 해당 메모리 공간을 지우고, 그 메모리 공간에 재할당 값을 저장하는 것이 아닌 `새로운 메모리 공간을 확보`하고 그 메모리 공간에 값을 저장한다.

<br />

## 가비지 콜렉터

> 💡 `가비지 콜렉터`는 애플리케이션이 할당한 메모리 공간을 주기적으로 검사하여 `더 이상 사용되지 않는 메모리를 해제`하는 기능

- 자바스크립트는 가비지 콜렉터를 내장하고 있는 `매니지드 언어`로서 `메모리 누수 방지`
- 불필요한 값들은 가비지 콜렉터에 의해 메모리에서 `자동 해제`되며, 언제 해결될지는 예측할 수 없음

<br />

## 식별자 네이밍 규칙

> 💡 `변수, 함수` 카멜 케이스(camelCase)

> 💡 `생성자 함수, 클래스` 파스칼 케이스(PascalCase)


- 식별자는 특수문자를 제외한 문자, 숫자, 언더스코어(_), 달러 기호($)를 포함할 수 있음
- 단, 식별자는 특수문자를 제외한 문자, 언더스코어(_), 달러 기호($)를 시작해야 함
- 숫자로 시작하는 것은 허용하지 않음
- 예약어는 식별자로 사용할 수 없음
- 대소문자를 구분함

```javascript 
// 카멜 케이스(camelCase)
var firstName;

// 스네이크 케이스(snake_case)
var first_name;

// 파스칼 케이스(PascalCase)
var FirstNmae;

// 헝가리언 케이스(typeHungarianCase
// type + identifier
var strFirstName;
// DOM 노드
var $elem = document.getElementById('myId');
// RxJS 옵저버블
var observable$ = fromEvent(document, 'click'); 
```
