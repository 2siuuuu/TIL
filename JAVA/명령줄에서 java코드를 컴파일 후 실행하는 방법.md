#java

명령줄에서 "Hello, World!" 프로그램을 컴파일하고 실행하는 것은 자바 개발의 기본입니다. 아래의 간단한 단계를 따라 진행할 수 있습니다.

### **1. 자바 코드 작성**

먼저, 텍스트 편집기(메모장, Visual Studio Code, Sublime Text 등)를 열어 아래와 같이 자바 코드를 작성합니다.

Java

```
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

이 파일을 `HelloWorld.java`라는 이름으로 저장합니다. **클래스 이름(`HelloWorld`)과 파일 이름이 반드시 일치해야 합니다.**

---

### **2. 명령 프롬프트(CMD) 또는 터미널 열기**

다음으로, `HelloWorld.java` 파일을 저장한 디렉토리에서 명령 프롬프트(Windows) 또는 터미널(macOS/Linux)을 엽니다.

- **Windows 팁:** 파일 탐색기에서 해당 폴더의 주소창에 `cmd`를 입력하고 Enter 키를 누르면 현재 위치에서 바로 명령 프롬프트가 열립니다.
    

---

### **3. 자바 코드 컴파일 (javac)**

명령줄에 아래 명령어를 입력하여 자바 소스 코드(`HelloWorld.java`)를 자바 바이트코드(`.class` 파일)로 컴파일합니다.

Shell

```
javac HelloWorld.java
```

컴파일이 성공적으로 완료되면 아무런 메시지가 나타나지 않고, 같은 폴더에 `HelloWorld.class` 파일이 생성된 것을 확인할 수 있습니다. 만약 오류가 발생하면, 코드에 오타가 있는지 다시 한번 확인해 보세요.

---

### **4. 프로그램 실행 (java)**

이제 컴파일된 자바 프로그램을 실행할 차례입니다. 아래 명령어를 입력하여 프로그램을 실행합니다.

Shell

```
java HelloWorld
```

**주의:** 실행할 때는 파일 확장자인 `.class`를 붙이지 않습니다.

명령어를 실행하면, 화면에 "Hello, World!"가 성공적으로 출력되는 것을 볼 수 있습니다.

Shell

```
Hello, World!
```