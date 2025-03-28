---
title: "자바의 반복문 - for, while"
date: 2025-03-27 09:42:31 +0900
categories: [Java, Basic]
tags: [Eclipse, Java, 기초, for, while, repeat, loop, 반복문]
math: true
toc: true # 패널 목차
#만약 너가 이 기능을 끄고싶다면 _config.yml파일로가서 toc값을 false로 바꾸어주면된다. 
pin: true
img_path: /assets/img/javaandeclipse/
image:
  path: assets/img/javaandeclipse/javaAndEclipse.webp
#  alt: 이클립스와 자바
---

<br>

> **for 문**: 반복 횟수가 정해진 경우 사용하며, 초기화 → 조건 검사 → 실행 → 증감 순으로 동작한다.  
> 예시: `for (int i = 0; i < 5; i++) { ... }`
  

> **while 문**: 특정 조건이 `true`인 동안 계속 실행되며, 조건을 만족하지 않으면 종료된다.  
> 예시: `while (condition) { ... }`

<br>

## 1. for 반복문
> for(`초기화`, `조건식`, `증감식`) { ... } 로 사용된다.
{: .prompt-info}  

<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고</figcaption>
</div>

```java
public class forMain {

  public static void main(String[] args) {
    for(int i = 1; i<11; i++) {
      //i++는 한바퀴를 돈 후에 i 에 1을 더한다. 즉 for문 내용을 한번 실행한 후 i + 1 이 연산된다.
      System.out.println(i+"번째 바퀴");
    }

    System.out.println("\n");
    for(int i = 1; i<11; ++i) {
      //전위 연산자도 동일하게 동작함
      System.out.println(i+"번째 바퀴");
    }

    //배열에 for문을 이용하기
    System.out.println("\n");
    List<String> kor = List.of("가","나","다","라","마","바","사","아","자","차","카","타","파","하");
    for(int i=0; i<kor.size(); i++) {
      System.out.printf(kor.get(i)+" ");
      if(i==kor.size()-1) System.out.println("\n");
    }
    for(String k : kor) {//향상된 for 문 위에 것과 동일하게 동작
      System.out.printf(k+" ");
    }
    System.out.println("\n");

    for(int i = 10; i>0; i--) {
      System.out.println(i);
    }

    //짝수 건너뛰기
    for(int i = 10; i>0; i--) {
      if(i%2==0) continue;
      System.out.println(i);
    }
    //변수 두개 활용
    for(int i=0, j=10; i<10; i++,j-- ) {
      System.out.printf(j+" ");
    }

  }
}
```
<div style="display: flex; justify-content: center; align-items: center; gap: 20px;">
  <img src="/assets/img/java/basics/forwhile/스크린샷 2025-03-27 093905.png" alt="이미지테스트설명" style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px; width: 100px; ">
  <img src="/assets/img/java/basics/forwhile/스크린샷 2025-03-27 093909.png" alt="이미지테스트설명" style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px; width: 100px; ">
  <img src="/assets/img/java/basics/forwhile/스크린샷 2025-03-27 093915.png" alt="이미지테스트설명" style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px; width: 100%; height: 60px">
  <img src="/assets/img/java/basics/forwhile/스크린샷 2025-03-27 093920.png" alt="이미지테스트설명" style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px; width: 100%; ">
</div>
<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">각각의 출력 결과</figcaption>
</div>

 <br> 

<p align="center">
  <strong>🚀 for문에서 <code>break</code> 와 <code>continue</code> 🚀</strong>
</p>

> **break**: 반복문을 즉시 종료하고 탈출한다.  
> 예시: 
> ```java 
> for (int i = 0; i < 10; i++) { 
>   if (i == 5) break; 
> } // i가 5가 되면 반복문 종료
> ```
>
> **continue**: 현재 반복을 건너뛰고 다음 반복을 실행한다.  
> 예시: 
> ```java
> for (int i = 0; i < 10; i++) { 
>   if (i == 5) continue; 
> } // i가 5일 때만 건너뛰고 다음 반복 실행
> ```
{: .prompt-tip}
 
<br>

---

## 2. while 반복문
> while(`조건식`) { ... } 로 사용된다. 조건이 참인 경우 계속 반복된다.
{: .prompt-info}

<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고</figcaption>
</div>

```java
public class forMain {

  public static void main(String[] args) {
    for(int i = 1; i<11; i++) {
      //i++는 한바퀴를 돈 후에 i 에 1을 더한다. 즉 for문 내용을 한번 실행한 후 i + 1 이 연산된다.
      System.out.println(i+"번째 바퀴");
    }

    System.out.println("\n");
    for(int i = 1; i<11; ++i) {
      //전위 연산자도 동일하게 동작함
      System.out.println(i+"번째 바퀴");
    }

    //배열에 for문을 이용하기
    System.out.println("\n");
    List<String> kor = List.of("가","나","다","라","마","바","사","아","자","차","카","타","파","하");
    for(int i=0; i<kor.size(); i++) {
      System.out.printf(kor.get(i)+" ");
      if(i==kor.size()-1) System.out.println("\n");
    }
    for(String k : kor) {//향상된 for 문 위에 것과 동일하게 동작
      System.out.printf(k+" ");
    }
    System.out.println("\n");

    for(int i = 10; i>0; i--) {
      System.out.println(i);
    }

    //짝수 건너뛰기
    for(int i = 10; i>0; i--) {
      if(i%2==0) continue;
      System.out.println(i);
    }
    //변수 두개 활용
    for(int i=0, j=10; i<10; i++,j-- ) {
      System.out.printf(j+" ");
    }

  }
}
```
<div style="display: flex; justify-content: center; align-items: center; gap: 20px;">
  <img src="/assets/img/java/basics/forwhile/스크린샷 2025-03-27 093905.png" alt="이미지테스트설명" style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px; width: 100px; ">
  <img src="/assets/img/java/basics/forwhile/스크린샷 2025-03-27 093909.png" alt="이미지테스트설명" style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px; width: 100px; ">
  <img src="/assets/img/java/basics/forwhile/스크린샷 2025-03-27 093915.png" alt="이미지테스트설명" style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px; width: 100%; height: 60px">
  <img src="/assets/img/java/basics/forwhile/스크린샷 2025-03-27 093920.png" alt="이미지테스트설명" style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px; width: 100%; ">
</div>
<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">각각의 출력 결과</figcaption>
</div>

<br>

<p align="center">
  <strong>🔄 while문 활용 팁 🔄</strong>
</p>

> **1. 무한 루프 (Infinite Loop)**  
> 특정 조건에서 `while` 문이 계속 실행되도록 만들 수 있다.  
> 예시:
> ```java
> while (true) {
>     System.out.println("무한 루프 실행 중...");
>     if (조건) break; // 특정 조건에서 탈출
> }
> ```

> **2. 입력을 받을 때 활용하기**  
> 사용자가 특정 값을 입력할 때까지 반복 실행할 수 있다.  
> 예시:
> ```java
> import java.util.Scanner;
> Scanner sc = new Scanner(System.in);
> String input;
> while (true) {
>     System.out.print("입력하세요 (exit 입력 시 종료): ");
>     input = sc.nextLine();
>     if (input.equals("exit")) break;
> }
> ```

> **3. 카운터 변수 활용**  
> `while` 문에서 카운터 변수를 활용해 특정 횟수만큼 실행할 수 있다.  
> 예시:
> ```java
> int count = 0;
> while (count < 5) {
>     System.out.println("반복 횟수: " + count);
>     count++;
> }
> ```

> **4. do-while 문과 비교**  
> `while` 문은 조건을 먼저 검사하지만, `do-while` 문은 한 번 실행한 후 조건을 검사한다.  
> 예시:
> ```java
> int num = 10;
> do {
>     System.out.println("최소 한 번 실행됨");
> } while (num < 5);
> ```
{: .prompt-tip}
