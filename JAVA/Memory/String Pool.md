## 무엇인가?

String Pool은 JVM이 관리하는 영역

- **JVM Runtime Data Area 중 하나**
    
- 이름은 보통 **String Constant Pool** 또는 **String Intern Pool**

***
## String Pool은 메모리의 “어디”에 존재하나?

Java 7 이후 (Java 8 포함, 현재 표준)
- **Heap 영역 안**에 존재
> Heap 안에 있지만 **GC 정책·생성 규칙은 일반 객체와 다르다**


