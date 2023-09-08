---
layout: single
title: "[시스템 프로그래밍] 1.5. Vi,Gcc,Make Utility의 간단한 사용법"
typora-root-url: ../
categories: System-Programming
tags: [Vi, GCC, Make]
author_profile: false
toc: true
use_math: false

---



# 들어가기에 앞서

오늘은 "시스템 프로그래밍" 진도를 나가기 전에 간단히 환경을 설정하는 시간입니다.  
Vi, Gcc를 설치하고 간단히 사용하는 법을 알려드릴 것이고 Build할 때 필요한 파일만 업데이트해주는 Make 명령어에 대해 알려드리겠습니다.

# Ubuntu 설치

제 노트북이 Windows이기 때문에 Linux 환경이 필요해서 Oracle VM VirtualBox를 설치하고 Ubuntu를 설치하였습니다.

처음에 부팅속도가 느린게 옛날 노트북을 보는 것 같았습니다. 그래도 Ubuntu를 계속 사용하다보면 나중에 속도가 괜찮아지는 것을 느꼈습니다.

저는 Ubuntu 속도를 높이기 위해 고정디스크 20GB, cpu(프로세서) 4개, 메모리 4GB를 할당했습니다.
제 노트북 스펙은 cpu: i7 11세대, 메모리 8GB, Disk 512GB입니다. 절반 정도를 할당해도 사용하는데 문제가 없었고 Ubuntu가 빠르게 돌아갔기 때문에 이 환경으로 계속 Ubuntu를 사용할 것 같습니다.

부팅시 비밀번호는 짧게 4개로 설정했는데 초반에 렉이 좀 걸리기 때문에 짧게 설정하길 잘한것 같습니다.

# Vi 설치, 사용법(+Vim)

Unix 환경에서 텍스트 에디터는 Emacs, Vi가 있습니다.  
Emacs는 FSF를 설립하신 Richard Stallman께서 만드셨고 여러가지 기능이 있는 강력한 에디터라고 합니다. 배우는데 시간이 걸리기 때문에 저희 수업에서는 Vi로 진행한다고 하셨습니다.

다행히 저는 Visual studio, Eclipse에서 확장자로 Vim 프로그램을 써본 적이 있었고 _virmc파일을 수정해 개인설정을 했었던 경험, 손에 익었던 경험이 있었기 때문에 생소한 주제는 아니었습니다.

Ubuntu를 설치하고 바로 확인해보았더니 vi가 이미 설치되어있었습니다. 찾아보니 Ubuntu에 기본으로 설치된 vi는 'vim-tiny'라는 vim의 축소판이라고 합니다.

```shell
vi --version
vi --v
```

위 명령어 중 하나를 Terminal에 쳐보시면 버전을 확인해보실 수 있습니다.

```shell
vi hello.c
```

위 명령어를 치시면 hello.c파일을 해당 경로에 만들어주고 vi 편집기를 열어줍니다.

## Vi를 왜 써야하지?

이쯤에서 Vi가 무엇이고 왜 사용해야되는지 의문을 가지실 수 있습니다. 저희가 원래 쓰는데 gui 프로그램이랑 많이 다르고 처음에 적응하는데 많이 힘듭니다.

제가 Vi를 처음 쓰게 된 계기는 유튜브에서 ''마우스 없이 코딩하는 법''을 보고 엄청나게 빠른 코드 타이핑을 동경했기 때문입니다.
Vi는 마우스 없이 키보드만으로 커서를 마음대로 옮기고 Key 몇개로 삭제, 삽입, 복사, 이동을 마음대로 할 수 있으며, 다양한 명령어로 업무효율을 아주 많이 높일 수 있습니다. Youtube에 Vi 관련 영상을 보시면 무슨 느낌인지 이해하실 수 있을 것입니다.

하지만 처음에 적응하는 것이 어려우실 수 있습니다. 저같은 경우에 2주동안 사용하다보니 처음엔 오히려 안 사용하는 것보다 느렸지만 지금은 편하게 쓰고 있습니다. 사용하시고 싶으시다면 나중에 시간 여유로우실 때, 연습해보시면 될 것 같습니다.

다행인 점은 제가 예전에 찾아보았을 때, 요즘에는 Visual studio 같은 gui 프로그램이 잘 구성되어있어서 개발하는 경우에는 Vi를 모르고 굳이 사용안해도 괜찮다는 것을 보았습니다.

만약 맛만 보시고 싶으시다면 Chrome에 Vimium 확장프로그램을 설치해보시는 것을 추천합니다. Vi는 추천안해도 Vimium만큼은 진짜 추천드려요. 진짜 편합니다.

## Vim 설치

Vi로 hello.c를 편집하기 시작했는데 밑에 Insert도 뜨지 않고 Backspace를 눌렀는데 커서가 앞으로 가는 현상이 발생했습니다.

이를 해결하기 위해 더 편리한 Vim을 설치하였습니다.

```
sudo apt update
sudo apt install vim
```

위 명령어로 설치했더니 Backspace도 잘 작동하고, 밑에 입력모드일때 insert라고 뜨는 것을 확인할 수 있었습니다.

## Vi 사용법

사실 이것은 저보다 Youtube에서 잘 설명하고 있기 때문에, 간단한 10분 영상을 찾아보시는 것이 도움이 되실 것 같습니다.

간단하게 설명을 하면 Command 모드에서는 단축키로 명령을 내릴 수 있고 손으로 입력은 불가능합니다.  
i,a,o를 통해 Insert 모드로 들어갈 수 있는데 이때는 평소와 비슷하게 입력을 하실 수 있습니다.  
Command 모드에서 ':'를 치시고 w를 통해 저장하고 q를 통해 나가실 수 있습니다.  
또, Command 모드에서는 w,b,h,j,k,l을 통해 커서를 이동하실 수 있습니다.

참고로 알려드리면 실수로 Ctrl-s를 누르면 갑자기 멈춰서 esc를 눌러도 먹통이 되는데 Ctrl-q를 누르시면 나가실 수 있습니다.  
그냥 먹통이 되시면 Ctrl-q, Ctrl-c, q 등등을 누르시면 빠져나가실 수 있을 겁니다.

## 초보자를 위한 도움될만한 명령어

```shell
ls # 해당 경로 폴더의 파일들을 보여줌
cd /folderName/ # ls에 존재하는 폴더를 foldername에 적으시면 그 폴더로 경로 이동합니다.
clear # 명령어가 너무 많아서 shell이 꽉 차면 clear할 수 있습니다.
```

# GCC 설치, 사용법

## GCC 설치

![gccInstall](/images/2023-09-08-basicGccMake/gccInstall.png)

처음에 버전을 확인하였는데 설치가 안되어있어서 설치를 진행했습니다.  
GCC도 Richard Stallman께서 GNU 프로젝트로 만드신 겁니다. 대단하신 분이에요..

## GCC 사용법

### -o

```shell
gcc hello.c
gcc hello.c -o hello
gcc -o hello hello.c
```

먼저 gcc hello.c 같은 명령어는 hello.c 파일을 실행파일로 바꿔줍니다.

gcc hello.c 라 치시면 저희가 따로 이름을 지정하지 않았기 때문에 a.out 파일이 만들어집니다. a.out은 실행파일입니다.

-o 뒤에 이름을 치시면 그 이름으로 실행파일이 만들어집니다. 지금은 hello라는 실행파일이 만들어집니다.  
처음에 헷갈렸는데 2번째 명령어나 3번째 명령어나 같은 것입니다. -o 뒤에는 무조건 파일이름이 들어가야되는 것만 지키면 됩니다.

### -w

- -w는 warning message를 모두 삭제하는 것입니다.
- -Wall은 모든 warning message를 보여줍니다.
- -wError은 warning을 컴파일이 안되는 error로 바꿉니다.

```shell
gcc -w test.c
gcc -Wall test.c
gcc -Werror test.c
```

### -std=VER

원하는 버전으로 컴파일이 가능합니다.

```shell
gcc -std=c11 test2.c
./a.out # a.out을 실행하는 명령어
```

### -O0, O1, O2, O3

O1에서 O3으로 갈수록 최적화의 강도가 세집니다.
속도가 빨라져서 좋겠지만 최적화되어 눈으로 이해하기 힘들 수 있습니다.

```shell
gcc -O1 -o hello hello.c
```

### -m32, -m64

32비트, 64비트용입니다.
32비트는 movl, addl, esi, edi를 쓰는 반면, 64비트는 movq, addq, rsi, rdi를 사용합니다.

### -g, g1, g2, g3(-ggdb3)

뒤로 갈수록 정보의 양이 많아집니다.

```shell
gcc -g -o test_d test.c
gcc -ggdbe -o test_d2 test.c
ls -al # 폴더의 파일정보들을 볼 수 있는 명령어
```

ls-al을 통해 보면 test_d2의 용량이 test_d보다 큰 것을 알 수 있습니다.

### -Dname

예시를 보여드리겠습니다.

``` c
#include <stdio.h>
int main(void)
{
#ifdef DEBUG_TEST
    printf("Debug Test\n");
#endif
    return 0;
}
```

```shell
gcc -DDEBUG_TEST test.c
./a.out #실행결과로 Debug Test가 출력됨
```

# Make

## Make를 왜 써야할까?

1개의 hello.c 파일이 수정되면 새로운 hello.o를 업데이트해서 링킹해줘야 합니다. 그리고 hello.o의 상위파일도 바뀌니 상위파일들을 업데이트 시켜줘야되죠.

만약 이렇게 하지않고 전체파일을 그때그때마다 전부 업데이트하면 어떻게 될까요?
상용 소프트웨어 경우, 전체 Rebuild를 하면 build하는데만 1시간이 넘는 경우가 허다하다합니다.

그런데 필요한 파일들만 찾아서 .o 파일로 바꿔주고 그것들을 링킹해줘서 하기란 어렵습니다. 더욱이 파일이 많을 경우에 말이죠.
다음은 sum.c, main.c 2개의 소스코드만 존재했을 때, sum 실행파일을 만드는 과정입니다.

```shell
gcc -Wall -c sum.c
gcc -Wall -c main.c
gcc -Wall -o sum main.o sum.o
```

main.o, sum.o를 만들고 실행파일을 만드는데 3줄이 필요합니다.

## Make 설치

```shell
sudo apt install make
```

위 명령어로 설치하시면 됩니다.

## 사용법

일단 우리는 Makefile이라는 스크립트 파일을 해당폴더에 만들어줘야 합니다.

make 명령어를 치면 해당 경로에서 Makefile을 찾습니다.

```shell
make
```

### Makefile 문법

```shell
sum: main.o sum.o
	gcc -o sum main.o sum.o
main.o: main.c sum.h
	gcc -c main.c
sum.o: sum.c sum.h
	gcc -c sum.c
```

1. Dependency: 파일이 의존하는 파일을 sum: main.o sum.o과 같이 작성합니다.
2. Recipe: gcc -o sum main.o sum.o와 같이 해당 파일을 만드는 요리법을 작성합니다.

### Makefile 원리

Target : dependent files  
Target파일이 dependent 파일보다 오래된 경우, 하위 파일이 업데이트 되었다는 뜻이므로 아래 Recipe 명령어를 실행해줍니다.

## Phony Targets

```shell
clean:
	rm sum *.o
backup:
	cp main.c main_bak.c
everything: clean backup
```

잘 보시면 dependent 파일이 없죠?  
이와 같은 경우에 make 명령어를 통해 recipe 명령어만 실행시킬 수 있습니다.

```shell
make clean
make backup
```

이러면 해당 target의 recipe가 실행됩니다.

## 변수 사용

변수를 사용할 때는 특수기호를 사용하면 절대 안되고 character만 사용합니다.

```shell
OBJECT= main.o sum.o
TARGET = sum
CC= gcc
CFLAGS= -Wall

$(Target): $(OBJECTS)
	$(CC) -o sum main.o sum.o
main.o: main.c sum.h
	$(CC) -c main.c
sum.o: sum.c sum.h
	$(CC) -c sum.c
```

$(변수명) 으로 사용하실 수 있습니다.

## Automatic Variable

- $@ : target 파일 변수
- $< : 필요한 파일 변수

```shell
OBJECT= main.o sum.o
TARGET = sum
CC= gcc
CFLAGS= -Wall

$(Target): $(OBJECTS)
	$(CC) -o $@ $<
main.o: main.c sum.h
	$(CC) -c $<
sum.o: sum.c sum.h
	$(CC) -c $<
```

# 마무리

지금까지 vi, gcc, make에 대한 간단한 설명을 적었습니다.
내용이 많다보니 너무 세세하게 적진 않았지만 공부하면서 알아둬야했던 핵심 줄기랑 시행착오 위주로 작성하였습니다.

앞으로 이를 활용해서 "시스템 프로그래밍" 공부들을 적어나가겠습니다. 감사합니다.