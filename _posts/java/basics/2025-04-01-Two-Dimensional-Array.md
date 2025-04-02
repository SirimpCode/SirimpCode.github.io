---
title: "2차원 배열 - 2 Dimensional Array"
date: 2025-04-01 16:32:21 +0900
categories: [Java, Basic]
tags: [Eclipse, Java, 기초, 배열, array, 2차원, Dimensional]
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

## 1. 2차원 배열
> `타입[][] 변수 = new 타입[크기][크기]` 로 선언한다.  
> ex) `int[][] a = new int[5][5]` 앞은 행의 크기 뒤는 열의 크기를 뜻함
{: .prompt-info}  

<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고</figcaption>
</div>

```java
public static void main(String[] args) {
  //1차원 배열
  int[] subjectArr = new int[5];
  //2차원 배열
  int[][] pointArr = new int[4][3]; // 행 = 4 ,  열 = 3
  pointArr[0][0] = 1;

  /*
   * index =>
   * ---------------------------
   * | [0][0] | [0][1] | [0][2]|
   * ---------------------------
   * | [1][0] | [1][1] | [1][2]|
   * ---------------------------
   * | [2][0] | [2][1] | [2][2]|
   * ---------------------------
   * | [3][0] | [3][1] | [3][2]|
   * ---------------------------
   *
   * */

  pointArr[0][0] = 10;
  pointArr[0][1] = 20;
  pointArr[0][2] = 30;

  pointArr[1][0] = 40;
  pointArr[1][1] = 50;
  pointArr[1][2] = 60;

  pointArr[2][0] = 70;
  pointArr[2][1] = 80;
  pointArr[2][2] = 90;

  pointArr[3][0] = 100;
  pointArr[3][1] = 100;
  pointArr[3][2] = 100;


  System.out.println("2차원 배열의 길이 => "+pointArr.length);// 4라고 나옴
  // .length 메서드는 행의 길이가 나온다.

  System.out.println("pointArr[0].length => "+ pointArr[0].length); // 3 이라고 나옴
  // .2차원배열명[행의인덱스].length 는 그 행에 존재하는 열의 길이(크기)가 나온다.
}
```

<div style="display: flex; justify-content: center; align-items: center; gap: 20px;">
  <img src="/assets/img/java/basics/array/스크린샷 2025-04-01 111958.png" alt="이미지테스트설명" style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px; width: 100%; ">
</div>
<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">출력 결과</figcaption>
</div>





<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">⬇️ 값을 테이블 형식으로 출력 해보기 ⬇️</figcaption>
</div>

```java
for(int i = 0; i < pointArr.length; i++) {
//바깥 for문에는 행이 돈다.
  for(int j = 0; j < pointArr[j].length; j++) {
  //안쪽 for문에는 열이 돈다.
    String add = j < pointArr[j].length-1 ? ",": "\n";
    System.out.printf("%d%s", pointArr[i][j], add);
  }
}
```



<div style="display: flex; justify-content: center; align-items: center; gap: 20px;">
  <img src="/assets/img/java/basics/array/스크린샷 2025-04-01 112921.png" alt="이미지테스트설명" style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px; width: 100%; ">
  </div>
<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">출력 결과</figcaption>
</div>

 <br> 

---


### - 응용 2차원 배열을 사용하여 총점과 평균 값 구하기
> `for(변수선언 : 배열){ ... }` 을 사용하여 배열에 효율적으로 반복문을 사용할 수 있다.
> - `new int[]` 은 생략 가능하다.
> - 대입되는 배열의 값을 기준으로 배열의 크기가 자동 지정된다.
> - 아래 코드는 `int[7]` 이다.
> - 즉 사용가능한 index 값은 `0 ~ 6` 까지 이고 `scores[7] = 100`  
>   이런식으로 사용할시 예외 `ArrayIndexOutOfBoundsException` 발생한다.
{: .prompt-info}

```java
/*
----------------------------------------------------
국어       영어       수학      총점    평균      학점   등수
----------------------------------------------------
90       80       70      240    80.0       B   4
80       85       76      241    80.3       B   2
80       85       76      241    80.3       B   2
85       70       90      245    81.7       B   1
60       80       50      190    63.3       D   5
====================================================
395       400       362   
79.0   80.0   72.4
	
	*/
System.out.println("\n=================== 성적결과 ===================\n");
//		이순신, 엄정화, 홍길동, 공유, 아이유 점수 구하기 과목은 국어 영어 수학 순
int[][] scoreArr = { {90,80,70},	//이순신
                    {80,85,76},	//엄정화
                    {80,85,76},	//홍길동
                    {85,70,90},	//공유
                    {60,80,50}		//아이유
}; 
		
System.out.println("--------------------------------------------------");
System.out.println("국어\t영어\t수학\t총점\t평균\t학점\t등수");
System.out.println("--------------------------------------------------");
//학생별 총점 저장 변수 
int[] scoreSum = new int[scoreArr.length];
//출력 결과 저장 변수
String[] result = new String[scoreArr.length];
for(int i = 0; i<scoreArr.length; i++) {
    int sum = 0;
    for(int j : scoreArr[i]) {
        sum += j;//국영수 합산
				if (result[i]==null) result[i]="";
        result[i] += j+"\t";//국영수 점수를 담는다
    }
    scoreSum[i] = sum;
}
//등수 저장 변수
int[] rankArr = new int[scoreArr.length];//등수 배열 인덱스는 각 학생과 동일
for(int i = 0; i<scoreArr.length; i++) {
    int rank = 1;
    for(int j : scoreSum) {
    if(scoreSum[i] < j) rank += 1;
    }
    rankArr[i] = rank;
}
for(int i = 0 ; i< scoreArr.length ; i++) {
    double avg = Math.round(scoreSum[i]/3d*10)/10d;//평균
    char rating = switch((int) avg/10) {//학점
    case 9 -> 'A';
    case 8 -> 'B';
    case 7 -> 'C';
    case 6 -> 'D';
    default -> 'F';
    };
    System.out.println(result[i]+scoreSum[i]+"\t"+avg+"\t"+rating+"\t"+rankArr[i]);
}
```

<div style="display: flex; justify-content: center; flex-direction: column; align-items: center; gap: 0px;">
  <img src="/assets/img/java/basics/array/스크린샷 2025-04-01 124710.png" alt="이미지테스트설명" style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px; width: 100%; ">
</div>
<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">출력 결과</figcaption>
</div>
<br>

---

## 2. 객체 배열과 for문 활용
> for문을 활용하여 객체 배열 돌리기
> - 스캐너에 입력된 값을 토대로 회원 인스턴스를 생성한다.
> - 회원 인스턴스를 배열에 넣는다.
> - 회원배열은 최대 3개까지 생성 할수 있다.
> - 아이디는 중복 될 수 없다.
> - 비밀번호는 영문자(대문자 or 소문자)와 숫자, 특수문자의 조합<br> 8 ~ 15 글자
> - 이름은 2 ~ 6 글자 한글로만 작성 가능
{: .prompt-info}

<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고</figcaption>
</div>

```java
public class MemberMain {

  private static MyMember[] memberArr = new MyMember[3];

  private static void addMember(MyMember[] memberArr, MyMember newMember) {
    for (int i = 0; i < memberArr.length; i++) {
      if (memberArr[i] == null) {
        memberArr[i] = newMember;
        System.out.println(newMember.getName() + "를  " + i+"번째 인덱스에 가입 시킴");
        return;
      }
    }
    System.out.println(newMember.getName()+"를 추가하지 못했어 회원 꽉참");
  }
  //중복확인
  private static boolean duplicationId(String id) {
    for(MyMember m : memberArr)
      if(m!=null)
        if(m.getNo().equals(id))
          return true;
    return false;
  }

  public static void main(String[] args) {
    Scanner sc = new Scanner(System.in);

    String userSelect = "";
    while( !(userSelect.equals("3")) ) {

      System.out.println("\n============ >> 메뉴 << ============\n"
        + "1.회원가입   2.모든회원조회   3.프로그램종료\n"
        + "=====================================");
      System.out.print("▷ 선택하세요 => ");
      userSelect = sc.nextLine().trim();
      // trim 으로 앞 뒤 모든 공백제거 ⬆️ (중앙에 낀 공백은 제거 되지 않는다.)
      switch(userSelect) {
        case "1" :
          String id = null;
          String pw = null;
          String name = null;
          while(true) {
            System.out.print("\n✔️아이디 => ");
            id = sc.nextLine();
            if(id.isBlank()) {
              System.out.println(">>[경고] 아이디값을 공백이 아닌 다른 값으로 입력하세요\n");
              continue;
            }else if(duplicationId(id)) {
              System.out.println(">>[경고] 아이디값 중복 다른 아이디로 설정하세요\n");
              continue;
            }
            break;
          }

          while(true) {
            System.out.print("\n✔️비밀번호 => ");
            pw = sc.nextLine();
            if(!MyUtil.passwordVerify(pw)) {
              System.out.println(">>[경고] 비밀번호는 8글자 이상 15글자 이하의 영문 대,소문자 및 숫자와 특수문자가 혼합되어야만 합니다.\n");
              continue;
            }
            break;
          }
          while(true) {
            System.out.print("\n✔️이름 => ");
            name = sc.nextLine();
            if(!MyUtil.nameVerify(name)) {
              System.out.println(">>[경고]성명은 공백이 없는 한글로만 2글자 이상 6글자 이하로 입력하세요!! \n");
              continue;
            }
            break;
          }

          MyMember newMember = MyMember.of(name,id, pw);
          addMember(memberArr, newMember);

          break;
        case "2" :
          for(int i=0;i< memberArr.length;i++) {
            if(memberArr[i] != null)
              System.out.println(i+1+"번째 유저 => "+memberArr[i].getInfo());
          }
          break;
        case "3" : break;
        default :
          System.out.println("\n\t다시 입력 하세요.");
          break;
      }


    }
    sc.close();
    System.out.println("\n=================종료=================");
  }
}

```
```java
//MyUtil.class
public static boolean passwordVerify(String pw) {
  return pw.matches("^(?=.*[a-zA-Z])(?=.*\\d)(?=.*[!@#$%^&*])[a-zA-Z\\d!@#$%^&*]{8,15}$");
}
public static boolean nameVerify(String name) {
  if(name.length()<2||name.length()>6) return false;
  for(char i : name.toCharArray())
    if(!(i>='가'&& i<='힣')) return false;
  return true;
}
```
<div style="display: flex; justify-content: center; align-items: center; gap: 20px;">
  <img src="/assets/img/java/basics/array/스크린샷 2025-03-31 172141.png" alt="이미지테스트설명" style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px; width: 90%; ">
</div>
<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">결과</figcaption>
</div>


<p align="center">
  <strong>🔄 while문 활용 팁 🔄</strong>
</p>

> **isEmpty**와 **isBlank**
> > | 메서드       | 설명 |
> > |-------------|-------------------------------------------|
> > | `isEmpty()` | 문자열의 길이가 0인지 확인 (`""`이면 `true`) |
> > | `isBlank()` | 공백 문자(공백, 탭, 개행)만 포함되었는지 확인 |
> 
> 
> <div style="text-align: center;">
> <figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">아래 코드 참고</figcaption>
> </div>
>
> ```java
> String emptyStr = "";
> String blankStr = "   ";
>
> System.out.println(emptyStr.isEmpty()); // true
> System.out.println(emptyStr.isBlank()); // true
>
> System.out.println(blankStr.isEmpty()); // false
> System.out.println(blankStr.isBlank()); // true
> ```
{: .prompt-tip}

> `null` 인 경우엔 두 메서드 다 `NullPointerException`이 발생한다.
> 
{: .prompt-danger}


<br>

---

<p align="center"><b>✨💡 팁 💡✨</b></p>

> 2차원 배열을 생성할때 각 행의 열의 개수가 같을 필요는 없다.
> - 배열안의 배열이라고 생각 하면 된다. 
{: .prompt-tip}

```java
public class TwoDemensionArrayMain3 {

  public static void main(String[] args) {
    int[][] num_arr = new int[4][];  // 4행 null열

    // 초기화가 안되어 있어서 NullPointerException 발생
    // num_arr[0][0] = 10;
    // num_arr[0][1] = 20;
    // num_arr[0][2] = 30;
    // num_arr[1][0] = 40;
    // num_arr[1][1] = 50;
    // num_arr[1][2] = 60;

    // 각 행을 초기화
    num_arr[0] = new int[3];  // 0행은 3열로 설정함.
    num_arr[1] = new int[2];  // 1행은 2열로 설정함.
    num_arr[2] = new int[4];  // 2행은 4열로 설정함.
    num_arr[3] = new int[3];  // 3행은 3열로 설정함.
    // 빈공간들은 기본값으로 초기화된다. ex) int = 0

    num_arr[0][0] = 10;
    num_arr[0][1] = 20;
    num_arr[0][2] = 30;

    // ArrayIndexOutOfBoundsException 발생
    // num_arr[1][2] = 30;

    for (int i = 0; i < num_arr.length; i++) {
      for (int j = 0; j < num_arr[i].length; j++) {
        String add = j < num_arr[i].length - 1 ? "," : "\n";
        System.out.printf("%2d%s", num_arr[i][j], add);
      }
    }

    System.out.println("\n------------------------------------------------------------------------------------------------------------------\n");

    int[][] numArr = {
      {10, 20, 30},
      {40, 50},
      {60, 70, 80, 90},
      {0}
    }; // 열 개수가 똑같을 필요는 없다.

    for (int i = 0; i < numArr.length; i++) {
      for (int j = 0; j < numArr[i].length; j++) {
        String add = j < numArr[i].length - 1 ? "," : "\n";
        System.out.printf("%2d%s", numArr[i][j], add);
      }
    }
  }
}
```
<div style="display: flex; justify-content: center; align-items: center; gap: 20px;">
  <img src="/assets/img/java/basics/array/스크린샷 2025-04-01 173322.png" alt="이미지테스트설명" style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px; width: 90%; ">
</div>
<div style="text-align: center;">
<figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">출력 결과</figcaption>
</div>
