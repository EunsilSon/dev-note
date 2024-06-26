# Java
### Integer
- `.parseInteger(String s)` : int 기본형 반환
- `.valueOf(String s)` : Integer 객체 반환

### Character
- `.getNumericValue(char ch)`
    - 0~9 : 정수 반환
    - A~Z, a~z : 10~35사이의 값
    - 유니코드 숫자가 아닌 문자 : -1

<br>


# String
- `String.format(String format, Object... args)` : 문자열 형식 지정 
  - 특정한 형식의 문자열과 인수를 사용해 포맷된 문자열을 반환
  - 문자열의 앞에 `%`를 붙이면 해당 위치에 변수의 값을 형식화 해 대입 가능
  - 기본적인 실수형은 모두 `double`로 인식하니, `float`로 출력 시 실수 뒤에 `f` 붙이기 

- `Integer.parseInt(String s, radix)` : 문자열을 n진수로 변환  (2진수 ~ 36진수 가능)

- `String.toCharArray()` : 문자열을 char형 배열로 쪼개기
    - `String str = new String(charArr)` : char형 배열을 합쳐 문자열 만들기 

- 문자열 자르기
    - `String.split(String regex)`
    - `String.substring(idx)`
    - `String.substring(start idx, end idx)` 

- 문자열 치환
    - `String.replace(CharSequence old, CharSequence new)` : 특정 문자 바꿀 때
    - `String.replaceAll(String regex, String replacement)` : 특정 패턴 바꿀 때

- `String.toUpperCase()`, `String.toLowerCase()` : 대소문자 변환
- `s.replaceAll("[^0-9]", "")` : 문자열에서 숫자만 출력
- `String.contains` : 문자열 내 존재 여부
    - 내부적으로 indexOf 를 사용하므로 문자열 내에 어느 부분이든 존재한다면  `true` 반환
- `String.startsWwith()` : 특정 문자열로 시작하는지 
- `String.endsWith()` : 특정 문자열로 끝나는지

<br><br>

# StringBuilder
```
StringBuilder sb = new StringBuilder
```
- 가변 객체
- 싱글스레드 환경에 사용하기 좋음

### 메서드
- `.reverse()` : 문자열 뒤집기

<br><br>

# Buffer
- 예외 처리 필수
    1. try/catch
    2. throws IOException

```
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
```

### 메서드
- `.read()` : 한 글자만 읽어 int형으로 반환
- `.readLine()` : 개행문자 단위로 String형으로 입력값 읽음

<br>

## StringTokenizer
```
StringTokenizer st = new StringTokenizer(br.readLine());
```
- `.nextToken()` : readLine()로 받은 값을 공백 단위로 구분해 순서대로 호출 가능

<br>

## Character
- `Character.isDigit(char)` : 숫자인지 아닌지 (return boolean)

<br><br>

# Math
- `Math.pow(Double, Double)` : 거듭제곱
- `Math.max(param1, param2)` : 최댓값
- `Math.min(param1, param2)` : 최솟값

<br><br>

# Collection Framework
## HashMap
>HashSet : `순서 X`  `중복 X`  
>HashMap : `순서 O`  `key null O` `key-value`  
>HashTable : `순서 X` `key null X` `key-value` `Thread-Safe`

- `map.containsKey()` : map에 특정 key 존재 여부
- `map.containsValue()` : map에 특정 value 존재 여부

## TreeSet
>- 데이터가 정렬된 상태로 저장
>- 중복 X
>- 순서 유지 X

```
TreeSet<E> tree = new TreeSet<>(); // 오름차순
TreeSet<E> tree = new TreeSet<>(Collections.reverseOrder()); // 내림차순
```