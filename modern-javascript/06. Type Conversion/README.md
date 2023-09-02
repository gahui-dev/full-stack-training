# 타입 변환과 단축 평가

> 💡 `명시적 타입 변환(타입 캐스팅)`과 `암묵적 타입 변환(타입 강제 변환)`이 있음

## 암묵적 타입 변환

> 💡 자바스크립트 엔진이 표현식을 평가할 때 개발자의 의도와는 상관없이 `코드의 문맥을 고려해 암묵적`으로 데이터 타입을 `강제 변환`

- 암묵적 타입 변환이 발생하면 `문자열, 숫자, 불리언`과 같은 `원시타입` 중 하나로 타입을 자동 변환

### 문자열 타입으로 변환

```javascript
// 숫자 타입
NaN + '';             // "NaN"
Infinity + '';        // "Infinity"

// null 타입
null + '';            // "null"

// undefined 타입   
undefined + '';       // "undefined"

// 심벌 타입
(Symbol()) + '';      // TypeError: Cannot convert a Symbol value to a string

// 객체 타입
({}) + '';            // "[object Object]"
Math + '';            // "[object Math]"
[] + '';              // ""
[10, 20] + '';        // "10,20"
(function(){}_ + '';  // "function(){}"
Array + '';           // "function Array() { [native code] }"
```

### 숫자 타입으로 변환

- 빈 문자열(''), 빈 배열([]), null, false → 0
- true → 1
- ⭐ 객체, 빈 배열이 아닌 배열, undefined → NaN

```javascript
// 문자열 타입 
+""; // 0
+"0"; // 0
+"1"; // 1
+"string" // NaN

// 불리언 타입
true; // 1
+false; // 0

// null 타입
+null; // 0

// undefined 타입
+undefined; // NaN

// 심벌 타입
+Symbol(); // TypeError: Cannot convert a Symbol value to a number

// 객체 타입
+{}; // NaN
+[]; // 0
+[10, 20]; // NaN
+function () {}; // NaN
```

### 불리언 타입으로 변환

- `조건식의 평가 결과`를 `불리언 타입`으로 암묵적 타입 변환함
- 불리언 타입이 아닌 값을 `Truthy 값(참으로 평가되는 값)` 또는 `Falsy 값(거짓으로 평가되는 값)`으로 구분

```javascript
// 전달받은 인수가 Falsy 값이면 true, Truthy 값이면 false 반환
function isFalsy(v) {
  return !v;
}

// 전달받은 인수가 Truthy 값이면 true, Falsy 값이면 false 반환
function isTruthy(v) {
  return !!v;
}

// 자바스크립트 엔진이 false로 평가하는 Falsy 값
isFalsy(false);
isFalsy(undefined);
isFalsy(null);
isFalsy(0);
isFalsy(-0);
isFalsy(NaN);
isFalsy(''); // 빈 문자열

// Falsy 값을 제외한 모든 값은 Truthy 값
isTruthy(true);
isTruthy('0') // 빈 문자열이 아닌 문자열은 Truthy 값
isTruthy({});
isTruthy(([]));
```

<br />

## 명시적 타입 변환

> 💡 개발자의 `의도`에 따라 `명시적`으로 타입을 변경

- 표준 빌트입 생성자 함수(String, Number, Boolean)을 new 연산자 없이 호출하는 방법
- 빌트인 메서드를 사용하는 방법
- 암묵적 타입 변환

### 문자열 타입으로 변환

1. `String 생성자 함수`를 `new 연산자 없이` 호출하는 방법
2. `Object.prototype.toString` 메서드를 사용하는 방법
3. `문자열 연결 연산자(+)`를 이용하는 방법

```javascript
// 1. String 생성자 함수를 new 연산자 없이 호출하는 방법
// 숫자 타입 → 문자열 타입
String(1);              // "1"
String(NaN);            // "NaN"
String(Infinity);       // "Infinity"
// 불리언 타입 → 문자열 타입
String(true);           // "true"
String(false);          // "false"

// 2. Object.prototype.toString 메서드를 사용하는 방법
// 숫자 타입 → 문자열 타입
(1).toString();         // "1"
(NaN).toString();       // "NaN";
(Infinity).toString();  // "Infinity"
// 불리언 타입 → 문자열 타입
(true).toString();      // "true"
(false).toString();     // "false"

// 3. 문자열 연결 연산자를 이용하는 방법
1 + '';                 // "1"
```

### 숫자 타입으로 변환

1. `Number 생성자 함수`를 `new 연산자 없이` 호출하는 방법
2. `parseInt, parseFloat` 함수를 사용하는 방법(`문자열`만 변환 가능)
3. `단항 산술 연산자(+), 산술 연산자(*)`를 이용하는 방법

```javascript
// 1. Number 생성자 함수를 new 연산자 없이 호출하는 방법
// 문자열 타입 → 숫자 타입
Number("0");            // 0
Number("-1");           // -1
Number("10.53");        // 10.53
// 불리언 타입 → 문자열 타입
Number(true);           // 1
Number(false);          // 0

// 2. parseInt, parseFloat 함수를 사용하는 방법(문자열만 변환 가능)
parseInt("0");          // 0
parseInt("-1");         // -1
parseInt("10.53");      // 10
parseFloat("10.53");    // 10.53

// 3-1. + 단항 산술 연산자를 이용하는 방법
+'0';                   // 0
+'10.53';               // 10.53
+true;                  // 1
+false;                 // 0

// 3-2. * 산술 연산자를 이용하는 방법
'0' * 1;                // 0
'-1' * 1;               // -1
'10.53' * 1;            // 10.53
true * 1;               // 1
false * 1;              // 0
```

### 불리언 타입으로 변환

1. `Boolean 생성자 함수`를 `new 연산자 없이` 호출하는 방법
2. `! 부정 논리 연산자`를 `두 번` 사용하는 방법

```javascript
// 1. Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
// 문자열 타입 → 불리언 타입
Boolean('x');           // true
Boolean('');            // false
Boolean('false');       // true
// 숫자 타입 → 불리언 타입
Boolean(0);             // false
Boolean(1);             // true
Boolean(NaN);           // false
Boolean(Infinity);      // true
// null 타입 → 불리언 타입
Boolean(null);          // false
// undefined 타입 → 불리언 타입
Boolean(undefined);     // false
// 객체 타입 → 불리언 타입
Boolean({});            // true
Boolean([]);            // true

// 2. ! 부정 논리 연산자를 두번 사용하는 방법
!!'x';                  // true
!!'';                   // false
!!0;                    // false
!!Infinity;             // true
!!null;                 // false
!!undefined             // false
!!{};                   // true
!![];                   // true
```

<br />

## 단축 평가

> 💡 표현식을 `평가하는 도중`에 `평가 결과가 확정`된 경우 `나머지 평가 과정을 생략`하는 것

### 논리 연산자를 사용한 단축 평가

- `논리곱(&&) 연산자`는 두 개의 피연산자가 `모두 true`로 평가될 때 true 반환
- 논리 연산의 결과를 결정하는 `두 번째 피연산자` 반환
- `논리합(||) 연산자`는 두 개의 피연산자 중 `하나만 true`로 평가되어도 true 반환
- 논리 연산의 결과를 결정한 `첫 번째 피연산자` 반환

| 단축 평가 표현식 | 평가 결과 |
| -- | -- |
| true \|\| anything | ture |
| false \|\| anything | anything |
| true && anyting | anything |
| false && anything | false |

```javascript
// 논리곱(&&) 연산자
"Cat" && "Dog"; // "Dog"
false && "Dog"; // "false"
"Cat" && false; // "false"

// 논리합(||) 연산자
"Cat" || "Dog"; // "Cat"
false || "Dog"; // "Dog"
"Cat" || false; // "Cat"

// 조건이 Truthy 값일 때 논리곱(&&) 연산자 표현식으로 if문 대체 가능
var done = true;
var message = '';
// if(done) message = '완료';
message = done && "완료";

// 조건이 `Falsy 값`일 때 `논리합(||) 연산자 표현식`으로 `if문 대체 가능`
done = false;
// if(!done) message = '미완료';
message = done || "미완료";
```

### 단축 평가가 유용하게 사용되는 상황

1. `객체`를 가리키기를 기대하는 변수가 `null 또는 undefined가 아닌지 확인`하고 프로퍼티를 참조할 때
2. `함수 매개변수`에 `기본값`을 설정할 때

```javascript
// 1. null 또는 undefined인 경우 객체의 프로퍼티를 참조하면 타입 에러 발생 
var elem = null;
var value = elem.value // TypeError: Cannot read property 'value' of null

// elem이 null이나 undefined와 같은 Falsy 값이면 elem으로 평가
// elem이 Truty 값이면 elem.value로 평가
value = elem && elem.value; // null
```

```javascript
// 2. 함수를 호출할 때 인수를 전달하지 않으면 매개변수에는 undefined 할당
// 단축 평가를 사용해 매개변수의 기본값을 설정하면 에러를 방지할 수 있음
function getStringLength(str) {
  str = str || '';
  return str.length;
}
getStringLength(); // 0

// ES6의 매개변수의 기본값 설정
function getStringLength(str = '') {
  return str.length;
}
getStringLength(); // 0
```

### 옵셔널 체이닝 연산자`(?.)`

> 💡 객체를 가리키기를 기대하는 변수가 `null` 또는 `undefine가` 아닌지 `확인`하고 `프로퍼티를 참조`할 때 유용

- 좌항의 피연산자가 `null 또는 undefined`인 경우 `undefined 반환`
- 그렇지 않은 경우 `우항의 프로퍼티 참조`를 이어감

```javascript
var elem = null;
var value = elem?.value;
```

- `옵셔널 체이닝 연산자(?.)` 도입 이전에는 `논리 연산자(&&)`를 사용한 단축 평가를 통해 `null 또는 undefined인지 확인`
```javascript
var elem = null;
var value = elem && elem.value; // null
```

```javascript
var str = '';
// 피연산자가 Falsy 값이라도 null 또는 undefined가 아니면 우항의 프로퍼티를 참조
var length = str?.length;
console.log(length); // 0
```

### null 병합 연산자`(??)`

> 💡 변수에 기본값을 설정할 때 유용

- 좌항의 피연산자가 `null 또는 undefined`인 경우 `우항의 피연산자를 반환`
- 그렇지 않으면 `좌항의 피연산자 반환`

```javascript
var foo = null ?? 'default string';
console.log(foo) // "default string"
```

- `null 병합 연산자(??)` 도입 이전에는 `논리 연산자(||)`를 사용한 단축 평가를 통해 `변수에 기본값 저장`

```javascript
// Falsy 값인 0이나 ''도 기본값으로서 유효하다면 예기치 않은 동작 발생 가능
var foo = '' || 'default string';
console.log(foo); // "default string"

// 좌항의 피연산자가 Falsy 값이라도 null 또는 undefined가 아니면 좌항의 피연산자 반환
var foo = '' ?? 'default string';
console.log(foo); // ""
```