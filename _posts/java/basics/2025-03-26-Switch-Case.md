---
title: "스위치-케이스문 - switch-case"
date: 2025-03-25 17:08:11 +0900
categories: [Java, Basic]
tags: [Eclipse, Java, 기초, switch, case, 스위치문]
math: true
toc: true # 패널 목차
#만약 너가 이 기능을 끄고싶다면 _config.yml파일로가서 toc값을 false로 바꾸어주면된다. 
pin: false
img_path: /assets/img/javaandeclipse/
image:
  path: assets/img/javaandeclipse/javaAndEclipse.webp
#  alt: 이클립스와 자바
---


## 1. 일반적인 switch 문
> - switch(value) 에서 value의 값이 case의 값과 맞을 때 진행된다. 
> - break를 안만나면 아래의 구문들도 전부 실행된다.
{: .prompt-info}
<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고</figcaption>
</div>

```java
private final char ratings;//변수
//ratings의 값이 A 일 경우 break 를 만나는 D 케이스문까지 전부 실행된다.
private String getGift2() {
  String response = "";
  switch(this.ratings) {
    case 'A' : response+="놀이공원이용권,";
    case 'B' : response+="피자,";
    case 'C' : response+="치킨,";
    case 'D' : response+="떡볶이"; break;
    default : response ="꿍밤";
  };
  return response;
}
```
<div style="display: flex; flex-direction: column; align-items: center; gap: 0px;">
  <img src="/assets/img/java/basics/switch/스크린샷 2025-03-26 171722.png" alt="출력 결과" style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px; width: 100%">
  <figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">출력 결과</figcaption>
</div>

> switch 문에는 { `byte` , `short` , `int` , `char` , `String` } 만 가능하다.
{: .prompt-warning}

<br>

---

## 2. 화살표(`->`)를 사용한 switch 문 

> `->` 를 사용한 switch 문은 `:` 를 사용한 switch 문과 다르게  
> 반환 값이 생기고 break를 사용하지 않는다.
{: .prompt-info}

<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고</figcaption>
</div>

```java
private final List<String> giftList = List.of(
  "놀이공원이용권","치킨","피자","아이스크림"
);
private String getGift() {//-> 이용시 반환값이 생기고 break 없이 그값이 반환된다.
  return switch(this.ratings) {
    case 'A' -> String.join(",", giftList);
    case 'B' -> String.join(",", giftList.subList(1, giftList.size()));
    case 'C' -> String.join(",", giftList.subList(2, giftList.size()));
    case 'D' -> String.join(",", giftList.subList(3, giftList.size()));
    default -> "꿀밤3대";
  };
}
```

<div style="text-align: center;">
  <figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">화살표 사용으로 반환값이 생겨 간단해 졌다.</figcaption>
</div>
<div style="display: flex; flex-direction: column; align-items: center; gap: 0px;">
  <img src="/assets/img/java/basics/switch/스크린샷 2025-03-26 172651.png" alt="출력 결과" style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px; width: 100%">
  <figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">출력 결과</figcaption>
</div>
<br>

---

> - **List 생성하는법 차이점**  
> List를 생성할때는 `Arrays.asList("str","str","str")` 과 `List.of("str","str","str")` 의 방법이 있다.
{: .prompt-tip}

<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 표 참고</figcaption>
</div>

| 구분             | Arrays.asList                                          | List.of                                               |
|------------------|--------------------------------------------------------|-------------------------------------------------------|
| **Java 버전**      | Java 1.2 이상 사용 가능                                    | Java 9 이상 사용 가능                                      |
| **불변성**        | 고정 크기 리스트<br>(요소 변경(set)은 가능하지만, 추가/삭제 불가) | 완전 불변 리스트<br>(요소 변경, 추가, 삭제 모두 불가)            |
| **null 허용 여부** | null 요소 허용                                           | null 요소 미허용 (null 포함 시 NullPointerException 발생)    |
| **내부 구현**      | 배열을 기반으로 하며 원본 배열과 연결되어 있음                   | 최적화된 불변 리스트로 독립적으로 관리됨                           |

요즘 Java 개발에서는 불변(immutable) List를 선호하는 추세입니다.
Java 9 이상부터 제공되는 **List.of()**를 사용하면 코드가 간결해지고, null 값에 대한 안전성도 보장되므로 많이 사용되고 있습니다.
와 같이 생성하면, 수정이 불가능한 리스트를 간단하게 만들 수 있습니다. 만약 리스트를 변경해야 한다면,
List<String> modifiableList = new ArrayList<>(List.of("놀이공원이용권", "치킨", "피자", "아이스크림"));
반면, **Arrays.asList()**는 여전히 사용되지만 반환되는 리스트는 고정 크기이므로 요소 추가나 삭제가 불가능해 유연성이 떨어집니다. 이러한 이유로 최신 개발 트렌드에서는 불변 객체를 기본으로 사용하고, 꼭 필요한 경우에만 변경 가능한 리스트를 별도로 생성하는 방식을 선호합니다.

이와 관련된 최신 트렌드와 모범 사례에 대해서는 여러 기술 블로그와 공식 문서를 참고할 수 있는데, 불변성을 통한 안정성과 코드 가독성이 주요 장점으로 부각되고 있습니다.
