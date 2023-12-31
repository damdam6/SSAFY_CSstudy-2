## 4.2 ERD와 정규화 과정

- ERD (Entity Relationship Diagram) : 데이터베이스를 구축할 때 가장 기초적인 뼈대로 릴레이션 간의 관계를 정의한 것
- 개체 속성과 개체 간 관계를 그림으로 표현한 것

### 4.2.1 ERD의 중요성

- 시스템의 요구사항을 기반으로 작성되어 이를 기반으로 데이터베이스를 구축
- 데이터베이스 구축 후에도 디버깅 or 비즈니스 프로세스 재설계가 필요한 경우에도 설계도 역할을 담당하기도 함
- 그러나 관계형 구조가 아닌 비정형 데이터는 충분히 표현할 수 없다

### 4.2.3 정규화

- 정규화 : 릴레이션을 여러개로 분리하는 과정
- 장점

  - 릴레이션 간의 잘못된 종속 관계로 인한 데이터베이스 **이상 현상**이 일어날 때 이를 해결
  - 저장공간을 효율적으로 사용
  - 새로운 속성 추가하여 DB 확장시 구조의 변경을 최소화할 수 있음

- 단점
  - 릴레이션의 분해로 인해 릴레이션의 연산이 많아져 오히려 응답 시간이 느려질 수도 있음
  - 이 때 반정규화를 통해 성능 향상 가능

* 이상현상
  - 삽입 이상 (insertion anomaly) : 원하지 않는 자료가 삽입된다든지, key가 없어 삽입하지 못하는(불필요한 데이터를 추가해야 삽입할 수 있음) 문제점
  - 삭제 이상 (deletion anomaly) : 하나의 자료만 삭제하고 싶지만, 그 자료가 포함된 튜플 전체가 삭제됨으로 원하지 않는 정보 손실이 발생하는 문제점
  - 갱신 이상 (update anomaly) : 일부만 변경하여 데이터가 불일치하는 모순, 또는 중복되는 튜플이 존재하게 되는 문제점.
    <br>
* 반정규화
  - 시스템 성능 향상을 위해 정규화된 데이터 모델을 통합
  * 테이블이 단순해지고 관리 효율성이 증가함
  * 데이터의 일관성이나 무결성이 보장되지 않을 수 있음
  * 의도적으로 중복을 생성하여 검색기능은 향상되나 갱신, 삭제 성능이 낮아짐
  * 아래의 경우 반정규화의 대상이 된다
    1. 수행 속도가 많이 느린 경우
    2. 테이블의 JOIN 연산을 지나치게 사용하여 데이터를 조회하는 것이 기술적으로 어려운 경우
    3. 테이블에 많은 데이터가 있고, 다량의 범위, 혹은 특정 범위를 자주 처리해야 하는 경우

<br>

- 정규형 (NF, Normal Form) : 정규화된 정도
  - 기본 정규형 : 제 1, 2, 3 정규형, 보이스/코드 정규형
  - 고급 정규형 : 제 4, 5 정규형

##### 정규형 원칙

1. 정보의 무손실 : 분해된 릴레이션이 표현하는 정보는 분해되기 전 정보를 모두 포함해야
2. 최소 데이터 중복 : 자료 중복성 감소되어야
3. 분리의 원칙 : 독립적인 관계는 별개의 릴레이션으로 표현해야
   - 각각의 릴레이션은 독립적으로 표현 가능해야

###### [정규형 참고 블로그](https://rebro.kr/160)

##### 제1정규형

- 릴레이션에 속하는 속성의 속성값이 모두 원자값(더 이상 쪼개질 수 없는 단위)으로만 구성되어야한다
- 릴레이션의 속성 값 중 한 개의 기본키에 대해 두 개 이상의 값을 가지는 반복집합이 있으면 안됨

- 발생할 수 있는 이상현상
  - 예시 : 학번, 과목번호를 기본키로 가지며 학번, 지도교수, 학과, 과목번호, 성적 속성을 가진다
  * 삽입 이상 : 학생이 새 과목을 수강 신청할 때 반드시 학생의 학과와 지도교수를 알아야 한다. (불필요한 정보)
  * 삭제 이상 : 300번 학생이 C400 과목을 취소하면, 해당 과목에 대한 정보가 모두 사라진다.
  * 갱신 이상 : 100번 학생이 지도교수를 변경할 때, P1인 행을 모두 찾아서 변경해주어야 한다.
- 이상 현상 발생 이유
  - 기본키가 아닌 속성들이 기본키에 완전 함수 종속되지 못하고 부분 함수 종속되기 때문
  - 즉, 기본키의 일부 속성에만 의존하기 때문

##### 제2정규형

- 제1정규형이면서 부분 함수의 종속성을 제거함 (기본키에 속하지 않는 속성 모두가 기본키에 완전 함수 종속)

- 주의할 점

  - 릴레이션을 분리할 때 동등한 릴레이션으로 분해
  - 정보 손실이 발생하지 않는 무손실 분해로 이루어져야

- 발생할 수 있는 이상현상
  - 예시 : 위 예시에서
  * 삽입 이상 : 지도교수가 학과에 소속되어 있음을 추가할 때 반드시 지도 학생이 있어야 한다. (불필요한 정보 필요)
  * 삭제 이상 : 300번 학생이 자퇴하는 경우 P3 교수의 학과 정보가 사라진다.
  * 갱신 이상 : 지도교수의 학과가 변경되는 경우 모두 찾아서 변경시켜주어야 한다. (지도교수가 동일한 학생이 여러 명 있는 경우)
- 이상 현상 발생 이유
  - 이행적 함수 종속성 (transitive FD): A -> B && B -> C && A -> C
  - 예시 : 학번 -> 지도교수, 지도교수 -> 학과, 학번 -> 학과
  * 지도교수의 학과를 추가하기 위해서 지도 학생까지 필요하게 되고, 학생이 자퇴하였는데 지도교수의 학과 정보가 사라지는 문제점이 발생

##### 제3정규형

- 제2정규형이면서 기본키가 아닌 모든 속성이 이행적 함수 종속을 만족하지 않는 상태
- 즉, 기본키에 속하지 않은 모든 속성이 기본키에 이행적 함수 종속이 아닐 때
- 즉, A->B && B->C 관계만 존재하고 A->C는 없게 릴레이션을 분리

##### 보이스/코드 정규형

- 제3정규형이면서 결정자가 후보키가 아닌 함수종속관계를 제거하여 **릴레이션의 함수종속관계에서 모든 결정자가 후보키인 상태**
- 강한 제3정규형이라고 부르기도 함
- 결정자란 ?
  - 함수 종속 관계에서 특정 종속자를 결정짓는 요소
  - X->Y일 때 X가 결정자, Y가 종속자
