# Call by Value & Call by Reference 

함수의 호출 방법에는 'Call by Value' 와 'Call by Reference' 가 있습니다.

### ✨Call by Value (값에 의한 호출)

인자로 받은 값을 복사하여 처리

장점 : 값을 복사하여 처리하기 때문에 안전하며 원래의 값이 보존된다.

단점 : 값을 복사하기 때문에 메모리 사용량이 늘어난다.

```
Class CallByValue{

    public static void swap(int x, int y){
        int tmp = x;
        x = y;
        y = tmp;
    }

    public static void main(String[] args){
        int a = 100;
        int b = 200;

        System.out.println("Swap 호출 전 : a = " + a + " , b = " + b);

        swap(a,b);

        System.out.println("Swap 호출 후 : a = " + a + " , b = " + b);
    }

}

```
위 코드에서 결과값은 아래와 같이 변수값이 Swap 호출 전과 Swap 호출 후가 같습니다.

```
Swap 호출 전 : a = 100, b = 200
Swap 호출 후 : a = 100, b = 200
```

즉, swap() 메서드 호출 시에 사용한 인자 a,b 와 swap() 메서드 내의 매개변수인 x,y는 서로 다릅니다.

### ✨Call by Reference (참조에 의한 호출)

인자로 받은 값의 주소를 참조하여 직접 값을 처리

장점 : 복사하지 않고 직접 참조를 하기 때문에 속도가 빠르다.

단점 : 직접 참조를 하기 때문에 기존 값이 영향을 받는다.

```
Class CallByReference{

    int val;

    CallByReference(int val){
        this.val = val;
    }

    public static void swap(CallByReference x, CallByReference y){
        int tmp = x.val;
        x.val = y.val;
        y.val = tmp;
    }

    public static void main(String[] args){
        CallByReference a = new CallByReference(100);
        CallByReference b = new CallByReference(200);

        System.out.println("Swap 호출 전 : a = " + a.val + " , b = " + b.val);

        swap(a,b);

        System.out.println("Swap 호출 후 : a = " + a.val + " , b = " + b.val);
    }

}
```

위 코드에서 결과값은 아래와 같이 변수값이 Swap 호출 전과 Swap 호출 후가 다릅니다.

```
Swap 호출 전 : a = 100, b = 200
Swap 호출 후 : a = 200, b = 100
```

기존 값이 영향을 받는 Call by Reference 의 단점을 보완하기 위해서는 "깊은 복사"를 사용하는 방법이 있습니다.

그러나 이 경우 메모리 소모, 속도 저하가 발생할 수도 있으므로 "Call by Reference" 와 "깊은 복사"를 상황에 맞게 적절히 선택해 사용하는 주의가 필요합니다.

## 📃예상문제
<!-- 공부한 내용을 바탕으로 예상 질문을 최소 1개 이상 작성해주세요.-->
1. Call by Value 와 Call by Reference 의 차이에 대해 간략히 설명해주세요. 
2. Java의 경우 어떻게 함수가 호출되는 지 설명해 주세요.
3. Call by Reference 의 단점과 이를 어떻게 보완할 수 있을지 설명해주세요.

## 🔗참고 자료
<!-- 공부 과정에서 참고한 자료가 있다면, 첨부해주세요-->
<!-- * [자료주제](링크)  -->
- 컴퓨터인터넷IT용어대사전
- https://github.com/Songwonseok/CS-Study?tab=readme-ov-file
-https://velog.io/@kwontae1313/JS%EC%9D%98-Call-by-Value-%EC%99%80-Call-by-Reference
