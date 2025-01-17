---
published: true
title: "스터디 2주차 - React 기본 hook 알아보기"
excerpt: "React/Next.js 스터디 2주차 기록"
categories: study
tags: React

# 목차
toc_label: React 기본 hook 알아보기
toc: false
toc_sticky: false
---

<br/>
React 환경에서 가장 많이 쓰이는 hook에 대해서 짚고 넘어가기로 했다.
- useState
- useEffect
- useMemo

## 1. useState

useState에 대해서 간략하게 알아보자.

```tsx
const [state, setState] = useState<타입>(초기값)
```

React는 상태의 변화에 따라서 렌더링이 이루어지기 때문에 이러한 상태를 정의하고 관리하기 위해 `useState`를 사용한다.
<br/><br/> 간단하게 얘기하면 흔히 개발할 때 사용하는 변수 개념으로 사용하는 훅이라고 생각하자.

#### 작성 예시

```tsx
const [num, setNum] = useState<number>(0)
// 0으로 초기값을 가진 num이라는 숫자 타입의 상태를 정의한다.
// num의 값을 변경하기 위해서는 setNum(값)을 사용한다.

// 신규 타입 정의
type ObjectType = {
  key: number
  value: string
}

const [data, setData] = useState<ObjectType>()
// 정의한 ObjectType이라는 타입의 상태인 data를 정의한다.
// 초기값 영역을 비워두면 undefined로 정해진다.
```

## 2. useEffect

useEffect에 대해서 간략하게 알아보자.

```tsx
useEffect(() => {
  return () => {}
}, [의존성])
```

`useEffect`는 두 개의 인수를 받는다. 첫 번째로는 콜백 함수, 두 번째로는 의존성 배열이다.<br/><br/>

간단하게 요약하면, `의존성에 포함된 상태값이 변할 때마다 콜백함수를 실행한다` 고 할 수 있지만, 사용하는 방식에 따라 다르게 동작하기 때문에 몇 가지 사용 방법을 살펴보자.

### 2-1 의존성 배열이 비어있는 경우

```tsx
useEffect(() => {
  console.log("실행")
}, [])
```

의존성 배열이 비어있다면, `useEffect`가 받은 콜백 함수는 컴포넌트가 마운트될 때 한 번 실행된다.

### 2-1 의존성 배열에 상태값이 있는 경우

```tsx
useEffect(() => {
  console.log("실행")
}, [state])
```

의존성 배열에 상태가 있다면, `useEffect`가 받은 콜백 함수는 컴포넌트가 마운트될 때 한 번, 그리고 상태값이 바뀔 때마다 실행된다.

### 2-2 콜백 함수의 return으로 함수가 올 경우

```tsx
useEffect(() => {
  console.log("실행")
  window.addEventListener("click", () => {})
  return () => {
    console.log("unmount")
    window.removeEventListener("click", () => {})
  }
}, [])
```

`useEffect`가 받은 콜백 함수가 함수를 return 하는 형태라면, 이 함수는 클린업 함수라고 볼 수 있으며 컴포넌트가 언마운트될 때 실행된다.<br/>(일반적으로 이벤트를 등록하고 지울 때 사용)

## 3. useMemo

useMemo에 대해서 간략하게 알아보자.

```tsx
const memoState = useMemo(() => {
  return 값
}, [의존성])
```

`useMemo`는 특정 연산 결과나 상태를 의존성 배열에 따라 반환하는 훅이다.
<br/>
`useEffect`와 같이 두 개의 인자를 받으며, 첫 번째 인자로는 return 값을 가진 함수,<br/> 두 번째 인자로는 의존성 배열을 받는다.

#### 작성 예시

```tsx
const [num, setNum] = useState<number>(10)

const addedNum = useMemo(() => {
  return num + 5
}, [num])
// num의 값이 setNum을 통해 바뀔 때마다 addedNum의 값도 변경된다.
// 이 경우, addedNum은 num보다 항상 5가 큰 값을 가진다.
```

### 정리

React를 통해서 화면 개발을 진행할 때 가장 많이 쓰이는 세 가지 훅에 대해서 살펴봤다. 이 외에도 `useCallback`, `useContext`, `useRef`, `useReducer` 등의 훅이 있으며 해당 훅들은 개발 진행하면서 추후에 짚어보기로 했다.
