# 자바api서버 리눅스 환경 수동배포



## 사전준비



### 1.java 설치

-  설치

```
sudo apt install openjdk-17-jdk
```

- 버전 확인

```
java -version
```

- environment 파일에서 JAVA_HOME 환경변수를 설정한다.

```
sudo vi /etc/environment

#enviroment
PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin"
JAVA_HOME="/usr/lib/jvm/java-17-openjdk-amd64"

```

- source 명령어를 실행하고, 변경값이 적용되었는지 확인

```
source /etc/environment
echo $JAVA_HOME
```

- java 삭제

```
sudo apt remove openjdk-17-jdk
```



### 2. git 설치

```
sudo apt-get install git
```





### 3. git clone

```
git clone git주소
```



### 4. 프로젝트 빌드 및 배포

- 권한 및 빌드

```
chmod +x gradlew  --> 권한
./gradlew clean build -x test  --> 빌드
```

- 프로젝트 시작

```
cd /build/libs/
nohup java -jar [빌드된 자바 파일] &

/build/libs/nohup java -jar [빌드된 자바 파일] &
```

- 프로젝트 재시작

```
fuser -k -n tcp 8080
```

- 프로젝트 로그 확인 

```
tail -f nohup.out
```



