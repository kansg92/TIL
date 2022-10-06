# Spring Boot Scheduler

### 1. XXXApplication.java 에 @EnableScheduling 추가

```java
@EnableScheduling
@SpringBootApplication
public class Day051Application {
	public static void main(String[] args) {
		SpringApplication.run(Day051Application.class, args);
	}

}
```

### 2. Configuration 생성

```java
package com.multi;

import org.springframework.context.annotation.Configuration;
import org.springframework.scheduling.annotation.SchedulingConfigurer;
import org.springframework.scheduling.concurrent.ThreadPoolTaskScheduler;
import org.springframework.scheduling.config.ScheduledTaskRegistrar;

@Configuration
public class ScheduleConfig implements SchedulingConfigurer

{
	private final int POOL_SIZE = 6;

	@Override
	public void configureTasks(ScheduledTaskRegistrar registry) {
		ThreadPoolTaskScheduler threadPoolTaskScheduler = new ThreadPoolTaskScheduler();

		threadPoolTaskScheduler.setPoolSize(POOL_SIZE);
		threadPoolTaskScheduler.setThreadNamePrefix("CommB-Scheduled-task-");
		threadPoolTaskScheduler.initialize();

		registry.setTaskScheduler(threadPoolTaskScheduler);
	}

}
```

### 3.Scheduler 생성

```java
package com.multi.controller;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.messaging.simp.SimpMessageSendingOperations;
import org.springframework.scheduling.annotation.Scheduled;
import org.springframework.stereotype.Component;

import com.multi.vo.Msg;

@Component
public class Scheduler {
	@Autowired
	private SimpMessageSendingOperations messagingTemplate;

	
    @Scheduled(cron = "*/15 * * * * *")
    public void cronJobDailyUpdate() {
    	
    	System.out.println("----------- Scheduler ------------");
    	Msg msg = new Msg();
    	msg.setContent("1");
    	msg.setContent1("2");
    	msg.setContent2("3");
    	msg.setContent3("4");
    	messagingTemplate.convertAndSend("/send", msg);
    }

    @Scheduled(cron = "1 0 0 1,8,15,22 * *")
    public void cronJobWeeklyUpdate(){

    }


}
```

```java
        초 분 시 일 월 요일
cron = "*  *  *  *  *  *"   

0 0 * * * * : 매 시 0분 0초에 작업
*/15 * * * * * : 매 15초마다 작업
0 0 0 1,8,17,26 * * : 매달 1, 8, 17, 26일 자정에 작업
0 0 10-20 * * * : 매일 10시 ~ 20시 한시간 간격으로 작업
0 0 9-18 * * 1-5 : 월 ~ 금(평일) 9 ~ 18시 매 정각에 작업
0 0 */3 4 * * : 매달 4일에 3시간 간격으로 작업
```