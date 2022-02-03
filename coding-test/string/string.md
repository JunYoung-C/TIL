# String
## Index
1. [유용한 개념](#1.-유용한-개념)
2. [자주 쓰이는 문자열 함수](#2.-자주-쓰이는-문자열-함수)
3. [자주 쓰이는 char형 함수](#3.-자주-쓰이는-char형-함수)
---

## 1. 유용한 개념

### char형 변수 입력받기

- Scanner를 이용하여 char형 변수를 직접 입력받을 수 없다.
- `char c = stdIn.next().charAt(0);`
- 문자열을 입력받은 후 0번 인덱스를 선택하는 방식으로 입력받을 수 있다.

### StringBuffer로 문자열 뒤집기

``` java
String str = "hello";
String reverse = new StringBuffer(str).reverse().toString();
// reverse = "olloeh"
```

- String은 + 연산을 하면 객체가 새로 생성된다.
- StringBuffer은 입력된 객체 하나로 변환 작업을 하는 것이다.
    - +연산과 같은 작업이 많을 경우 유리하다.
- StringBuffer은 toSring으로 String형변환이 가능하다.

### 아스키 코드

- A ~ Z는 65 ~ 90, a ~ z는 97 ~ 122이다.
- (char)(대문자 + 32)를 하면 소문자로 변환된다.
- 0 ~ 9는 48 ~ 57이다.

### 10진수 <-> 2진수, 8진수, 16진수

- 10진수 -> 2진수, 8진수, 16진수

``` java
int num10 = 77;
String num2 = Integer.toBinaryString(num10); // 1001101
String num8 = Integer.toOctalString(num10); // 115
String num16 = Integer.toHexString(num10); // 4d
```

- 2진수, 8진수, 16진수 -> 10진수

``` java
int num10_2 = Integer.parseInt(num2, 2); // 77
int num10_8 = Integer.parseInt(num8, 8); // 77
int num10_16 = Integer.parseInt(num16, 16); // 77
```

## 2. 자주 쓰이는 문자열 함수

- `str.toCharArray()` : 문자열을 char형 배열로 변환
- `String.valueOf()` : `str.toCharArray()`로 변환된 문자를 `String.valueOf(배열)`에 넣으면 문자열로 변환된다.
- `str.split()` : 문자열을 특정 기준에 따라 분리하고 문자열 배열 반환. regex가 `" "`일 경우 공백을 기준으로 문자열 분리. 배열 크기 조절 가능
- `str.indexOf()` : 특정 문자나 문자열을 앞에서부터 처음 발견되는 인덱스를 반환한다. 찾지 못할 경우 -1을 반환
- `str.lastIndexOf()` : 특정 문자나 문자열을 뒤에서부터 처음 발견되는 인덱스를 반환한다. 찾지 못할 경우 -1을 반환
- `str.substring()` : 시작과 끝 인덱스, 시작 인덱스를 지정하여 해당 구간의 문자열을 반환한다. 끝 인덱스를 지정하면 끝 인덱스 - 1까지 반환한다.
- `str1.equals(str2)` : str1과 str2가 서로 같은 문자열이면 true 반환. ==는 문자열 비교하므로 주의하여 사용한다.
- `str1.equalsIgnoreCase(str2)` : str1과 str2가 대소문자 상관없이 같은 문자열이면 true 반환.
- `str.replaceAll(String regex, String replacement)` : 정규식에 해당되는 여러 문자열을 변환하여 반환한다.
- `str.replace(charSequence target, charSequence replacement)` : 특정 문자열을 변환하여 반환한다.

## 3. 자주 쓰이는 char형 함수

- `Character.isAlphabetic(c)` : c가 알파벳이면 true, 아니면 false 반환
- `Character.isDigit(c)` : c가 숫자면 true, 아니면 false 반환


