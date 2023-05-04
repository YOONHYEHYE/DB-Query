# DB Qurey 기초

## DB

    DB(DataBase)
        - 데이터베이스는 데이터에 특화된 서버
        - 서버에서 파일로 저장해 사용해도 되지만, 원하는 데이터만 가져올 수 없기 때문에
          모든 데이터를 불러와 서버에서 필터링하기 때문에 데이터베이스가 필요하다.
        - 쿼리문을 통해서 필터링

        - DB용어 정리
            + Field
                column(열)의 가장 작은 단위의 데이터
                특정한 데이터 타입과 크기를 지정

            + Record = Tuple
                논리적으로 연관된 필드의 집합 엑셀 row(행)에 해당
                여러 필드가 모여 한 레코드를 이룸

            + Table = File
                서로 연관된 레코드의 집합을 테이블 또는 파일이라 함

            + Entity
                현실 세계에 존재하는 것을 데이터베이스 상에서 표현하기 위해 사용하는 추상적인 개념 일종의 비유

                데이터베이스에 ID, 나이, 클래스 라는 정보들을 통해 '고객'이라는 엔티티(객체)를 표현하고 구분 함

## SQL

    SQL(Structure Query Language) -> 구조화 된 Query 언어
        - 데이터베이스 용 프로그래밍 언어, 데이터베이스에 쿼리를 보내 원하는 데이터만을 추출
        - Query -> 저장되어 있는 정보를 필터 하기 위한 질문
        - 1986년 ANSI, 1987년 ISO의 기준이다.
        - 데이터베이스를 CRUD (Create, Read, Upadate, Delete)
          새로운 DB를 만들고, 조회하고, 갱신하고, 삭제

        - RDBMS(Relation Database Management System)
            + 데이터 테이블이라 불리는 데이터베이스 객체로 저장된다
            + 테이블은 연관된 데이터의 컬렉션이고 표 형식으로 이뤄짐

        - DataBase Tables
            + 데이터베이스는 하나 이상의 테이블로 이뤄져 있고,
              테이블 이름을 조회해 데이터를 확인함
            + 대문자 사용
            + SQL의 세미콜론은 SQL 구문을 분리하는 기준적인 방법

## SQL 문법

        SELECT - 데이터 추출하여 조회
        UPDATE - 데이터 갱신
        DELETE - DB로 부터 데이터 삭제
        INSERT INTO - DB에 새로운 데이터를 삽입
        CREATE DATABASE - 새로운 DB 생성
        ALTER DATABASE - DB를 생성
        CREATE TABLE - 새로운 테이블 생성
        ALTER TABLE - 테이블 수정
        DROP TABEL - 테이블 삭제
        CREATE INDEX - 검색key와 같은 인덱스 생성
        DROP INDEX - 인덱스 삭제

    1. SELECT
        - 데이터베이스로 부터 데이터를 선택하기 위해 사용
        - 반환된 데이터는  result-set이라 불리는 result table에 저장됨
        - 모든 필드 선택은 '*'을 사용
            ex) SELECT * FROM USERS;
            -> USERS 테이블에 있는 모든 데이터를 조회
        - 중복되는 데이터를 제외하고 조회 DISTINCT(구별)을 사용
            ex) SELECT DISTINCT NAME FROM USERS;
            -> USERS 테이블에서 중복된 이름을 제외하고 조회

    2. WHERE
        - 조건이 TRUE 인 기록만 추출
            ex) SELECT * FROM USERS WHERE NAME= '윤혜경';
            -> NAME이 윤혜경인 데이터의 모든 데이터 조회
            ex) SELECT NAME FROM USERS WHERE ID= 254;
            -> ID가 254인 데이터의 이름 조회

        '=' -> 같은 값
        '>' -> 더 큰 값
        '<' -> 더 작은 값
        '>=' -> 크거나 같은 값
        '<=' -> 작거나 같은 값
        '<>' -> 같이 않은 값만 ('!='도 사용)

        - BETWEEN : 특정범위
            ex) SELECT * FROM USERS WHERE AGE BETWEEN 20 AND 30;
            -> 나이 20~30세 사이 사용자 데이터 조회

        - LIKE : 같은 패턴
            ex) SELECT * FROM USERS WHERE NAME LIKE '윤%';
            -> 이름이 윤으로 시작하는 사용자 데이터 조회

        - IN : 특정한 여러 값들
            ex) SELECT * FROM USERS WHERE NAME IN ('윤혜경', 김땡땡);
            -> 이름이 윤혜경과 김땡땡인 사용자 데이터 조회

        - AND: 모든 조건이 TRUE
            ex) SELECT * FROM USERS WHERE NAEM= '윤혜경' AND ID= 235;
            -> 이름이 윤혜경이고 ID가 235인 데이터를 조회

        - OR: 어떤 조건이든 TURE
            ex) SELECT * FROM USERS WHERE NAME= '윤혜경' OR NAME= '김땡땡';
            -> 이름이 윤혜경 이거나 김땡땡인 데이터를 조회

        - NOT: 조건을 뺀 나머지
            ex) SELECT * FROM USERS WHERE NOT NAME= '윤혜경';
            -> 이름이 윤혜경이 아닌 데이터를 조회

        - AND, OR 같이 쓰는 방법
            ex) SELECT * FROM USERS WHERE NAME= '윤혜경' AND (ID= 235 OR ID= 237);
            -> 이름이 윤혜경이고 ID가 235 이거나 237인 데이터를 조회

        - AND, OR 같이 쓰는 방법
            ex) SELECT * FROM USERS WHERE NOT NAME= '윤혜경' AND NOT ID= 235;
            -> 이름이 윤혜경이고 ID가 235인 데이터를 제외한 나머지 조회

        - ORDER
            + 오름차순, 내림차순으로 정렬
            + default 오름차순 내림차순은 DESC

            ex) SELECT * FROM USERS OREDR BY NAME;
            -> 이름이 오름차순으로 정렬되어 조회

            ex) SELECT * FROM USERS OREDR BY NAME DESC;
            -> 이름이 내림차순으로 정렬되어 조회

            ex) SELECT * FROM USERS OREDR BY NAME, ID;
            -> 이름이 오름차순으로 정렬되고 같은 이름이면 ID 오름차순으로 정렬됨

            ex) SELECT * FROM USERS OREDR BY NAME ASC, ID DESC;
            -> 이름이 오름차순으로 정렬되고 같은 이름이면 ID 내림차순으로 정렬됨

        - INSERT INTO
            + 테이블에 새로운 데이터를 삽입

            ex) INSERT INTO USERS (NAME, ID, AGE, ADDRESS) VALUES('윤혜경', 235, 34, '서울특별시');
            -> USERS테이블 열에 VALUES 값을 순서대로 넣음

            ex) INSERT INTO USERS(NAME, ID, AGE, ADDRESS) VALUES('윤혜경', 235, 34);
            -> USERS테이블 열에 VALUES 값을 순서대로 넣고, ADDRESS 데이터는 없음으로 NULL 처리

        - NULL
            + 데이터 값이 없음
            + 데이블의 필드가 필수가 아니라면 새로운 레코드를 삽입하거나
              해당 필드에 값을 추가하는 것 없이 갱신하는 것이 가능하다.
              그리고 그 필드는 NULL 값으로 저장

        - IS NULL
            ex) SELECT NAME, ID, AGE, ADDRESS FROM USERS WHERE ADDRESS IS NULL
            -> USERS테이블에서 ADDRESS가 NULL인 값을 조회

        - IS NOT NULL
            ex) SELECT NAME, ID, AGE, ADDRESS FROM USERS WHERE ADDRESS IS NOT NULL
            -> USERS테이블에서 ADDRESS가 NULL이 아닌 값을 조회

## SQL Wildcards Characters

    + 문자열 하나 이상의 문자를 대체
    + SQL LIKE 연산자와 함께 사용
    + LIKE 연산자는 열에서 특정한 패턴을 찾기 위해 WHERE 절에서 사용됨

    + Wildcard Characters in SQL Server
        - '%': 0또는 그 이상의 문자를 표시
            ex)SELECT * FROM USERS WHERE ADDRESS LIKE '서울특별시%';
            -> USERS 테이블에 ADDRESS에 서울특별시로 시작하는 값 조회

        - '_': 하나의 문자를 표시
            ex)SELECT * FROM USERS WHERE ADDRESS LIKE '서_특_시';
            -> USERS 테이블에 ADDRESS에 서()특()시에 해당하는 값 조회

        - '[]': 브라켓 안의 문자중 하나를 표시
            ex)SELECT * FROM USERS WHERE ADDRESS LIKE '[서경]%';
            -> USERS 테이블에 ADDRESS에 서, 경으로 시작하는 값 조회

        - '!': 브라켓 안의 없는 문자를 표시
            ex)SELECT * FROM USERS WHERE ADDRESS LIKE '[!서경]%';
            -> USERS 테이블에 ADDRESS에 서, 경으로 시작하지 않는 값 조회

        - '-': 문자의 범위를 표시
            ex)SELECT * FROM USERS WHERE ADDRESS NOT LIKE '[서경]%';
            -> USERS 테이블에 ADDRESS에 서, 경으로 시작하는 값 조회

## SQL Aliases

    + alias는 테이블, 테이블 열에 임시로 이름을 주는데 사용
    + alias는 더 읽기 쉬운 열 이름을 만드는데 사용
    + 하나의 alias는 쿼리가 지속되는 동안만 존재

        ex)SELECT ID AS USERID FROM USERS;
        -> USERS 테이블의 ID 를 USERID로 보이게

        ex)SELECT NAME AS USERNAM, ID AS [number] FROM USERS;
        -> USERS 테이블의 공백이 있는 allias는 "" 또는 []로 묶기

        ex)SELECT NAME , INFO(ID, AGE, ADDRESS) AS INFOMATION FROM USERS;
        -> ID, AGE, ADDRESS를 묶어서 INFOMATION으로 보이게 필터링

        ex)SELECT u.ID, u.ADDRESS, c.ID FROM USERS AS u, COMPANY AS c; WHRER c.ID= 11457 AND u.ID=c.ID
        -> USERS 테이블을 u, COMPANY테이블을  c로 해서 각 테이블에서 필요한 WHRER 조건에 해당하는 값 조회

## SQL Joins

    + 두개 이상의 테이블 행을 결합

        - (INNER) JOIN : 두 테이블에서 매치되는 값의 레코드 반환

            ex) SELECT USERS.ID, COMPANY.ID, USERS.DATE
                FROM USERS
                INNER JOIN COMPANY ON USERS.ID=COMPANY.ID;
            -> USERS 테이블 ID와 COMPANY 테이블 ID가 같은 값 중에 두 테이블에서 필요한 열들의 값을 필터링

            * TABLE 3개
            ex) SELECT USERS.ID, COMPANY.ID, COIN.ID
                FROM ((USERS
                INNER JOIN COMPANY ON USERS.ID = COMPANY.ID)
                INNER JOIN COIN ON USERS.ID = COIN.ID);
            -> USERS 테이블 ID와 COMPANY 테이블 ID가 같은 값 중에 두 테이블에서 필요한 열들의 값을 필터링,
               USERS 테이블 ID와 COIN 테이블 ID가 같은 값 중에 두 테이블에서 필요한 열들의 값을 필터링

        - LEFT (OUTER) JOIN : 매치되는 오른쪽 테이블의 레코드 + 왼쪽의 모든 레코드를 반환

            LEFT JOIN 키워드는 왼쪽 테이블의 모든 레코드와 오른쪽 테이블의 매치된 레코드를 반환
            만약 매치되는 항목이 없다면 오른쪽의 결과는 NULL

            ex) SELECT USERS.ID, COMPANY.ID, USERS.DATE
                FROM USERS
                LEFT JOIN COMPANY ON USERS.ID=COMPANY.ID;
                ORDER BY USERS.ID
            -> USERS 테이블 모든 레코드와 COMPANY 테이블의 매칭되는 레코드를 조회

        - RIGHT (OUTER) JOIN : 매치되는 왼쪽 테이블의 레코드 + 오른쪽의 모든 레코드를 반환

            RIGHT JOIN 키워드는 오른쪽 테이블의 모든 레코드와 왼쪽 테이블의 매치된 레코드를 반환
            매치되는 항목이 없다면 왼쪽으로 부터의 결과는 NULL

            ex) SELECT Orders.OrderID, Employees.LastName, Employees.FirstName
                FROM Orders
                RIGHT JOIN Employees
                ON Orders.EmployeeID = Employees.EmployeeID
                ORDER BY Orders.OrderID;
