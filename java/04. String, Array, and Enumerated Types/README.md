# 문자열, 배열, 열거 타입

## 01. 문자열

### 문자열 선언과 생성

- 문자열은 `String` 타입의 변수 선언
- `String` 타입의 변수는 `큰따옴표("")`로 감싸서 나타낸 `문자열 리터럴`을 사용해서 초기화
- `String `타입은 자바가 기본으로 제공하는 `클래스`
  - 자바는 문자열 리터럴을 내부적으로 `String 객체`로 처리
  -` String 객체를 생성`하면 String 클래스의 `생성자 호출`
  - 문자열 리터럴은 내부적으로 `new String()`을 호출해 생성한 객체
  - ⭐ `내용이 같은` 문자열 리터럴이라면 `기존 리터럴` 공유


```java
String 변수;              // String 타입의 변수 선언
변수 = "문자열";           // String 타입의 변수에 문자열 대입

String s1 = "안녕, 자바";  // String 타입의 변수 선언과 초기화
```

### 문자열 메서드

- String 클래스에서 제공하는 문자열 비교 메서드
  | 메서드 | 설명 |
  | -- | -- |
  | int compareTo(String s) | 문자열을 사전 순으로 비교해 정숫값 반환 |
  | int compareTolgnoreCase(String s) | 대·소문자를 무시하고, 문자열을 사전 순으로 비교 |
  | boolean equals(String s) | 주어진 문자열 s와 현재 문자열을 비교한 후 true/ false 반환 |
  | boolean equalsIgnoreCase(String s) | 주어진 문자열 s와 현재 문자열을 대소문자 구분 없이 비교한 후 true/false 반환 |

- String 클래스에서 제공하는 유용한 메서드
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

- String 클래스에서 제공하는 정적 메서드
  | 메서드 | 설명 |
  | -- | -- |
  | String format() | 주어진 포맷에 맞춘 문자열을 반환 |
  | String join() | 주어진 구분자와 연결한 문자열을 반환 |
  | String valueOf() | 각종 기초 타입이나 객체를 문자열로 반환 |

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
int scores[5];    // 배열을 참조할 변수를 선언할 때는 배열 크기를 지정할 수 없음

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

### 동적 배열

- 크기가 유동적인 배열을 지원하기 위해 `ArrayList 클래스` 제공
- 인덱스를 사용해 원소에 접근하며 원소의 개수에 따라 `자동으로 크기 변경`
- 특정 인덱스에 원소를 추가하거나 제거하면, `자동으로 인덱스 조정`

```java
ArrayList<참조타입> 참조변수 = new ArrayList<>();

참조변수.add(데이터)          // 데이터를 동적으로 배열에 원소로 추가
참조변수.remove(인덱스번호)    // 동적 배열에서 인덱스 번호의 원소를 제거
참조변수.get(인덱스번호)       // 동적 배열에서 인덱스 번호의 원소를 가져오기
참조변수.size()              // 동적 배열에 포함된 원소의 개수
```

<br />

## 03. 배열 응용 

### 배열을 위한 반복문

> 💡 `for ~ each문`은 주로 배열이나 컬렉션 원소를 처리하는데 사용

- `for ~ each 문`은 모든 원소를 `처음부터 하나씩 for ~ each 문의 변수에 대입한 후 처리`
  - 특정 원소를 나타내는 인덱스가 필요 없음
- `for ~ each 문`은 final 타입
  -  반복할 때마다 새로운 지역 변수가 생성됨

```java
for(타입 변수 : 배열_혹은_컬렉션) {}
```

### 객체의 배열

> 💡 객체도 배열의 원소로 사용할 수 있음

- 객체 배열은 `객체를 참조하는 주소`를 원소로 구성(객체 참조 변수의 배열)

```java
class Circle {
  double radius;

  public Circle(double radius) {
    this.radius = radius;
  }

  public double getRadius() {
    return redius;
  }

  double findArea() {
    return 3.14 * radius * radius;
  }
}

public class CircleArrayDemo {
  public static void main(String[] args) {
    // 5개의 Circle 객체를 가진 배열 변수를 선언
    Circle[] circles = new Circle[5];

    for (int i = 0; i < circles.length; i++) {
      // Circle 객체를 생성해서 배열의 각 원소에 대입
      circles[i] = new Circle(i + 1.0);
      system.out.prinf("원의 널비(반지름 : %.1f) = %.2f\n",
        // i번째 객체 배열의 radius 필드 값과 findArea() 메서드 값 
        circles[i].radius, circles[i].findArea());
    }
  }
}
```