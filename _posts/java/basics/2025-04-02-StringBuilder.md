---
title: "StringBuilder와 StringBuffer"
date: 2025-04-02 16:52:21 +0900
categories: [Java, Basic]
tags: [Eclipse, Java, 기초, 문자열, String, StringBuilder, StringBuffer]
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

## 1. StringBuilder 사용 이유
> String 변수선언후 값을 변경 할때마다 메모리가 낭비 된다.
{: .prompt-info}

<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고</figcaption>
</div>

```java
public static void main(String[] args) {
  String name = "일순신"; // 메모리상에 name 1개 소모
  name += ",이순신";  // 메모리상에 name 1개 소모
  name += ",삼순신";  // 메모리상에 name 1개 소모
  name += ",사순신";  // 메모리상에 name 1개 소모
  name += ",오순신";  // 메모리상에 name 1개 소모
  name += ",육순신";  // 메모리상에 name 1개 소모
  name += ",칠순신";  // 메모리상에 name 1개 소모
  name += ",팔순신";  // 메모리상에 name 1개 소모
  name += ",구순신";  // 메모리상에 name 1개 소모
  name += ",십순신";  // 메모리상에 name 1개 소모
  //매번 메모리상의 name 이 소모가 된다.
}
```

<br>

---


## 2. StringBuffer 와 StringBuilder

### 2-1. StringBuffer

<p align="center">
  <strong>🚀 StringBuffer의 특징 🚀</strong>
</p>

> StringBuffer 는 Multi thread 를 지원해준다.  
> 그래서 Multi thread 로 움직이는 게임에는 StringBuffer 를 사용한다.  
> StringBuffer 는 StringBuilder 보다 무겁고 동작속도가 떨어지지만  
> Multi thread 를 지원해주므로 게임에서 사용하는 것이 적합하다.
{: .prompt-info}


<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고</figcaption>
</div>

```java
StringBuffer sb1 = new StringBuffer();
sb1.append("일순신");
sb1.append(",이순신");
sb1.append(",삼순신");
sb1.append(",사순신");
sb1.append(",오순신");
sb1.append(",육순신");
sb1.append(",칠순신");
sb1.append(",팔순신");
sb1.append(",구순신");
sb1.append(",십순신");
System.out.println(sb1);
```

<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">최상단의 코드 출력 결과와 동일하다.<br>캡처는 하단 참고</figcaption>
</div>

<br>

---

### 2-2. StringBuilder

<p align="center">
  <strong>🚀 StringBuilder의 특징 🚀</strong>
</p>

> StringBuilder 는 Multi thread 를 지원해주지 못하고  
> StringBuilder 는 Single thread 만 지원해준다.  
> Single thread 로 움직이는 웹에는 StringBuilder 를 사용한다.  
> 왜냐하면 StringBuilder 가 StringBuffer 보다 가볍고 또한 동작속도가   
> 빠르므로 그렇다.
{: .prompt-info}

<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고 StringBuffer와 동일하다.</figcaption>
</div>

```java
StringBuilder sb2 = new StringBuilder();
sb2.append("일순신");
sb2.append(",이순신");
sb2.append(",삼순신");
sb2.append(",사순신");
sb2.append(",오순신");
sb2.append(",육순신");
sb2.append(",칠순신");
sb2.append(",팔순신");
sb2.append(",구순신");
sb2.append(",십순신");
System.out.println(sb2);
```

<div style="display: flex; justify-content: center; align-items: center; gap: 20px;">
  <img src="/assets/img/java/basics/string/스크린샷 2025-04-02 172109.png" alt="이미지테스트설명" style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px; width: 100%; ">
</div>
<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">상위 세 코드의 출력 결과</figcaption>
</div>


<br>

---

## 3. 사용해보기

### 3-1. 초기화 시키기

> 사용되던 `StringBuilder` 에 append를 계속 한다면 원래 값에 쌓이기만할 것이다.  
> 따라서 기존값을 전부 없애고 새로운 값을 추가 하고자 할때는 두가지 방법이 있다.
> 1. 길이를 0으로 바꾸기
> 2. 인스턴스를 새로 생성해버리기
{: .prompt-info}

<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고</figcaption>
</div>

```java
//sb2 초기화 하기
sb2.setLength(0);
sb2.append("다시 처음부터 시작");
sb2.append("덧 붙임");
sb2.append("끝");
System.out.println(sb2);
//두번째 방법 인스턴스 새로 만들어버림
sb2 = new StringBuilder();
sb2.append("또 다시 처음부터 시작");
sb2.append("또 덧 붙임");
sb2.append("또 끝");
System.out.println(sb2);
```

<br>

---

### 3-2. 문자열 뒤집기

> reverse 내장 메서드로 간단하게 구현할 수 있다.  
> ex) `stringBuilder.reverse()` 
{: .prompt-info}

<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고</figcaption>
</div>

```java
//문자열 거꾸로 뒤집기
String str = "안녕하세요";
StringBuilder sb3 = new StringBuilder(str);
sb3.reverse();//문자열을 뒤집어 버림
System.out.println(sb3);//기대값 요세하녕안
```


