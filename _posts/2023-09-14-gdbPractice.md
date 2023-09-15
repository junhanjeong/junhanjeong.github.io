---
layout: single
title: "[시스템 프로그래밍] 1.5.5 GDB 디버거 간단한 사용법"
typora-root-url: ../
categories: System-Programming
tags: [GDB]
author_profile: false
toc: true
use_math: false

---



# Debug 도입

* MARK2 컴퓨터의 에러를 찾아내는 과정에서 Debug라는 용어를 처음 사용하게 되었다.
* bug란 incorrect, unexpected한 결과를 일으키는 error이다.
* debugging이란 bug를 찾고 해결하는 과정이다.
* debugger의 목적은 다음과 같습니다.
  * 디버깅: bugs를 찾는 것을 도와준다.
  * 동적 분석: 다른 프로그램의 흐름을 이해하기 위함
* debugger의 기능은 다음과 같습니다.
  * 프로그램을 정지하고 시작하고 통제할 수 있다.
  * 멈췄을 때, 내부가 무슨 상태인지 확인할 수 있다.
* Debugging의 4가지 용어
  * Test, Stabilize(재현), Localize, Correction
  * stabilize, localize가 거의 90%라고 할정도로 대부분의 비율을 차지한다.
* 디버깅 경험
  * 예전에 경험했던 비슷한 버그를 찾을 수 있다.
  * 의심되는 지점에 printf를 통해 대충 localize하고 디버깅을 시작할 수 있다.
  * 최근 변화된 것을 중점으로 디버거를 사용할 수 있다.

# GDB(GNU Debugger)

# 도입

* gdb hello로 프로그램과 같이 gdb를 메모리에 올려놓음
  아직 hello 프로그램이 실행된 것은 아님
* run으로 start execution
* breakpoint 설정 가능
* print / x / display 로 변수 조사 가능
* kill로 execution 종료
* quit으로 gdb 종료
* gdb도 유틸리티이기 때문에 다른 프로그램을 통제할 수 없습니다.  
  실질적으로는 커널에 ptrace라는 시스템콜을 보내고 커널을 통해 프로그램을 통제하는 방식입니다.

```bash
gcc -o hello hello.c -g # -g로 debug mode compile
./hello # 실행하기
```

## 명령어 미리보기

```bash
run
break main.c:1 # file에 설정
b 1 # current source file일 때, main.c: 생략 가능
b main #함수에 설정
delete N # 중단점 삭제
next # 또는 n
step # 또는 s / 함수 안으로 들어감
print E # 또는 p E / 변수값 출력
continue # 또는 c / 다음 중단점으로 뛰기
kill
quit
info source # current sourcefile 알수 있음
info b # breakpoint 다 보여줌 #1, #2 같은 형태로 나옴
```

## Segmentation fault

접근할 수 없거나 할당되지 않은 주소에 접근할 때 뜨는 에러

## 과정

```bash
gdb ./matloff # starting gdb
run # start program
backtrace
bt # 어디서 호출했는지 알려줌
up
down
list main.c:15 # 위아래 총 10줄 보여줌 / 엔터 치면 다음 라인 / l 줄임말
info source # current source file
list # 다음 10라인
list - # 이전 10라인
kill
quit
print j
print is_prime[147328]
break main
info b # 중단점 모두 보기
finish # step에서 나오기 / 약자 없음
break prime.c:7 if k >= 9 # 조건부 중단점 설정
cond 2 k>=15 # 2번 중단점 조건 변경
ignore 2 10 # 2번 중단점 10번 무시
advance 19 # 19번 라인까지 수행
```

보통 터미널 여러개 띄워놓고 한다. (편집기, 컴파일 핸들링, GDB)

## 다른 명령어

```bash
gcc -g3 -fno-stack-protector -o encrypt encrypt.c # 스택 보호 기능 해제
display 변수 # 계속 보여줌
d display N # N번 삭제
x /1wd &x # 메모리 접근 보여줌
```

## Watchpoints

변수값이 바뀔때마다 멈추게 가능

```bash
p $key # 결과값 0x7fffffffe51c
wa *(int *) 0x7fffffffe51c
```