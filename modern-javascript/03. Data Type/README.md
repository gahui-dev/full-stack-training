# 데이터 타입(Data Type)

## 데이터 타입

> 💡 ES6는 `7개`의 데이터 타입을 제공하며 `원시타입`과 `객체타입`으로 분류

### 원시타입

| 데이터 타입          | 설명                                                |
| -------------------- | --------------------------------------------------- |
| 숫자(number) 타입    | 숫자. 정수와 실수 구분 없이 하나의 숫자 타입만 존재 |
| 문자열(string) 타입  | 문자열                                              |
| 불리언(boolean) 타입 | 논리적 참(true)과 거짓(false)                       |
| undefined 타입       | var 키워드로 선언된 변수에 암묵적으로 할당되는 값   |
| null 타입            | 값이 없다는 것을 의도적으로 명시할 때 사용하는 값   |
| 심벌(symbol) 타입    | ES6에서 추가된 7번째 타입                           |

### 객체 타입

- 객체, 함수, 배열 등

<br />

## 숫자 타입

> 💡 ECMAScript 사양에 따르면 `숫자 타입`의 값은 `배정밀도 64비트 부동소수점 형식`을 따름 => 모든 수를 `실수`로 처리

```javascript
// 모두 숫자 타입
var integer = 10; // 정수
var double = 10.12; // 실수
var negative = -20; // 음의 정수
```

> 💡 자바스크립트는 2진수, 8진수, 16진수를 표현하기 위한 데이터 타입을 제공하지 않기 때문에 모두 `10진수`로 해석

```javascript
var binary = 0b01000001; // 2진수
var octal = 0o101; // 8진수
var hex = 0x41; // 16진수

// 표기법만 다를 뿐 모두 같은 값
console.log(binary); //65
console.log(octal); //65
console.log(hex); //65
console.log(binary === octal); // true
console.log(octal === hex); // true
```

> 💡 정수로 표시된다 해도 사실은 실수

```javascript
// 숫자 타입은 모두 실수로 처리됨
console.log(1 === 1.0); //true
console.log(4 / 2); // 2
console.log(3 / 2); // 1.5
```

> 💡 숫자 타입은 추가적으로 세 가지 특별한 값을 표현할 수 있음

- `Infinity`: 양의 무한대
- `-Infinity`: 음의 무한대
- `NaN`: 산술 연산 불가(not-a-number)

```javascript
// 숫자 타입의 세 가지 특별한 값
console.log(1 / 0); // Infinity
console.log(10 / -0); // -Infinity
console.log(1 * 'string'); // NaN
```

<br />

## 문자열 타입

> 💡 `텍스트` 데이터를 나타내는데 사용, 0개 이상의 `16비트 유니코드 문자(UTF-16)의 집합`으로 전 세계 대부분의 문자 표현

- ` 작은따옴표(''), 큰따옴표(""), 백틱(``) `으로 텍스트를 감쌈
- 자바스크립트의 문자열은 `원시 타입`이며 `변경 불가능한 값`
  - C는 문자의 배열로 문자열을 표현하고, 자바는 문자열을 객체로 표현
  - 문자열이 생성되면 그 문자열을 변경할 수 없다는 것을 의미

```javascript
// 문자열 타입
var string;
string = '문자열'; // 작은따옴표
string = '문자열'; // 큰따옴표
string = `문자열`; // 백틱(ES6)
string = '작은 따옴표로 감싼 문자열 내의 "큰따옴표"는 문자열로 인식된다.';
string = "큰따옴표로 감싼 문자열 내의 '작은따옴표'는 문자열로 인식된다.";
```

## 템플릿 리터럴(template literal)

> 💡 `멀티라인 문자열`, `표현식 삽입`, `태그드 템플릿` 등 편리한 문자열 처리 기능 제공

- ` 백틱(``) `을 사용해 표현
- 템플릿 리터럴은 런타임에 일반 문자열로 변환되어 처리

### 멀티라인 문자열

> 💡 이스케이프 시퀀스를 사용하지 않고 `줄바꿈 허용`, 모든 `공백`도 있는 `그대로 적용`

```javascript
var template = `<ul>
	<li><a href="#">Home</a></li>
</ul>`;

// 결과
<ul>
  <li>
    <a href='#'>Home</a>
  </li>
</ul>;
```

### 표현식 삽입

> 💡 문자열 연산자 (+) 보다 가독성 좋고 간편하게 문자열 조합

- 표현식을 삽인하려면 `${}` 으로 표현식을 감쌈
- 이때 평가 결과가 문자열이 아니더라도 `문자열`로 타입이 `강제 변환`되어 삽입

```javascript
var first = 'Ga-hee';
var last = 'Lee';

// ES6: 표현식 삽입
console.log(`My name is ${first} ${last}.`); // My name is Ga-hee Lee.
```

<br />

## 불리언 타입

> 💡 논리적 `참, 거짓`을 나타내는 `true`와 `false` 뿐

<br />

## undefined 타입

> 💡 undefined 타입의 값은 `undefined`가 유일

- var 키워드로 `선언`한 변수는 암묵적으로 `undefined로 초기화` 됨
  - 변수 선언으로 확보된 메모리 공간을 처음 할당이 이뤄질 때까지 빈 상태(대부분 비어있지 않고 쓰레기 값이 들어있음)로 내버려두지 않고 자바스크립트 엔진이 undefined로 초기화
- 즉, 개발자가 `의도적으로 할당하기 위한 값이 아님`
- 변수에 값이 없다는 것을 명시하고 싶을 때는 `null`을 할당

```javascript
// 참조한 변수가 선언 이후,
// 값이 할당된 적이 없는 초기화되지 않은 변수
var foo;
console.log(foo); // undefined
```

<br />

## null 타입

> 💡 변수에 값이 없다는 것을 `의도적으로 명시(의도적 부재)`할 때 사용

- 변수에 `null`을 할당하는 것은 변수가 이전에 참조하던 값을` 더 이상 참조하지 않겠다`는 의미
- 이전에 할당되어 있던 값에 대한 `참조를 명시적으로 제거`하는 의미
- 자바스크립트 엔진은 누구도 참조하지 않는 메모리 공간에 대해 `가비지 콜렉션` 수행

```javascript
var foo = 'Lee';

// 이전 참조를 제거. foo 변수는 더 이상 'Lee'를 참조하지 않음
// 유용해 보이지는 않음. 변수의 스코프를 좁게 만들어 변수 자체를 재빨리 소멸시키는 편이 나음
foo = null;
```

- 함수가 유효한 값을 반환할 수 없는 경우 명시적으로 null을 반환하기도 함

```html
<!DOCTYPE html>
<html>
  <body>
    <script>
      // HTML 문서에 myClass 클래스를 갖는 요소가 없다면 null 반환
      var element = document.querySelector('.myObj');
      console.log(element); // null
    </script>
  </body>
</html>
```

<br />

## 심벌 타입

> 💡 변경 불가능한 `원시 타입`의 값

- 이름이 충돌할 위험이 없는 `객체의 유일한 프로퍼티 키`를 만들기 위해 사용
- `Symbol 함수`를 호출해 생성
- 외부에 노출되지 않으며, 다른 값과 절대 중복되지 않는 유일무이한 값

```javascript
// 심벌 값 생성
var key = Symbol('key');
console.log(typeof key); // symbol

// 객체 생성
var obj = {};

// 이름이 충돌할 위험이 없는 유일무이한 값인 심벌을 프로퍼티 키로 사용
obj[key] = 'value';
console.log(obj[key]);
```

<br />

## 객체 타입

> 💡 자바스크립트를 이루고 있는 거의 모든 것은 객체

<br />

## 데이터 타입의 필요성

### 데이터 타입에 의한 메모리 공간의 확보와 참조

> 💡 메모리에 값을 저장하려면 몇 바이트의 `메모리 공간을 사용`해야 `낭비와 손실 없이` 값을 저장할 수 있는 지 알아야 함

- ECMAScript 사양은 문자열과 숫자 타입 외의 데이터 타입의 크기를 명시적으로 규정하고 있지 않음
- 단, `숫자 타입`은 `배정밀도 64비트 부동소수점` 형식 사용
- 컴파일러 또는 인터프리터는 `심벌 테이블`이라 부르는 자료 구조를 통해 `식별자`를 `키로 바인딩된 값`의 `메모리 주소, 데이터 타입, 스코프 등`을 관리

### 데이터 타입에 의한 값의 해석

- 모든 값은 데이터 타입을 가지며, 메모리에 2진수, 즉 비트의 나열로 저장됨
- 메모리에 저장된 값은 `데이터 타입`에 따라 `다르게 해석`

### 데이터 타입이 필요한 이유

- 값을 저장할 때 확보해야 하는 `메모리 공간의 크기`를 결정하기 위해
- 값을 참조할 때 한 번 읽어 들여야 할 `메모리 공간의 크기`를 결정하기 위해
- 메모리에서 읽어 들인 `2진수를 어떻게 해석`할지 결정하기 위해

<br />

## 동적 타이핑

### 동적 타입 언어와 정적 타입 언어

> 💡 자바스크립트의 변수는 선언이 아닌 `할당에 의해` 타입이 `결정(타입 추론)`됨

- 재할당에 의해 변수의 타입은 언제든지 동적으로 변할 수 있음
- 정적 타입 언어(C, Java, 코틀린 등)과 구분하기 위해 `동적 타입 언어`라함
- 현재 변수에 `할당되어 있는 값`에 의해 변수의 타입이 `동적으로 결정`됨

### 동적 타입 언어와 변수

> 💡 유연성은 높지만 신뢰성을 떨어짐

- 변수 값은 언제든지 변경될 수 있기 때문에 복잡한 프로그램에서 변화하는 변수 값을 추적하기 어려울 수 있음
- 값의 변경에 의해 타입도 언제든지 변경될 수 있음
- 변수를 사용할 때 주의사항
  - 꼭 필요한 경우에 한해 `제한적`으로 사용
  - 변수의 `스코프`는 최대한 `좁게` 만들어 부작용 억제
  - 전역 변수는 최대한 사용하지 않기
  - 변수보다는 `상수`를 사용해 값 변경 억제
  - 변수 이름은 목적이나 의미를 파악할 수 있도록 네이밍
