# Oracle 설치

Mac에서 Oracle 사용

다운로드 할 이미지 찾기

`docker search oracle -xe-11g`

jasppen 이미지 다운로드

`docker pull jaspeen/oracle-xe-11g`

다운로드 한 이미지 목록 확인

 `docker images`

컨테이너 생성과 실행

`docker run --name oracle11g-test -d -p 8080:8080 -p 1521:1521 jaspeen/oracle-xe-11g`

실행 중인 컨테이너 목록 확인 

`docker ps`

## Oracle Database SQL Plus 실행

docker에서 Oracle 데이터베이스 접속

`docker exec -it oracle11g-test sqlplus`

`user-name : system` 

`password : oracle` 

exit 명령어로 종료

docker에서 Oracle DB 명령어 사용

…