---
published: true
title: "스터디 4주차 - tanstack-query(in client component)"
excerpt: "React/Next.js 스터디 4주차 기록"
categories: study
tags: React

# 목차
toc_label: tanstack query로 api 사용하기(client component)
toc: false
toc_sticky: false
---

<br/>
Next.js에서 Server Components를 제공하게 되면서 지금까지 사용했던 `tanstack query`에 의문이 생겼다. Server Components에서 `tanstack query`를 적절하게 사용하는 방법을 학습하기 전에, 기존에 Client Components에서는 어떻게 사용되었는지 되짚어보자.

## 1. tanstack query를 사용하기 위한 QueryClientProvider 설정

### 1-1. page router에서의 사용 방법

Next.js의 page router 방식을 사용했을 때에는 `_document.tsx` 혹은 `_app.tsx`에 `QueryClientProvider`를 감싸주고 queryClient를 넣어주면 사용할 수 있었다.

<script src="https://gist.github.com/TaeSuPark/43489592ddc04195ce30f0b0fcb7db4f.js"></script>

### 1-2. app router에서의 사용 방법

app router 환경에서는 Root layout에 해당 Provider를 감싸주는 방식으로 구현된다.

> root layout에서 'use client'를 사용한다면?

이 방식은 Next.js에서 server component를 적절히 사용하기 위해서는 권장되지 않는다. 그렇기 때문에 별도의 registry를 만들어서 layout으로 import하는 방식을 추천한다. <br/>(CSS-in-JS의 Provider도 이와 같은 방식으로 사용한다.)

[참고 링크](https://nextjs.org/docs/app/building-your-application/styling/css-in-js#styled-components)

<script src="https://gist.github.com/TaeSuPark/abb80f519b76326405905ee9ba6a8e37.js"></script>

<script src="https://gist.github.com/TaeSuPark/4f3c94834fe8248faf9770b110680d0b.js"></script>

## 2. api와 useQuery

### 2-1. api 작성

본격적으로 `useQuery`를 사용하기 앞서, 간단한 api를 만들어보자.
해당 api의 출처는 [여기](https://thecatapi.com/)<br/>

<script src="https://gist.github.com/TaeSuPark/e1401dd8d9f50ce42e15bb36797dc9cc.js"></script>

### 2-2. useQuery로 데이터 가져오기

이제 `useQuery`를 통해 데이터를 가져온다. `page.tsx`가 server component이므로 아쉽지만 당장은 `'use client'`를 추가로 작성해준다.

<script src="https://gist.github.com/TaeSuPark/c9a38f9064fb6f6249d38e779c267ee3.js"></script>

<br/>
중점적으로 봐야 할 코드만 따로 잘라 확인해보자.

```tsx
...
const { data, isLoading } = useQuery({
  queryKey: ["catImg"], // 해당 api를 식별하는 키
  queryFn: getCatImg, // 만들어놓은 api 함수
})

// data - api가 실행되고 나서 반환되는 값 (실행 완료 전 undefined)
// isLoading - api가 실행중일 때 true를 반환하는 boolean 값
...
```

`useQuery`는 컴포넌트가 렌더될 때 실행된다. 따라서 별도의 함수를 통해 api를 실행하는 `useMutate`와는 차이가 있다.

쿼리 키를 통해서 해당 api를 식별하게 되며 내부적으로 데이터를 캐싱하고 관리한다. 쿼리 키에 상태값이 들어간 경우 해당 상태값이 변함에 따라 api를 다시 실행할 수 있다.

```tsx
...
// 쿼리의 캐시와 상호작용하는 객체(Providers에서 넣어주었다)
const queryClient = useQueryClient()

...
const invaildateCatImg = () => {
    // 해당 쿼리의 키 값을 통해 식별하고 invalidate시킨다.(api의 재실행)
    queryClient.invalidateQueries({ queryKey: ["catImg"] })
  }
...
```

쿼리 키를 통해 식별하여 해당 api를 강제로 invalidate시켜 다시 호출될 수 있도록 하는 코드를 작성했다.
이 함수는 button의 onclick에서 사용되어 버튼을 누르면 api를 다시 불러오는 기능을 한다.

### 정리

간단하게 `useQuery`를 사용해 client component에서 api를 호출하는 방법을 알아보았다. useQuery는 이 외에도 select, staleTime 등의 api와 관련된 다양한 기능들을 제공한다.

다음엔 `useMutate`의 사용법을 간략히 알아보고 본격적으로 Server Components에서의 동작에 대해 알아봐야겠다.
