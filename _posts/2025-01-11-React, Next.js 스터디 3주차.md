---
published: true
title: "스터디 3주차(1) - styled-components"
excerpt: "React/Next.js 스터디 3주차 기록(1)"
categories: study
tags: React

# 목차
toc_label: styled-components와 간단한 Card 컴포넌트
toc: false
toc_sticky: false
---

<br/>
스터디에서 CSS-in-JS 라이브러리로 프로젝트를 진행하기로 했기 때문에 가장 대표적인 <br/>두 라이브러리 중 선택하기로 했다.
- `styled-components`
- `emotion`

사용하는 방식이 크게 다르지 않아 emotion으로 진행하려 했으나 app Router 내의 Server Component 위에서 정상적으로 동작하지 않았고 Next.js의 공식 문서에서 다음과 같은 내용을 확인할 수 있었다.

<img src="/assets/images/css-in-js-notice.png" width="550"/>

[해당내용 링크](https://nextjs.org/docs/app/building-your-application/styling/css-in-js)

지원을 위해 노력...을 안하는 `emotion`을 대신해서 `styled-components`로 진행했다.

## 1. styled-components

`styled-component`를 통해 간단한 Card 컴포넌트를 만들어보자.

### 1-1. styled-components 없이 구현

먼저, 기본적인 Card.tsx를 만들어준다.

<script src="https://gist.github.com/TaeSuPark/47310b6975ce26737771d5bf94af7110.js"></script>

### 1-2. styled-components로 변경

위의 코드를 `styled-components`를 통해 코드를 바꿔보자.

<script src="https://gist.github.com/TaeSuPark/427d93520dd26e7d52c0084a5acc9067.js"></script>

CardContainer라는 컴포넌트를 `styled-components`를 통해 만들고, 이를 사용해서 Card 컴포넌트를 작성했다.

### 1-3. styled-components의 props 전달

재사용에 용이하며 props의 전달을 통해 상태에 따라 적용되는 디자인을 변경할 수도 있다.

<script src="https://gist.github.com/TaeSuPark/944370f58f0202f8ecfc7c37ab03e3f4.js"></script>

### 정리

간단하게 `styled-components`를 사용해서 Card 컴포넌트를 만들어봤다. 이제 다양한 컴포넌트를 디자인할 수 있게 되었다. 나중에는 ThemeProvider를 사용해서 전역으로 theme를 지정하여 프로젝트 전체 디자인을 통일시킬 예정이다.
