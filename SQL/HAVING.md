#sql 

그룹 전용 필터이다.
HAVING으로 묶인 것을 그룹으로 보고 그 그룹에 필터를 가한다.



일반적으로 [[GROUP BY]]로 묶인 결과에 조건을 거는 구문

보통 [[GROUP BY]]와 함께 사용.
그러나 집계 함수가 있다면 사용 가능
- 이 경우는 전체를 하나의 그룹으로 보고 조건을 거는 것.
- 예시 :
```sql
SELECT COUNT(*)
FROM employees
HAVING COUNT(*) > 10;
```


중요:

- WHERE는 **묶기 전**
    
- `HAVING`은 **묶은 후**

묶기 전 이란, GROUP BY 이전 단계에서 실행되는 걸 말한다.
```sql
SELECT department, AVG(salary)
FROM employees
WHERE salary >= 3000
GROUP BY department;
```
먼저 행을 거르고 → 그 다음 묶는다.

