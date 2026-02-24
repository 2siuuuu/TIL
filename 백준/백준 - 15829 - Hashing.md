백준 - 15829 - Hashing

https://www.acmicpc.net/problem/15829

해시 함수?

서로소?
- 최대 공약수?
	- 공약수?

이 문제는 문제에서 알려주는 해시 함수를 구현해서 입력으로 주어지는 값을 해시 값으로 바꿔, 출력하려면 어떻게 코드를 작성해야 하는지 묻는다.

처음엔 해시 함수를 구현하고 결과값만 출력하면 되는 단순한 문제라고 생각하고 정답을 제출했다. 그건50점짜리 정답이었다.

```java
 import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        StringBuilder sb = new StringBuilder();

        //L
        int L = Integer.parseInt(br.readLine());
        String str = br.readLine();

        //str이 "abc"라면 각 문자 하나하나를 수열로 변환
        int total = 0;
        for (int i = 0; i < L; i++) {
            int alphaTonum = (str.charAt(i) - 'a')+1;
            int timesR = alphaTonum * (int)Math.pow(31,i);
            total += timesR;
        }
        int answer = total % 1234567891;



        sb.append(answer);

        //출력
        bw.write(sb.toString());
        bw.flush();
        bw.close();
        br.close();
    }

}
```

이 해시함수는 L이 5이하인 케이스에서는 잘 동작했지만, 
L이 50이하인 케이스에서는 수의 범위를 벗어나서 동작하지 않았기에 절반만 맞았던 것이다.

나는 그 해결 방법으로 데이터를 담는 변수의 그릇을 존나 키우면 된다라는 생각을 갖고서는 그 방법을 찾아보다 BigInteger라는 클래스의 존재를 알게되었다. 물론 이 방법은 먹혔고, 나는 100점을 받을 수 있었다.

```java
import java.io.*;
import java.util.StringTokenizer;
import java.math.BigInteger;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        StringBuilder sb = new StringBuilder();

        //L
        int L = Integer.parseInt(br.readLine());
        String str = br.readLine();

        //str이 "abc"라면 각 문자 하나하나를 수열로 변환
        BigInteger total = new BigInteger("0");
        for (int i = 0; i < L; i++) {
            int alphaTonum = (str.charAt(i) - 'a')+1;
            BigInteger Rbase = new BigInteger("31");
            BigInteger square = Rbase.pow(i);
            BigInteger timesnum = square.multiply(BigInteger.valueOf(alphaTonum));
            total = total.add(timesnum);
        }
        BigInteger answer = total.mod(BigInteger.valueOf(1234567891));



        sb.append(answer);

        //출력
        bw.write(sb.toString());
        bw.flush();
        bw.close();
        br.close();
    }

}
```

물론 100점을 받았으니 거기서 만족하고 자러갔을 수도 있었다. 실제로 그럴 뻔 했는데, 우연히 다른 사람이 제출한 코드를 보니 long 자료형 만으로 100점을 맞은 것을 확인했다.

코드도 더 단순했다. 당시 내 지식으로는 직관적으로 이해가 되지 않았기때문에 바로 Gemini에게 물어봤다.

그 대화에서 모듈러 연산의 분배 법칙이라는 것을 알게 되었다.


$$(A \times B) \pmod M = ((A \pmod M) \times (B \pmod M)) \pmod M$$

"
즉, 엄청 큰 수를 만든 다음에 $M$으로 나누는 것과, **중간중간 계속 $M$으로 나눈 나머지만 남겨서 곱하는 것**은 결국 결과가 같습니다.
"
라고 하는 법칙을 알게되었다. 
이걸 알게되었으니 내 코드는 더 단순해질 수 있으면서 출제자의 의도(로 추정되는)를 반영한 것이 될 수 있어 보였다. 그래서 수정해보았다.

결국 난 

$$
\left( \sum_{i=0}^{2^n-1} \bigl(a_i \bmod M\bigr)\,\bigl(p^i \bmod M\bigr) \right) \bmod M
$$
이걸 구현하면 되는거고 이걸 간단히 표현하면

$$
\sum_{i=0}^{2^n-1} a_i p^i \;\bmod M
$$
문제에서 등장하는 식이 된다. 모듈러 연산의 분배 법칙을 알았던 사람에겐 쉬운 문제였을 것이다.


하지만 이 방법을 알았음에도 50점을 받았는데, 원인은 제곱을 하는 과정에 있었다.

```java
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        StringBuilder sb = new StringBuilder();

        //L
        int L = Integer.parseInt(br.readLine());
        String str = br.readLine();

        //str이 "abc"라면 각 문자 하나하나를 수열로 변환
        long total = 0;
        int r = 31;
        int m = 1234567891;
        for (int i = 0; i < L; i++) {
            int alphaTonum = (str.charAt(i) - 'a')+1;
            long left = alphaTonum % m;
            long right = (int) Math.pow(r,i) % m;
            total += left * right; 
        }
        long answer = total % m;
        
        sb.append(answer);

        //출력
        bw.write(sb.toString());
        bw.flush();
        bw.close();
        br.close();
    }

}
```


마지막 50점 받은 이유  :

```
long right = (int) Math.pow(r,i) % m;
```

아래는 Gemini의 답변인데, 요약하자면 제곱을 한 값을 강제로 int로 형변환 하면서 값이 int의 max값으로 고정되어 버리고, 이를 나머지 연산 해버리니까 이상한 값이 되어버리는 것이다.
그것 외에도 Math.pow메서드로 제곱을 먼저 해버리면 값은 이미 커져버리기 때문에 int나 long의 범위를 벗어나게 된다.

***
 1. **근본적인 원인: Math.pow()의 한계와 형변환**

앞서 $31^{24}$만 해도 엄청난 크기의 숫자라고 말씀드렸었죠?

`Math.pow(31, 50)`을 실행하면 자바는 이 거대한 숫자를 `double` 타입으로 억지로 계산합니다. 그리고 이 어마어마한 결과를 `(int)`로 강제 형변환(Casting)하면, 자바는 `int`가 담을 수 있는 최대치인 **`2147483647`**로 뭉뚱그려버립니다.

즉, $i$가 조금만 커져도 `Math.pow(r, i)`는 이미 망가진 값이 되고, 그 망가진 값을 `% m` 해봤자 엉뚱한 결과가 나올 수밖에 없습니다.

 2. **모듈러 연산의 잘못된 적용 시점**

모듈러 연산의 핵심은 **"커지기 전에 미리 나눈다"**입니다.

작성하신 코드는 다 커져서 터져버린 값(`Math.pow`)에 뒤늦게 `% m`을 적용하고 있습니다. 거듭제곱을 하는 **과정 속에서** 계속 나머지를 구해줘야 합니다.

***

**최종 답**

```java
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        StringBuilder sb = new StringBuilder();

        //L
        int L = Integer.parseInt(br.readLine());
        String str = br.readLine();

        //str이 "abc"라면 각 문자 하나하나를 수열로 변환
        long total = 0;
        int r = 31;
        int m = 1234567891;
        long pow = 1;
        for (int i = 0; i < L; i++) {
            int alphaTonum = (str.charAt(i) - 'a')+1;
            total += (alphaTonum * pow) % m;
            pow = (pow*31) % m;
        }
        long answer = total % m;

        sb.append(answer);

        //출력
        bw.write(sb.toString());
        bw.flush();
        bw.close();
        br.close();
    }

}
```