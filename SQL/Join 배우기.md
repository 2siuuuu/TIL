# 예제 테이블

**students**

| student_id(pk) | name    | age | major            |
| -------------- | ------- | --- | ---------------- |
| 1              | Alice   | 20  | Computer Science |
| 2              | Bob     | 22  | Mathematics      |
| 3              | Charlie | 21  | Physics          |
| 4              | David   | 23  | Computer Science |

**courses**

| course_id | course_name    | professor |
|-----------|---------------|-----------|
| 101       | Database      | Kim       |
| 102       | Algorithms    | Lee       |
| 103       | Linear Algebra| Park      |


**enrollments**
학생이 어떤 강의를 수강하였고 어떤 성적을 받았는지 볼 수 있는 테이블이다.

| enrollment_id | student_id(fk) | course_id (fk) | grade |
| ------------- | -------------- | -------------- | ----- |
| 1             | 1              | 101            | A     |
| 2             | 1              | 102            | B     |
| 3             | 2              | 103            | A     |
| 4             | 3              | 101            | C     |

# 문제 1

>모든 수강 정보를 출력하시오.  
출력: 학생이름, 강의이름, 성적



모든 수강 정보를 출력한다?

수강 정보란 무엇이다 라고 정의를 해야 한다
수강 정보:
수강이란 강의를 듣는 것이다. 강의는 학생이 듣는다.
즉 수강 정보는 어떤 학생이 어떤 강의를 듣는지 알 수 있는 정보를 의미한다
그러므로

학생이름 - 강의 이름 이 매칭되어야 한다.
근데 출력을 학생 이름, 강의 이름, 성적. 총 3개가 출력되어야 한다.

그러므로 학생 이름 - 강의 이름 - 성적이 매칭되어야 한다.

**우선 student 테이블과 enrollments 테이블을 연관지을 수 있겠다.**
왜냐하면 각자가  student_id를 가지고 있기 때문이다.

만약 students테이블과 가장 먼저 join할 대상 테이블로, enrollments테이블 대신 courses 테이블이 가능한가?
연관 지을 수 없다. 왜냐하면 서로 연관되는 컬럼이 하나도 없기 때문이다. 그러므로 먼저 join을 하는 대상은
enrollments인 것이다.

그렇기 때문에 아래와 같이 join을 할 수 있다.

```sql
select *
from students s
JOIN enrollments e ON s.student_id = e.student_id
```

이것의 의미는
~~students 테이블을 enrollments테이블과 join할 건데 어떤 기준으로 할 거냐면 student_id를 기준으로 할 거다.~~(이 설명은 내가 보기에 너무 두루뭉실하다.)
나는 처음에는 위 처럼밖에 설명할 수 없었다. 저것보다 더 나은 설명을 하려고 혼자 머리를 쓰며 스트레스 받는 건 너무나 비효율적이라고 생각하기도 했고 실제로도 그러하기 때문에 gemini에게 물어봤다.
https://gemini.google.com/share/9059d91ad915

총 두 가지 버전의 설명을 알려주었는데, 아래의 설명이 내게 있어 더 이해가 잘 되는 설명이었다. 그와 동시에 쿼리문과 이 설명을 번갈아 가며 보면, 어떤 결과가 나올지 예상이 되는 좋은 설명이라고 생각했다.

>Students 테이블(s)을 기준으로 Enrollments 테이블(e)을 탐색하여, `s.student_id`와 `e.student_id`가 일치하는 교집합(Intersection) 데이터만 결합하여 출력하라.




자 그럼 student 테이블과 enrollments 테이블이 연결된다. student_id를 기준으로.
두 테이블이 하나의 테이블로 합쳐진다. 그 결과 : 아래와 같이 붙는다.

| student\_id | name    | age | major            | enrollment\_id | student\_id | course\_id | grade |
| :---------- | :------ | :-- | :--------------- | :------------- | :---------- | :--------- | :---- |
| 1           | Alice   | 20  | Computer Science | 1              | 1           | 101        | A     |
| 1           | Alice   | 20  | Computer Science | 2              | 1           | 102        | B     |
| 2           | Bob     | 22  | Mathematics      | 3              | 2           | 103        | A     |
| 3           | Charlie | 21  | Physics          | 4              | 3           | 101        | C     |
여기서 궁금한 건, 붙는 순서가 어떻게 되느냐 이다.
이 질문도, 위의 링크 (https://gemini.google.com/share/9059d91ad915) 에서 질문하였다.

내가 원하는 대답을 해줬고, 그 덕분에 Join의 동작 방식을 제대로 이해할 수 있었다. 
역시 문제 해결은 방향이 중요한 것 같다. 아까는 머리 좀 써보겠다고 결과만 보고 어떤 원리로 저렇게 나오는 건지 생각해보느라 시간을 많이 썼는데, 이걸 빨리 이해하고 넘어가야 하는데 이해가 안 된 채로 원리를 추측, 암호 풀듯이 하려다 보니까 싫증이 나고 스트레스를 받는 것이다. 
나는 어떻게든 이해하면 되는 것이다. 여긴 시험장이 아니다. 그래서 어떤 도움이든 받으면 된다. 다음부터는 가능한 한 내가 할 수 있는 수단 방법을 가리지 말고 이해하고 넘어가야 한다!

그리고 이 시점에서 원래 풀려고 했던 문제를 풀 수 있었다.
원래 풀려 했던 문제는 정보처리기사 24년 3회 실기 문제 3번이었기 때문이다.
이제는 이 문제를 확실하게 풀 수 있게 되었다.