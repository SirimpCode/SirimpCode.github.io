---
title: "자바의 기본 클래스 'Math' - Math static method"
date: 2025-03-27 09:12:31 +0900
categories: [Java, Basic]
tags: [Eclipse, Java, 기초, Math, static]
math: true
toc: false # 패널 목차
#만약 너가 이 기능을 끄고싶다면 _config.yml파일로가서 toc값을 false로 바꾸어주면된다. 
pin: false
img_path: /assets/img/javaandeclipse/
image:
  path: assets/img/javaandeclipse/javaAndEclipse.webp
#  alt: 이클립스와 자바
---


## Math 클래스의 static 메서드
<blockquote>
  <p style="font-size: 0.9em;">자바에는 간단하게 연산을 도와주는 <strong>Math</strong> 클래스의 <strong>static method</strong>가 존재한다.</p>
</blockquote>
{: .prompt-info}  

<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고</figcaption>
</div>

```java
public class MathMain {
  public static void main(String[] args) {
    double db1 = 59.53123, db2 = 86.23543;
    System.out.println("그냥 출력 "+db1+" "+db2);

    //반올림하기
    System.out.println("그냥 반올림 "+Math.round(db1)+" "+ Math.round(db2));

    //원하는 특정한 곳에서 반올림
    System.out.println("특정한곳 반올림 "+(Math.round(db1*100))/100d+" "+ Math.round(db2*100)/100d);

    //올림 기냥 무지성으로 올려버림
    System.out.println("\n올림 "+Math.ceil(db1)+" "+ Math.ceil(db2));
    //내림 그냥 소수점 버림
    System.out.println("내림 "+Math.floor(db1)+" "+ Math.floor(db2));

    //절대값 
    int a = 20, b = -30;
    System.out.println(a+" "+b);
    System.out.println("\n절대 값 "+Math.abs(a)+" "+Math.abs(b));
  }
}
```
<div style="display: flex; flex-direction: column; align-items: center; gap: 0px;">
  <img src="/assets/img/java/basics/math/스크린샷 2025-03-27 091203.png" alt="출력 결과" style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px; width: 100%">
  <figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">출력 결과</figcaption>
</div>
<br>

---

| 메서드 |  예제 |
|--------|------|
| `Math.ceil(double a)` |  `Math.ceil(4.3) -> 5.0` |
| `Math.floor(double a)` |  `Math.floor(4.9) -> 4.0` |
| `Math.round(float a)` |  `Math.round(4.5) -> 5` |
| `Math.round(double a)` |  `Math.round(4.5) -> 5L` |
| `Math.abs(int a)` |  `Math.abs(-10) -> 10` |
| `Math.abs(double a)` |  `Math.abs(-10.5) -> 10.5` |

<br>
