# 문자열, 배열 열거 타입

## 01. 문자열

### 문자열 선언과 생성

- `String` 타입의 변수 선언
- `String` 타입의 변수는 `큰따옴표("")`로 감싸서 나타낸 `문자열 리터럴`을 사용해서 초기화
- `String `타입은 자바가 기본으로 제공하는 `클래스`
  - 자바는 문자열 리터럴을 내부적으로 `String 객체`로 처리
  -` String 객체를 생성`하면 String 클래스의 `생성자 호출`
  - 문자열 리터럴은 내부적으로 `new String()`을 호출해 생성한 객체
  - ⭐ `내용이 같은` 문자열 리터럴이라면 `기존 리터럴` 공유


```java
String 변수; // String 타입의 변수 선언
변수 = "문자열"; // String 타입의 변수에 문자열 대입

String s1 = "안녕, 자바"; // String 타입의 변수 선언과 초기화
```

### 문자열 메서드

- 문자열 비교 메서드
  | 메서드 | 설명 |
  | -- | -- |
  | int compareTo(String s) | 문자열을 사전 순으로 비교해 정숫값 반환 |
  | int compareTolgnoreCase(String s) | 대·소문자를 무시하고, 문자열을 사전 순으로 비교 |
  | boolean equals(String s) | 주어진 문자열 s와 현재 문자열을 비교한 후 true/ false 반환 |
  | boolean equalsIgnoreCase(String s) | 주어진 문자열 s와 현재 문자열을 대소문자 구분 없이 비교한 후 true/false 반환 |

- 문자열 메서드
  | 메서드 | 설명 |
  | -- | -- |
  | char charAt(int index) | index가 지정한 문자열 반환 |
  | String concat(String s) | 주어진 문자열 s를 현재 문자열 뒤에 연결 |
  | boolean contains(String s) | 문자열 s를 포함하는지 조사 |
  | boolean endsWith(String s) | 끝나는 문자열이 s인지 조사 |
  | int indexOf(String s) | 문자열 s가 나타난 위치를 반환 |
  | boolean isBlank() | 길이가 0 혹은 공백 있으면 true 반환 |
  | boolean isEmpty() | 길이가 0 이면 true 반환 |
  | int length() | 길이를 반환 |
  | String repeat(int c) | c번 반복한 문자열 반환 |
  | boolean startsWith(String s) | 시작하는 문자열이 s인지 조사 |
  | String subsbring(int index) | index부터 시작하는 문자열의 일부를 반환 |
  | String toLowerCase() | 모두 소문자로 변환 |
  | String toUpperCase() | 모두 대문자로 변환 |
  | String trim() | 앞뒤에 있는 공백을 제거한 후 반환 |

<br />

## 02. 배열 

> 💡 `타입이 동일`한 여러 데이터의 `연속`된 기억 공간

### 배열의 선언과 생성

- 배열을 사용하기 위해 참조할 `변수를 선언`하고, `배열 객체`를 생성해야함
- `배열의 크기`는 배열이 `생성`될 때 정해지며, `length` 필드에 저장

```java
// 배열을 참조할 변수 선언
int[] scores1; 
int scores2[];
// 배열을 참조할 변수를 선언할 때는 배열 크기를 지정할 수 없음
int scores[5]; 

// 배열 객체 생성
// 선언과 동시에 초기화
int[] scores = new int[4];
// 방법 1
int[] scores = {100, 90, 85, 70};
// 방법 2
int[] scores = new int[] {100, 90, 85, 75};
// 방법 3
int[] scores;
scores = new int[] {100, 90, 85, 75};
```

### 배열 원소의 접근과 배열 크기

- `배열이름[인덱스]`로 접근
- 인덱스의 값은 `0`부터 시작해 양의 정수
- 마지막 인덱스는 배열 크기보다 `하나 작은 정수`가 됨

### 다차원 배열

```java
// 3행 5열 scores 배열 생성
int[][] scores = new int[3][5];
```