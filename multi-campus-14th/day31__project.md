# 📢day31__개인 플젝 진행.

### hilight chart

[hilightChart](https://www.highcharts.com/) 사이트 통해서 차트 양식을 가져올 수 있다.

- 화면  js

```javascript
<script>
function display(ajaxdata){
	const chart = Highcharts.chart('container', {
	    title: {
	        text: 'Chart.update'
	    },
	    subtitle: {
	        text: 'Plain'
	    },
	    xAxis: {
	        categories: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']
	    },
	    series: [{
	        type: 'column',
	        colorByPoint: true,
	        data: ajaxdata,
	        showInLegend: false
	    }]
	});

	document.getElementById('plain').addEventListener('click', () => {
	    chart.update({
	        chart: {
	            inverted: false,
	            polar: false
	        },
	        subtitle: {
	            text: 'Plain'
	        }
	    });
	});

	document.getElementById('inverted').addEventListener('click', () => {
	    chart.update({
	        chart: {
	            inverted: true,
	            polar: false
	        },
	        subtitle: {
	            text: 'Inverted'
	        }
	    });
	});

	document.getElementById('polar').addEventListener('click', () => {
	    chart.update({
	        chart: {
	            inverted: false,
	            polar: true
	        },
	        subtitle: {
	            text: 'Polar'
	        }
	    });
	});
};

function getdata(){
	$.ajax({
		url:'getchart',
		success:function(data){
			display(data);
		}
	})
	
};

$(document).ready(function(){
	$('button').click(function(){
		getdata();
		
	});
	
});

</script>
```

- 자바 data정보

```java
	@RequestMapping("/getchart")	
	public Object getchart() {
		JSONArray ja = new JSONArray();
		for(int i = 0; i < 15; i++) {
			Random r = new Random();
			int data = r.nextInt(50)+1;
			ja.add(data);
		}
		return ja;
	}
	
```







### 개인 프로젝트 준비(day06)

1. 주제 선정
   1. 그래도 나름 도움되는 웹을 만들어보자. (daily report??)
2. 화면 설계
   1. 대문 (대문화면 로그인,  회원가입 go to dailtyreport )
   2. 주화면  메인 기능 : 매일습관(습관수정) ,dailyreport노출, 
   2. 로그인화면, 회원가입 화면 만들기.
   2. dailyreport : 표작성.and 표추가기능. 시간설정 어떻게할지 고민해보아야함.
   2. 주간,월간 report는 추가 만들기.
3. 테마 서치
   - 메인 테마 :  https://startbootstrap.com/previews/sb-admin-angular
4. 개발 환경 구축
5. 시스템 개발
5. 5월 24일 발표 예정.





