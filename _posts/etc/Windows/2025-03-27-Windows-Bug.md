---
title: "윈도우 win+r 실행 메뉴에서 notepad wt 등 스토어앱 실행 오류"
date: 2025-03-27 14:37:11 +0900
categories: [etc, Windows]
tags: [에러, 버그, error, windows, 윈도우, 실행 메뉴]
math: true
toc: false # 패널 목차
#만약 너가 이 기능을 끄고싶다면 _config.yml파일로가서 toc값을 false로 바꾸어주면된다. 
pin: false
image:
  path: /assets/img/etc/Windows/windows.jpg
#  alt: 이클립스와 자바
---

# 에러 증상 및 해결 방법

---

## 1. 에러 증상

- **Win+R 단축키**로 실행 메뉴에서,
  - **Microsoft Store**에서 다운로드 받은 **notepad (업데이트된 메모장)**, **wt (Windows Terminal)** 등이 실행되지 않음
- 반면, **calc, cmd** 등 기본 제공 앱은 정상 동작

---

## 2. 증상 상세 확인

- Win+R에서 `eventvwr` 입력 시, 이벤트 뷰어를 통해 로그를 확인할 수 있다.
<div style="display: flex; flex-direction: column; align-items: center; gap: 0px;">
  <img src="/assets/img/etc/Windows/eventviewer.png" alt="참고 이미지" style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px; width: 100%">
  <figcaption style="font-size: 12px; color: gray; opacity: 0.8; margin-bottom: 15px">참고 이미지</figcaption>
</div>

---

## 3. 해결 방법

### ◆ Microsoft Visual C++ 재설치 (ucrtbase.dll 관련 문제 해결)

- **문제 원인:**
  - **Windows Terminal**(및 notepad 등)이 `ucrtbase.dll`에서 충돌하고 있다.
  - 해당 파일은 **Microsoft Visual C++ Redistributable**의 일부이다.

- **해결 단계:**

  1. **Microsoft Visual C++ Redistributable 삭제**
    - 제어판의 **프로그램 추가/제거**에서 기존의 Microsoft Visual C++ Redistributable을 모두 삭제.

  2. **최신 C++ 런타임 재설치**
    - Microsoft 공식 사이트에서 최신 VC++ 재배포 가능 패키지(64비트)를 다운로드.
    - 다운로드 받은 파일을 실행하여 설치.

  3. **앱 재설치 및 시스템 재부팅**
    - 이상 동작하던 **notepad, wt** 등 앱들을 삭제한 후, 다시 설치.
    - 시스템을 재부팅한 후, **wt (Windows Terminal)** 등이 정상적으로 실행되는지 확인.

