# 이벤트 Capturing, Propagation, Bubbling and Once

<img src="https://user-images.githubusercontent.com/56066290/190587808-433ecea8-88f5-43da-94ce-0017dd8f1fe5.png" width="200">
<img src="https://user-images.githubusercontent.com/56066290/190588369-2165a4f7-a046-4dbb-974f-92871b162f81.png" width="200">

위 같은 중첩된 div 구조가 있다.

<br/>

## 버블링

- 한 요소에 이벤트가 발생하면, 이 요소에 할당된 핸들러가 동작하고, 이어서 부모요소들의 핸들러가 동작하는 현상.
- 가장 최상단의 조상요소, `document`를 만날 때까지 이 과정이 반복된다!

예를 들어서, **`three`에 클릭 이벤트를 발생시키면** `three` -> `two` -> `one` 순서로 요소의 클릭 이벤트 핸들러가 동작하게 된다.

그럼 여기서 각 동작에 대해서 `e.target`과 `e.currentTarget`를 콘솔로 찍어봤을 때,
<img src="https://user-images.githubusercontent.com/56066290/190588917-cd9ed617-2c57-4a06-85e6-c1184d8b70fc.png" width="200">
로 찍혔다. 그래서 이제 두 대상 객체가 어떤 것을 가리키는지 명확하게 이해가 됐다.

- `e.target` : **실제 이벤트를 동작한, 시작한** '타깃'요소! 그렇기 때문에 버블링이 진행되는 동안에도 변하지 않는다.
- `e.currentTarget` : **현재 이벤트가 동작되고 있는** 요소! 즉 this와 같다.

<br/>

## 캡쳐링

- 버블링은 이벤트가 상위 요소로 전파하는 단계라면, 캡쳐링은 버블링 전에 이벤트가 하위 요소로 전파되는 단계이다.
- 그전에 표준 DOM 이벤트에서 정의한 이벤트 흐름 3가지를 먼저 공부하자.

1. 캡쳐링 단계
2. 타겟 단계
3. 버블링 단계

<img src="https://user-images.githubusercontent.com/56066290/190592863-2232d569-51c9-42f6-b1ef-3a8edb144bd2.png" width="300">

`<td>`를 클릭하면,

1. 이벤트가 최상위 조상에서 먼저 시작해 아래로 전파된다 (캡쳐링)
2. 이벤트가 타깃 요소에 도착해 실행된 후 (타깃단계)
3. 다시 최상위 조상으로 위로 전파된다 (버블링단계)

아까와 같이 예를 들어서, **`three`에 클릭 이벤트를 발생시키면** `one` -> `two` -> `three` 순서로 요소의 클릭 이벤트 핸들러가 동작하게 되는 것이다.

<br/>

핸들러를 어느 단계에서 동작하게 할지는 `capture` 옵션으로 조절할 수 있다.

```js
divs.forEach((div) =>
  div.addEventListener("click", logText, { capture: true | false })
);
```

- `false`: 디폴트, 버블링 단계서 동작
- `true` : 캡쳐링 단계서 동작

<br/>

## E.stopPropagation ?

- 말 그대로, 버블링/캡쳐링 단계에서 더 이상 이벤트의 전파를 중지한다는 메서드이다.

**`three`에 클릭 이벤트를 발생시켰을 때, `e.stopPropagation` 이 있다면**

- 버블링 단계에선, `three` 요소 이벤트 핸들러만 동작
- 캡쳐링 단계에선, `one` 요소 이벤트 핸들러만 동작

<br />

## addEventListener의 3번째 옵션 객체 ?

```js
element.addEventListener("click", doSomething, {
  capture: true | false,
  once: true | false,
  passive: true | false,
});
```

- once : true면 해당 요소의 이벤트가 딱 한번만 실행된다!
  클릭 후에 `element.removeEventListener("click", doSomething)`을 하는 것과 같다!
  이 옵션은 알아두면 나중에 쓰일 곳이 많아보여서 흥미로웠다! 버튼을 더이상 클릭하지 않기를 바라는 가게 체크아웃 버튼이나, 한번만 실행해야 하는 복잡한 기술을 사용해야 되는 상황에서 유용할 듯 싶다

<br/>

## 배운 점

사실 이벤트 캡쳐링이나 버블링의 개념을 어렴풋하게는 알고 있었다. 이론 강의시간이나 이전 프로젝트에서 봤던 개념이었기 때문이다. 하지만 이렇게 짧은 강의와 실습을 하면서 내 방식으로 정리를 하다보니 어렴풋했던 개념이 조금이라도 선명해진 것 같아졌다. 뭔가 더 친해진 느낌? 다음에 프로젝트를 진행하면서 비슷한 개념을 사용해야 할 때 기분좋게 아는 척 정도 할 수 있을 정도? ㅎㅎ..

표준 DOM 이벤트가 정의한 이벤트 흐름 단계도 배우게 됐는데 나중에 모던 JS 책 이벤트 챕터에서 만나면 또 반갑게 읽을 수 있을 것 같다.
