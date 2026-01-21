static field (class field)

# static field
```java
public class C {
	String s;
	static int a;
}
```
a는 static field 이다.

static field는 class field라고도 부른다.

static field의 저장 공간 : Method Area

[[instance field|field a]]는 생성되는 instance의 heap memory에 저장된다.

# 주의 사항

static field는 클래스명으로 접근하도록 하자.
[그 이유](https://telegra.ph/static-field%EB%8A%94-%ED%81%B4%EB%9E%98%EC%8A%A4%EB%AA%85%EC%9C%BC%EB%A1%9C-%EC%A0%91%EA%B7%BC%ED%95%B4%EC%95%BC-%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0-01-21)

