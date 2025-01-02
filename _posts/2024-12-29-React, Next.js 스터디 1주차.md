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

프로젝트 경로에 `typescript` 기반의 기본적인 `Next.js` 프로젝트가 생성된다. 기존에<br/> 진행했던 프로젝트와 다른 점은 page router에서 app router로의 전환이다.

### 2-1. Page Router

Page Router 방식의 라우팅 방식은 Next 13 이전 버전부터 사용되던 방식으로,
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

App Router 방식의 라우팅 방식은 Next 13이 나오고 추가된 라우팅 방식이다.<br/>
지금까지 Page Router를 주로 사용해왔으나 App Router에서의 장점이 <br/>매력적이라 사용해보기로 했다.

- Layout을 통해 특정 구간에서의 공통 레이아웃까지 지정이 가능
- app 디렉토리 내부의 모든 컴포넌트는 기본적으로 서버 컴포넌트
- loading.js, React Suspense를 통해 로딩 UI 쉽게 적용

아래 구조를 확인해보자.

```
> src/
    > app/
        > home/
            > page.tsx
        > login/
            > page.tsx
        > item/
            > list/
                > page.tsx
        > layout.tsx
        > page.tsx
```

Page Router와 달리 폴더의 경로대로 라우팅이 이루어지며 page.tsx로 화면을 작성한다.
각 화면마다 layout을 적용하여 중첩 layout을 사용할 수 있다.

- `http://127.0.0.1:3000 (app/page.tsx)`
- `http://127.0.0.1:3000/home (app/home/page.tsx)`
- `http://127.0.0.1:3000/login (app/login/page.tsx)`
- `http://127.0.0.1:3000/item/list (app/item/list/page.tsx)`

이 외에도 다양한 사용 방법이 있으며 next.js 공식 문서에 자세히 설명되어 있다.<br/>
[참고 Link](https://nextjs.org/docs/app/building-your-application/routing)

### 정리

라우팅과 관련된 파일 구조를 확인해 봤을 때, Page Router가 좀 더 단순하고 직관적으로 <br/>되어있다고 생각한다.
하지만 Server Component의 도입, 부분적인 Layout 적용 등 최신 Next에서 좀 더 권장되는 라우팅 방식이기 때문에
적극적으로 사용해보면서 그 장점을 찾아가기로 하자.
