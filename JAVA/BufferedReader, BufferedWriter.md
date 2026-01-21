
# Scanner와 System.out.println과의 차이

[★장점과 단점 자세히](https://chatgpt.com/s/t_696481fc1de48191920db7b389f3f187)
아래만 보지 말고 위 내용 꼭 숙지

- Scanner / System.out.println
장: 쉽고 간단
단 : 느림

- BufferedReader (+ StringTokenizer or split) / BufferedWriter (또는 PrintWriter)
장 : 빠름
단 : 복잡 + 일일이 설정 귀찮
***
예시 코드

정수 n을 입력받고, n번 반복하는 for문 안에서 정수를 입력받아서 x 2 하여 출력하는 프로그램

```java
import java.io.*;  
import java.util.*;  
  
public class Main {  
    public static void main(String[] args) throws IOException {  
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));  
        StringBuilder sb = new StringBuilder();  
        StringTokenizer st;  
  
        int n = Integer.parseInt(br.readLine());  
        // br.readLine() 으로 입력된 한 줄 전체를 문자열로 저장.  
        // Integer.parseInt 한 이유는 입력값을 숫자로 기대하고 있기 때문이다.  
        // 여기서 n은 for문의 반복횟수를 의미한다.  
        for (int i = 0; i < n; i++) {  
            st = new StringTokenizer(br.readLine());  
            // 다시 입력이 활성화 되고, 사용자가 입력한 내용을 한 줄 읽는다. 문자열로. 그 한 줄을 토큰 단위로 잘라낸다.  
            //  
            int x = Integer.parseInt(st.nextToken());  
            // 잘라낸 토큰 중 첫 번째 토큰을 가져와서 Int 타입으로 변환하여 x에 저장.  
  
            sb.append(x * 2).append('\n');  
            // StringBuilder에 차곡차곡 쌓는 과정. x에 2를 곱한 값을 더하고, 개행문자를 더한다.  
        }  
  
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));  
        bw.write(sb.toString()); // 출력 코드  
        bw.flush(); // 남아있는 데이터를 모두 출력시킴  
  
  
        bw.close();  
        br.close();  
  
    }  
}
```


***
# 사용법

## BufferedWriter

BufferedWriter 클래스이다.

### method

- write()
매개 변수로

## Import
```java
import java.io.*;  
import java.util.*;
```

## 예외 처리

메서드 선언부에 `throws IOException`
- 다른 방식도 존재.

```
public static void main(String[] args) throws IOException { ... }
```

https://gemini.google.com/share/ac7c6deeaf73
- try catch / throws IOException 둘 중 어떤 것을 사용해야 함? 그리고 둘의 차이는?
- 왜 예외 처리를 해야 하는가?
	- 마지막에 예외 처리를 더 깔끔하고 안전하게 해주는 **`try-with-resources`** 구문에 대해서 언급함.

## BufferedReader 객체 생성
`BufferedReader br = new BufferedReader(new InputStreamReader(System.in));`
- 위 코드를 이해하는 과정 : 총 3단계
- System.in
- InputStreamReader
- BufferedReader
- 그리고 위 3개 코드의 의미 : 


***
# StringTokenizer

## StringTokenizer의 메서드

countTokens()[^1]

***

# 활용할 수 있는 메서드

String.split()[^1]

[^1]: https://gemini.google.com/share/8c48e14ee89c
