# 📢day30__Ajax

## 웹에서 비동기 방식

- 웹에서 특정부분만 데이터를 뿌려서 화면은 그대로 있고, 특정영역에만 데이터가 게속해서 수정되는 형식을 말한다.
- 웹서버에서 데이터를 받아와서 특정 영역의 데이터만 바꾸어야 하기 때문에 통신이 필요하다.



## AJAX

### AJAX란??

- AJAX(Asynchronous JavaScript and XML)는 비동기 통신을 지원 하는 방식이며, 라이브러리형태로 존재한다.
  - 2005년 2월 18일 미국 adaptivepath라는 회사의 웹 사이트에 에세이 하나가 올라 왔다. 제목은 "Ajax : A new Approach to web Applications"이고 작성자는 Jesse James Garrett이다. 여기서 AJAX는 시작 되었다.
- AJAX는 새로운 언어가 아닌 JavaScript에 추가된 통신 방식이다.
- 화면 전체를 재로드 하지 않고도 서버에서 특정 데이터를 송수신 할 수 있다.
- Ajax는 빠르고 동적인 웹 페이지를 만들기위한 기술이다.
- AJAX는 웹 페이지가 서버와 데이터를 교환하여 비동기 적으로 업데이트 할 수 있다. 이는 전체 페이지를 재로드 하지 않고, 웹 페이지의 일부를 갱신 할 수 있다는 것을 의미한다.



### JavaScript에서 AJAX

- JavaScript에서 제공 하는 XMLHttpRequest object를 이용하여 구현 한다.

```javascript
<script> 
    function loadXMLDoc() 
		{ var xmlhttp; 
         	if (window.XMLHttpRequest) { xmlhttp=new XMLHttpRequest(); // IE7+, Firefox, Chrome, Opera, Safari }
            else{ xmlhttp=new ActiveXObject("Microsoft.XMLHTTP"); // IE6, IE5
            }
            xmlhttp.onreadystatechange=function(){ 
            if (xmlhttp.readyState==4 && xmlhttp.status==200){ 			                     document.getElementById("myDiv").innerHTML=xmlhttp.responseText; 			   }
            }                                         			                           xmlhttp.open("GET","ajax_info.txt",true); 
           	xmlhttp.send(); 
            } 
</script>
```



#### 1단계 : XMLHttpRequest 객체 생성

- JavaScript의 내장 객체인 XMLHTttpRequest를 생성
- 생성 시 웹브라우저에 따라 달리 생성

```javascript
var xmlhttp;
if (window.XMLHttpRequest) {
xmlhttp=new XMLHttpRequest(); // IE7+, Firefox, Chrome, Opera, Safari
}else{
xmlhttp=new ActiveXObject("Microsoft.XMLHTTP"); // IE6, IE5
}
```

#### 2단계 : 서버에서 결과를 받을 준비.

- 서버에 요청 후 결과를 받을 준비를 한다
- 서버에서 결과를 현재 화면에 출력할 준비를 한다.

```javascript
xmlhttp.onreadystatechange=function(){ 
	if (xmlhttp.readyState==4 && xmlhttp.status==200){ 		
		document.getElementById("myDiv").innerHTML=xmlhttp.responseText; 
	} 
}
```

#### 3단계 :서버에 요청.

- `open()` 함수를 이용하여 서버에 전송 준비.
- `send()`함수를 통해 서버에 전송.

```javascript
xmlhttp.open("GET",“serverApp.jsp",true);
xmlhttp.send();
```

| Method                 | Description                                                  |
| ---------------------- | ------------------------------------------------------------ |
| open(method,url,async) | method: the type of request: GET or POST <br />url: the location of the file on the server <br />async: true (asynchronous) or false (synchronous) |
| send(string)           | Sends the request off to the server. <br />string: Only used for POST requests |

```javasc
xmlhttp.open("POST"," serverApp.jsp",true);
xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded"); 
xmlhttp.send("fname=Henry&lname=Ford");
```



### jQuery를 이용한 AJAX

- jQuery에서 기본적인 `$.ajax()`를 제공 한다.

```javascript
$("button").click(function(){
    $.ajax({
        url: “serverApp.jsp",
        success: function(result){
        	$("#div1").html(result); 
    	}

	}); 
});
```







### 기타사항

- AJAX는 한글을 지원하지 않기 때문에 서버에서 한글을 읽을 수 있도록 인코딩을 해주어야 한다.

  ```java
  	@RequestMapping("/gettime")
  	@ResponseBody
  	public void gettime(HttpServletResponse rep) {
  		PrintWriter out = null;
  		try {
  			rep.setCharacterEncoding("UTF-8");
  			out = rep.getWriter();
  			Date d = new Date();
  			out.print("서버 Time:"+d.toString());
  			out.close();
  		} catch (IOException e) {
  			e.printStackTrace();
  		}
  	}
  ```

  