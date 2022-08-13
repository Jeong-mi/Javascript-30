# HTML5 video player 커스텀하기

```js
function togglePlay() {
  // pause된 상태라면 play하고, 아니라면 pause해라
  const method = video.paused ? "play" : "pause";
  video[method]();
}
```

`video.paused`를 `this.paused`로 바꾸면  
아래의 `toggle.addEventListener("click", togglePlay);` 때문에 토글버튼은 작동하지 않는다!!

---

```js
<button data-hello="5" data-skip="-10" class="player__button">
  « 10s
</button>
```

- data-*에서 *은 아무거나 내가 넣고 싶은 문자로 넣어줄 수 있는 것이다.
- 사용할 때는

```js
button.addEventListener("click", skip);
console.log(this.dataset.hello);
video.currentTime += parseFloat(this.dataset.skip);
```

처럼 `this.dataset.*`로 사용하면 된다!!

---

![image](https://user-images.githubusercontent.com/56066290/184465837-d268788e-4fe7-4015-8a9e-72176ffc9240.png)

- progressbar의 길이(width)가 flexBasis, 즉 현재 재생 구간!
  `progressBar.style.flexBasis = `${percent}%`;`

---

![image](https://user-images.githubusercontent.com/56066290/184466032-dc1f6cec-8f0a-44b8-b40b-2b62e58ab472.png)

```js
video.addEventListener("timeupdate", handleProgress);
```

- `timeupdate` 이벤트는 HTMLMediaElement이다.
- `currentTime` 속성이 변경되었을 때 이벤트가 동작한다!
- 예를 들어, skip 버튼을 눌렀을 때나 재생중일 때
- `progress` 이벤트도 비슷하게 동작을 한다 동작한다
  ***
- 막대바의 range 조절할 때는 event로 *change*와 *mousemove*를 사용하자!
  ***
- video 속성의 `duration`은 해당 비디오의 총 재생시간을 말한다.
  mdn참고: https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement

  ***

- offsetX : 이벤트가 걸려있는 DOM 객체를 기준으로 좌표를 출력
- clientX: 브라우저가 기준인 좌표. 스크롤은 무시하고 해당 페이지의 상단을 0으로 측정
- screen : 전체 모니터 스크린이 기준인 절대 좌표. 브라우저를 움직여도 값은 같다.
- page : 문서가 기준. 스크롤 화면을 포함해서 측정.
