---
published: true
title: "React 개발에서 많이 쓰는 javascript 구문 정리"
excerpt: "개발하면서 자주 마주치게 되는 친구들"
categories: programming
tags: React

# 목차
toc_label: React 개발에서 많이 쓰는 javascript 구문 정리
toc: false
toc_sticky: false
---

<br/>
React 환경에서 프론트엔드 개발을 하면서 많이 마주치는 js/ts 구문을 정리해보자.

## 1. map

```javascript
let data = [1, 2, 3, 4, 5]
let map1 = data.map((v) => v + 2) // [3, 4, 5, 6, 7]
let map2 = data.map((v, index) => index) // [0, 1, 2, 3, 4]
```

배열로 되어있는 데이터를 map을 통해서 작성한 반환값에 따른 새로운 배열로 반환하는 구문이다.

구조를 상세하게 살펴보면, `배열.map(화살표 함수)` 인 것을 알 수 있고 화살표 함수의 인자로는 데이터와 index 값을 받아올 수 있다.

해당 구문을 통해 새로운 데이터가 만들어져도 원본 데이터는 변하지 않는다.

<br/>
React 컴포넌트와도 자주 사용되는데, 데이터만 변하고 형태는 같은 컴포넌트가 반복될 경우 다음과 같은 형태로 사용할 수 있다.

```jsx
// jsx, tsx 에서의 사용
return (
  <Container>
    {listData.map((v, idx) => (
      <Card key={v.key} data={v} />
    ))}
  </Container>
)
```

[참고 Link](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

## 2. filter

```javascript
let data = [1, 2, 3, 4, 5]
let filter1 = data.filter((v) => v > 2) // [3, 4, 5]
let filter2 = data.filter((v, index) => index > 2) // [3, 4]
```

배열을 돌면서 filter 내의 조건을 만족하는 데이터만을 걸러서 새로운 배열로 반환하는 구문이다.

`map`과 마찬가지로 `배열.filter(화살표 함수)` 형태이며 역시 index를 지원한다.

화살표 함수의 반환값은 `boolean`이어야 한다.

해당 구문을 통해 새로운 데이터가 만들어져도 원본 데이터는 변하지 않는다.

[참고 Link](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

## 3. reduce

```javascript
let data = [1, 2, 3, 4, 5]
let reduce1 = data.reduce((acc, cur) => acc + cur, 0)
// 0(시작값) + 1 + 2 + 3 + 4 + 5의 결과인 15
```

시작값부터 시작해서, 이전까지의 연산값과 현재 값을 통해 반복적인 연산을 실행하고 그 결과를 반환한다.

`배열.reduce((누적값, 현재값) => 실행되는 연산과 반환값, 시작값)`으로 되어있고 반환하는 값은 연산의 최종 결과값이다.

[참고 Link](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)

## 정리

react랑 js/ts 환경에서 개발을 하다보면 가장 많이 사용하고 마주치게 된다고 생각되는 3가지를 간단하게 정리해봤다. 

이 외에도 split, join 등 데이터를 파싱해서 나타내거나 가공할 때 많이 쓰는 구문들이 있는데 

MDN Web Docs에 설명이 굉장히 잘 되어있어서 많은 도움이 되었다.
