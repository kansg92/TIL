# day56__

## NCP 환경 설정



### Apach-Tomcat 설치



#### 1. JDK 설치 후 진행



#### 2. Apach-Tomcat Download

```
wget http://archive.apache.org/dist/tomcat/tomcat-8/v8.5.27/bin/apache-tomcat-8.5.27.tar.gz
```



#### 3. 압축 해제

```
tar zxvf apache-tomcat-8.5.27.tar.gz
ls
```



#### 4. 실행

```
cd /root/apache-tomcat-8.5.27/bin
./startup.sh         -실행
./shutdown.sh      -정지
```



#### 5. 실행 확인

```
 ps -ef | grep tomcat
 
```



####  6. PC에서 접속

https:// 공인 IP : 8080