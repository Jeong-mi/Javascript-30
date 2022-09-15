# Click and Drag to Scroll (드래그해서 옆으로 스크롤되게 하기)

<img src="https://user-images.githubusercontent.com/56066290/190089627-e4ed33e8-3551-48cb-af4b-870687f45804.gif" width="250" height="">

<br/>

## 코드 해석

1. 클릭했을 때 앵커의 시작점 `startX`는 `e.pageX - slider.offsetLeft;`로 구할 수 있다

- slider가 margin값을 가지고 있다면 `pageX`로만 가지고 현재 앵커값을 구하면 안된다
- 앵커의 기준은 slider이기 때문에, 전체 페이지 기준인 `pageX`에서 slider가 마진값을 가지고 있을 경우에 대비해서 `slider.offsetLeft`를 빼주어야 시작점을 구할 수 있다.
- 마진값이 없다면 `slider.offsetLeft`는 0이 될 것이다

- **생각해 본 다른 코드!** : `각 아이템.offsetX`

```html
<div class="items">
  <div class="item item1">01</div>
  <div class="item item2">02</div>
  ...
  <div class="item item25">25</div>
</div>
```

- 일 때, 각각의 `item1` `item2` `item3` 의 offsetX를 구해도 똑같은 `startX`값을 구할 수 있을 것 같다!
- 다만, 현재 클릭한 아이템이 어떤 아이템인지 알아야 하는 게 복잡해 보인다.

<br/>

2. `slider.scrollLeft`

- 사실 `scrollLeft`는 생소했다! 이번 공부로 알게 된 속성이다!
- 수직 스크롤 바의 위치를 알기 위해선 `element.scrollTop`을, 수평 스크롤 바의 위치를 알기 위해선 `element.scrollLeft`르 사용하면 된다.

<br/>

3. `mousemove`이벤트에서 `e.preventDefault`를 함으로써 !

- 안에 있는 텍스트를 선택하거나 왼쪽으로 미끄러지는 것 또는 브라우저가 실제로 어떤 텍스트를 선택하려고 한다고 생각할 수 있는 다른 이상한 것들을 막을 수 있게 된다.
- `e.preventDefault`는 예로 `onSubmit`시의 새로고침을 중단시키는 것과 같이, **브라우저 고유의 동작을 중단시키는 역할**을 하기 때문이다.

<br/>

4. `mousemove`이벤트에서 `slider.scrollLeft = scrollLeft - walk;`하기

```js
const x = e.pageX - slider.offsetLeft;
const walk = (x - startX) * 3;
slider.scrollLeft = scrollLeft - walk;
```

- `startX`: 마우스를 클릭한 지점의 시작점
- `walk` : 클릭한 지점부터 왼쪽 또는 오른쪽 방향으로 얼마나 move했는지 알 수 있음
  - 음수라면 왼쪽, 양수라면 오른쪽으로 이동한 것임
- `scrollLeft` : 마우스를 클릭한 지점의 스크롤 바의 위치
- 그래서 `scrollLeft`에서 `walk`를 빼준 값이 바뀐 스크롤 바의 위치가 되는 것이다!

<br/>

## 새롭게 공부한 내용

- `element.scrollTop` : 수직 스크롤바의 현재 위치   
<img src="https://user-images.githubusercontent.com/56066290/190090569-d9264e86-22c5-4623-8834-13b370b3ea82.png" width="200" height="">

- `element.scrollLeft` : 수평 스크롤바의 현재 위치   
<img src="https://user-images.githubusercontent.com/56066290/190090646-91d4a945-cee0-4696-8481-1eb38ed16e2f.png" width="200" height="">
