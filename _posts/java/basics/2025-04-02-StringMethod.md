---
title: "자바의 문자열 활용 - String.class의 메서드"
date: 2025-04-02 09:12:21 +0900
categories: [Java, Basic]
tags: [Eclipse, Java, 기초, 문자열, String, substring, indexOf, split, join, replace, contains]
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

## 1. for 문을 활용 문자열 뒤집기

<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고</figcaption>
</div>

```java
String str = "안녕하세요";
String result = "";
//문자열 뒤집기 
for(int i = str.length()-1; i>=0; i--)
  result += str.charAt(i);
		
System.out.println(result);/*"요세하녕안"*/


/*toCharArray() 활용*/
for(char i : str.toCharArray()) {
  System.out.print("|'"+i+"'");
  if (i == str.charAt(str.length()-1))
    System.out.println("|");
}
```

<br>

---

## 2. substring 과 indexOf

### 2-1. substring
> **`String.class`의 substring 메서드**
> - 파라미터는 1개 또는 2개를 사용한다.  
> - 파라미터가 1개 일때는 시작 인덱스
> - 파라미터가 2개 일때는 시작 인덱스와 끝 인덱스
> - `str.substring(1,str.length()-1)` 이런식으로 사용
{: .prompt-info}


> 끝 인덱스 지정시 해당 인덱스를 제외한 그 앞부분까지 나온다.
> `String str = "안녕하세요"`
> `str.substring(1,4)` => "녕하세"
{: .prompt-danger}

<br>

---

### 2-2. indexOf
> **`String.class`의 indexOf 메서드**
> - 파라미터는 1개 또는 2개를 사용한다.
> - 파라미터가 1개일 때는 찾고자 하는 문자 또는 문자열
> - 파라미터가 2개일 때는 찾고자 하는 문자 또는 문자열과  
> 시작 인덱스
> - 예시: `str.indexOf('안')`, `str.indexOf('하', 2)`
{: .prompt-info}


<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">위 두 메서드를 활용한 코드</figcaption>
</div>

```java
//퀴즈 파일명만 꺼내오기
String[] pathFileNameArr = {
  "C:/mydocument/resume/나의이력서.hwp",
  "D:/mymusic.mp3",
  "C:/photo/니얼굴.jpg"
};
//lastIndexOf를 활용
for(String path : pathFileNameArr) {
  int index = path.lastIndexOf("/");
  System.out.println(path.substring(index+1));
}

System.out.println("--------------------------------------------------------");//공백

//그냥 indexOf 활용 이번엔 확장자도 없애봤음
for(String path : pathFileNameArr) {
  int index = 0;
  int lastIndex = 0;
  for(int i = path.length()-1 ; i>=0; i-- ) {
    if(lastIndex == 0)
        if(path.charAt(i)=='.')
            lastIndex = i;
    if(path.charAt(i)=='/') {
        index = i;
        break;
    }
  }
  System.out.println(path.substring(index+1,lastIndex));
}


```



<div style="display: flex; justify-content: center; align-items: center; gap: 20px;">
  <img src="/assets/img/java/basics/string/스크린샷 2025-04-02 102319.png" alt="이미지테스트설명" style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px; width: 100%; ">
  </div>
<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">출력 결과</figcaption>
</div>

 <br> 

---


### 2-3. split 
> **`String.class`의 split 메서드**
> - 문자열을 구분자로 잘라서 `String` 타입의 배열로 돌려준다.
> - 구분자를 기준으로 배열로 나뉘고, 구분자는 제거된다.
{: .prompt-info}

```java
//split 
String food = "제육볶음,볶음밥,닭가슴살,함박스테이크,소고기덮밥";
String[] foodArr = food.split(",");
		
for(int i = 0 ; i<foodArr.length; i++) {
  System.out.println(i+1+"."+foodArr[i]);
}
```

<div style="display: flex; justify-content: center; flex-direction: column; align-items: center; gap: 0px;">
  <img src="/assets/img/java/basics/string/스크린샷 2025-04-02 111627.png" alt="이미지테스트설명" style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px; width: 100%; ">
</div>
<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">출력 결과</figcaption>
</div>

> **`split` 사용시 주의사항**
> - `.`
> - `|`
> - `/`  
> 위의 특수문자를 split에 사용 시 `\\` 를 앞에 적어줘야 된다.
> - ex)   
> `String food = "제육볶음.볶음밥.닭가슴살.함박스테이크.소고기덮밥";`
> `String[] foodArr = food.split("\\.");`
{: .prompt-danger}

> 탭과 같은 특수문자는 출력문에 사용하는것처럼
> - `\t`
> 이런식으로 적어주면 적용된다.
> - `\\,` , `\\\t`  원래 콤마나 탭도 이렇게 적어줘야 된다.
{: .prompt-tip}

<br>

---
#### -tip.　**split** 사용 할때 팁

> **구분자**가 여러개 일 경우 참고
> - `|` 로 구분하여 작성하거나 `[` `]` 대괄호를 사용한다.
> - 아래 코드는 `.` `,` `|` `탭` 을 기준으로 나눈 코드이다.
> 
> <div style="text-align: center;">
> <figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고</figcaption>
> </div>
> 
> ```java
> String food = "제육볶음,볶음밥.닭가슴살|함박스테이크	소고기덮밥	라면";
> String[] foodArr = food.split("\\.|,|\\||\t");
> // '|'로 구분하고 \\.	,	|	\t    이렇게 총 네개로 끊었다.
> for(int i = 0 ; i<foodArr.length; i++) {
>   System.out.println(i+1+"."+foodArr[i]);
> }
>		
> String food2 = "제육볶음,볶음밥.닭가슴살|함박스테이크	소고기덮밥	라면";
> String[] foodArr2 = food2.split("[.|,\t]");
> // 대괄호 안에 작성하면 가독성이 더 좋아진다. 의미는 위에것과 동일함
> for(int i = 0 ; i<foodArr2.length; i++) {
> System.out.println(i+1+"."+foodArr2[i]);
> }
> ```
{: .prompt-tip}
 
> **문자열**에서 `\` 의 활용
> - \ 를 escape 문자라고 부른다.
> - 문자열안에 문자를 있는 그대로 넣고 싶을때 사용
> 
> <div style="text-align: center;">
> <figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고</figcaption>
> </div>
>
> ```java
> System.out.println("나의 이름은 \"이순신\" 입니다.");
> // 나의 이름은 "이순신" 입니다.
>
> System.out.println("C:\\NCS\\workspace_java");
> // C:\NCS\workspace_java
```
{: .prompt-tip}

<br>

---



## 3. join

### 3-1. join
> **`String.class`의 join 메서드**
> - 첫 번째 파라미터는 구분자(delimiter)를 지정한다.
> - 두 번째 파라미터는 가변인자(varargs) 또는 Iterable을 사용한다.
> - 배열이나 컬렉션의 각 요소를 지정한 구분자로 연결하여 하나의 문자열을 반환한다.
> - 예시:   
`String.join("-", "Java", "Python", "C++")` → "Java-Python-C++"
{: .prompt-info}

<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">위 메서드를 활용한 코드 예제</figcaption>
</div>

```java
// 가변인자를 활용하여 문자열 연결하기
String languages = String.join("-", "Java", "Python", "C++");
System.out.println(languages); // 출력: Java-Python-C++

// Iterable을 활용하여 문자열 연결하기
List<String> fruits = Arrays.asList("apple", "banana", "cherry");
String fruitString = String.join(", ", fruits);
System.out.println(fruitString); // 출력: apple, banana, cherry
```

<br>

---

### 3-2. 활용

> 문자열에 있는 숫자를 `split`과 `join`을 활용 하여 연산하기
> - 기대값 = $2,000,000 + $500,000 = 2500000
{: .prompt-info}

<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고</figcaption>
</div>

```java
String money1 = "$2,000,000";
String money2 = "$500,000";
int money3 = 0;
String[] sp1 = money1.split("[$,]");
String[] sp2 = money2.split("[$,]");
        
String s1 = money1.join("", money1.split("[$,]"));
String s2 = money2.join("", money2.split("[$,]"));
        
money3+=Integer.parseInt(s1);
money3+=Integer.parseInt(s2);
System.out.println(money1 + " + " + money2 + " = "+ money3);
```

<br>

---

## 4. replace


> `replace`
> - 문자열 내에 지정한 문자 또는 문자열을 다른 문자 또는 문자열로 치환함
> - 두 개의 파라미터를 사용: 첫 번째는 치환 대상, 두 번째는 치환할 문자열
> - 문자열 내에 해당하는 모든 부분을 새로운 문자열로 대체하여 결과 문자열을 반환함
> - 예시: `str.replace("old", "new")`
{: .prompt-info}

<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">위 메서드를 활용한 코드 예제</figcaption>
</div>


```java
String sentence = "Java is powerful. Java is popular.";
String newSentence = sentence.replace("Java", "Python");
System.out.println(newSentence); 
// 출력: Python is powerful. Python is popular.
```


```java
//replaceAll  해당 문자열을 새로운 문자열로 전부 치환 한다.
String names = "한석규-두석규-세석규-네석규-오석규";
System.out.println(names);//한석규-두석규-세석규-네석규-오석규
names = names.replaceAll("석규", "SK");
System.out.println(names);//한SK-두SK-세SK-네SK-오SK
//replaceFirst  해당 문자열의 첫번째 값만 새로운 문자열로 치환한다.
names = names.replaceFirst("SK", "석규");
System.out.println(names);//한석규-두SK-세SK-네SK-오SK
```
<div style="display: flex; justify-content: center; align-items: center; gap: 20px;">
  <img src="/assets/img/java/basics/string/스크린샷 2025-04-02 140749.png" alt="이미지테스트설명" style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px; width: 90%; ">
</div>
<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">출력 결과</figcaption>
</div>

---

<p align="center">
  <strong>🔄 replace 와 replaceAll 의 차이🔄</strong>
</p>

> `replace` vs `replaceAll`
> - **replace**
>   - 지정한 문자나 문자열을 그대로 찾아서 변경함 (정규식 미적용)
>   - 단순 문자열 치환에 사용되며, 입력값을 리터럴로 취급함
> - **replaceAll**
>   - 첫 번째 파라미터를 정규식으로 해석하여 패턴에 맞는 모든 부분을 변경함
>   - 복잡한 패턴 매칭 및 치환이 필요할 때 사용됨
{: .prompt-tip}



<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고</figcaption>
</div>

```java
String text = "abc123abc456";

// replace는 리터럴 치환 (정규식 미적용)
String replaced = text.replace("abc", "XYZ");
System.out.println(replaced); // 출력: XYZ123XYZ456

// replaceAll은 정규식 적용 치환
String replacedAll = text.replaceAll("\\d", "#"); // 숫자를 모두 '#'로 변경
System.out.println(replacedAll); // 출력: abc###abc###
```

---

<p align="center">
  <strong>🤜 replace 응용 하기 🤛</strong>
</p>

> - 여러 석규들로 특정 조건에만 replace를 적용
{: .prompt-tip}

```java
names = "한SK-두SK-세SK-네SK-오SK";
//replaceFirst 를 사용하여 첫번째, 두번째, 세번째 "SK" 를 "석규"로 변환
String[] nameArr1 = names.split("-");
for(int i = 0; i<3; i++)
    nameArr1[i] = nameArr1[i].replace("SK", "석규");

System.out.println("첫번째 문제 : "+ String.join("-", nameArr1));

//홀수번째 나오는 "SK" 를 "석규"로 변환
names = "한SK-두SK-세SK-네SK-오SK";
String[] nameArr = names.split("-");
for(int i = 0; i< nameArr.length; i++)
    if(i%2==0)
        nameArr[i] = names.split("-")[i].replace("SK", "석규");

System.out.println("두번째 문제 : "+String.join("-", nameArr));
```

<div style="display: flex; justify-content: center; flex-direction: column; align-items: center; gap: 0px;">
  <img src="/assets/img/java/basics/string/스크린샷 2025-04-02 144116.png" alt="이미지테스트설명" style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px; width: 100%; ">
</div>
<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">출력 결과</figcaption>
</div>

<br>

---

## 5. contains

> `contains`
> - 문자열 내에 특정 문자 또는 문자열이 포함되어 있는지를 확인함
> - 포함되어 있으면 `true`, 그렇지 않으면 `false`를 반환함
> - 예시: `str.contains("Java")`
{: .prompt-info}

<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">위 메서드를 활용한 코드 예제</figcaption>
</div>

```java
String sentence = "Java is a versatile programming language.";
boolean containsJava = sentence.contains("Java");
System.out.println("Contains 'Java': " + containsJava); // 출력: Contains 'Java': true

boolean containsPython = sentence.contains("Python");
System.out.println("Contains 'Python': " + containsPython); // 출력: Contains 'Python': false
```

> 만약 대소문자 구분을 안하고 비교하고 싶을 시  
> `toLowerCase()` 나 `toUpperCase()` 를 사용하면 된다.
> - ex) `str.toLowerCase().contains("java")`
{: .prompt-tip}

<br>

---

## 6. 기타 함수들

### 6-1. repeat

> `repeat` 
> - 해당 문자열을 파라미터로 주어진 수 만큼 반복 시킨다.
{: .prompt-info}
<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고</figcaption>
</div>

```java
//repeat : 문자열을 파라미터로 주어진 수 만큼 반복
System.out.println("\n"+"=".repeat(100) + "\n"); // =가 100번 찍힌다.
System.out.println("\n"+"안녕 ".repeat(50) + "\n"); // 안녕 이 50번 찍힌다.

```

<br>

---

### 6-2. strip

> `strip` , `stripLeading` , `stripTrailing`
> - strip : 문자열 공백 제거 (문자열 사이에 있는건 제거 안됨)
> - stripLeading : 문자열 앞의 공백 제거
> - stripTrailing : 문자열 뒤의 공백 제거
{: .prompt-info}

<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고</figcaption>
</div>

```java
System.out.println(" 안 녕 안녕 헿 헤   헤    ".strip());
System.out.println(" 안 녕 안녕 헿 헤   헤    ".stripLeading());
System.out.println(" 안 녕 안녕 헿 헤   헤    ".stripTrailing());
```

<div style="display: flex; justify-content: center; flex-direction: column; align-items: center; gap: 0px;">
  <img src="/assets/img/java/basics/string/스크린샷 2025-04-02 124726.png" alt="이미지테스트설명" style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px; width: 100%; ">
</div>
<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">strip 은 앞뒤 공백이 제거<br>stripLeading 은 앞 공백<br>stripTrailing 은 뒤 공백이 제거 되었다.</figcaption>
</div>

<br>

---

## 7. startWith와 endWith

> 문자열의 시작 부분 또는 끝나는 부분에 활용 한다.
> ex)
> `str.startWith("뭐야")` ➡️  "뭐야" 로 시작 한다면 `true` 아니면 `false`
{: .prompt-info}

<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고</figcaption>
</div>

```java
// "건강" 이라는 문자열로 시작하는 것만 출력
//startWith 활용
for(String a : contents) {
  if(a.startsWith("건강"))
    System.out.println(a);
}
//indexOf 활용
for(String a : contents) {
  if(a.indexOf("건강")==0)
    System.out.println(a);
}
System.out.println("=================".repeat(10));
//하세요 라는 문자열로 끝나는 것만 출력
for(String a : contents) {
  if(a.endsWith("하세요"))
    System.out.println(a);
}
System.out.println("=================".repeat(10));
//substring 활용 (뒤에서 3번째의 index 번호를 사용해서 하세요라는 문자열인지 확인)
for(String a : contents) {
  int length = a.length();
  int doIt = "하세요".length();
  int index = length - doIt;
  if( a.substring(index).equals("하세요"))
    System.out.println(a);
}
```

<br>

---

## 8. trim

> `trim`
> - 문자열 앞뒤의 불필요한 공백(whitespace)을 제거함
> - 내부에 있는 공백은 제거되지 않음
> - 기존부터 사용되던 메서드로, 공백 문자의 범위가 제한적임 (예: ASCII 스페이스, 탭, 개행 문자 등)
> - 예시: `str.trim()`
{: .prompt-info}



<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고</figcaption>
</div>

```java
String text = "   Hello, World!   ";
System.out.println("[" + text.trim() + "]"); // 출력: [Hello, World!]
```

<br>

---

<p align="center">
  <strong>🔄 trim vs strip 🔄</strong>
</p>

> **trim 과 strip 차이점**
> - **trim**
>   - 문자열의 앞뒤에 있는 공백(ASCII 공백, 탭, 개행 등)을 제거함.
>   - 모든 유니코드 공백 문자를 제거하지는 못할 수 있음.
> - **strip**
>   - Java 11부터 추가된 메서드로, 모든 유니코드 공백 문자를 제거함.
>   - `Character.isWhitespace()` 기준으로 공백을 판단하여 처리함.
{: .prompt-tip}

```java
public class TrimStripExample {
    public static void main(String[] args) {
        // 유니코드 공백 문자 (예: en space: \u2002) 포함 문자열
        String original = "\u2002\u2002Hello, World!\u2002\u2002";

        // trim: 주로 ASCII 공백만 제거
        String trimmed = original.trim();
        // strip: 모든 유니코드 공백을 제거 (Java 11 이상)
        String stripped = original.strip();

        System.out.println("Original: [" + original + "]");
        System.out.println("trim():   [" + trimmed + "]");
        System.out.println("strip():  [" + stripped + "]");
      // 예상 출력 (trim()은 유니코드 공백을 제거하지 않음):
      // 원본:    [  Hello, World!  ]
      // trim():  [  Hello, World!  ]
      // strip(): [Hello, World!]
    }
}

```

<div style="text-align: center;"> <figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">두 메서드의 차이점을 보여주는 예제</figcaption> </div>


<br>

---

## 9. liens()
> `"문자열".lines().toArray()`
> - "문자열" 에서 줄 단위(`\n`)로 나뉘어 있는 문자열을 배열로 반환
{: .prompt-info}

<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고</figcaption>
</div>

```java
Object[] objArr = "한줄\n두줄\n세줄\n네줄\n다섯줄\n여섯줄".lines().toArray(); 
for(Object obj:objArr) {
  if(obj instanceof String)
    System.out.println(((String) obj));
}
```

<div style="display: flex; justify-content: center; flex-direction: column; align-items: center; gap: 0px;">
  <img src="/assets/img/java/basics/string/스크린샷 2025-04-02 163124.png" alt="이미지테스트설명" style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px; width: 100%; ">
</div>
<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">출력 결과</figcaption>
</div>

<br>

---


## 10. jdk17부터 사용되는 `"""` 
> 기존에 문자열내에서 `\n` 이나 `\"` 와 같이 사용되던 문자들이  
> `"""`를 사용하면 가독성이 매우 향상된다.
{: .prompt-info}

<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고</figcaption>
</div>

```java
String msg = """
  안녕하세요
  오늘은 수요일 입니다.
  즐거운 오후 되세요.
  """;
String oldMsg = "안녕하세요\n오늘은 수요일 입니다.\n즐거운 오후 되세요.";
//위의 두 문자열은 서로 동일하게 출력된다.       
System.out.println(msg);
System.out.println(oldMsg);
```

<div style="display: flex; justify-content: center; flex-direction: column; align-items: center; gap: 0px;">
  <img src="/assets/img/java/basics/string/스크린샷 2025-04-02 163748.png" alt="이미지테스트설명" style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px; width: 100%; ">
</div>
<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">출력 결과</figcaption>
</div>

<br>

---


