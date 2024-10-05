# 좋은 객체 지향 설계의 5가지 원칙(SOLID)

## 1. SOLID

- SRP(단일 책임 원칙)
- OCP(개방-폐쇄 원칙)
- LSP(리스코프 치환 원칙)
- ISP(인터페이스 분리 원칙)
- DIP(의존관계 역전 원칙)

### SRP 단일 책임 원칙

- 한 클래스는 하나의 책임만 가져야 함
- ‘하나의 책임’ → 기준은 ‘변경’. 변경이 있을 때 파급 효과가 적어야함
- ex. UI 변경, 객체의 생성과 사용을 분리

### OCP 개방-폐쇄 원칙

- 확장에는 열려 있고 변경에는 닫혀 있어야함
- 기능을 확장할 때 기존 코드 변경을 최소화해야한다
- 다형성을 활용
- 인터페이스를 구현한 새로운 클래스 만들어서 새로운 기능을 구현
- 문제점
  ```Java
      public class MemberService {
          private MemberRepository memberRepository = new MemoryMemberRepository();
      }
  ```
  ```Java
      public class MemberService{
          // private MemberRepository memberRepository = new MemoryMemberRepository();
          private MemberRepository memberRepository = new JdbcMemberRepository();
      }
  ```
  → 구현 객체를 변경하려면 클라이언트 코드를 변경해야함. 다형성 사용했는데 OCP원칙 지킬 수 없음
  → 객체 생성, 관계 맺어주는 별도의 설정자 필요함 ⇒ 스프링 컨테이너가 해준다

### LSP 리스코프 치환 원칙

- 구현체를 만들 때 인터페이스의 규약을 지켜서 만들어야 함
- 다형성을 지원하기 위한 원칙

### ISP 인터페이스 분리 원칙

- 특정 클라이언트를 위한 인터페이스 여러개가 범용 인터페이스 하나보다 좋음
- 자동차 인터페이스를 운전 인터페이스, 정비 인터페이스로 분리
- 사용자 클라이언트를 운전자 클라이언트, 정비사 클라이언트로 분리
- 정비 인터페이스가 변해도 운전자 클라이언트에게 영향 주지 않음

### DIP 의존관계 역전 원칙

- 구현 클래스가 인터페이스를 바라보게 해야한다
- 역할에 의존하게 해야 한다
  ```Java
      public class MemberService {
          private MemberRepository memberRepository = new MemoryMemberRepository();
      }
  ```
  ```Java
      public class MemberService{
          // private MemberRepository memberRepository = new MemoryMemberRepository();
          private MemberRepository memberRepository = new JdbcMemberRepository();
      }
  ```
  → MemberService는 인터페이스에 의존하지만, MemoryMemberRepository에도 의존하고 있음, 구현 클래스를 직접 선택하고 있음
  → DIP 위반

### 정리

- 객체 지향의 핵심은 다형성
- 그런데 다형성 만으로는 OCP, DIP를 지킬 수 없다
- 다형성 만으로는 구현 객체를 변경할 때 클라이언트 코드도 변경해야한다
- MemberService가 MemberRepository라는 인터페이스에만 의존하도록 해야하는데 그러려면 뭔가가 더 필요하다

## 2. 객체 지향 설계와 스프링

- 스프링은 다음 기술로 다형성 + OCP, DIP를 가능하게 함
  - DI(Dependency Injection): 의존관계, 의존성 주입
  - DI 컨테이너 제공: 자바 객체들을 컨테이너 안에 넣고 의존관계 주입하는 기능 제공
- 클라이언트 코드의 변경 없이 기능 확장

### 정리

- 모든 설계에 역할과 구현을 분리
- 모든 설계에 인터페이스 부여 (이상적)
- 간단한 인터페이스를 만들어서 일단 개발하고, 추후에 정해지는 내용들로 갈아끼우면 됨
- 하지만 인터페이스를 도입하면 추상화라는 비용 발생, 개발자가 구현클래스 코드를 열어봐야함
- 기능 확장 가능성이 없으면 구체 클래스를 직접 쓰고, 나중에 필요할 때 인터페이스 도입해도 됨

## 예상 질문

<!-- 공부한 내용을 바탕으로 예상 질문을 최소 1개 이상 작성해주세요.-->

1. 객체지향 설계 원칙 5가지에 대해 설명해주세요.
2. 스프링의 의존성 주입(DI)가 필요한 이유가 무엇인가요?

## 참고 자료

<!-- 공부 과정에서 참고한 자료가 있다면, 첨부해주세요-->
<!-- * [자료주제](링크)  -->

- 토비의 스프링 3.1 (이일민)
