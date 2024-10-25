# 정규화

이상현상이 있는 릴레이션을 분해하여 이상현상을 없애는 과정.  
테이블 간에 중복된 데이터를 허용하지 않음으로써 무결성(Integrity)를 유지할 수 있음, DB의 저장 용량도 줄일 수 있음.

## 제1 정규화

테이블의 컬럼이 원자값(하나의 값)을 갖도록 테이블을 분해하는 것.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FNRCAQ%2Fbtrj110vGrs%2Fn1XpWYrc5RdtwYRpeuwHQK%2Fimg.png)
과목 컬럼에 여러 개의 값을 가지고 있으므로 제1 정규형을 만족하지 못하고 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FVJ4EU%2Fbtrj2ABojKV%2F9t35vgqac4GMBVYYBIIKs0%2Fimg.png)
위와 같이 각 칼럼이 원자값을 갖도록 테이블을 분해하면 제1 정규형을 만족하게 된다.

## 제2 정규화

제1 정규화를 진행한 테이블에 대해 완전 함수 종속을 만족하도록 테이블을 분해하는 것
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FpwqKp%2Fbtrj2WEouSq%2FrHLj2INEMyM1PkzYkWATK1%2Fimg.png)
위 테이블에서는 (학생번호, 과목)으로 기본키가 구성되어 있는데, 지도교수 칼럼은 이 기본키 칼럼 중에서 과목 칼럼에만 종속된다. (부분 함수 종속)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FskXwR%2Fbtrj0U2B6V9%2Fs4xUYsd8DBZwLLew4gJ0Ik%2Fimg.png)
위와 같이 테이블을 분해하면 모든 칼럼이 기본키에 대해 완전 함수 종속을 만족하게 되어, 제2 정규형을 만족한다.

## 제3 정규화

기본키를 제외한 모든 칼럼들이, 이행적 함수 종속성이 없도록 테이블을 분해하는 것  
이행적 종속이란, A -> B, B -> C가 성립할 때 A -> C가 성립되는 것을 의미함
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxUsSs%2Fbtrj4sJJchb%2FjZhQDFOYYSNkqM75cG87w0%2Fimg.png)
위 테이블에서는, ID를 알면 등급을 알 수 있으므로 ID -> 등급이다. 등급을 알면 할인율을 알 수 있으므로 등급 -> 할인율이다. 따라서 ID -> 할인율이라는 이행적 함수 종속성이 존재한다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdYnxPO%2FbtrP8O3VPDg%2FDfyMkh8K5mnKFBp35BOJYk%2Fimg.png)
위와 같이 테이블을 분해하면 모든 테이블에 이행적 함수 종속성이 제거되어 제3 정규형을 만족하게 된다.

## BCNF

제3 정규화를 진행한 테이블에 대해 모든 결정자가 후보키가 되도록 테이블을 분해하는 것
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FtpoYs%2Fbtrj0WF7W9S%2FLzze4LuSZFnkaOxBFinSlK%2Fimg.png)
위 테이블에서는 학생번호, 과목 기본키를 가지고 지도 교수를 알 수 있다. 그런데 지도교수에 따라 과목이 결정되므로 지도교수 -> 과목 종속이 성립한다. 이처럼 후보키가 아닌 칼럼(지도교수)가 특정 칼럼(과목)의 결정자가 된 상황에서는 BCNF 정규형을 만족하지 않는다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbDpCpQ%2FbtrP9j99LpS%2F4SlIuGmJLNSCsoWvLARRtK%2Fimg.png)
위와 같이 테이블을 분해하면, 모든 결정자가 후보키가 되므로 BCNF 정규형을 만족하게 된다.

## 제4 정규화 이후

일반적으로 정규화는 BCNF 정규화까지만 실행하는 경우가 많다. 그 이상의 정규화를 하게 되면 오히려 정규화의 단점이 나타날 수 있다.

### 정규화의 단점

- 릴레이션의 분해로 인해 릴레이션 간 join 연산이 많아지고, 응답 속도가 늦어질 수 있다.
- join이 많이 발생하여 성능 저하가 나타나면, 반정규화를 적용해야할 수 있다.

## 예상 질문

- 정규화를 해야하는 이유를 포함해 정규화의 개념에 대해 설명해주세요.

<!-- 공부한 내용을 바탕으로 예상 질문을 최소 1개 이상 작성해주세요.-->

## 참고 자료

- [정규화(Normalization)란?](https://code-lab1.tistory.com/48)
- [정규화(Normalization) 쉽게 이해하기](https://mangkyu.tistory.com/110)

<!-- 공부 과정에서 참고한 자료가 있다면, 첨부해주세요-->
<!-- * [자료주제](링크)  -->
