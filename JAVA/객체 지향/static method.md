객체를 생성하지 않고도 **`클래스명.메서드명()`** 으로 바로 호출할 수 있는 메서드

# 특징

**인스턴스 변수 접근 불가:** `static` 메서드는 객체 생성 없이 실행되므로, 객체가 생성되어야만 존재하는 '인스턴스 변수'나 '`this`' 키워드를 사용할 수 없습니다.


```java
class Calculator {
    int result = 0; // 인스턴스 변수

    // 1. Static 메서드: 공용 계산기 (객체 상태와 상관없음)
    static int add(int a, int b) {
        return a + b;
        // return result + a; // [에러!] static 메서드에서 인스턴스 변수 접근 불가
    }

    // 2. 인스턴스 메서드: 이 계산기만의 누적값 출력
    void showResult() {
        System.out.println("현재 결과: " + result);
    }
}

public class Main {
    public static void main(String[] args) {
        // 객체 생성 없이 바로 사용 가능
        int sum = Calculator.add(10, 20); 
        System.out.println(sum);
    }
}
```