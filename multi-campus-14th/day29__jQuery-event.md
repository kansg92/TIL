# 📢day29__jQuery Events



## jQuery



### jQuery for-each문

- index : n번째 
- item : 배열

```javascript
	$(d).each(function(index,item){		
	});
	
```



### jQuery Event



| Method                                                       | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `click()`                                                    | 클릭 이벤트 처리                                             |
| `dblclick()`                                                 | 더불 클릭 이벤트 처리                                        |
| `mouseenter()`                                               | 마우스가 해당 element 안으로 이동 했을 때 이벤트 처리        |
| `mouseleave()`                                               | 마우스가 해당 element 밖으로 이동 했을 때 이벤트 처리        |
| `mousedown()`                                                | 마우스가 해당 element 에서 클릭 했을 때 이벤트 처리          |
| `mouseup()`                                                  | 마우스가 해당 element 에서 클릭을 햐제 했을 때 이벤트 처리   |
| `hover()`                                                    | 마우스가 해당 element 에 들어가고 나갈 때 각각 이벤트 처리   |
| `focus()` and ` blur()`                                      | Form tag에서 포커스가 들어가고 나갈 때 가각 이벤트 처리      |
| `keyup()`                                                    | input field                                                  |
| `hide()`                                                     | 해당 Element를 없어 지게 한다. 해당 영역도 사라진다.         |
| `show()`                                                     | 해당 Element를 다시 나타나게 한다                            |
| `toggle()`                                                   | 한번 클릭 시 없어 지고 두 번 클릭 시 나타나게 한다.          |
| `fadeIn()`                                                   | 해당 Element를 서서히 없어 지게 한다. 해당 영역도 사라진다.  |
| `fadeOut()`                                                  | 해당 Element를 서서히 다시 나타나게 한다.                    |
| `fadeToggle()`                                               | 한번 클릭 시 없어 지고 두 번 클릭 시 나타나게 한다.          |
| `slideDown()`                                                | 해당 Element를 서서히 하단으로 펼쳐 지게 한다.               |
| `slideUp()`                                                  | 해당 Element를 서서히 위로 닫아 준다.                        |
| `slideToggle()`                                              | 한번 클릭 시 내려가고 두 번 클릭 시 위로 올라간다.           |
| **HTML GET/SET**                                             |                                                              |
| `text()`                                                     | 해당 Element의 content를 스트링으로 받아 온다.               |
| `html()`                                                     | 해당 Element의 content를 HTML 스트링으로 받아 온다.          |
| `val()`                                                      | Form에서 입력 된 값을 받아 온다.                             |
| `attr()`                                                     | 해당 Element의 속성 값을 가지고 온다.                        |
| `$(‘#id’).text(‘test’)`                                      | 특정 Element 영역에 특정 스트링 값을 셋팅 한다.              |
| `$(‘#id’).html(‘<p>test</p>’)`                               | 특정 Element 영역에 특정 HTML 값을 셋팅 한다.                |
| `$(‘#id’).val(‘test’)`                                       | 특정 Form 영역에 값을 셋팅 한다.                             |
| `$(‘#id’).attr(‘href’,’www.jquery.com’)`                     | 특정 Element의 속성 값을 셋팅 할 수 있다.                    |
| `append()`                                                   | Element 영역의 가장 뒷 부분에 HTML을 추가 할 수 있다.        |
| `prepend()`                                                  | Element 영역의 가장 앞 부분에 HTML을 추가 할 수 있다.        |
| `after()`                                                    | 특정 Element의 앞에 HTML를 추가 한다.                        |
| `before()`                                                   | 특정 Element의 뒤에 HTML를 추가 한다.                        |
| `remove()`                                                   | 선택 한 Element 영역을 삭제 한다. 영역까지 사라진다.         |
| `empty()`                                                    | 선택 한 Element의 내부 정보만 삭제 한다. 영역은 유지 한다.   |
| **Get and Set CSS Classes**                                  |                                                              |
| `addClass()`                                                 | 특정 Element에 선언된 class를 삽입 할 수 있다.               |
| `removeClass()`                                              | 특정 Element에 선언된 class를 제거 할 수 있다.               |
| `toggleClass()`                                              | 한번 클릭 시 class 적용 두번 클릭 시 class 제거.             |
| `$(‘#p’)css(‘color’)`                                        | 특정 영역의 Element 에 적용 된 css 값을 받아 온다.           |
| `$(‘#p’)css(‘color’, ’black’)`                               | 특정 영역의 Element의 CSS를 셋팅 할 수 있다.                 |
| `$("p").css(<br/>{<br/>"background-color": "yellow",<br/>"font-size": "200%“<br/>}<br/>);` | 특정 영역의 Element의 CSS속성을 동시 에 여러 개 셋팅 할 수 있다. |
| **Traversing Filtering**                                     |                                                              |
| `$(‘td’).first()`                                            | td들 중에 첫 번째 td를 선택                                  |
| `$(‘td’).last()`                                             | td들 중에 마지막 td를 선택                                   |
| `$(‘td’).eq(0)`                                              | td들 중에 특정 위치에 있는 td를 선택(0번부터 시작)           |
| `$(‘td’). filter(".intro")`                                  | td들 중에 특정 속성의 td만을 선택                            |
| `$(‘td’).not($(‘td’).eq(2))`                                 | td들 중에 선택 한 td를 제외하고 나머지 모두를 선택           |

hide
