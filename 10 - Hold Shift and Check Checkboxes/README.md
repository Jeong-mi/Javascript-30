# shift 키를 이용해서 여러 개의 checkbox 체크하기

- firstChecked: shift키로 누르기 전 첫번째 체크박스
- inBetween: 처음 체크박스와 마지막 체크박스 사이의 것들을 구분하기 위한 flag

1. shift키를 누르고 마지막 체크박스를 눌렀을 때 if문으로 들어간다
2. 각 싱글 checkbox를 forEach문으로 돌게 된다.  
   `checkbox === this` : 마지막 체크박스  
   `checkbox === firstChecked` : 첫번째 체크박스

> - inBetween이 true일 때만 해당 체크박스를 checked로 바꿔준다.
> - 마지막 체크박스일 때 다시 inBetween을 false로 해줌으로써 체크를 멈춘다.

=> 구글 메일이나 어떤 상황에서 shift 키로 여러개를 선택해야 할 상황에서 유용하게 쓰일 스킬!
