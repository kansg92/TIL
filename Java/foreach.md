# foreach 반복문



## 기존 for문 구조

```java
// for 문
for(초기화; 조건식; 증감식;){
	조건식이 true일 경우 수행할 코드
}

//ex
String [] numbers = {"one","two","three","4"}
for(int i = 0; i < numbers.length; i++){
    System.out.println("numbers[i]")
}
```



#### 결과

```java
one
two
three
4	
```



## foreach Loop

```java
// for each 문
for (type variation: iterate){
	body-of-loop
}

// ex
String [] numbers = {"one","two","three","4"}
for(String num : numbers){
    System.out.println(num);
}
```

- iterate : loop를 돌릴 객체
- type은 루프를 돌릴 수 있는 형태인 배열 또는 ArrayList등이 가능
- literate 객체에서 한개씩 순차적으로 variation에 대입되어 for문을 수행



#### ArrayList 재구현 하는 경우 

```java
// ArrayList ex
ArrayList<String> numbers = new ArrayList<String>();
numbers.add("one");
numbers.add("two");
numbers.add("three");
numbers.add("4");

for(String num: numbers){
	System.out.println(num);
}
```



## foreach문의 제약사항

- 따로 반복횟수를 명시하는게 불가능
- 1스텝식 순차적으로 반복할때만 사용이 가능하다.





---

##### 참조 자료

https://wikidocs.net/264