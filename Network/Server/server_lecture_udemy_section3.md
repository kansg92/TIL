# 누구나 따라 할 수 있는 서버 클론코딩 



## Section2 - 리눅스 환경 구축



### 서브 도메인

도메인을 더 기억하기 쉽게 만든것

- www.jcwebs.org/abs ---> abc.jcwebs.org

- https://m.naver.com 
- https://cafe.naver



### Redirction

- http or ip주소로 접속시 -> https이하 도메인으로 접속되게 만들어 놓은것..





### 리눅스 서버환경 구축

#### 1. nginx,php,mysql 설치

1. wic scp를 통해 putty로 aws 에 원격접속하여 터미널을 킴

2. nginx 설치

   ```
   sudo apt update 
   
   sudo apt install nginx
   
   nginx -v   --> 설치확인
   ```

3. MYSQL설치

   - ```
     sudo apt install mysql-server
     
     sudo mysql_secure_installation --> mysql 보안설정
     
     
     sudo mysql -u root -p    --> mysql 접속
     ```

   - [mysql_secure_installation 셋팅중 error 나올시 참조]: https://seong6496.tistory.com/322

4. PHP설치

   - ```
     sudo apt install php-fpm php-mysql
     php -v --> php 설치확인
     
     ```

5.  브라우저에 탄력적IP 입력하여 nginx 서버 뜨는지 확인

![image-20230212152244904](C:\Users\kan\AppData\Roaming\Typora\typora-user-images\image-20230212152244904.png)

#### 2. nginx 와 php 연동

```
cd /var/www/html 
sudo vi phpinfo.php 

<?php
        phpinfo();
?>
작성후 저장

cd /etc/nginx/sites-available
sudo vi default

        # pass PHP scripts to FastCGI server
        #
        location ~ \.php$ {								-> 주석해제
                include snippets/fastcgi-php.conf;		-> 주석해제
        #
        #       # With php-fpm (or other unix sockets):
                fastcgi_pass unix:/run/php/php8.1-fpm.sock;	-> 주석해제 후 설치된 php버전으로 변경
        #       # With php-cgi (or other tcp sockets):
        #       fastcgi_pass 127.0.0.1:9000;
        }	--> 주석해제

cd /etc/nginx
sudo vi nginx.conf


http {

        ##
        # Basic Settings
        ##

        sendfile on;
        tcp_nopush on;
        types_hash_max_size 2048;
        # server_tokens off;

         server_names_hash_bucket_size 64;		-> 주석해제
        # server_name_in_redirect off;


sudo nginx -t  --> 잘되었는지 test

sudo service nginx restart --> nginx restart

ip주소/phpinfo.php 브라우저 검색하여 php접속해서 php확인.


```



#### 3. 도메인 구입하여 적용

1. 가비아에서 도메인 구입( 제일 저렴한것이 1년 500원)
2. DNS관리에서  A  타입 @, www 추가 TTL:3600
3. CNAME타입 도메인주소. 추가 TTL:3600

```
cd /etc/nginx/sites-available
sudo vi default

 server_name jjapflix.store www.jjapflix.store; --> 서버네임 변경
 


```

4.  브라우저에서 도메인 검색

#### 4. 서브 도메인 적용

1.  파일 디렉토리 생성..

```
cd /var/www/html
sudo mkdir dev
sudo mkdir prod

```

2. dev, prod 디렉토리안에 index.html 생성
3. 서버블록 생성

```
cd /etc/nginx/sites-available
sudo vi default


server {
        listen 80;
        listen [::]:80;

        root /var/www/html/dev;
        index index.html;

        server_name dev.jjapflix.store;

        location / {
                try_files $uri $uri/ =404;
        }
}

server {
        listen 80;
        listen [::]:80;

        root /var/www/html/prod;
        index index.html;

        server_name prod.jjapflix.store;

        location / {
                try_files $uri $uri/ =404;
        }
}

작성..
```



#### 5. 리다이렉션 적용

1. 서버블록 추가

```

server {
        listen 80;
        server_name 13.124.0.228;
        return 301 http://jjapflix.store$request_uri;
}


https 를 적용한 후에 https로 변경.
```

2. IP 주소로 검색하면 도메인으로 브라우저가 검색 되면 완료..



### 6 HTTPS 적용하기

- ec2 ubuntu 22.04 let's Encrypt

#### 1. Cerbot설치

```
sudo snap install core
sudo snap refresh core

* 기존 서버에 cerbot이 설치되어 있는경우 삭제
sudo apt remove certbot

sudo snap install --classic certbot

* 다른 패키지와 충돌을 피하기위해 심볼릭을 걸어둠

sudo ln -s /snap/bin/certbot /usr/bin/certbot

```



#### 2. Nginx 구성 확인

#### 3. 방화벽을 통한 HTTPS 허용

(ufw를 사용할 경우) 방화벽 상태를 확인합니다.

```
sudo ufw status
```

다음과 같거나 HTTPS(443) 포트가 열려 있지 않다면 HTTPS를 허용합니다.

```
Output
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere                  
Nginx HTTP                 ALLOW       Anywhere                  
OpenSSH (v6)               ALLOW       Anywhere (v6)             
Nginx HTTP (v6)            ALLOW       Anywhere (v6)
```





[ufw 방화벽설정](https://kugancity.tistory.com/entry/ubuntu%EC%97%90%EC%84%9C-%EB%B0%A9%ED%99%94%EB%B2%BD-%EC%84%A4%EC%A0%95-UFW)

[ufw 방화병설정2](https://jjeongil.tistory.com/1281)

#### 4. SSL 인증서 받기

```
sudo certbot --nginx -d example.com -d www.example.com
* 서브도메인 추가시 같이 적용된다...
```

1. 명령을 실행하고 나면 이메일 주소를 입력하고 진행한다.
2. 

#### 5. Cerbot 자동 갱신 확인

- Let's Encrypt의 인증서는 90일동안만 유효하기 때문에 자동 갱신하도록 하는게 좋다.

```
sudo systemctl status snap.certbot.renew.service

sudo certbot renew --dry-run
*오류가 나지않는다면 성공!

*적용을 다하고나니 default에 server가 생겻다.

server {
    if ($host = www.jjapflix.store) {
        return 301 https://$host$request_uri;
    } # managed by Certbot


    if ($host = jjapflix.store) {
        return 301 https://$host$request_uri;
    } # managed by Certbot


        listen 80 default_server;
        listen [::]:80 default_server;

        server_name jjapflix.store www.jjapflix.store;
    return 404; # managed by Certbot



```

[nginx https letsencrypt 적용 참고사이트](https://velog.io/@tlqhrm/Ubuntu-22.04%EC%97%90%EC%84%9C-Nginx%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%B4-%EB%AC%B4%EB%A3%8C-Https-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0)

##### 2시간가량 https가 도메인 적용이 안되었는데 인바운드 규칙에 https를 추가하지 않아서였다... 

