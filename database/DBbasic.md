메타데이터: database를 정의하거나 기술하는 data

ex) 데이터 유형,구조 ,제약 조건, 인덱스 등등

## 데이터 모델

**DB의 구조를 기술하는데 사용될 수 있는 개념들이 모인 집합

-DB 구조를 추상화해서 표현할 수있는 수단

conceptual data models

일반 사용자들이 쉽게 이해할수있는 모델 ex)ER-diagram

VDL로 정의할수 있음

logical data models

디테일하게 DB를 구조화 할 수 있는 개념,데이터가 컴퓨터에 저장될 때의 구조와 크게 다르지 않음

DDL로 정의할 수 있음

ex) relational data model, 0bject-reational data model

physical data models

컴퓨터에 어떻게 파일 형태로 저장되는지를 기술할 수 있는 수단을 제공

## 스키마

데이터 모델을 바탕으로 DB의 구조를 기술 한 것, 한번 정해진 후에는 자주 바뀌지 않음

three-schema architecture

각 레벨을 독립시켜서 어느 레벨에서의 변화가 상위 레벨에 영향을 주지 않기 위함

database system을 구축하는 아키텍처중 하나

user application으로 부터 물리적인 DB를 분리 시키는 목적

external scheas=user views

특정 유저들이 필요로 하는 데이터만 표현

conceptual schema

전체 DB에 대한 구조를 기술, 물리적인 저장 구조에 관한 내용은 숨김

ex)entites, relationships, data types

internal schema

물리적으로 데이터가 어떻게 저장되는지 physical data models을 통해 표현

mysql에서는 DATABASE와 SCHEMA가 같은 뜻을 의미

## 정규화

릴레이션 간의 잘못된 종속 관계로 인해 DB 이상 현상이 일어나서 여러 개로 분리하는 과정

## 트랜잭션

데이터베이스에서 하나의 논리적 기능을 수행하기 위한 작업의 단위

여러 SQL문들을 단일 작업으로 묶어서 나눠질 수 없게 만든 것

AUTOCOMMIT

START Transaction →   xxx  → Commit 하면 끝

@Transactinal

@Schedule

각 transaction 내의 operations 들의 순서는 바꾸지 않음
@Serail Schedule

transaction들이 겹치지 않고 한 번에 하나씩 실행되는 schedule

Nonserial Schedule

겹쳐짐

### 원자성

커밋,롤백

### 격리성

트랜 잭션 수행시 서로 끼어들지 못하는 것을 말함

격리 수준에 따라 발생하는 현상

팬텀 리드: 한 트랜잭션 내에서 동일한 쿼리를 보냈을 때 조회 결과가 다른 경우

반복 가능하지 않은조회: 트랜잭션 내의 같은 행에 두번 이상 조회가 발생 했는데 그 값이 다른 경우

더티 리드

격리 수준

SERIALIZABLE: 트랜잭션을 순차적으로 진행시키는 것

매우 엄격한 수준으로 해당 행에 대해 격리시키고, 이후 트랜잭션이 일어난다면 기다려야함

REPEATABLE_READ: 하나의 트랜잭션이 수정한 행을 다른 트랜잭션이 수정할 수 없도록 막아줌

But 새로운 행을 추가하는 것을 막지않음
READ_COMMITED: 가장 많이 사용되는 격리 수준, 커밋 완료된 데이터에 대해서만 조회 허용

READ_UNCOMMITED:가장 낮은 격리 수준, 데이터 무결성을 위해 되도록 사용X

### 지속성

저널링,롤백, 체크섬

### 일관성

## 인덱스

데이터를 빠르게 찾을 수 있는 하나의 장치

B-트리로 이루어져있음

루트노드,리프 노드, 브랜치 노드로 나뉜다

## DDL

WHERE 절

where 절에 있는 조건 값의 결과가 TRUE 인 tuple만 선택 된다

⇒결과가 FALSE거나 UNKNOWN이면 tuple은 선택되지 않음

NOT in과 NOT EXISTS의 차이

### 조인

implicit join: from절에는 table만 나열하고 where절에 join condition을 명시하는 방식

오래된 방식, 가독성이 떨어짐

explicit join: from절에 join키워드와 함께 테이블들을 명시

가독성이 좋음, 복잡한 join 쿼리 작성 중에도 실수한 가능성이 적음

inner join: 두 table에서 join 조건을 만족하는 tuple들로 결과 table을 만드는 조인

join 조건에서 null 값을 가지는 tuple은 결과 테이블에 포함되지 않음

USING을 사용하면 간편하게 작성할수 있음 두 개의 값이 하나로 표현이 됨

outer join: 두 table에서 join 조건을 만족하지않는 tuple들로 결과 table을 만드는 조인

1. lett join
2. right join
3. full join

equi join

join 조건에서 = 을 사용하는 join

natural join

두 테이블에서 같은 이름을 가지는 모든 값에 대해서 equi join을 표현

같은 컬럼의 이름이 값이 다르다면 값을 반환하지 않음

croos join

두 테이블에서 모든 값으로 만들 수 있는 모든 조합

## 트리거

Trigger

update,delete, insert 작성 가능

단점:소스 코드로는 발견할 수 없는 로직이기 때문에 어떤 동작이 일어나는지 파악하기 어려움