#java

```
public class HelloWorld {  
    public static void main(String[] args) {  
        System.out.println("Hello, World!");  
    }  
}
```

# 발생할 수 있는 오류

## `String[] args` vs. `String args`

오류 원인:
`String[] args` 대신 `String args`로 작성해서 오류가 발생했다.


String 옆 `[]`의 의미: 
args 변수를 배열로 선언하겠다.


그렇기 때문에 `String args` 는 그냥 문자열 하나만 저장하는 변수로 선언하겠다는 의미가 된다.

명령줄에서 프로그램 실행 시, 다음과 같은 명령어를 입력하게 됨.
`java HelloWorld arg1 arg2`

사용자가 입력한 arg1, arg2는 위 코드 상 `args`라는 '배열'에 들어가게 된다.

즉 배열엔 다음과 같이 값이 저장될 것이다.
`[1][arg2]`
`[0][arg1]`

이제 저 값들을 main 함수에서 활용할 수 있게 되는 것임.

---



---

### **`String[] args` vs. `String args`**

- **`String[] args`**: 이것은 `String` **배열**을 의미합니다. 📦📦📦
    
    - `[]` 기호는 이 변수가 여러 개의 문자열(`String`)을 담을 수 있는 배열이라는 것을 나타냅니다.
        
    - 프로그램을 명령줄에서 실행할 때, `java HelloWorld arg1 arg2`처럼 프로그램 이름 뒤에 붙는 여러 인자(argument)들을 받아서 이 배열에 순서대로 저장합니다.
        
    - 즉, `args`는 명령줄 인자들의 **목록** 또는 **집합**을 담기 위한 변수입니다.
        
- **`String args`**: 이것은 단 하나의 `String` **문자열**을 의미합니다. 📦
    
    - 배열 기호 `[]`가 없으므로, 이 변수는 오직 하나의 문자열만 담을 수 있습니다.
        

---

### **오류가 발생하는 이유 ❓**

자바는 프로그램을 실행할 때, 약속된 **특정한 형태의 `main` 메서드**를 찾아서 실행하도록 설계되었습니다. 그 약속된 형태가 바로 다음과 같습니다.

Java

```
public static void main(String[] args)
```

자바 실행 환경(JRE)은 프로그램을 시작하기 위해 위와 **정확히 일치하는** 메서드를 찾습니다. 하지만 사용자의 코드에 있는 `main(String args)`는 이 약속된 형태와 다릅니다. 매개변수(parameter)가 `String` 배열(`String[]`)이 아니라 그냥 `String`이기 때문이죠.

따라서 자바는 "프로그램의 시작점을 찾을 수 없습니다. `public static void main(String[] args)` 형태로 된 `main` 메서드를 정의해주세요."라는 에러 메시지를 보여주는 것입니다.

---

### **코드 수정 ✅**

문제를 해결하려면 `main` 메서드의 매개변수를 `String args`에서 `String[] args`로 수정해주면 됩니다.

Java

```
public class HelloWorld {
    // String 뒤에 배열을 의미하는 []를 추가합니다.
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

이렇게 수정하고 다시 컴파일(`javac HelloWorld.java`)하고 실행(`java HelloWorld`)하면 "Hello, World!"가 정상적으로 출력됩니다.