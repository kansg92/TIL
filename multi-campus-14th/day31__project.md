# ๐ขday31__๊ฐ์ธ ํ์  ์งํ.

### hilight chart

[hilightChart](https://www.highcharts.com/) ์ฌ์ดํธ ํตํด์ ์ฐจํธ ์์์ ๊ฐ์ ธ์ฌ ์ ์๋ค.

- ํ๋ฉด  js

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

- ์๋ฐ data์ ๋ณด

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







### ๊ฐ์ธ ํ๋ก์ ํธ ์ค๋น(day06)

1. ์ฃผ์  ์ ์ 
   1. ๊ทธ๋๋ ๋๋ฆ ๋์๋๋ ์น์ ๋ง๋ค์ด๋ณด์. (daily report??)
2. ํ๋ฉด ์ค๊ณ
   1. ๋๋ฌธ (๋๋ฌธํ๋ฉด ๋ก๊ทธ์ธ,  ํ์๊ฐ์ go to dailtyreport )
   2. ์ฃผํ๋ฉด  ๋ฉ์ธ ๊ธฐ๋ฅ : ๋งค์ผ์ต๊ด(์ต๊ด์์ ) ,dailyreport๋ธ์ถ, 
   2. ๋ก๊ทธ์ธํ๋ฉด, ํ์๊ฐ์ ํ๋ฉด ๋ง๋ค๊ธฐ.
   2. dailyreport : ํ์์ฑ.and ํ์ถ๊ฐ๊ธฐ๋ฅ. ์๊ฐ์ค์  ์ด๋ป๊ฒํ ์ง ๊ณ ๋ฏผํด๋ณด์์ผํจ.
   2. ์ฃผ๊ฐ,์๊ฐ report๋ ์ถ๊ฐ ๋ง๋ค๊ธฐ.
3. ํ๋ง ์์น
   - ๋ฉ์ธ ํ๋ง :  https://startbootstrap.com/previews/sb-admin-angular
4. ๊ฐ๋ฐ ํ๊ฒฝ ๊ตฌ์ถ
5. ์์คํ ๊ฐ๋ฐ
5. 5์ 24์ผ ๋ฐํ ์์ .





