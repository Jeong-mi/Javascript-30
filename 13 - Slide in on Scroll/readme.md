# Slide in on Scroll

![slide](https://user-images.githubusercontent.com/56066290/185592914-6fdacb97-79b7-422b-a09e-6ed7b5f16722.gif)  
 
<br />  

## 전체적인 설명을 그림으로 표현

![image](https://user-images.githubusercontent.com/56066290/185601195-e75bb926-a18b-4eec-8f52-3a4db5452738.png)

1. debouncing
2. window event   
<br />

## 디바운싱?

- 연이어 호출되는 함수들 중 마지막 함수(또는 제일 처음)만 호출되도록 하는 것
- 동일한 작업 처리 요청이 n번 발생했을 때 일을 단 한 번만 수행하겠다는 것   

<br />

## 현재 화면의 스크롤 정보를 가져오는 방법

```js
//화면의 Y축의 상단값
// 스크롤했을 때 현재 뷰포트 위쪽 모서리의 Y좌표
window.scrollY;

// 현재 보이는 창의 내부 높이
window.innerHeight;

//화면의 Y축의 하단값
window.scrollY + window.innerHeight;
```

![image](https://user-images.githubusercontent.com/56066290/185589967-64d4d31e-31cf-4ece-8f0c-666c59d989d7.png)

<br />

## 요소.offsetTop, 요소.offsetParent
![image](https://user-images.githubusercontent.com/56066290/185597718-261d790e-1a82-4fdd-9aa5-295de8e903e0.png)

`slideImage.offsetParent` : 해당 요소를 렌더링할 때, 좌표 계산에 사용되는 가장 가까운 조상요소의 참조를 반환함.

`slideImage.offsetTop` : offsetParent를 기준으로 아래쪽으로 얼마나 떨어져있는지를 나타냄
<br />

![image](https://user-images.githubusercontent.com/56066290/185590411-1fe7938c-b86f-4014-9d87-c648a0b3e31a.png)
