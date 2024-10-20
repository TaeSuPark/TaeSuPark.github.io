---
published: true
title: "React와 state"
excerpt: "react에서는 왜 state라는 녀석을 사용할까?"
categories: programming
tags: React

# 목차
toc_label: React의 state
toc: false
toc_sticky: false
---

최근 진행했던 면접에서 react와 관련해서 굉장히 단순한 질문을 받았다.

    -  react에서는 왜 state를 사용하는가?

지금 와서 생각해보면 아주 간단한 문제였는데 이걸 대답을 못했다...
결국 헛소리만 하다가 면접장 문을 닫고나서야 기억이 나더라.

React에서는 일반적인 변수를 사용할 경우 해당 변수가 값이 바뀌더라도 새롭게 렌더링되지 않는다.
하지만 react의 state를 useState를 통해 사용하게 될 경우 state의 변경을 감지해서 화면이 새롭게 렌더링된다.

이 단순한걸 대답을 못하고 버벅이다니... 너무 당연하게 사용하고 있어서 순간 생각이 멈췄던 것 같다.
