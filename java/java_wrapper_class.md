# Java Wrapper Class

자바는 기본 타입(byte, char, short, int, long, float, double, boolean)의 값을 갖는 객체를 생성할 수 있고, 이러한 객체를 wrapper 객체라고 한다.  
wrapper 객체는 자신이 포장하고 있는 기본 타입의 값을 변경할 수 없고, 단지 객체로 생성하는 것만 가능하다. 이러한 wrapper 객체가 필요한 이유는 collection 객체 때문. collection 객체에는 깁기본 타입의 값은 저장이 불가능하고, 객체만 저장할 수 있다.

## Wrapper class의 종류

| 기본 타입 | wrapper 클래스 |
| --------- | -------------- |
| byte      | Byte           |
| char      | Character      |
| short     | Short          |
| int       | Integer        |
| long      | Long           |
| float     | Float          |
| double    | Double         |
| boolean   | Boolean        |

## 박싱(Boxing)과 언박싱(UnBoxing)

Boxing: 기본 타입의 값 -> wapper 객체로 만드는 과정
UnBoxing: wrapper 객체에서 기본 타입의 값을 얻어내는 과정

```Java
    Integer obj = 100; // boxing
    int value = obj; // unboxing
```

```Java
    Integer num1 = new Integer(7); // boxing
    int int1 = num1.intValue();    // unboxing

    Character ch = new Character('X'); // boxing
    char c = ch.charValue();           // unboxing
```

## 문자열을 기본 타입으로 변환

wrapper 클래스는 문자열을 기본 타입 값으로 변환할 떄도 사용된다. `parse + (기본타입 이름)`으로 되어있는 정적 메소드를 이용하면 된다.

```Java
    // String -> int
    String str = "30000";
    int value = Integer.parseIng(str);

    // String -> float
    String str = "12.345";
    float value = Float.parseFloat(str);

    // String -> boolean
    String str = "true";
    boolean value = Boolean.parseBoolean(str);
```

## wrapper class 내부 값 비교

wrapper 객체는 내부의 값을 비교하기 위해서 ==와 != 연산자를 사용할 수 없다. 이 두 연산자는 wapper 객체 내부의 값을 비교하는 것이 아니라, 객체의 주소값을 비교한다.

```Java
    Integer obj1 = 300;
    Integer obj2 = 300;
    System.out.println(obj1==obj2); // false
```

위와 같은 경우, 두 Integer 객체는 동일한 값을 가지고 있지만, == 연산의 결과는 false이다. (주소값이 다르므로)

그런데 예외가 있다. 아래 타입에 대해 해당하는 값을 갖는 wrapper 객체는 공유되므로, ==와 != 연산자로 비교할 수 있다.
|타입|값의 범위|
|---|---|
|boolean|true,false|
|char|\u0000 ~ \u007f|
|byte, short, int| -128 ~ 127|

하지만 이것 또한 객체 내부의 실제 값을 비교하는 게 아니라, 객체의 주소값을 비교하는 것이다.  
wrapper 객체 안에 정확히 어떤 값이 저장될 지 모르는 상황이라면 ==과 != 연산자 대신, equals() 라는 메소드로 내부의 값을 비교하는 것이 좋다.

```Java
    Integer num1 = new Integer(300);
    Integer num2 = new Integer(500);
    Integer num3 = new Integer(300);


    System.out.println(num1 < num2);       // true
    System.out.println(num1 == num3);      // false
    System.out.println(num1.equals(num3)); // true
```

## 예상 질문

<!-- 공부한 내용을 바탕으로 예상 질문을 최소 1개 이상 작성해주세요.-->

1. 자바의 wrapper 클래스가 무엇인지, 기본 타입과 어떻게 다른지 설명해주세요.
2. 자바의 wrapper 클래스가 필요한 이유를 설명해주세요.

## 참고 자료

<!-- 공부 과정에서 참고한 자료가 있다면, 첨부해주세요-->
<!-- * [자료주제](링크)  -->

- 이것이 자바다 (신용권, 임경균)
- [TCP School - Wrapper 클래스](https://tcpschool.com/java/java_api_wrapper)
