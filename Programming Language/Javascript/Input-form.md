## [입력 양식: 버튼]

<br/>

### _버튼_

<br/>

> 클릭 이벤트

- button
- input type="button" <br/>
  (cf. input:button)

<br/>

> submit 이벤트

- form => input type="submit" <br/>
  (cf. input:submit)
- form 태그에 이벤트 연결 (input 태그로 연결 X)
- form 태그 안에 button 태그 있으면 input submit 과 동일하게 작동 <br/>
  => form 태그 안에 input type으로 button 지정 (submit 이벤트 발생 X)

#

## [입력 양식: 글자 입력]

<br/>

### _글자 입력_

<br/>

> input type="text" (한 줄 입력) <br/>
> textarea 태그 (여러 줄 입력) <br/>

- value 속성으로 값 추출
- change event, keydown/keyup/keypress event
- key event 발생 순서: keydown -> keypress -> 입력 양식에 값 들어감 -> keyup
- change event: 해당 input 태그 전체에 값 입력 마쳤을 때

> p 태그에 contenteditable="true" 속성과 값 지정 (글자 직접 수정 가능) <br/>

#

### [참고]

- input type을 JS에서 가져올 시, document.querySelector('input[type=button]');

#

### [레퍼런스]

[Reference1](https://www.youtube.com/watch?v=n2EBSjdIAzo&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=46)
[Reference2](https://www.youtube.com/watch?v=xXeDA06E0EA&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=47)
