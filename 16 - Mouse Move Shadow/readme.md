# CSS Text Shadow Mouse Move Effect

<img src="https://user-images.githubusercontent.com/56066290/189621504-274cddde-0aeb-4537-b17b-f01df2680890.gif" width="" height="250" />

## text-shadow ?

offset-x | offset-y | blur-radius | color
`text-shadow: 1px 1px 2px black;`

<br/>

## 코드 해석!

- `offsetX`와 `offsetY`는 좌표계산에 가장 가까운 조상요소를 기준으로 얼마나 떨어져있는지 계산함.
- 조상 요소는 `body`가 될 수 있고, `hero` 클래스를 가지는 `div` 태그가 될 수 있다.

```js
hero.addEventListener("mousemove", shadow);

function shadow(e) {
  console.log(this, e.target);
}
```

- `this`는 항상 `hero` 클래스를 가지는 `div` 태그를 가리키지만,
- `e.target`은 마우스를 움직이면서
  <img src="https://user-images.githubusercontent.com/56066290/189603922-b31506ae-d71f-4cc5-8c60-604c0c180e4f.png" width="100" height="100" />
  일 땐
  <img src="https://user-images.githubusercontent.com/56066290/189603719-c38a29c0-9c07-4d17-a034-56897213b86d.png" width="400" height="80" />
  이고,

  <img src="https://user-images.githubusercontent.com/56066290/189603974-43b76137-a248-4dc1-940a-2f44fc062c17.png" width="100" height="50" />
  일 땐
  <img src="https://user-images.githubusercontent.com/56066290/189603778-20303789-b08a-4562-a153-6546524ffe79.png" width="400" height="80" />
  으로 확인된다.

그래서

- 마우스가 `hero` 영역 안에 있는 경우,
- x, y에 각각 `e.target.offsetLeft`와 `e.target.offsetTop`을 더해주면,
- 마우스가 `hero`안에 있더라도 `body`를 조상요소를 했을 경우의 좌표값으로 계산해 낼 수 있다.

<br/>

## 새로 알게 된 `contentEditable` 속성!

- 거의 모든 html 요소에 속성을 추가하여 텍스트 편집기를 만들 수 있다!
- `input`이나 `textarea` 로 수정할 필요없이 간단하게 `contentEditable=true` 속성만 추가해줘도 편집 모드로 변경할 수 있다.
- 그렇기 때문에, `div`를 `input`으로 바꿨을 때 발생하는 스타일 변경을 신경쓰지 않아도 돼서 편리할 수 있다!
