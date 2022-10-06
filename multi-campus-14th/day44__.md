# 📢day44



### ModelAttribute

- 모든 페이지 네비,헤더 같은 메뉴를 만들 때 사용하는 어노테이션.

```java
	@ModelAttribute("catelist")
	public List<CateVO> makemenu(){
		List<CateVO> catelist = null;
		try {
			catelist = catebiz.getmain();
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
		return catelist;
	}
```



