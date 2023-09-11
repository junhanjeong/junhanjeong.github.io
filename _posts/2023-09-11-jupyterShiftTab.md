---
layout: single
title: "Jupyter notebook의 shift tab(tooltip) 단축키가 작동하지 않을 때 해결법"
typora-root-url: ../
categories: Udemy
tags: [jupyter-notebook, shift-tab, tooltip]
author_profile: false
toc: false
use_math: false
---





# 현상

tab으로 자동완성 기능은 잘 되나 shift tab으로 tooltip이 뜨지 않을때

# 해결법

ipython이 깔려있는지 확인하세요.

1. git bash에 입력
   ```bash
   ipython
   ```

2. command not found라고 뜰 경우 git bash에 입력
   ```bash
   conda install ipython
   ```

3. jupyter notebook 재시작 후 shift tab 되는지 확인

이러면 잘 작동합니다!  
구글링해도 잘 안나와서 이것저것 시도해보다 알아냈는데 저같은 사람이 있을까봐 포스팅합니다. 도움되셨길 바래요.