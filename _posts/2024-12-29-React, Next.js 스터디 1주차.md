---
published: true
title: "스터디 1주차 - Next.js와 pnpm으로 프로젝트 셋팅하기"
excerpt: "React/Next.js 스터디 1주차 기록"
categories: study
tags: React

# 목차
toc_label: Next.js와 pnpm으로 프로젝트 셋팅하기
toc: false
toc_sticky: false
---

<br/>
프론트엔드 스터디를 시작하기 앞서, 기본적인 프로젝트 셋팅을 진행했다.
- macOS 환경
- VSCode

## 1. pnpm 설치

전역으로 `pnpm`을 설치

```
npm install -g pnpm
```

지금까지의 개인 프로젝트에서는 `yarn berry` 환경에서 진행했다. 프로젝트 셋팅을 하면서
<br/>
느꼈던 번거로운 부분들이 있었고 차이점을 알아보고자 `pnpm`으로 진행하게 되었다.

## 2. create next-app 실행

프로젝트 경로에서 명령어 실행

```
pnpm create next-app [프로젝트명] --typescript
```

프로젝트 경로에 `typescript` 기반의 기본적인 `Next.js` 프로젝트가 생성된다. 기존에<br/> 개발했던 프로젝트와 다른 점은 page router에서 app router로의 전환이다.

### 2-1. Page Router

Page Router 방식의 라우팅 방식은 Next 13 이전 버전에서 주로 사용되던 방식으로,
src 밑의 pages라는 폴더 내의 파일 구조를 기준으로 라우팅을 처리한다.<br/><br/>
아래 구조를 확인해보자.

```
> src/
    > pages/
        > items/
            > list.tsx
        > home.tsx
        > login.tsx
    > index.tsx (메인 화면)
    > _app.tsx (애플리케이션의 최상위 root 컴포넌트. 공통 레이아웃 등 설정)
    > _document.tsx (공통적으로 적용되는 HTML 태그, 설정 등 처리)
```

이와 같은 경로에서는 다음과 같은 라우팅이 이루어진다.
localhost를 예시로 들어보자. <br/> \_app.tsx와 \_document.tsx는 page를 생성하지 않는다.

- `http://127.0.0.1:3000 (index.tsx)`
- `http://127.0.0.1:3000/home (home.tsx)`
- `http://127.0.0.1:3000/login (login.tsx)`
- `http://127.0.0.1:3000/item/list (list.tsx)`

[참고 Link](https://nextjs.org/docs/pages/getting-started/project-structure)

### 2-2. App Router

[참고 Link](https://nextjs.org/docs/app/getting-started/layouts-and-pages)

### 3. 프로젝트 환경 초기화

### 정리
