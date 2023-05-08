# Call By Reference
- 참조에 의한 호출
- 참조값(주소 또는 포인터)을 넘겨줌
- Stack 영역에 있는 참조 변수가 Heap 영역에 있는 객체를 가리킴
- 전달받은 값을 변경하면 원본도 같이 변경됨
- 저장되는 곳: Heap Area

<br><br>

# Call By Value
- 값을 호출
- 인자의 메모리에 저장된 **값** 복사
- 전달받은 값을 변경해도 원본은 변경되지 않음
- 저장되는 곳: Stack Area

<br><br>

## Java에는 Call By Reference가 존재하지 않는다
> - Java에서의 매개변수는 **Call By Value로만 동작**되며, 원시값이 복사되느냐 주소값이 복사되느냐의 차이이다.  
> - 매개변수에 복사된 값이 primitive(기본형)냐, reference(참조형)냐에 따라서 값이 **직접 복사될 것인지, 주소 값만 복사될 것인지** 정해진다.

<br><br>

## swap 예시
```
class CallByValue {
    public static void swap(int x, int y) {
      int temp = x;
      x = y;
      y = temp;
    }

    public static void main(String[] args) {
      int a = 10;
      int b = 20;
      System.out.printf("a=%d, b=%d"); // 첫 번째 출력

      swap(a, b);

      System.out.println("a=%d, b=%d"); // 두 번째 출력
    }
}
```
## 출력
```
a=10, b=20
a=10, b=20
```
분명 swap 메서드로 a와 b를 바꾸었는데 왜 출력은 그대로일까?  

**swap() 메서드 호출 시 사용한 인자 a, b와 swap() 메서드의 매개변수 x, y는 다르기 때문이다.**  
a와 b의 값을 메서드로 전달할 때 **값이 복사되어서** x와 y의 메모리에 담겨지기 때문에 swap() 메서드내에서 값을 교환해도 a와 b는 영향을 받지 않는다.