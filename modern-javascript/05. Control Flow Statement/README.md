# 제어문(Control flow statement)

> 💡 `조건`에 따라 코드 블록을 실행(`조건문`)하거나 반복 실행(`반복문`)할 때 사용

## 블록문

> 💡 `하나의 실행 단위`로 `코드 블록` 또는 블록이라 함

- 단독으로 사용할 수 있으나 일반적으로 `제어문`이나 `함수를 정의`할 때 사용
- 세미콜론을 붙이지 않음

<br />

## 조건문

> 💡 주어진 `조건식의 평가 결과`에 따라 코드 블록(블록문)의 실행을 결정

- if...else 문 : 논리적 참, 거짓
- switch 문 : 다양한 상황

### if...else 문

> 💡 주어진 `조건식`의 평과 결과, 즉 `논리적 참 또는 거짓`에 따라 실행할 코드 블록 결정

- if 문의 조건식은 `불리언 값`으로 평가되어야 함
- 불리언 값이 아닐 경우 자바스크립트 엔진에 의해 암묵적으로 `불리언 값으로 강제 변환`

```javascript
if(조건식1) {
  // 조건식 1이 참이면 이 코드 블록 실행
} else if(조건식2) {
  // 조건식 2가 참이면 이 코드 블록 실행
} else {
  // 조건식1, 2가 모두 거짓이면 이 코드 블록 실행
}
```

### switch 문

> 💡 주어진 `표현식`을 평가하여 그 값과 일치하는 표현식을 갖는 `case 문으로 실행 흐름`을 옮김

- `default 문` : switch 문의 표현식과 일치하는 case 문이 없을 때 이동
- `break 문` : 코드 블록에서 `탈출`하는 역할
  - `폴스루(fall through)` : swtich 문을 탈출하지 않고 끝날 떄까지 이후의 모든 case 문과 default 문을 실행
  - default 문에는 생략하는 것이 일반적

```javascript
switch(표현식) {
  case 표현식1:
    switch 문의 표현식과 표현식1이 일치하면 실행될 문;
    break;
  case 표현식2:
    swtich 문의 표현식과 표현식2가 일치하면 실행될 문;
    break;
  default:
    switch 문의 표현식과 일치하는 case 문이 없을 때 실행될 문;
}
```

<br />

## 반복문

> 💡 `조건식`의 평가 결과가 `참`인 경우 코드 블록 실행하고, 그 후 `조건식이 거짓일 때까지` 반복

- 📝 반복문을 대체할 수 있는 다양한 기능 : forEach메서드, for...in문, for..of문 등이 있음

<br />

### for 문

> 💡 `조건식이 거짓으로 평가`될 때까지 코드 블록을 반복 실행

- `반복 횟수가 명확`할 때 주로 사용
- for문은 i (iteration을 의미) 변수를 사용하는 것이 일반적

```javascript
for(변수 선언문 또는 할당문; 조건식; 증감식) {
  조건식이 참인 경우 반복 실행될 문
}

// 1. for 문을 실행하면 변수 선언문 let i = 0 실행, 변수 선언문은 단 한번만 실행
// 2. 조건식 실행, 현재 i의 변수 값은 0 이므로 조건식 평과 결과 true
// 3. 평가 결과가 true 이므로 코드 블록 실행, (주의)증감문으로 실행 흐름 이동 X
// 4. 코드 블록의 실행이 종료되면 증감식 i++ 실행, i 변수 값 1
// 5. 다시 조건식 실행, 조건식 평가 결과 true 이므로 코드 블록 다시 실행 후 i 변수 값 2
// 6. 조건식의 평가 결과가 false 이므로 for 문 실행 종료
for(let i = 0; i < 2; i++) {
  console.log(i)
}
```

### while 문

> 💡 `조건식의 평가 결과가 참`이면 코드 블록을 반복 실행

- `반복 횟수가 불명확`할 때 주로 사용
- 조건문의 평가 결과가 거짓이 되면 코드 블록을 실행하지 않고 종료
- 조건식의 평가 결과가 불리언 값이 아니면 강제 변환하여 구별

```javascript
let count = 0;

while(count < 3) { // count가 3보다 작을 때 까지 코드 블록 반복 실행
  console.log(count);
  count++;
}

// 무한 루프
while(true) {
  conosle.log(count);
  count++;
  // 무한루프에서 탈출하기 위해 if 문으로 탈출 조건을 만들어 break 문으로 탈출
  if(count == 3) break; 
}
```

### do ... while 문

> 💡 `코드 블록을 먼저 실행`하고 조건식을 평가, 코드 블록은 무조건 한 번 이상 실행

```javascript
let count = 0;

do {
  console.log(count);
  count++;
} while(count < 3);
```

<br />

## break 문

> 💡 `레이블 문, 반복문, switch 문`의 코드 블록에서 `탈출`

- 반복문과 switch 문에서 사용하며 반복문을 더 이상 진행하지 않아도 될 때 불필요한 반복을 회피

  ```javascript
  let string = 'Hello world.';
  let search = 'l';
  let index;

  for(let i = 0; i < string.length; i++) {
    if(string[i] === search) {
      index = i;
      break; // 반복문 탈출
    }
  }
  console.log(index); //2
  console.log(string.indexOf(search)); // 참고
  ```


- `레이블 문` : `식별자`가 붙은 문
  - 프로그램의 `실행 순서를 제어`하는데 사용
  - 일반적으로 권장하지 않으며 가독성이 나빠지고 오류 발생 가능성이 높아짐

  ```javascript
  // foo 라는 식별자가 붙은 레이블 문
  // 레이블 문을 탈출하려면 break 문에 레이블 식별자 지정
  foo: {
    console.log(1);
    break foo; // foo 레이블 블록문을 탈출
    conosle.log(2);
  }
  console.log(Done!);
  ```

<br />

## continue 문

> 💡 `반복문`의 코드 블록을 현 지점에서 `중단`하고 `반복문의 증감식으로 실행 흐름 이동`

- break 문처럼 반복문을 탈출하지 않음

  ```javascript
    let string = 'Hello world.';
    let search = 'l';
    let count = 0;

    for(let i = 0; i < string.length; i++) {
      // 'l'이 아니면 현 지점에서 실행을 중단하고 반복문의 증감식으로 이동
      if(string[i] !== search) continue;
      count++; // continue 문이 실행되면 이 문은 실행되지 않음
    }

  // continue 문을 사용하지 않으면 if 문 내에 코드를 작성해야 함
    for(let i = 0; i <string.length; i++) {
      if(string[i] === search) {
        count++;
        // code ~
      }
    }

    // continue 문을 사용하면 if 문 밖에 코드를 작성할 수 있음
    for(let i = 0; i <string.length; i++) {
      if(string[i] !== search) continue;
      count++;
        // code ~
    }
    ```