## dev tool 콘솔창에 표현할 수 있는 trick 10 가지

#

![image](https://user-images.githubusercontent.com/56066290/183107664-a99249fe-1f69-477f-a9d0-8c472488141f.png)

```
// Regular
console.log("Hello");

// Interpolated
console.log("Hello I am a %s string!", "💩");

// Styled
console.log(
  "%c I am some great text",
  "font-size: 30px; background: aqua; text-shadow: 10px 10px 0 gray"
);

// warning!
console.warn("Oh NOO");

// Error :|
console.error("Shit!!");

// Info
console.info("Crocodiles eat 3-4 people per year");
```

#

- 첫번째 파라미터의 평가가 옳다면 아무것도 표시되지 않고, 옳지 않다면 두번째 파라미터가 error로 출력됨

![image](https://user-images.githubusercontent.com/56066290/183107956-0e5a4a19-550c-4a1a-a0b2-6ba5465b6f03.png)

```
// Testing
const p = document.querySelector("p");
console.assert(p.classList.contains("ouch"), "That is wrong!");
```

#

- console.log는 HTML과 같은 트리 구조로 출력
  - DOM 요소에 대해 특별한 처리를 제공
- console.dir은 JSON과 같은 트리 구조로 출력
  - 종종 DOM JS 객체의 전체 표현을 보려고 할 때 유용
    ![image](https://user-images.githubusercontent.com/56066290/183108858-42270158-9034-433a-a069-c85521a8d661.png)

```
// Viewing DOM Elements
console.log(p);
console.dir(p);
```

#

![image](https://user-images.githubusercontent.com/56066290/183109591-6034fcbc-e04b-4db3-bb13-0a18943aaa79.png)

```
// Grouping together
dogs.forEach((dog) => {
  console.groupCollapsed(`${dog.name}`);
  console.log(`This is ${dog.name}`);
  console.log(`${dog.name} is ${dog.age} years old`);
  console.log(`${dog.name} is ${dog.age * 7} years old`);
  console.groupEnd(`${dog.name}`);
});
```

#

- time: 해당 요청의 타이머를 재서 처리 시간을 쉽게 확인하는 데 유용
- table: 객체로 구성된 배열을 한눈에 보기 쉬워짐

![image](https://user-images.githubusercontent.com/56066290/183109739-396d9e6a-6376-4c3c-9d06-ce5cec82452b.png)

```
// timing
console.time("fetching data");
fetch("https://api.github.com/users/wesbos")
  .then((data) => data.json())
  .then((data) => {
    console.timeEnd("fetching data");
    console.log(data);
  });


//table
console.table(dogs);
```
