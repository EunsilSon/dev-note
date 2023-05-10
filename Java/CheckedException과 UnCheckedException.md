# 오류(Error)와 예외(Exception)의 차이
- Error
  - 개발자가 미리 예측하여 방지할 수 없는 비정상적인 상황
  - StackOverflowError, OutOfMemoryError 등
- Exception
  - 개발자가 구현한 로직에서 발생한 실수 또는 사용자의 영향에 의해 발생
  - 개발자가 미리 예측해 방지할 수 있기 때문에 **예외 처리(Exception Handle)** 가 필요
  - NullPointerException, ArrayIndexOutOfBoundsException 등

<br>

# CheckedException
- RuntimeException 하위 클래스를 제외한 Exception 클래스의 모든 하위 클래스
  - 컴파일 시점에서 발견
- 반드시 명시적인 예외 처리를 해야함
  1. ```try ~ catch```
  2. ```throws```
- 롤백 X
- FileNotFoundException, ClassNotFoundException 등


<br>

# UnCheckedException
- RuntimeException 하위 클래스
  - 런타임 시점에서 발견 (실행 중에)
- 명시적인 예외 처리를 하지 않음
  - 개발자의 실수에 의해 발생하는 예외이기 때문
- 롤백 O
- ArrayIndexOutOfBoundsException, NullPointerException 등

<br>

>### 내 마음대로 요약
> - CheckedException  
>   - 명시적인 예외 처리를 한다 → 컴파일 시점에서 발견되니까 미리 예측을 못하니 미리 예상하고 처리 해두는 것
> - UnCheckedException
>   - 명시적인 예외 처리를 하지 않는다 → 실행 시점에서 발견되니까 미리 예측해서 Exception이 안 뜨게할 수 있음