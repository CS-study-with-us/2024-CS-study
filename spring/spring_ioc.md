## 제어의 역전(Inversion of Control)

메서드나 객체의 호출 작업을 개발자가 아닌 스프링에게 제어권을 넘기는 것을 말합니다.
이전까지는 개발자가 객체의 생성을 관리하며 제어했지만 스프링을 사용하게 되면 스프링 컨테이너에게 제어권을 넘겨 스프링 컨테이너가 흐름을 제어하게 됩니다.

```
public class Point {
private A a;

public Point() {
   a = new A();
}

}
```
원래는 위처럼 개발자가 직접 객체를 생성하여 제어를 관리해주어야 했습니다.

```
public class Point {

@Autowired
private A a;


}
```
하지만 스프링에서는 A라는 객체가 @Autowired를 통해 객체를 주입받아 스프링 컨테이너에서 관리를 받고 있고 있습니다.
<br>이것을 제어의 역전이라 부르고 개발자가 해야 할 제어를 스프링 컨테이너에서 대신 해주는 것입니다.


## IoC 의 장점

- 객체간 결합도를 낮춘다.
- 유연한 코드 작성 가능하다.
- 가독성이 올라간다.
- 코드의 중복을 방지한다.
- 유지보수가 용이하다.

## 의존성 주입 (Dependency Injection)
제어의 역전의 한 종류라고 할 수 있으며,
객체를 직접 생성하는 게 아닌 외부(IOC 컨테이너)에서 생성한 후 주입시켜주는 방식입니다.
코드의 결합도를 낮추고 재사용성 및 테스트 용이성을 향상시킵니다.

* 의존성이란?<br>
만약 A와 B라는 두 개의 클래스가 존재할 때, A 클래스에서 B 클래스의 기능을 사용하기 위해 B 클래스에 구현되어 있는 어떤 메서드를 호출하는 상황이 있다면, A 클래스는 B 클래스에 의존하게 됩니다.


### 종류
- 생성자 주입 ( Constructor Injection )
- Setter 주입 ( Setter Injection)
- 필드 주입 ( Field Injection )


#### 생성자 주입(Constructor Injection)
```
public class A {
private B b;

    public A(B b) {
        this.b = b;
    }
}
```

스프링에서 권장하는 방식입니다.

#### Setter 주입(Setter Injection)
```
public class A {
private B b;

    public void setB(B b) {
        this.b = b;
    }
}
```

#### 인터페이스 주입(Interface Injection)
```
public interface BInjection {
void inject(B b);
}

public A implements BInjection {
private B b;

    @Override
    public void inject(B b) {
        this.b = b;
    }
}
```



## 예상 질문

1. 제어의 역전에 대해 설명해주세요.
2. 제어의 역전의 장점을 설명해주세요.

## 참고 자료

<!-- 공부 과정에서 참고한 자료가 있다면, 첨부해주세요-->
<!-- * [자료주제](링크)  -->

- [IoC의 정의/장점](https://isoomni.tistory.com/entry/TISPRING-IOC-DI-%EC%A0%95%EC%9D%98-%EC%9E%A5%EC%A0%90)
- [제어의 역전(IoC, DI, AOP)](https://innovation123.tistory.com/167)