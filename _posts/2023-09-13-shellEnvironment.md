---
layout: single
title: "[오픈소스SW개론] 2. Shell Environment"
typora-root-url: ../
categories: openSource-SW-introduction
tags: [shell]
author_profile: false
toc: true
use_math: false

---



# 들어가기에 앞서 #

학교 Innovation Academy에 대비해 Udemy 강좌 수강에 집중하느라 블로그에 포스팅할 시간이 별로 없는 것 같습니다..
그래도 나중을 위한 기록으로 꾸준히 포스팅해나가겠습니다.

# Shell의 Advantages and Disadvantages

* Advantages
  * 사용하기 쉽고 재활용성 높다.
  * Java, C, Web 같은 이질적인 언어들한테 적용 가능(glue code)
  * 성능 기대 못하지만 사용하기 쉽고 자동화 쉬움
* Disadvantages
  * 느리고 complex/performance-sensitive 문제에는 어울리지 않음
  * 에러 발생하기가 쉬움
    ex) rm -rf test* / rm -rf test *

# Shell Variables

* Environment variables
  * 자식에게 전달
* Built-in environment variables
  * predefine된 변수
  * 모두 대문자

## Set

![tmp1](/images/2023-09-13-shellEnvironment/tmp1.JPG)

```bash
varname=value # 변수 설정, 띄어쓰기 안됨
echo $varname # 변수 출력
set # 모든 변수 출력
set|more # 한 화면까지 출력, Enter치면 한줄씩 더 보여줌
```

## unset

![temp2](/images/2023-09-13-shellEnvironment/temp2.JPG)

```bash
unset varname # 변수 삭제
set|grep My # My 포함된 변수 출력
```

## export and env(printenv)

![temp3](/images/2023-09-13-shellEnvironment/temp3.JPG)

```bash
export varname=value # environment variable로 set
env # set과 다르게 환경변수만 모두 보여줌
printenv # 동일함
```

![temp4](/images/2023-09-13-shellEnvironment/temp4.JPG)

```bash
bash # 내부 배쉬로 들어감
exit # 나옴
pstree | grep bash # bash를 치고 이 명령어를 쳤더니 bash가 2번 뜨는것을 확인할 수 있음
```

export로 선언한 환경변수는 bash로 또 들어가도 값이 남아있음.

## export -n

![tmp5](/images/2023-09-13-shellEnvironment/tmp5.JPG)

```bash
export -n varname # 변수 삭제가 아니라 환경변수 설정을 소멸시킴
```

## Built-in envrionment value

env으로 보면, 설정하지 않은 환경변수들이 있는 것을 볼 수 있다.  
모두 대문자로 설정되어야 한다.  
(ex. HOME, PATH, PWD, SHELL, OSTYPE)

![tno6](/images/2023-09-13-shellEnvironment/tno6.JPG)

:으로 directory name이 구분되어있고 shell에서 command를 치면 이 경로들에서 매번 찾는다. 경로를 없애면 ls 명령어를 쳐도 command not found가 뜰 수 있다.

PATH=$PATH":/home/you/bin" 으로 뒤에 directory를 추가할 수 있다.

![tmp6](/images/2023-09-14-shellEnvironment/tmp6.JPG)

```bash
type more
type ls
```

type 명령어는 /bin/more 같은 경로에 있는 실행 파일인지, 아니면 쉘 내장 명령어나 별칭인지를 알려준다.

![tmp7](/images/2023-09-14-shellEnvironment/tmp7.JPG)

```bash
echo $HOME # HOME 변수 출력
cd # HOME으로 이동
pwd # 현재위치 출력
$HOME=위치 # HOME 변수 설정가능, 위에 Deesktop은 오타임
```

하지만 HOME과 같은 변수 설정은 터미널 종료시 모두 초기화가 됩니다.  
따라서, 영구적으로 유지하고 싶으면 '~/.bashrc' 파일을 이용해야합니다.