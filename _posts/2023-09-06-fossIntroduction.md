---
layout: single
title: "오픈소스의 등장과 여러가지 라이센스"
typora-root-url: ../
categories: openSource-SW-introduction
tags: [Free-Software, GNU, Open-source, License]
author_profile: false
toc: true
use_math: false
---



# 들어가기에 앞서 #

앞으로 학교 컴퓨터공학과 전공 수업인 오픈소스SW개론에 대해 복습한 내용을 적어보려고 합니다.

시작은 오픈소스의 개념, License에 대한 내용부터 Bash, Git, Numpy, panas 사용, 그리고 AI 관련인 Scikit-Learn, Tensorflow로 이어질 예정입니다.

오늘은 오픈소스의 등장배경과 여러가지 종류의 라이센스들에 대해 적어보도록 하겠습니다.



# 라이센스란 무엇인가? #

License는 read, modify, distribute하는 permission을 주는 대신, Obligation을 부여하는 계약이라고 볼 수 있습니다.

몇몇 코드는 License가 Unknown할 수 있는데, 그래서 마음껏 사용할 수 있는게 아니라 permission이 없다는 의미이므로 더욱 조심해야 됩니다.

아래 사진을 보시면 github에서 오른쪽에 MIT license라 써져있는 것이 License입니다.

![github_license_ex](/images/2023-09-06-license/github_license_ex.JPG)



# 라이센스 등장 배경 #

## Free Software ##

1970-80년대에는 소스코드가 공개되지 않는 독점 소프트웨어가 대부분을 이뤘습니다. 돈을 주고 프로그램을 사와도 수정, 배포할 권리까지 주어지진 않았습니다.

이에 반발하여 생겨난 것이 Free Software(자유 소프트웨어)입니다. Richard Stallman이라는 분이 만드셨는데, 이렇게 블랙박스로 코드공개가 안되어있으면 발전이 이뤄질 수 없기 때문에 이념적으로 주장하신 내용입니다.

여기서 free는 무료가 아니라 freedom(자유)를 의미하는데 4가지 자유는 다음과 같습니다.

1. 프로그램을 run할 자유
2. 코드를 modify할 자유
3. Copy한 코드를 distribute할 자유
4. 수정한 코드를 배포할 자유

리차드 스톨만은 '소프트웨어를 공유하고 변경할 자유'를 보장하기 위해 Free Software Foundation(FSF)을 설립했습니다.

##  GNU 프로젝트 ##

FSF에서는 Closed 소프트웨어를 적으로 두고 모든 SW 코드를 공개하기 위해 GNU 프로젝트를 실행합니다. 컴파일러, Bash 등등 모두 완성하고 운영체제만 남아있었는데 Linus Torvalds가 Linux를 만들면서 프로젝트가 완성되었습니다.

## Copyleft license ##

Copyleft 라이센스는 소스코드를 공개하고 run, modify, distribute할 permission을 제공합니다. 그동안과 다르게 마음껏 소스코드를 활용할 수 있게 되었습니다.

하지만 Obligation으로는 reciprocal(상호주의적)이라는 특징이 있습니다. 한마디로, 소스코드를 제공받아 사용했으면 자신도 소스코드를 공개할 의무가 있다는 것입니다.

Obligation을 안 지키면, Permission이 모두 없어지는 것이기 때문에 매우 강력한 license라고 할 수 있습니다.

### GPL(Genreal Public License) ###

GPL은 첫번째 copyleft license입니다.

소스코드를 마음껏 쓸 permission을 주는 대신, obligation이 있습니다. **바로 소스코드를 공개할 때, 같은 license로 배포해야된다는 것입니다.** Free Software 운동을 확산시키기 위한 수단이라고 할 수 있습니다. 단, 소스코드를 쓴다고 무조건 올려야되는 것이 아니라, 소프트웨어를 배포할 때만 소스코드를 공개하면 되는 것입니다.

소스코드 공개 범위는 한 프로그램의 linking한 파일 모두입니다. 예를 들어, 소스코드 a를 받아서 수정하고 다른 원래 코드 b,c랑 linking했을 때 a,b,c 모두 공개해야 됩니다.

### LGPL(Lesser General Public License) ###

GPL처럼 파일 모두를 공개하면 제약이 너무 강하기 때문에 생겨난 보다 약해진 license입니다.

아까와 동일한 상태일 때, 링킹한 파일은 제외하고 수정한 a파일만 공개하면 되는 것입니다.



## Open Source Software ##

### 성당과 시장 ###

Eric S.Raymond는 '성당과 시장'이라는 책을 작성했습니다. 그는 GNU 프로젝트를 참여했었는데 그 때 GCC 같은 프로그램들은 성당을 쌓아올리듯이 소수의 전문가들이 모여 만들었다면, Linux는 모든 사람들이 시장처럼 시끌벅쩍하게 참여해서 만들었는데 2개의 프로그램 모두 성공적이었다고 기술했습니다.

그리고 Linus의 법칙으로 '보는 눈이 많으면 버그가 사라진다'라는 말을 적었습니다.

### 도입 배경 ###

Free Software는 기업이 꺼려하는 2가지 문제점이 있습니다. Free라는 말은 원래 'Freedom(자유)'를 의미하지만 '무료'로 착각하기 쉬워 기업들이 꺼려한다는 점이 있고, 소스코드가 곧 기업의 경쟁력인데 이를 공개하면 경쟁력을 잃는다는 점입니다.

그래서 Eric S.Raymond는 Open Source라는 말을 만들었고 이때, relicense할 권리가 주어집니다. 원래 동일한 license를 배포해야되는데, 이제는 안해도 되고 소스코드를 무조건 공개하지 않아도 됩니다.

Free Software는 Copyleft 라이센스로 강력한 제약이 있었다면, Open Source는 Permissive 라이센스로 적은 제약으로 자유롭게 코드를 사용할 수 있습니다.

| Free Software         | Open Source              |
| --------------------- | ------------------------ |
| 모든 user의 권리 보장 | 개발자, 기업의 권리 보장 |
| Copyleft              | Permissive               |
| 이념적                | 현실적, 실용적           |

## Copyleft vs Permissive ##

|            | Copyleft             | Permissive                   |
| ---------- | -------------------- | ---------------------------- |
| 종류       | AGPL, GPL, LGPL, MPL | BSD, MIT, Apache             |
| Project ex | Linux, GCC, Firefox  | Android, Apache, PHP, Python |

부가설명을 하자면, AGPL은 GPL보다 강력한 Copyleft 라이센스이고 원래 SW를 배포할 때만 공개하면 되는데 배포안해도 되는 프로그램(ex. 서버)가 있기 때문에 그러한 취약점을 보완해서 더 강력한 규제를 만든 라이센스입니다.

## Shareware, Freeware, FOSS ##

일반인들에게 사용되는 용어입니다.

- FOSS(Free and Open Source Software): 같이 묶어서 부르는 말입니다. 자유를 libre라고 해서 FLOSS라고 쓰기도 합니다.
- Freeware: binary 코드를 제공받아 마음껏 사용가능하지만, 소스코드가 공개되어있지 않으므로 독점 소프트웨어라 할 수 있습니다. Free라는 말이 붙어있지만 Free Software가 아닙니다.
- Shareware: 시간적, 공간적 제약을 둔 SW입니다. 이 역시, 사유 소프트웨어에 해당됩니다.

대부분의 freeware나 shareware는 FS, OSS가 아닙니다.

## License 카데고리 ##

1. FOSS

   - Strong copyleft: GPL, AGPL
   - Weak copyleft: LGPL, MPL, EPL
   - Permissive: MIT, BSD, Apache

2. Proprietary

3. Public Domain(공용 소프트웨어)

   저작권이 없습니다. 저작권은 기본적으로 주어지기 때문에 법적인 절차를 거쳐야합니다.

1,2번은 Copyright protected입니다. Open source는 엄연히 Copyleft로 보호되는 저작물입니다.

## 왜 오픈소스인가? ##

FS가 이념적이었다면 OSS는 현실적, 실용적이고 기업들의 후원을 받으며 발전했습니다.

OSS 커뮤니티가 활발하다는 가정하에, 빠른 패치가 이뤄집니다. 이럴 경우, 본인 회사에서 특징 a만큼 더해서 코드를 수정했고 공유하지 않았다고 가정을 해봅시다. 그 후, 패치가 이뤄져서 코드가 여러개가 변경되었는데, 거기다 원래 특징 a를 유지한 채 b를 더 추가하고싶다하면  똑같은 작업으로 a를 또 추가해줘야하는 번거로움이 있습니다.

## FOSS의 장점과 단점 ##

장점

- Lower cost
- 개발 시간, 비용 단축
- 퀄리티 좋음(보는 눈이 많으면 버그가 사라진다)
- 즉각즉각 피드백과 Support를 받을 수 있다.
- 'Vendor Lock-in'을 피할 수 있다. FOSS 외에 SW를 샀는데 이를 위해 다른 SW를 사용하거나 구입하는 것을 피할 수 있다. (비유를 들면 Window를 샀더니 Explorer을 써야되는 느낌입니다.)

단, Hidden cost가 있을 수 있고, 커뮤니티가 활발하다는 가정하에 즉각적인 Support와 퀄리티가 보장된다.

단점

- user-friendly 하지 않을 수 있다. 의사결정 때, 민주절차를 거치고 이상적으로 이뤄지기 때문에 윤리성을 어기면서 빠르고 직관적이게 적용하는 것이 안된다.
- 특허 보복 가능성: 특허권을 내려고 했을 때, 막힐 수 있다.
- Hidden cost: 예를 들면, 윈도우 사용자가 Linux를 사용하라고 지시받았을 때, 설치하고 Training하는데 Hidden cost가 든다.

## 그 외 ##

- Korea Copyright Commission에 저작권 관련 문제를 문의할 수 있다.
- GPL 같은 라이센스들은 다른 라이센스들과 충돌할 수 있어서 버전이 바뀌기도 한다. (ex. GPL 3.0)
- CodeEyes와 같은 프로그램을 사용하면 무슨 코드를 사용했고 license가 무엇인지 쫙 뜬다고 한다.

## 마무리 ##

처음 학교에서 배운 수업을 정리해보았는데, 생각보다 시간이 오래 걸린다는 것을 느꼈습니다. 그래도 같은 내용을 여러번 읽어서 확실히 정리되는 느낌이라 앞으로 시간이 오래 걸리더라도 꾸준히 포스팅하도록 노력해보겠습니다. 감사합니다.

