# Java Stream API

자바의 Stream API는 Java 8에서 추가된 기능으로, 컬렉션이나 배열의 데이터를 함수형 프로그래밍 방식으로 처리할 수 있도록 해준다.

## Stream의 특징

1. 선언적(Declarative)

- 데이터를 어떻게 처리할지보다 무엇을 할지를 명시한다.
  - 예: list.stream().filter(...).map(...).collect(...)

2. 함수형 프로그래밍(Functional Programming)

- 람다식과 결합해 데이터 처리를 간결하게 표현한다.

3. 지연 연산(Lazy Evaluation)

- 스트림의 중간 연산은 실제로 데이터를 처리하지 않고, 최종 연산이 호출될 때가 되어서야 처리한다. -> 불필요한 연산 줄일 수 있음

4. 파이프라인 처리

- 여러 연산을 파이프라인 형태로 연결해 처리함. 스트림은 데이터 소스를 기반으로 만들어지고, 중간 연산으로 변환되어 최종 연산에서 결과를 얻을 수 있다.

5. 병렬 처리

- parallelStream()을 사용하면 여러 스레드를 활용해 병렬로 데이터를 처리할 수 있다.

## Stream의 구성 요소

1. 데이터 소스

- 컬렉션(Collection), 배열(Array), 파일 등

2. 중간 연산 (Intermediate Operations)

- 스트림을 변환하거나 필터링하는 연산
- 중간 연산은 lazy하게 평가되며, 최종 연산이 호출될 때까지 실제 처리가 일어나지 않는다.
  - 예: filter(), map(), sorted(), distinct(), limit()

3. 최종 연산 (Terminal Operations)

- 스트림에서 데이터를 최종적으로 처리하는 연산
- 중간 연산 결과를 실제로 처리해 결과를 반환한다.
  - 예: forEach(), collect(), reduce(), count()

## 주요 메소드

### 1. filter()

주어진 조건을 만족하는 요소만을 필터링

```Java
    List<String> names = Arrays.asList("John", "Jane", "Jack", "Doe");
    List<String> filteredNames = names.stream()
                                  .filter(name -> name.startsWith("J"))
                                  .collect(Collectors.toList());
    System.out.println(filteredNames); // [John, Jane, Jack]
```

### 2. map()

스트림의 각 요소를 변환

```Java
    List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
    List<Integer> squares = numbers.stream()
                               .map(n -> n * n)
                               .collect(Collectors.toList());
    System.out.println(squares); // [1, 4, 9, 16, 25]
```

### 3. sorted()

스트림의 요소들을 정렬

```Java
    List<String> names = Arrays.asList("John", "Jane", "Jack", "Doe");
    List<String> sortedNames = names.stream()
                                .sorted()
                                .collect(Collectors.toList());
    System.out.println(sortedNames); // [Doe, Jack, Jane, John]
```

### 4. forEach()

각 요소에 대해 주어진 동작을 수행

```Java
    List<String> names = Arrays.asList("John", "Jane", "Jack", "Doe");
    names.stream().forEach(name -> System.out.println(name));
```

### 5. collect()

스트림의 데이터를 특정 컬렉션이나 데이터 구조로 변환

```Java
    List<String> names = Arrays.asList("John", "Jane", "Jack", "Doe");
    List<String> result = names.stream()
                           .filter(name -> name.length() > 3)
                           .collect(Collectors.toList());
    System.out.println(result); // [John, Jane, Jack]
```

## 예상 질문

<!-- 공부한 내용을 바탕으로 예상 질문을 최소 1개 이상 작성해주세요.-->

1. Stream API와 for-each 루프의 차이점은 무엇이고, 언제 Stream API를 사용하는 것이 유리한지 설명해주세요.
2. Stream에서 중간 연산과 최종 연산의 차이점은 무엇인지 설명해주세요.

## 참고 자료

<!-- 공부 과정에서 참고한 자료가 있다면, 첨부해주세요-->
<!-- * [자료주제](링크)  -->

- 이것이 자바다 (신용권, 임경균)
