## 동기와 비동기
![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbAH5tM%2Fbtq805FioAi%2Fyu7eXmpbnJd2tnhlzGvYOK%2Fimg.jpg)

#### 동기 처리
한 작업이 끝나야 다음 작업이 시작되는 순차적인 처리 방식을 말합니다. 이는 작업의 완료를 기다리는 동안 다른 작업을 수행할 수 없기 때문에 특정 작업의 처리 시간이 길어질 경우 전체적인 시스템의 반응 속도가 느려질 수 있습니다.
왜냐하면 동기 처리 방식에서는 호출된 함수가 작업을 완료할 때까지 호출한 함수가 대기해야 하기 때문입니다. 이는 작업의 순서를 보장하지만, 효율성 측면에서는 단점이 될 수 있습니다.

#### 비동기 처리
한 작업이 끝나기를 기다리지 않고 다음 작업을 바로 시작할 수 있는 처리 방식입니다. 이는 작업의 완료 여부와 상관없이 다른 작업을 동시에 진행할 수 있어 시스템의 효율성을 높일 수 있습니다.
비동기 처리 방식에서는 작업의 완료를 기다리지 않고, 작업이 완료되면 그 결과를 처리할 콜백 함수를 호출합니다. 이는 시스템의 자원을 효율적으로 사용할 수 있게 하며, 사용자 경험을 향상시킬 수 있습니다.

## 자바에서의 비동기 처리

비동기 처리 방식은 자바에서 Future, CompletableFuture, @Async 어노테이션 등을 통해 구현할 수 있습니다. 이러한 방식은 작업의 완료를 기다리지 않고 바로 다음 작업으로 넘어갈 수 있어, 시스템의 자원을 보다 효율적으로 사용할 수 있습니다.

예를 들어, CompletableFuture를 사용하면 비동기 작업의 결과를 반환받고 이 결과를 처리하는 콜백 함수를 등록할 수 있습니다. 이는 복잡한 비동기 로직을 보다 쉽게 구현할 수 있게 합니다.

따라서, 자바에서는 애플리케이션의 요구 사항에 따라 적절한 동기 또는 비동기 처리 방식을 선택하여 사용할 수 있습니다. 이는 애플리케이션의 성능과 사용자 경험을 최적화하는 데 중요한 역할을 합니다.

## CompletableFuture
자바에서 비동기 작업을 처리하기 위해 사용되는 클래스입니다. 기존의 Future의 한계를 개선하여 비동기 연산을 더 유연하게 처리할 수 있도록 도와줍니다. CompletableFuture는 다양한 방식으로 비동기 작업을 수행할 수 있으며, 다른 연산과 결합하거나, 결과를 기다리거나, 예외 처리를 쉽게 할 수 있습니다.
```
public class CompletableFuture<T> implements Future<T>, CompletionStage<T> {    ...}
```


1. runAsync()
   <br>반환값이 없는 비동기 작업을 실행할 때 사용됩니다. Runnable 인터페이스를 받아서 실행되며, 결과값이 필요 없는 작업을 처리할 때 적합합니다.
   사용 예시: 예를 들어, 로그 기록과 같이 결과를 필요로 하지 않는 작업을 백그라운드에서 실행할 때 사용됩니다.
2. supplyAsync()
   <br> 반환값이 있는 비동기 작업을 실행할 때 사용됩니다. Supplier<T> 인터페이스를 받아 작업이 완료되면 결과값을 반환합니다. 결과를 반환하기 때문에 이후의 작업에서 그 결과를 활용할 수 있습니다.

3. join()
   <br> 비동기 작업의 완료를 기다린 후 그 결과를 반환합니다. get()과 유사하지만 join()은 체크 예외를 던지지 않는다는 차이점이 있습니다. 그래서 코드가 더 간결해지며 예외 처리에 대한 부담이 적습니다.

#### runAsync() 예제코드
```
public class CompletableFutureExample {
    public static void main(String[] args) {
        // runAsync로 비동기 작업 실행
        CompletableFuture<Void> future = CompletableFuture.runAsync(() -> {
            System.out.println("비동기 작업 수행 중...");
        });

        // 작업 완료까지 기다림
        future.join();  // 결과를 반환하지 않음
        System.out.println("비동기 작업 완료");
    }
}
```

#### supplyAsync() 예제코드

```
public class SupplyAsyncExample {
public static void main(String[] args) {
// supplyAsync로 비동기 작업 실행 및 결과 반환
CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
// 비동기 작업
return "비동기 작업 결과";
});

        // 작업 완료 후 결과 가져오기
        String result = future.join();  // 결과를 기다림
        System.out.println(result);  // "비동기 작업 결과" 출력
    }
}
```


## 비동기 처리 실생활 사례

1. 소셜 미디어 피드 로딩: 사용자가 소셜 미디어 앱을 열 때 서버에 데이터를 요청하고, 피드 데이터가 도착하면 화면에 표시됩니다. 이 과정에서 사용자는 앱을 계속 사용할 수 있으며, 피드가 로드되는 동안 다른 작업도 가능합니다.
2. 웹사이트 이미지 로딩: 웹페이지를 로드할 때, 모든 이미지가 완전히 로드되지 않더라도 텍스트나 다른 콘텐츠는 먼저 표시됩니다. 이미지 로딩이 완료되면 그때 화면에 나타나는데, 이 과정이 비동기적으로 처리됩니다.
3. 대용량으로 파일을 처리해야하는 어플리케이션

## 예상 질문

1. 동기처리와 비동기 처리의 차이점을 설명해주세요.
2. 비동기 처리는 어떨 때 사용하는지 예시를 설명해주세요.

## 참고 자료

<!-- 공부 과정에서 참고한 자료가 있다면, 첨부해주세요-->
<!-- * [자료주제](링크)  -->

- [비동기의 원리와 비동기 제어 사례](https://heo-dev-0229.tistory.com/41)
- [비동기 프로그래밍의 이해와 실제 적용 사례](https://f-lab.kr/insight/understanding-and-applying-asynchronous-programming)