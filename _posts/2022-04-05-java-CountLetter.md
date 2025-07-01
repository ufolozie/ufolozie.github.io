---
layout: post
title: "[Java] 문자 발생 횟수 계산 예제"
description: 사용자로부터 입력받은 문자열에서 각각의 문자들이 나타나는 횟수를 계산하는 예제 프로그램
tags: [Java]
---

#### 문제 설명

1. 26개의 정수를 저장할 수 있는 배열 count 선언
2. 사용자로부터 읽어들인 문자열을 저장할 수 있는 변수 buffer 선언

#### 조건

- 배열 count의 요소의 값이 0인 알파벳은 출력에서 제외
- 대문자를 포함하여 문자 횟수를 출력 (2가지 방법)  
  ① 대→소문자 변환하여 출력  
  ② 대/소문자 구분하여 출력

①의 경우, .toLowerCase() 메소드를 사용하고,

②의 경우, 대/소문자 두 가지 배열을 선언해야 한다. 앞서 선언한 배열 count는 정수 26개만을 담을 수 있게 설계되었고, 이는 알파벳 소문자(혹은 대문자)의 개수와 일치하기 때문이다.

<br>

## **1.**

```java
/*
* 대문자를 소문자로 변환하여 문자 횟수를 출력
*/
import java.util.Scanner; // Scanner 클래스 포함

public class CountLetter {
    public static void main(String[] args) {

        // 사용자의 입력을 받기 위해 Scanner 클래스의 객체 생성
        Scanner scan = new Scanner(System.in);

        // 26개의 정수를 저장할 수 있는 배열 count를 선언하고 생성
        int[] count = new int[26];

        System.out.println("문자열을 입력하시오: ");
        String buffer = scan.nextLine(); // Scanner 객체인 scan을 이용하여 사용자로부터 문자열을 읽어들임

        // 각 문자가 등장하는 횟수를 계산함
        for (int i = 0; i < buffer.length(); i++) {
            // String으로 저장된 문자열 buffer 중 한 글자만 선택해서 char 타입으로 변환
            char ch = buffer.charAt(i);
            count[ch - 'a']++; // count[ch - 'a'] 값을 1 증가시킴
        }

        // 배열에 저장된 횟수를 출력하는 반복 루프
        for (int i = 0; i < count.length; i ++) {
            if (count[i] != 0)
                System.out.println((char)(i + 'a') + ": " + count[i]);
        }
    }
}
```

실행 결과, <u>공백 및 대문자 포함 시 오류</u>가 발생하였다.

#### **⚠️ 오류 메시지**

```java
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: Index -24 out of bounds for length 26
        at CountLetter.main(CountLetter.java:25)
```

#### **📌 오류 발생 구간**

```java
for (int i = 0; i < buffer.length(); i++) {
    char ch = buffer.charAt(i);
    count[ch - 'a']++; // line 25
}
```

<br>

### **예외처리 해야 할 부분**

***try { 각 문자가 등장하는 횟수 계산 }*  
*catch { 대문자 → 소문자 변환 }*  
*finally { 각 문자가 등장하는 횟수 계산 }***

문자열 buffer에서 각 문자가 등장하는 횟수를 계산하는 for문 내부에 try-catch문을 중첩하여 **대문자 예외처리를 위한 코드를 추가**하였다.

`try { // char ch = buffer.charAt(i); count[ch - 'a']++; }`  
`catch { // (대문자 입력 시) buffer = buffer.toLowerCase(); … }`

```java
for (int i = 0; i < buffer.length(); i++) {
    try {
        char ch = buffer.charAt(i);
        count[ch - 'a']++;
    } catch (ArrayIndexOutOfBoundsException e) {
        buffer = buffer.toLowerCase();
        char ch = buffer.charAt(i);
        count[ch - 'a']++;
    }
}
```

위와 같이 작성한 결과, 대문자는 정상적으로 처리되었으나 <u>공백 포함 시 오류</u>가 발생하였다.

이를 수정하기 위해 **입력 받은 문자열에서 공백을 제거**하였고, 순서는 공백 → 대문자로 진행하였다. (반대로 처리할 시 이전 코드와 동일한 오류 발생)

#### **✅ 정리**

- 사용자로부터 문자열을 받아 String buffer에 저장한 뒤, buffer 내 공백을 제거
- 대문자가 입력으로 들어왔을 경우의 예외처리를 위해 for문 내부에 try-catch문을 삽입
- count 값이 0이 아닌 요소들을 출력

<br>

## **2.**

```java
/*
* count의 값이 0인 알파벳은 출력에서 제외함
* 대/소문자를 구분하여 횟수를 출력함
*/
import java.util.Scanner; // Scanner 클래스 포함

public class CountLetter {
    public static void main(String[] args) {

        // 사용자의 입력을 받기 위해 Scanner 클래스의 객체 생성
        Scanner scan = new Scanner(System.in);

        // 26개의 정수를 저장할 수 있는 대문자 배열 countUpper와 소문자 배열 countLower를 선언하고 생성
        int[] countUpper = new int[26];
        int[] countLower = new int[26];

        System.out.printf("문자열을 입력하시오: ");
        String buffer = scan.nextLine(); // Scanner 객체인 scan을 이용하여 사용자로부터 문자열을 읽어들임
        buffer = buffer.replaceAll(" ", ""); // 문자열에 포함되어 있는 공백 제거

        // 각 문자가 등장하는 횟수를 계산하는 반복 루프
        for (int i = 0; i < buffer.length(); i++) {
            char ch = buffer.charAt(i); // 문자열에서 하나의 문자만 가져옴
            // 대문자/소문자에 따른 예외처리를 위한 코드 삽입 
            try {
                countUpper[ch - 'A']++; // ch가 대문자이면 countUpper 배열의 해당 알파벳(인덱스)의 횟수(값)를 1만큼 증가시킴
            } catch (ArrayIndexOutOfBoundsException e) { // ch가 소문자여서 ArrayIndexOutOfBoundsException이 발생할 시
                countLower[ch - 'a']++; // countLower 배열의 해당 알파벳(인덱스)의 횟수(값)를 1만큼 증가시킴
            }
        }

        // 배열에 저장된 횟수를 출력하는 반복 루프
        // 대문자의 횟수 출력
        for (int i = 0; i < countUpper.length; i ++) {
            if (countUpper[i] != 0) // 값이 0인 요소는 출력에서 제외시킴
            System.out.println("(대문자) " + (char)(i + 'A') + ": " + countUpper[i]);
        }
        // 소문자의 횟수 출력
        for (int i = 0; i < countLower.length; i ++) { 
            if (countLower[i] != 0) // 값이 0인 요소는 출력에서 제외시킴
            System.out.println("(소문자) " + (char)(i + 'a') + ": " + countLower[i]);
        }
    }
}
```

<br>

### **피드백**

- `buffer.replaceAll(" ", "");` 와 같은 라이브러리를 사용하지 않고 코딩으로 해결할 것. 어차피 'a'보다 크다면 공백문자가 될 수 없음. (공백문자는 'a'보다 작은 값)
- 대/소문자 배열 길이를 알고 있으므로 ArrayIndexOutOfBoundsException을 할 필요는 없음. 다만, 입력 시 받은 배열의 문자가 알파벳이 아닐 경우 이러한 예외처리 가능.
- 문자로 캐스팅해서 이를 출력하기보다는 printf문을 사용하여 %c로 바로 변환하는 것을 추천함

<br>

## **3. 최종 코드**

```java
import java.util.Scanner; // Scanner 클래스 포함

public class CountLetters {
    public static void main(String[] args) {

        // 사용자의 입력을 받기 위해 Scanner 클래스의 객체 생성
        Scanner scan = new Scanner(System.in);

        // 26개의 정수를 저장할 수 있는 대문자 배열 countUpper와 소문자 배열 countLower를 선언하고 생성
        int[] countUpper = new int[26];
        int[] countLower = new int[26];

        System.out.printf("문자열을 입력하시오: ");
        String buffer = scan.nextLine(); // Scanner 객체인 scan을 이용하여 사용자로부터 문자열을 읽어들임

        // 각 문자가 등장하는 횟수를 계산하는 반복 루프
        for (int i = 0; i < buffer.length(); i++) {
            char ch = buffer.charAt(i); // 문자열에서 하나의 문자만 가져옴
            if (ch >= 'A' && ch <= 'Z') countUpper[ch - 'A']++; // ch가 대문자이면 countUpper 배열의 해당 알파벳(인덱스)의 횟수(값)를 1만큼 증가시킴
            else { // ch가 대문자가 아닐 때
                // ch가 공백문자이거나 알파벳이 아닌 문자일 경우 예외처리
                try { 
                    countLower[ch - 'a']++; // ch가 소문자이면 countLower 배열의 해당 알파벳(인덱스)의 횟수(값)를 1만큼 증가시킴
                } catch (ArrayIndexOutOfBoundsException e) {
                    // 에러 무시
                }
            }
        }

        // 배열에 저장된 횟수를 출력하는 반복 루프
        // 대문자의 횟수 출력
        for (int i = 0; i < countUpper.length; i ++) {
            if (countUpper[i] != 0) // 값이 0인 요소는 출력에서 제외시킴
                System.out.printf("(대문자) %c:  %d%n", i + 'A', countUpper[i]);
        }
        // 소문자의 횟수 출력
        for (int i = 0; i < countLower.length; i ++) { 
            if (countLower[i] != 0) // 값이 0인 요소는 출력에서 제외시킴
                System.out.printf("(소문자) %c:  %d%n", i + 'a', countLower[i]);
        }
    }
}
```

<br>
