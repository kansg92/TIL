# ๐ขday30__Ajax

## ์น์์ ๋น๋๊ธฐ ๋ฐฉ์

- ์น์์ ํน์ ๋ถ๋ถ๋ง ๋ฐ์ดํฐ๋ฅผ ๋ฟ๋ ค์ ํ๋ฉด์ ๊ทธ๋๋ก ์๊ณ , ํน์ ์์ญ์๋ง ๋ฐ์ดํฐ๊ฐ ๊ฒ์ํด์ ์์ ๋๋ ํ์์ ๋งํ๋ค.
- ์น์๋ฒ์์ ๋ฐ์ดํฐ๋ฅผ ๋ฐ์์์ ํน์  ์์ญ์ ๋ฐ์ดํฐ๋ง ๋ฐ๊พธ์ด์ผ ํ๊ธฐ ๋๋ฌธ์ ํต์ ์ด ํ์ํ๋ค.



## AJAX

### AJAX๋??

- AJAX(Asynchronous JavaScript and XML)๋ ๋น๋๊ธฐ ํต์ ์ ์ง์ ํ๋ ๋ฐฉ์์ด๋ฉฐ, ๋ผ์ด๋ธ๋ฌ๋ฆฌํํ๋ก ์กด์ฌํ๋ค.
  - 2005๋ 2์ 18์ผ ๋ฏธ๊ตญ adaptivepath๋ผ๋ ํ์ฌ์ ์น ์ฌ์ดํธ์ ์์ธ์ด ํ๋๊ฐ ์ฌ๋ผ ์๋ค. ์ ๋ชฉ์ "Ajax : A new Approach to web Applications"์ด๊ณ  ์์ฑ์๋ Jesse James Garrett์ด๋ค. ์ฌ๊ธฐ์ AJAX๋ ์์ ๋์๋ค.
- AJAX๋ ์๋ก์ด ์ธ์ด๊ฐ ์๋ JavaScript์ ์ถ๊ฐ๋ ํต์  ๋ฐฉ์์ด๋ค.
- ํ๋ฉด ์ ์ฒด๋ฅผ ์ฌ๋ก๋ ํ์ง ์๊ณ ๋ ์๋ฒ์์ ํน์  ๋ฐ์ดํฐ๋ฅผ ์ก์์  ํ  ์ ์๋ค.
- Ajax๋ ๋น ๋ฅด๊ณ  ๋์ ์ธ ์น ํ์ด์ง๋ฅผ ๋ง๋ค๊ธฐ์ํ ๊ธฐ์ ์ด๋ค.
- AJAX๋ ์น ํ์ด์ง๊ฐ ์๋ฒ์ ๋ฐ์ดํฐ๋ฅผ ๊ตํํ์ฌ ๋น๋๊ธฐ ์ ์ผ๋ก ์๋ฐ์ดํธ ํ  ์ ์๋ค. ์ด๋ ์ ์ฒด ํ์ด์ง๋ฅผ ์ฌ๋ก๋ ํ์ง ์๊ณ , ์น ํ์ด์ง์ ์ผ๋ถ๋ฅผ ๊ฐฑ์  ํ  ์ ์๋ค๋ ๊ฒ์ ์๋ฏธํ๋ค.



### JavaScript์์ AJAX

- JavaScript์์ ์ ๊ณต ํ๋ XMLHttpRequest object๋ฅผ ์ด์ฉํ์ฌ ๊ตฌํ ํ๋ค.

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



#### 1๋จ๊ณ : XMLHttpRequest ๊ฐ์ฒด ์์ฑ

- JavaScript์ ๋ด์ฅ ๊ฐ์ฒด์ธ XMLHTttpRequest๋ฅผ ์์ฑ
- ์์ฑ ์ ์น๋ธ๋ผ์ฐ์ ์ ๋ฐ๋ผ ๋ฌ๋ฆฌ ์์ฑ

```javascript
var xmlhttp;
if (window.XMLHttpRequest) {
xmlhttp=new XMLHttpRequest(); // IE7+, Firefox, Chrome, Opera, Safari
}else{
xmlhttp=new ActiveXObject("Microsoft.XMLHTTP"); // IE6, IE5
}
```

#### 2๋จ๊ณ : ์๋ฒ์์ ๊ฒฐ๊ณผ๋ฅผ ๋ฐ์ ์ค๋น.

- ์๋ฒ์ ์์ฒญ ํ ๊ฒฐ๊ณผ๋ฅผ ๋ฐ์ ์ค๋น๋ฅผ ํ๋ค
- ์๋ฒ์์ ๊ฒฐ๊ณผ๋ฅผ ํ์ฌ ํ๋ฉด์ ์ถ๋ ฅํ  ์ค๋น๋ฅผ ํ๋ค.

```javascript
xmlhttp.onreadystatechange=function(){ 
	if (xmlhttp.readyState==4 && xmlhttp.status==200){ 		
		document.getElementById("myDiv").innerHTML=xmlhttp.responseText; 
	} 
}
```

#### 3๋จ๊ณ :์๋ฒ์ ์์ฒญ.

- `open()` ํจ์๋ฅผ ์ด์ฉํ์ฌ ์๋ฒ์ ์ ์ก ์ค๋น.
- `send()`ํจ์๋ฅผ ํตํด ์๋ฒ์ ์ ์ก.

```javascript
xmlhttp.open("GET",โserverApp.jsp",true);
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



### jQuery๋ฅผ ์ด์ฉํ AJAX

- jQuery์์ ๊ธฐ๋ณธ์ ์ธ `$.ajax()`๋ฅผ ์ ๊ณต ํ๋ค.

```javascript
$("button").click(function(){
    $.ajax({
        url: โserverApp.jsp",
        success: function(result){
        	$("#div1").html(result); 
    	}

	}); 
});
```







### ๊ธฐํ์ฌํญ

- AJAX๋ ํ๊ธ์ ์ง์ํ์ง ์๊ธฐ ๋๋ฌธ์ ์๋ฒ์์ ํ๊ธ์ ์ฝ์ ์ ์๋๋ก ์ธ์ฝ๋ฉ์ ํด์ฃผ์ด์ผ ํ๋ค.

  ```java
  	@RequestMapping("/gettime")
  	@ResponseBody
  	public void gettime(HttpServletResponse rep) {
  		PrintWriter out = null;
  		try {
  			rep.setCharacterEncoding("UTF-8");
  			out = rep.getWriter();
  			Date d = new Date();
  			out.print("์๋ฒ Time:"+d.toString());
  			out.close();
  		} catch (IOException e) {
  			e.printStackTrace();
  		}
  	}
  ```

  