# day42__spring web에서 파일 업로드



### (1). util.java 파일 생성, save되는 클래스 생성

```java
package com.multi.frame;

import java.io.FileOutputStream;
import org.springframework.web.multipart.MultipartFile;

public class Util {
	public static void saveFile(MultipartFile mf) {
        // 저장되는 파일 걍로
		String dir = "C:\\muticampus\\spring\\shopadmin\\src\\main\\resources\\static\\img\\";
		byte [] data;
        //파일의 이름을 변수에 담아줌.
		String imgname = mf.getOriginalFilename();
		try {
			data = mf.getBytes();
			FileOutputStream fo = 
					new FileOutputStream(dir+imgname);
			fo.write(data);
			fo.close();
		}catch(Exception e) {
			
		}
		
	}
	
}
```

### (2) controller

```java
	@RequestMapping("/addimpl")//name,price,cid,mf(->imgname)날라옴!
	public String addimpl(Model m, ProductVO p) {
		String imgname = p.getMf().getOriginalFilename();
		p.setImgname(imgname);
		
		try {
			biz.register(p);
			Util.saveFile(p.getMf()); // 유틸에 저장.
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
		return "redirect:select";
	}
```



### (3) 화면단 - javascript

```javascript
$(document).ready(function(){

	
	$('#register_btn').click(function(){
		$('.user').attr({
			'enctype':'multipart/form-data', // 인코딩타입을 설정해줌.
			'method' : 'post',
			'action' : 'addimpl'
		});
		$('.user').submit();
	});
	
});
```

### (4) 화면단 - HTML

```html
           <div class="form-group">
                IMG<input type="file" class="form-control form-control-user"
                    name="mf" >
            </div>
			<!-- type=file, name=mf로 지정. -->
```

