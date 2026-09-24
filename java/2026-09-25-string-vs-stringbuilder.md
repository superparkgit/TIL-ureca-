# String과 StringBuilder

- 날짜: 2026-09-25
- 상태: 오늘의 학습 자료·연습 과제
- 연계 문제: [백준 2908 상수](https://www.acmicpc.net/problem/2908)

## 1. String은 불변 객체다

Java의 `String` 객체는 생성된 뒤 내부 문자열을 변경할 수 없다. 문자열을
연결하면 기존 객체가 바뀌는 것이 아니라 결과를 담은 새로운 객체가 만들어진다.

```java
String word = "Java";
word = word + " Study";
```

두 번째 줄에서 `"Java"` 객체가 수정되는 것이 아니다. `"Java Study"`라는
새 문자열이 만들어지고 `word`가 새 객체를 가리킨다.

문자열이 불변이면 여러 코드가 같은 문자열을 공유해도 값이 갑자기 바뀌지 않아
안전하고, 문자열 풀과 해시값을 효율적으로 활용할 수 있다.

## 2. 반복 연결이 비효율적인 이유

반복문에서 `String`에 계속 문자를 붙이면 매번 새로운 문자열을 만들고 기존
내용을 복사한다. 문자열 길이가 커질수록 생성되는 임시 객체와 복사 비용이
늘어난다.

```java
String result = "";
for (int i = 0; i < 1_000; i++) {
    result += i;
}
```

문자열을 여러 번 변경해야 할 때는 변경 가능한 버퍼를 가진
`StringBuilder`가 더 적합하다.

```java
StringBuilder builder = new StringBuilder();
for (int i = 0; i < 1_000; i++) {
    builder.append(i);
}
String result = builder.toString();
```

## 3. StringBuilder의 주요 메서드

| 메서드 | 역할 |
| --- | --- |
| `append(value)` | 문자열 뒤에 값을 추가한다. |
| `insert(index, value)` | 지정 위치에 값을 삽입한다. |
| `delete(start, end)` | 범위의 문자를 삭제한다. |
| `reverse()` | 내부 문자 순서를 뒤집는다. |
| `toString()` | 최종 결과를 `String`으로 변환한다. |

`reverse()`는 새로운 `StringBuilder`를 만드는 것이 아니라 현재 객체의 내부
순서를 바꾸고 같은 객체를 반환한다.

```java
StringBuilder builder = new StringBuilder("123");
StringBuilder returned = builder.reverse();

System.out.println(builder);              // 321
System.out.println(builder == returned);  // true
```

## 4. 알고리즘 문제에 적용하기

숫자를 문자열로 받으면 각 자릿수를 계산하지 않고 간단히 뒤집을 수 있다.

```java
private static int reverseNumber(String number) {
    return Integer.parseInt(
            new StringBuilder(number).reverse().toString()
    );
}
```

- `StringBuilder(number)`: 입력 문자열로 변경 가능한 객체를 만든다.
- `reverse()`: 문자 순서를 뒤집는다.
- `toString()`: 다시 `String`으로 변환한다.
- `Integer.parseInt()`: 기본형 `int`로 변환한다.

## 5. StringBuilder와 StringBuffer

`StringBuilder`는 메서드가 동기화되어 있지 않아 일반적인 단일 스레드 문자열
조작에 적합하다. `StringBuffer`는 동기화를 제공하지만 그만큼 추가 비용이
있다. 여러 스레드가 같은 객체를 실제로 공유하는 상황인지 먼저 판단해야 한다.

## 핵심 질문

1. `String`이 불변이라는 것은 어떤 의미인가?
2. 반복문 안에서 `result += value`를 피해야 하는 이유는 무엇인가?
3. `reverse()` 호출 후 기존 `StringBuilder`의 값은 어떻게 되는가?
4. `Integer.parseInt()`와 `Integer.valueOf()`의 반환형은 어떻게 다른가?
5. 여러 스레드가 같은 문자열 버퍼를 공유한다면 무엇을 고려해야 하는가?

## 직접 해볼 연습

1. `StringBuilder.reverse()` 없이 `"hello"`를 뒤집는다.
2. `append()`를 사용해 1부터 10까지 쉼표로 연결한다.
3. 숫자 `120`을 문자열 방식과 나눗셈 방식으로 각각 뒤집어 결과를 비교한다.
4. 백준 2908 코드를 보지 않고 다시 작성하고 온라인 채점 결과를 기록한다.

## 복습 기록

- 이해한 내용:
- 헷갈린 내용:
- 직접 작성한 코드의 결과:
- 다시 볼 날짜:
