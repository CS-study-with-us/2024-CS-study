# ORM(JPA,JPQL)

### ✨ ORM
* Object Relational Mapping
* 자바의 객체와 데이터베이스를 연결하는 프로그래밍 기법.

### ✨ ORM 장점
* SQL 을 공부하여 직접 작성하지 않아도, 사용하는 언어로 데이터베이스에 접근할 수 있습니다.

    따라서, SQL지식의 필요성이 줄어들고 개발 프로세스가 간소화될 수 있습니다.
* 객체지향적으로 코드를 작성할 수 있습니다.
* 데이터베이스 시스템에 대한 종속성이 줄어듭니다.

### ✨ ORM 단점
* 프로젝트의 복잡성이 높거나 무거운 쿼리는 사용 난이도가 올라가거나 ORM으로 해결이 어려운 경우가 있습니다.

### ✨ ORM 종류
* Flask : SQLAlchemy
* Django : 내장 ORM
* JAVA : Hybernate, JPA
* Node.js : Sequalize

### ✨ JPA
* Java Persistence API
* 자바에서 관계형 데이터베이스를 사용하는 방식을 정의한 인터페이스.
* 자바 객체와 데이터베이스를 연결해 데이터를 관리.

### ✨ JPQL
* Jakarta Persistence Query Language
* 데이터베이스에 저장된 엔티티를 쿼리하는데 사용.
* 데이터베이스 테이블이 아닌, 엔티티 객체를 대상으로 쿼리.
* SQL과 문법이 유사.

### ✨JPA VS JPQL
JPA는 기본적인 CRUD 작업에 용이하지만, 조인과 서브쿼리 등에는 취약하다는 문제점이 있습니다.

이에 JPQL 을 직접 만들어 처리하여 이 문제를 해결할 수 있습니다.

하지만, JPQL 은 기본 문자열로 작성되기 때문에, 컴파일 시 에러를 발생시키지 않는다는 문제점이 있습니다. 

또한, 동적으로 쿼리언어를 작성하는 데 효율적이지 못합니다.

## 📃예상문제
<!-- 공부한 내용을 바탕으로 예상 질문을 최소 1개 이상 작성해주세요.-->
1. JPA 와 JPQL의 차이점에 대해 설명해주세요. 

## 🔗참고 자료
<!-- 공부 과정에서 참고한 자료가 있다면, 첨부해주세요-->
<!-- * [자료주제](링크)  -->
- 스프링 부트 3 백엔드 개발자 되기
- https://why-dev.tistory.com/284
- https://velog.io/@mpfo0106/ORMOject-Relational-Mapping-Framework-%EB%9E%80
- https://ittrue.tistory.com/270