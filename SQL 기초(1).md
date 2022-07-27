# SQL 기초(1)

**테이블에서 특정 열 선택하기**

사원 테이블에서 사원 번호와 이름과 월급을 출력
`SELECT empno, ename, sal FROM emp;`

**테이블에서 모든 열 선택하기**

`SELECT * FROM emp;`

**모든 컬럼을 출력하고 맨 끝에 다시 한번 특정 컬럼을 한번 더 출력해야 하는 경우**

`SELECT dept.*, deptno from dept;`

**컬럼 별칭을 사용하여 출력되는 컬럼명 변경하기**

`SELECT empno as 사원번호, ename as 사원이름, sal as "Salary" FROM emp;`

**컬럼 별칭에 더블 쿼테이션 마크를 감싸줘야 하는 경우**

1. 대소문자를 구분하여 출력할 때
2. 공백문자를 출력할 때
3. 특수문자를 출력할 때($, _, #만 가능)

수식을 사용하여 결과를 출력할 때 컬럼 별칭이 유용!

수식에 컬럼 별칭을 사용하면 ORDER BY을 사용할 때 유용함.

`SELECT ename, sal *(12 + 3000) FROM emp;`

`SELECT ename, sal *(12 + 3000) as 월급 FROM emp;`

`SELECT ename, sal *(12 + 3000) as 월급 FROM emp ORDER BY 월급 desc;`

**연결 연산자 사용하기**

`SELECT ename || sal FROM emp;`

![스크린샷 2022-07-27 오후 1.37.27.png](SQL%20%E1%84%80%E1%85%B5%E1%84%8E%E1%85%A9(1)%2065bc33075c0b4062b9a5598592222fe1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2022-07-27_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_1.37.27.png)

연결 연산자 사용 시 컬럼과 컬럼을 서로 연결해서 출력 가능

`SELECT ename || '의 월급은 ' || sal || '입니다.' as 월급정보 FROM emp;`

![스크린샷 2022-07-27 오후 1.42.17.png](SQL%20%E1%84%80%E1%85%B5%E1%84%8E%E1%85%A9(1)%2065bc33075c0b4062b9a5598592222fe1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2022-07-27_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_1.42.17.png)

**중복된 데이터를 제거해서 출력하기**

`SELECT DISTINCT job FROM emp;`

`SELECT UNIQUE job FROM emp;`

![스크린샷 2022-07-27 오후 1.44.18.png](SQL%20%E1%84%80%E1%85%B5%E1%84%8E%E1%85%A9(1)%2065bc33075c0b4062b9a5598592222fe1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2022-07-27_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_1.44.18.png)

월급이 낮은 순으로 정렬

`SELECT ename, sal FROM emp ORDER BY sal asc;`

| 정렬 방식 | 정렬 옵션 | 축약 |
| --- | --- | --- |
| 오름차순 | ASCENDING | ASC |
| 내림차순 | DESCENDING | DESC |

ORDER BY절이 가장 맨 마지막에실행 되므로 SELECT절에 사용한 컬럼 별칭을 ORDER BY절에 사용 가능

`SELECT ename, sal as 월급 FROM emp ORDER BY 월급 asc;`

`SELECT ename, deptno, sal FROM emp ORDER BY deptno asc, sal desc;`

**WHERE절 배우기 1️⃣**

숫자 데이터 검색

`SELECT ename, sal, job FROM emp WHERE sal = 3000;`

 기타 비교 연산자

| 연산자 | 의미 |
| --- | --- |
| BETWEEN AND |  ~ 사이에 있는 |
| LIKE | 일치하는 문자 패턴 검색 |
| IS NULL | NULL 값인지 여부 |
| IN | 값 리스트 중 일치하는 값 검색 |

`SELECT ename as 이름, sal as 월급 FROM emp WHERE sal >= 3000;`

**WHERE절 배우기 2️⃣**

문자와 날짜 검색

`SELECT ename, sal, job, hiredate, deptno FROM emp WHERE ename='SCOTT';`

`SELECT ename, hiredate FROM emp WHERE hiredate = '81/11/17';`

날짜 형식 알아내기

`SELECT * FROM NLS_SESSION_PARAMETERS WHERE PARAMETER = 'NLS_DATE_FORMAT';`

![스크린샷 2022-07-27 오후 2.11.16.png](SQL%20%E1%84%80%E1%85%B5%E1%84%8E%E1%85%A9(1)%2065bc33075c0b4062b9a5598592222fe1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2022-07-27_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_2.11.16.png)

산술 연산자 배우기

`SELECT ename, sal*12 as 연봉 FROM emp WHERE sal*12 >= 3600;`

`SELECT sal + comm FROM emp WHERE ename = 'KING';` - NULL 출력

`SELECT sal + *NVL*(comm, 0) FROM emp WHERE ename = 'KING';` - 5000 출력

NVL 함수 : NULL 데이터를 처리하는 함수

비교 연산자 배우기

`SELECT ename, sal, job, deptno FROM emp WHERE sal <= 1200;`

`SELECT ename, sal FROM emp WHERE sal BETWEEN 100 AND 3000;`

BETWEEN AND 사용 시 주의사항

“BETWEEN 하한값 AND 상한값” 순으로 작성 !

`SELECT ename, sal FROM emp WHERE ename LIKE 'S%';`

% - 와일드 카드 : 어떠한 철자가 와도 상관 없고 철자의 개수가 몇 개가 되든 관계 없다 ~

NULL을 검색하기 위해서는 is null을 사용해야 한다.

NULL이 아닌 데이터를 검색할 때도 COMM ≠ NULL을 사용하여 검색 불가

`SELECT ename, comm FROM emp WHERE comm is null;`

in 연산자를 이용해 SALESMAN, ANALYST, MANAGER인 사원들을 한 번에 조회

= 연산자는 하나의 값만 조회가 가능. in 연산자는 여러 리스트의 값을 조회 가능!

`SELECT ename, sal, job FROM emp WHERE job in ('SALESMAN', 'ANALYST', 'MANAGER');`

`SELECT ename, sal, job FROM emp WHERE job='SALESMAN' AND sal >= 1200;`