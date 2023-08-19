## 01. 자바 프로그램 기본 구조

### 01-1. 자바 프로그램 기본 구조

- 소스 파일 = 클래스 > 메서드 > 실행문
- 클래스(class)
    - 객체 지향 언어에서 클래스는 프로그램을 개발하는 단위
    - 클래스 내부에는 여러 개의 메서드가 포함될 수 있음
- 메서드(method)
    - 수행할 작업을 나열한 코드의 모임
    - 자바 애플리케이션은 main() 메서드부터 실행을 시작
- 실행문(statement)
    - 작업을 지시하는 변수 선언, 값 저장, 메서드 호출 등의 코드를 의미
- 주석문
    - 프로그램에 덧붙이는 설명문으로 컴파일러가 무시하는 문장
    - 행 주석 ⇒ // 부터 행 끝까지를 주석으로 처리
    - 범위 주석 ⇒  /* 와 */ 사이를 주석으로 처리
    - 문서 주석 ⇒ /** 와 */ 사이를 주석으로 처리하되 javadoc.exe 명령어로 API 문서를 생성하는데 사용

## 02. 식별자

### 02-1. 식별자

- 문자, 언더바(_), $로 시작해야 함
- 한글도 가능하며, 영문자는 대소문자를 구분
- +, - 등 연산자를 포함하면 안됨
- 자바 키워드를 사용하면 안됨

```java
// 변수와 메서드는 모두 소문자로 표기
// 복합 단어일 때 두 번째 단어부터 단어의 첫 자만 대문자로 표기
int thisYear;
String currentPosition;
boolean isEmpty;
public int getYear() {}

// 클래스와 인터페이스는 첫 자만 대문자로 표기
// 복합 단어일 때 각 단어의 첫 자만 대문자로 표기
public class HelloDemo {}
public interface MyRunnable {}

// 상수는 전체 대문자 표기
// 복합 단어일 때 언더바(_)로 연결
final int NUBMER_ONE = 1;
final double PI = 3.141592;
```

### 02-2. 자바 키워드

| 분류 | 키워드 |
| --- | --- |
| 데이터 타입 | byte, char, short, int, long, float, double, boolean |
| 접근 지정자 | private, protected, public |
| 제어문 | if, else, for, while, do, break, continue, switch, case |
| 클래스와 객체 | class, interface, enum, extends, implements, new, this, super, instanceof, null |
| 예외 처리 | try, catch, finally, throw, throws |
| 기타 | abstract, assert, const, default, false, final, import, native, package, return, static, strictfp, synchronized, transient, true, void, volatile |

## 03. 변수

### 03-1. 변수의 개념

- 프로그램은 메모리 공간에 데이터를 보관
- 여러 메모리 공간을 변수로 구분
- 이를 구분하기 위해 데이터 타입을 사용

### 03-2. 데이터 타입과 리터럴

- 데이터 타입은 값과 값을 다룰 수 있는 연산의 집합
- 기초 타입 ⇒ 정수, 문자, 실수, 논리

| 분류 | 기초 타입 | 기억 공간 크기 | 기본값 | 값의 범위 |
| --- | --- | --- | --- | --- |
| 정수 | byte | 8비트 | 0 | -128~127 |
|  | short | 16비트 | 0 | -32,768~32,767 |
|  | int | 32비트 | 0 | -2,147,483,648~2,147,483,647 |
|  | long | 64비트 | 0L | -9,223,372,036,854,775,808 ~ -9,223,372,036,854,775,807 |
| 문자 | char | 16비트 | \0000 | 0(’\u0000’)~65,535(’\uFFFF’) |
| 실수 | float | 32비트 | 0.0f | 약 ±3.4*10^-38 ~ ±3.4*10^38 |
|  | double | 64비트 | 0.0d | 약 ±1.7*10^-308~±1.7*10^308 |
| 논리 | boolean | 8비트 | false | true와 false |
- 참조 타입 ⇒ 배열, 열거, 클래스, 인터페이스