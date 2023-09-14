---
layout: single
title: "[오픈소스SW개론] 3. Command expansions and substitutions"
typora-root-url: ../
categories: openSource-SW-introduction
tags: [shell]
author_profile: false
toc: true
use_math: false

---



# Expansions and Substitutions

* Bash에서 command를 실행하기 직전
  * Bash는 command line에 syntax elements가 있는지 확인함
  * Bash는 이러한 special elements를 스캔하고 해석하여 changed command line으로 도출함
  * 이 과정을 새 text로 expanded되거나 substituted된다고 말함
* Bash는 정의된 방식으로 expansions과 substitutions을 수행함
  * Brace, Tilde, Parameter, Arithmetic, ...

# Brace Expansion({})

![tmp1](/images/2023-09-14-commandExpansion/tmp1.JPG)

```bash
echo a{1,2,3} # a1 a2 a3로 출력
echo {1} #단일 항목은 expansion 안됨
echo {1, 2} #space 사용하면 expansion 안됨
echo {1,2}{a,b} #여러개 expansion 가능
echo {5..12..2} # 정해진 간격으로 숫자 또는 문자 나열 가능
```

![temp2](/images/2023-09-14-commandExpansion/temp2.JPG)

**Brace Expansion은 expansion-handling에서 가장 첫번째로 일어남!!**

따라서 위의 명령어에서 A1, A2가 없기 때문에 아무것도 출력이 되지 않았다.  
아래와 같은 명령어로 응용 가능하다.

```bash
mkdir /home/test/{foo,bar,cat}
touch test{1,2,3}.txt
```

# Tilde Expansion(~)

```bash
echo ~ 
echo $HOME # ~는 $HOME을 의미
echo ~+
echo $PWD # ~+는 $PWD를 의미
echo ~- # 이전 working directory 의미
```

# Parameter Eapansion(${})

$Parameter 또는 ${Parameter} 사용  
모호함을 줄이기 위해 {}를 넣어준다.

![tmp3](/images/2023-09-14-commandExpansion/tmp3.JPG)

```bash
${Parameter:-default} # :-는 unset or null일때
${Parameter-default} # :-는 unset일때
```

![tmp4](/images/2023-09-14-commandExpansion/tmp4.JPG)

# Command Substitution($())

$(command-name) or `로 쓰인다.

```bash
# 예제
$(whoami) and `hostname`
```

![tmp5](/images/2023-09-14-commandExpansion/tmp5.JPG)

* 여러 개 쓸때는 `이 아니라 ()를 쓰는 게 정확하다.
* $(;)에서 ;로 명령어 여러개를 순차적으로 실행시킬 수 있다.

# Arithmetic Expansion($(()))

![tmp6](/images/2023-09-14-commandExpansion/tmp6.JPG)

```bash
$((산술식))
expr $a + $b
```

기본적으로 변수를 줄때 문자열로 인식하기 때문에 이 조건이 필요하다.  
expr로 계산이 가능하고 값 타입을 잘 줘야 계산이 된다.

# 중간정리

우선순위는 {}, ~ 가 제일 높고, 그다음 $를 이용한 expansion, substitution이다.  

* ${a}, ${a:-5} Parameter Expansion
* $((1+2)) Arithmetic Expansion
* $(date;cal) Command Expansion

위 $를 이용한 expansion, substitution은 우선순위가 같고 여러개 있을 때 왼쪽에서 오른쪽으로 수행된다고 보면 된다.

# Filename Expansion(*,?,[])

*, ?, [set]  와일드카드이다.

```bash
#특이점
ls test?.py # 만약 test1.py 같은 파일이 존재하지 않는다면 와일드카드 발동이 안된다.
#cannot access 'test?.py'라고 결과가 나올 것이다.
ls *.[^ch] # ^는 그 set의 elements를 제외한 것이다.
ls test?.[c-o] # [c-o]로 범위로 불러올 수 있다.
```

파일을 찾을 때, test?.{c..o}로 찾으면 각각의 파일에 대해서 와일드카드 발동이 안되서 cannot access 'test?.d'와 같은 문구가 여러개 뜰 수 있다.  
따라서, ls test?.[c-o]로 찾는 것이 현명하다.  
**brace expansion({})이 항상 filename expansion([])보다 빠름을 기억해라!!**

# Metacharacters

 space, tab, newline, >, >>등 shell에서 특별한 의미를 가지고 있는 문자들이다.

# Quotes(\\,',")

metacharacter 같은 특별한 역할을 제거하고 싶을 때 사용 가능하다.  
ex. space를 무시하고 싶을 때

* Escape character(\\)
* Single quote('') : 모두 무시
* Double quote("") : parameter expansion, command expansion 제외하고 무시

## \\

```bash
touch \* # 와일드카드 무시하고 *라는 파일 생성
touch test\?.py # test?.py 파일 생성
echo \$USER # $USER 출력($ 역할 무시)
```

## Single vs Double quote

* single: Strong quote
* double: weak quote (command substitution과 parameter expansion은 실행시킴)

```bash
echo 'path is $PATH' # path is $PATH 출력
echo "path is $PATH" # path is /bin... 출력
echo "Today is $(date)" # Today is Tue .. 출력
```