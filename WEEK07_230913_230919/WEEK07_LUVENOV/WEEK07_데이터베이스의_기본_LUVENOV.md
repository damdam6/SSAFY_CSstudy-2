# WEEK07_데이터베이스의 기본

---

# 4.1 데이터베이스의 기본

---

- 데이터베이스(DB, DataBase)는 일정한 규칙, 혹은 규약을 통해 구조화되어 저장되는 데이터 모음
- **DBMS** : 해당 데이터베이스를 제어, 관리하는 통합 시스템 (**DataBase Management System**)
- 데이터베이스 내부 데이터들은 특정 DBMS마다 정의된 쿼리 언어를 통해 삽입, 삭제, 수정, 조회 등 수행
- 데이터베이스는 실시간 접근과 동시 공유 가능

![Untitled](WEEK07_데이터베이스의_기본_image/Untitled.png)

- 데이터베이스 위에 DBMS가 있고 그 위에 응용 프로그램이 있으며, 이러한 구조를 기반으로 데이터를 주고받음
    
    ex ) MySQL이라는 DBMS가 있고 그 위에 응용 프로그램에 속하는 Node.js나 php에서 해당 데이터베이스 안에 있는 데이터를 끄집어내 해당 데이터 관련 로직 구축
    

## 4.1.1 엔터티(entity)

- 사람, 장소, 물건, 사건, 개념 등 여러 개의 속성을 지닌 명사 의미
    
    ex ) 회원 "엔터티” / 이름, 아이디, 주소, 전화번호 등의 “속성”
    
- 속성은 서비스의 요구 사항에 맞춰 정해짐

### 약한 엔터티와 강한 엔터티

- A가 혼자서는 존재하지 못하고 B의 존재 여부에 종속적 → A : 약한 엔터티, B : 강한 엔터티

## 4.1.2 릴레이션(relation)

- 데이터베이스에서 저보를 구분하여 저장하는 기본 단위
- 엔터티에 관한 데이터를 데이터베이스는 릴레이션 하나에 담아서 관리
- 릴레이션은 관계형 데이터베이스에서는 ‘테이블’이라고 하며, NoSQL 데이터베이스에서는 ‘컬렉션’이라고 함

![Untitled](WEEK07_데이터베이스의_기본_image/Untitled%201.png)

→ 회원이라는 엔터티가 데이터베이스에서 관리될 때 릴레이션으로 변화

### 테이블과 컬렉션

- 데이터베이스 종류
    - 관계형 데이터베이스(MySQL)
        - 구조 : 레코드 - 테이블 - 데이터베이스
    - NoSQL 데이터베이스(MongoDB
        - 구조 : 도큐먼트 - 컬렉션 - 데이터베이스

![Untitled](WEEK07_데이터베이스의_기본_image/Untitled%202.png)

→ 레코드가 쌓여서 테이블, 테이블이 쌓여서 데이터베이스

## 4.1.3 속성(attribute)

- 릴레이션에서 관리하는 구체적이며 고유한 이름을 갖는 정보
    
    ex ) 차 "엔터티” / 차 넘버, 바퀴 수, 차 색깔, 차종 등의 “속성”
    

## 4.1.4 도메인(domain)

- 릴레이션에 포함된 각각의 속성들이 가질 수 있는 값의 집합
    
    ex ) 성별 “속성” / {남,여} 라는 값을 가질 수 있음
    

![Untitled](WEEK07_데이터베이스의_기본_image/Untitled%203.png)

## 4.1.5 필드와 레코드

- 앞의 내용을 기반으로 데이터베이스에서 필드와 레코드로 구성된 테이블 생성 가능

![Untitled](WEEK07_데이터베이스의_기본_image/Untitled%204.png)

→ 회원이라는 엔터티은 member 테이블로 속성인 이름, 아이디 등을 가지고 있으며 name, ID, adress 필드를 가짐

→ 레코드(**튜플**) : 테이블에 쌓이는 행(row) 단위의 데이터

### 필드 타입

- 필드는 타입을 가지며( ex. 이름 : 문자열, 전화번호 : 숫자) DBMS마다 상이
1. **숫자**
- TINYINT, SMALLINT, MEDIUMINT, INT, BIGINT 등

![Untitled](WEEK07_데이터베이스의_기본_image/Untitled%205.png)

1. **날짜 타입**
- DATE
    - 날짜 부분은 있으나 시간 부분이 없는 값
    - 지원 범위 : 1000-01-01 ~ 9999-12-31
    - 용량 : 3byte
- DATETIME
    - 날짜 및 시간 부분을 모두 포함하는 값
    - 지원 범위 : 1000-01-01 00:00:00 ~ 9999-12-31 23:59:59
    - 용량 : 8byte
- TIMESTAMP
    - 날짜 및 시간 부분을 모두 포함하는 값
    - 지원 범위 : 1970-01-01 00:00:01 ~ 2038-01-19 03:14:07
    - 용량 : 4byte
1. **문자 타입**
- CHAR & VARCHAR
    - 수를 입력해서 몇 자까지 입력할지 설정
        
        ex ) CHAR(30)는 30자까지 입력 가능
        
    - CHAR
        - 고정 길이 문자열(0 ~ 255)
        - 레코드 저장 시 무조건 선언한 길이 값으로 ‘고정’해서 저장
            
            ex ) CHAR(100)으로 선언 시 10글자를 저장해도 100byte 저장
            
    - VARCHAR
        - 가변 길이 문자열(0 ~ 65,535)
        - 입력된 데이터에 따라 용량을 가변시켜 저장
            
            ex ) VARCHAR(1000)으로 선언했더라도 10글자만 저장했다면 10글자 해당 byte + 길이기록용 1byte로 저장
            
    - CHAR은 유동적이지 않은 길이의 데이터 저장 시 효율적, VARCHAR은 유동적 길이를 가진 데이터 저장 시 효율적
- TEXT & BLOB
    - 큰 데이터 저장 시 사용
    - TEXT
        - 큰 문자열 저장에 사용되며 주로 게시판 본문 저장 시
    - BLOB
        - 이미지, 동영상 등 큰 데이터 저장 시 사용
        - 보통은 아마존의 이미지 호스팅 서비스인 S3를 이용하는 등 서버에 파일을 올리고 파일에 관한 경로를 VARCHAR로 저장
- ENUM & SET
    - 문자열을 열거한 타입
    - ENUM
        - ENUM(’x-small’, ‘small’, ‘medium’, ‘large’, ‘x-large’) 형태로 쓰이며, 이 중 하나만 선택하는 단일 선택만 가능
        - ENUM 리스트에 없는 잘못된 값 삽입 시 빈 문자열이 대신 삽입
        - ENUM 이용 시 x-small 등이 0, 1으로 매핑되어 메모리를 적게 사용하는 이점 존재
        - 최대 65,535개의 요소를 넣을 수 있음
    - SET
        - ENUM과 비슷하지만 여러 개의 데이터 선택 가능
        - 비트 단위 연산 가능
        - 최대 64개의 요소를 넣을 수 있음
    - ENUM이나 SET 사용 시 공간적 이점을 볼 수 있으나 애플리케이션의 수정에 따라 데이터베이스의 ENUM이나 SET에서 정의한 목록을 수정해야 한다는 단점 존재

## 4.1.6 관계

- 데이터베이스에 테이블은 여러 개 존재하며 서로의 관계가 정의되어 있음
- 관계화살표를 통해 관계 표시
    
    ![Untitled](WEEK07_데이터베이스의_기본_image/Untitled%206.png)
    

### 1:1 관계

ex ) 유저 당 유저 이메일 한 개씩

- 테이블을 두 개의 테이블로 나눠 테이블의 구조를 더 이해하기 쉽게 만듦

### 1:N 관계

ex ) 유저 당 여러 개의 상품을 장바구니에 담기 가능(0개의 경우도 포함)

- 한 개체가 다른 많은 개체를 포함하는 관계

### N:M 관계

ex ) 학생↔강읜 // 학생은 여러 강의 수강 가능, 강의도 여러 학생 포함 가능

- 테이블 두개를 직접적으로 연결해서 구축 X
- 1:N, 1:M이라는 관계를 갖는 테이블 두 개로 나눠서 설정

## 4.1.7 키

- 테이블 간의 관계를 조금 더 명확하게 하고 테이블 자체의 인덱스를 위해 설정된 장치

![Untitled](WEEK07_데이터베이스의_기본_image/Untitled%207.png)

→ 키 간의 관계

→ 슈퍼키는 유일성을 가지고 후보키는 최소성까지 가지며, 후보키 중 기본키로 선택X 시 대체키

→ 유일성은 중복값이 없고, 최소성은 필드를 조합하지 않고 최소 필드만 써서 키 형성 가능

### 기본키(Primary Key, PK, 프라이머키)

- 유일성과 최소성 만족
- 테이블의 데이터 중 고유하게 존재하는 속성이며 기본키에 해당하는 데이터는 **중복 불가 (중복 시 기본키로 설정 불가)**
- 자연키와 인조키 중 골라 설정
    - 자연키 : 중복된 값들을 제외하며 중복되지 않은 것을 ‘자연스러’ 뽑다가 나오는 키(언젠가는 변하는 속성을 가짐)
    - 인조키 : 인위적으로 고유식별자를 설정하여 생성한 키(변하지 않음) → 보통 기본키로 설정

### 외래키(Foreign Key, FK)

- 다른 테이블의 기본키를 그대로 참조하는 값으로, 개체와의 관계 식별 시 사용
- 중복 가능

### 후보키(Candidate Key)

- 기본키가 될 수 있는 후보들이며 유일성과 최소성 동시에 만족

### 대체키(Alternate Key)

- 후보키가 두 개 이상일 경우 어느 하나를 기본키로 지정하고 남은 후보키

### 슈퍼키(Super Key)

- 각 레코드를 유일하게 식별 가능한 유일성을 갖춘 키