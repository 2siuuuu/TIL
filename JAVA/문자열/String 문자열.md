
# 문자열 하나를 저장하면 어디에 저장되는가

```java
public class Main {
	static void main(String[] args) {
		String st = "A";
		String st1 = "A";
		String st2 = new String("B");
	}
}
```

"A" 는 어디에 저장되는가?
**[[String Pool|String Constant Pool]]** 에 저장된다. 정확히는 문자열 상수 풀에 저장되는 건, "A"의 주솟값이다.
즉 문자열 리터럴 "A"는 [[Intern|intern되었다.]]

st1은 st가 가리키는 문자열 풀의 공간 상의 "A"의 주소를 가리킨다. 결국 st와 st1은 같은 주소값을 담고 있다.

st2는 heap에 저장되는 "B"의 주소값을 가리킨다. 

# 문자열 객체 생성 시 동작 과정

```java

String d = new String("A");
```

이 한 줄에서 실제로 일어나는 일:
1. `"A"` 리터럴을 확인한다.
	- String Pool에 `"A"`가 있는지 확인
	- 없으면 String Pool에 생성, 있으면 재사용.  어떻게 재사용? ↓
2. new String("A")
	- Pool의 `"A"`를 복사
	- Heap에 새로운 String 객체 생성



# String Class 메서드

## chatAt()
숫자로 된 문자열을 하나씩 떼어 int 형 데이터로 변환한다.
예시:
```java
String s = br.readLine(); // "12345"

for (int i = 0; i < s.length(); i++) {
    int num = s.charAt(i) - '0';
    // num = 1, 2, 3, 4, 5
}
```

## [[Intern|intern]](String val)

예시:
```java
String x = new String("A");
String y = x.intern();
// String s = 어떤문자열.intern();
```
동작 방식
x는 heap에 저장된 "A"의 참조를 저장하고 있음
`x.intern()` 시 JVM의 판단:
String Pool에 **같은 내용의 문자열이 이미 있는가?** ->
- YES → 그 문자열의 참조 반환
- NO → Pool에 등록하고 그 참조 반환

결과적으로 `y`는 **[[Intern|intern]]된 문자열**을 가리킨다.

# 문자 character
[문자 하나 입력 -> 아스키 코드 출력](https://chatgpt.com/share/696dc66a-7aa8-800d-9505-4701f6ea447a)

