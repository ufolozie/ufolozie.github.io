---
title: "[Java/자바] 루프 변환 예제 (LoopTest)"
date: 2022-03-30 00:00:00 +0900
categories: [Lab, Java]
tags: [java]
---

> for / while / do while 의 세 가지 반복문을 사용하여 1부터 100까지의 숫자 중 홀수의 합을 구하는 프로그램

<br>

```java
public class LoopTest {
    public static void main(String[] args) { // main 함수 호출
        forTest(); // for문을 사용하는 메서드 호출
        whileTest(); // while문을 사용하는 메서드 호출
        dowhileTest(); // do-while문을 사용하는 메서드 호출
    }

    public static void forTest() { // for문을 사용하는 메서드
        int sum, i; // 변수 선언
        System.out.println("for문 이용"); // 문구 출력
        for (sum = 0, i = 1; i <= 100; i++) { // 1부터 100까지 i를 1씩 증가시키며 반복
            if (i % 2 == 0) continue; // i가 짝수면 증감식으로 이동
            sum += i; // i가 홀수면 sum 갱신
        }
        System.out.printf("\tsum = %d\n", sum); // 들여쓰기 후 sum 출력하고 줄바꿈
    }

    public static void whileTest() { // while문을 사용하는 메서드
        int sum = 0, i = 0; // 변수 선언 및 초기화
        System.out.println("while문 이용"); // 문구 출력
        while (i < 100) {
            i++; // i을 1씩 증가시키며, i가 100이 될 때 마지막으로 하위 실행문을 실행함
            if (i % 2 == 0) continue; // i가 짝수면 조건식으로 이동
            sum += i; // i가 홀수면 sum 갱신
        };
        System.out.printf("\tsum = %d\n", sum); // 들여쓰기 후 sum 출력하고 줄바꿈
    }

    public static void dowhileTest() { // do-while문을 사용하는 메서드
        int sum = 0, i = 0; // 변수 선언 및 초기화
        System.out.println("do-while문 이용"); // 문구 출력
        do {
            i++; // i을 1씩 증가시키며, i가 100이 될 때 마지막으로 하위 실행문을 실행함
            if (i % 2 == 0) continue; // i가 짝수면 조건식으로 이동
            sum += i; // i가 홀수면 sum 갱신
        } while (i < 100);
        System.out.printf("\tsum = %d", sum); // 들여쓰기 후 sum 출력
    }
}
```
