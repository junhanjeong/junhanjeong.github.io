---
layout: single
title: "[시스템 프로그래밍] 1. A tour of Computer System"
typora-root-url: ../
categories: System-Programming
tags: [System-Programming]
author_profile: false
toc: true
use_math: false
---



# 소스코드를 실행파일로 변환 #

## 정보는 비트와 약속으로 구성된다 ##

Source File은 ASCII 코드로 정수로 표현해 컴퓨터가 이를 표현할 수 있다. ASCII 코드라는 약속을 통해 동일하게 표현 가능한 것이다.

File은 크게 사람이 읽을 수 있는 Text파일과 0101로 이뤄진 Binary 파일로 나뉠 수 있다.

## 컴파일하는 방식 ##

1. 전처리기
   hello.c 라는 소스코드(text 파일)는 전처리기에 의해 #include, #define 같은 지시어들을 전부 대체하는 역할을 한다. 그러면 hello.i라는 수정된 소스코드(text 파일)이 나온다.
   보통 #include 파일을 대체하면 extern 이라는 키워드가 앞에 붙게 되는데 의미는 '이 파일에 원하는 것이 없다 알려주고 링킹과정에 나올테니 일단 넘겨' 라는 뜻이다.
2. 컴파일러
   hello.i 파일은 컴파일러에 의해 어셈블리 파일로 바뀐다. hello.s 라는 파일(text)이 나오는데 니모닉 심볼이라고 부른다.
   이는 기계어와 1대1 매칭되고 사람이 읽을 수 있는 text 파일이며 하드웨어에 dependence하기 때문에 아키텍쳐마다 다르다는 특징이 있다.
3. 어셈블러
   hello.s 파일을 컴퓨터가 읽을 수 있는 Binary 파일로 바꿔준다. hello.o 파일이고 0101로 이뤄져있어 사람이 읽기 힘들다. 바로 실행은 불가능하고 링킹되어야 실행 가능하다.
4. 링커
   hello.o 파일과 printf가 정의된 printf.o 파일이 링킹되어야 비로소 hello.elf 라는 파일이 생기고 실행이 가능해진다.
   printf.o 파일에는 심볼테이블이 붙어있다. main, printf 같은 심볼이 있는데 해당 코드에서 찾으면 "T"라고 나오고 Undefined이면 "U"라고 뜨고 다른 곳에서 찾아 링킹한다.

# Running the program #

## 커널, 쉘, 유틸리티 ##

hello.c 파일을 실행하면 hello.elf 파일이 Disk 위에 올라간다. 그리고 DMA 방식으로 메모리에 적재된다.

메모리에 적재되는 것은 크게 커널과 유틸리티이다. 커널은 시스템이 켜질때 메모리에 안착된다. 유틸리티 중에 유틸리티 for 유틸리티 로 쉘이 있다. 쉘은 주로 로그인할 때 메모리에 적재된다. Linux에서는 Bash를 쓰고 gui, tui 유형의 쉘이 있다. 쉘은 명령어를 받길 기다리고 엔터를 치면 command를 실행한다. command는 내장명령, 외부명령이 있다.
## 컴퓨터 구조 ##

크게 CPU, Memory, IO로 볼 수 있다.
### 폴링 방식 vs DMA 방식 ###

기존 폴링 방식은 cpu가 DIsk controller가 idle할 때까지 대기하는 방식이다. cpu는 속도가 아주 빠르고 Disk io는 느린데 cpu가 기다리는게 아주 비효율적이다.

DMA 방식은 cpu는 일하게 냅두고 Memory에 DIsk에 적재된 hello.elf의 명령어를 모두 Copy하는 것이다. 그러면 cpu, disk controller가 각자 일하고 복사가 끝나면 cpu가 메모리에 접근해 hello.elf를 실행할 수 있다.

방식은 다음과 같다.

1. CPU가 Disk에게 메모리에 복사하라고 명령
2. DMA 방식으로 Disk에서 메모리에 복사
3. Disk Controller가 cpu에 끝났다고 알려줌(인터럽트)

### CPU 일하는 방식 ###

CPU 안에는 PC, IR, 레지스터 파일, ALU, 캐시가 있다.
PC(프로그램 카운터)는 다음에 실행할 명령어의 주소를 가진다.
IR(Instruction 레지스터)는 명령어를 저장한다.
ALU는 만능계산기라고 보면 된다.
레지스터 파일은 ALU가 계산한 임시결과를 저장한다.
캐시는 과거 데이터를 기반으로 앞으로 쓰일 중복된 데이터를 '로컬리티'라는 개념으로 저장해놔서 불필요한 이동을 줄인다.

CPU는 다음 일만 수행한다.

1. PC에서 메모리에 접근하여 명령어를 fetch하여 IR에 저장한다.
2. IR에 저장된 명령어를 decode한다.
3. execution한다.

fetch, decode, execution을 계속 반복하면서 cpu는 계속 일을 수행한다.

레지스터 파일이 존재하는 이유는 ALU에서 계산한 임시결과들을 메모리에 저장하면 나중에 BUS를 통해 접근해야되서 시간이 소요되기 때문에 CPU안에다 임시결과를 저장하는 것이다.

캐시는 시간적, 공간적 로컬리티 개념으로 과거데이터를 저장해서 후에 그 데이터가 또 쓰이면 메모리에 다시 접근하는 것이 아니라 CPU 안에서 바로바로 꺼내서 쓸 수 있는 것이다.

### S램, D램 ###

비싸지만 속도가 빠른 S램을 CPU와 가까이 배치하고 느리지만 가격이 낮은 D램을 Main Memory로 쓴다.
CPU의 캐시는 SRAM, Main 메모리는 DRAM이라고 보면 된다.

## OS(운영체제) ##

우리는 키보드, 모니터와 관련된 명령어를 치지않고 hello.c 파일을 실행시킬 수 있다. 그 이유는 OS가 보조해주기 때문이다. OS의 목적은 다음과 같다.

1. 사용자가 이상하게 써서 시스템 고장내는걸 막기위함
2. 사용자에게 Simple하고 편리한 환경을 제공하기 위함
3. 안 보이는 곳에서 효율적으로 자원을 관리하기 위함

OS의 중요개념은 다음 3가지이다. Processor, Main memory, Files. 
추후에 OS 수업이나 이 수업의 후반부에서 자세히 배울 예정이다.
