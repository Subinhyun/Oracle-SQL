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