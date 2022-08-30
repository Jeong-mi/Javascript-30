# Key Sequence Detection

![image](https://user-images.githubusercontent.com/56066290/187349237-a9eb06fa-55df-42c4-885f-b67a94c18b30.png)

- 키보드 이벤트를 활용한 프로젝트!  
  <br/>

1. 알파벳이나 키보드를 눌렀을 때 이벤트를 pressed 리스트에 추가

```js
window.addEventListener("keyup", (e) => {
  pressed.push(e.key);
});
```

2. `splice` 메서드를 사용해서 secretCode 길이로 고정되도록 pressed 배열을 자른다

```js
pressed.splice(-secretCode.length - 1, pressed.length - secretCode.length);
```

3. pressed 배열에 secretCode 문자열이 있다면 유니콘 띄워주기~!

```js
if (pressed.join("").includes(secretCode)) {
  console.log("DING DING~!");
  cornify_add();
}
```

<br/>

### splice 배열 메서드

`splice(start[,deleteCount[,item1[,item2...]]])`

- start : 배열의 변경을 시작할 인덱스

  - **음수**인 경우 : 배열의 **끝에서부터** 요소를 센다
  - **배열의 길이보다 큰 수**인 경우 : 실제 시작 인덱스는 배열의 길이로 설정
  - **절대값이 배열의 길이보다 큰 경우** : 0으로 세팅

- deleteCount : 배열에서 제거할 요소의 수

  - **0이거나 음수**인 경우 : 어떤 요소도 제거하지 않음
  - **생략** 이거나 **값이 배열의 길이-start보다 큰경우** : start부터 모든 요소 제거

<br/>

### 코드 설명

```js
const secretCode = "developer"; // 길이: 9

pressed.splice(-secretCode.length - 1, pressed.length - secretCode.length);
```

1. `pressed = ["a", "b", "c"]`

- start: 절대값이 배열의 길이보다 큰 경우 -> 0으로 세팅
- deleteCount: 음수인 경우 -> 어떤 요소도 제거하지 않음

2. `pressed = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j']`

- start: 음수인 경우 -> 배열의 끝에서부터 시작
- deleteCount: 값이 배열의 길이-start보다 큰경우 -> start부터 모든 요소 제거
