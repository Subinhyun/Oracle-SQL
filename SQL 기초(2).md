# SQL 기초(2)

대소문자 변환 함수 

`SELECT *UPPER*(ename), *LOWER*(ename), *INITCAP*(ename) FROM emp;`

UPPER 함수 : 대문자

LOWER 함수 : 소문자 

INITCAP 함수 : 첫 번째 철자만 대문자로출력하고 나머지 소문자로 출력

`SELECT ENAME, SAL FROM emp WHERE *LOWER*(ename)='scott';`

`SELECT *SUBSTR*('SMITH', 1, 3) FROM DUAL;`

SUBSTR 함수 : 문자에서 특정 위치의 문자열을 추출

`SELECT ename, *LENGTH*(ename) FROM emp;`

LENGTH 함수 : 문자열의 길이를 출력하는 함수

**문자에서 특정 철자의 위치 출력하기**

`SELECT *INSTR*('SMITH', 'M') FROM DUAL;`

INSTR 함수 : 문자에서 특정 철자의 위치를 출력하는 함수 

`SELECT *SUBSTR*('abcdefgh@naver.com', *INSTR*('abcdefgh@naver.com', '@')+1) FROM DUAL;`

출력 결과 : naver.com

`SELECT *RTRIM*(*SUBSTR*('abcdefgh@naver.com', *INSTR*('abcdefgh@naver.com', '@')+1), '.com') FROM DUAL;`

출력 결과 : naver

**특정 철자를 다른 철자로 변경하기**

`SELECT ename, *REPLACE*(sal, 0, '*') FROM emp;`

월급의 숫자 0을 *로 변경해서 출력

REPLACE 함수 : 특정 철자를 다른 철자로 변경하는 문자 함수

**특정 철자를 N개 만큼 채우기**

`SELECT ename, *LPAD*(sal, 10, '*') as salary1, *RPAD*(sal, 10, '*') as salary2 FROM emp;`

LPAD - 왼쪽으로 채워넣다

RPAD - 오른쪽으로 채워넣다

특정 철자 잘라내기(TRIM, RTRIM, LTRIM)

`SELECT 'smith', *LTRIM*('smith', 's'), *RTRIM*('smith', 'h'), *TRIM*('s' from 'smiths') FROM dual;`

LTRIM(’smith’, ‘s’) : 왼쪽 철자 s 잘라서 출력

RTRIM(’smith’, ‘h’) : 오른쪽 철자 h 잘라서 출력

TRIM(’s’ from ‘smiths’) : 양쪽 데이터 잘라서 출력

반올림해서 출력하기(ROUND)

`SELECT '876.567' as 숫자, *ROUND*(876.567, 1) FROM dual;`

숫자를 버리고 출력하기(TRUNC)

`SELECT '876.567' as 숫자, *TRUNC*(876.567, 1) FROM dual;`

나눈 나머지 값 출력하기(MOD)

`SELECT *MOD*(10,3) FROM DUAL;`

날짜 간 개월 수 출력하기(MONTHS_BETWEN)

`SELECT ename, *MONTHS_BETWEEN*(*sysdate*, hiredate) FROM emp;`

MONTHS_BETWEN(최신 날짜, 예전 날짜)

개월 수 더한 날짜 출력하기(ADD_MONTHS)

`SELECT *ADD_MONTHS*(*TO_DATE*('2019-05-01', 'RRRR-MM-DD'), 100) FROM DUAL;`

`SELECT *TO_DATE*('2019-05-01', 'RRRR-MM-DD') + interval '1-3' year(1) to month FROM DUAL;`

SYSDATE + (INTERVAL '1' YEAR)

- -1년 더하기

SYSDATE + (INTERVAL '1' MONTH)

- -1개월 더하기

SYSDATE + (INTERVAL '1' DAY)

- -1일 더하기

SYSDATE + (INTERVAL '1' HOUR)

- -1시간 더하기

SYSDATE + (INTERVAL '1' MINUTE)

- -1분 더하기

SYSDATE + (INTERVAL '1' SECOND)

- -1초 더하기

SYSDATE + (INTERVAL '02:10' HOUR TO MINUTE)

- -2시간10분 더하기

SYSDATE + (INTERVAL '01:30' MINUTE TO SECOND)

- -1분30초 더하기

특정 날짜 뒤에 오는 요일 날짜 출력하기(NEXT_DAY)

`SELECT '2019/05/22' as 날짜, *NEXT_DAY*('2019/05/22', '월요일') FROM DUAL;`

특정 날짜가 있는 달의 마지막 날짜 출력하기(LAST_DAY)

`SELECT '2019/05/22' as 날짜, *LAST_DAY*('2019/05/22') as "마지막 날짜" FROM DUAL;`

문자형으로 데이터 유형 변환하기(TO_CHAR)

`SELECT ename, *TO_CHAR*(hiredate, 'DAY') as 요일, *TO_CHAR*(sal, '999.999') as 월급 FROM emp WHERE ename='SCOTT';`

TO_CHAR(sal, ‘999.999’)는 월급을 출력할 때 천 단위를 표시하여 출력

TO_CHAR : 숫자 데이터 → 문자형으로 변환, 날짜 데이터 → 문자형으로 변환

날짜형으로 데이터 유형 변환하기(TO_DATE)

`SELECT ename, hiredate FROM emp WHERE hiredate = *TO_DATE*('81/11/17', 'RR/MM/DD');`

현재 접속한 세션의 날짜 형식을 확인하는 쿼리

> SELECT * FROM NLS_SESSION_PARAMETERS
WHERE parameter = 'NLS_DATE_FORMAT';
> 

암시적 형 변환 이해하기

`SELECT ename, sal FROM emp WHERE sal = '3000';`

‘숫자형=문자형' 비교 가능? - 오라클에서 암시적으로 (‘숫자형=숫자형') 형 변환을 하기 때문에 에러가 발생하지 않고 검색된다.

NULL 값 대신 다른 데이터 출력하기(NVL, NVL2)

`SELECT ename, comm, *NVL*(comm, 0) FROM emp;`

```java
SELECT ename, sal, comm,NVL2(comm, sal+comm, sal) FROM emp
WHERE job IN ('SALESMAN', 'ANALYST');
```

> NVL : 대상의 값이 NULL 인 경우 지정한 값으로 치환
> 

> NVL2 : 대상의 값이 **NULL 인 경우.** 와 **NULL이 아닌 경우**를 지정한 값으로 치환
>