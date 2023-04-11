# Docker Compose

+ 웹 시스템에서는 여러개의 Docker 컨테이너가 협력하면서 작동
+ Docker Compose는 여러 컨테이너를 모아서 관리하는 툴
+ docker-compose.yml
  + 컨테이너의 구성정보 정의(호스트상의 여러 켄테이너를 일괄적으로 관리)

```
ubuntuuser@DESKTOP-5JEDT7B:~/dockertext2/chap07$ cat docker-compose.yml
version: '3.3'
services:
  # WebServer config
  webserver:
    build: .
    ports:
     - "80:80"
    depends_on:
     - redis

  # Redis config
  redis:
    image: redis:4.0
```

1. 버전 지정 : version: '3.3'
2. 위의 경우 webserver와 redis라는 이름의 서비스 2개 정의
3. webserver 서비스는 커렌트 디렉토리에있는 Dockerfile에 정의한 구성의 이미지를 build
   + 외부에 대해 80번 포트 공개(port:)
   + 이 컨테이너는 redis 서비스에 의존
4. redis 서비스는 Docker Hub에 공개된 redis:4.0 이미지를 가져옴



```
docker-compose ps : compose 확인

docker-compose up : compose 시작

docker-compose stop : compose 정지

docker-compose down : compose 리소스 삭제
```





**샘플 애플리케이션의 컨테이너 시작**

+ 브라우저에서 로컬 머신의 80번 포트인 아래의 주소로 액세스하면 샘플
  + Docker Hub로부터 redis서비스에서 사용할 redis:4.0의 이미지 다운
  + webserver에서 사용할 이미지가 Dockerfile 바탕으로 빌드
  + 준비가 끝난 redis 서비스의 컨테이너를 시작하고 계속해서 webserver 서비스의 컨테이너 시작

```
ubuntuuser@DESKTOP-5JEDT7B:~/dockertext2/chap07$ docker-compose up
Creating network "chap07_default" with the default driver
Pulling redis (redis:4.0)...
4.0: Pulling from library/redis
54fec2fa59d0: Pull complete
9c94e11103d9: Pull complete
04ab1bfc453f: Pull complete
7988789e1fb7: Pull complete
8ce1bab2086c: Pull complete
40e134f79af1: Pull complete
Digest: sha256:2e03fdd159f4a08d2165ca1c92adde438ae4e3e6b0f74322ce013a78ee81c88d
Status: Downloaded newer image for redis:4.0
Building webserver
[+] Building 87.8s (12/12) FINISHED
 => [internal] load build definition from Dockerfile                                                               0.2s
 => => transferring dockerfile: 594B                                                                               0.0s
 => [internal] load .dockerignore                                                                                  0.3s
 => => transferring context: 2B                                                                                    0.0s
 => [internal] load metadata for docker.io/library/python:3.6                                                      5.7s
 => [internal] load build context                                                                                  0.1s
 => => transferring context: 349.76kB                                                                              0.0s
 => [1/7] FROM docker.io/library/python:3.6@sha256:f8652afaf88c25f0d22354d547d892591067aa4026a7fa9a6819df9f300af  60.2s
 => => resolve docker.io/library/python:3.6@sha256:f8652afaf88c25f0d22354d547d892591067aa4026a7fa9a6819df9f300af6  0.1s
 => => sha256:0e29546d541cdbd309281d21a73a9d1db78665c1b95b74f32b009e0b77a6e1e3 54.92MB / 54.92MB                  11.5s
 => => sha256:f8652afaf88c25f0d22354d547d892591067aa4026a7fa9a6819df9f300af6fc 1.86kB / 1.86kB                     0.0s
 => => sha256:d097a4907a8ec079df5ac31872359c2de510f82214c0448e926393b376d3b60d 2.22kB / 2.22kB                     0.0s
 => => sha256:cb5b7ae361722f070eca53f35823ed21baa85d61d5d95cd5a95ab53d740cdd56 10.87MB / 10.87MB                   2.8s
 => => sha256:54260638d07c5e3ad24c6e21fc889abbc8486a27634c0892086ff71f3f44b104 9.27kB / 9.27kB                     0.0s
 => => sha256:9b829c73b52b92b97d5c07a54fb0f3e921995a296c714b53a32ae67d19231fcd 5.15MB / 5.15MB                     0.9s
 => => sha256:6494e4811622b31c027ccac322ca463937fd805f569a93e6f15c01aade718793 54.57MB / 54.57MB                  20.1s
 => => sha256:6f9f74896dfa93fe0172f594faba85e0b4e8a0481a0fefd9112efc7e4d3c78f7 196.51MB / 196.51MB                38.5s
 => => sha256:5e3b1213efc56598e78bd602983945c164de2a37205e06a62dada823124dc743 6.29MB / 6.29MB                    15.1s
 => => extracting sha256:0e29546d541cdbd309281d21a73a9d1db78665c1b95b74f32b009e0b77a6e1e3                         10.9s
 => => sha256:9fddfdc56334f2e6efad7e241bf5e7459c40ed105c5478676f41c1244bd96752 14.21MB / 14.21MB                  19.2s
 => => sha256:404f02044bac0432ca522cbb9f254b1c91fcea6806bfeef0be0b243b2f31bab7 235B / 235B                        19.8s
 => => sha256:c4f42be2be53b900ebffc040c1df13de538434ccc5f5d954a56848a6169a3a3f 2.21MB / 2.21MB                    22.1s
 => => extracting sha256:9b829c73b52b92b97d5c07a54fb0f3e921995a296c714b53a32ae67d19231fcd                          1.3s
 => => extracting sha256:cb5b7ae361722f070eca53f35823ed21baa85d61d5d95cd5a95ab53d740cdd56                          1.3s
 => => extracting sha256:6494e4811622b31c027ccac322ca463937fd805f569a93e6f15c01aade718793                          9.0s
 => => extracting sha256:6f9f74896dfa93fe0172f594faba85e0b4e8a0481a0fefd9112efc7e4d3c78f7                         17.0s
 => => extracting sha256:5e3b1213efc56598e78bd602983945c164de2a37205e06a62dada823124dc743                          0.7s
 => => extracting sha256:9fddfdc56334f2e6efad7e241bf5e7459c40ed105c5478676f41c1244bd96752                          1.5s
 => => extracting sha256:404f02044bac0432ca522cbb9f254b1c91fcea6806bfeef0be0b243b2f31bab7                          0.0s
 => => extracting sha256:c4f42be2be53b900ebffc040c1df13de538434ccc5f5d954a56848a6169a3a3f                          0.7s
 => [2/7] RUN pip install --upgrade pip                                                                           10.5s
 => [3/7] COPY requirements.txt /opt/imageview/                                                                    0.1s
 => [4/7] RUN pip install --no-cache-dir -r /opt/imageview/requirements.txt                                        9.3s
 => [5/7] COPY app.py /opt/imageview/                                                                              0.1s
 => [6/7] COPY templates/ /opt/imageview/templates/                                                                0.1s
 => [7/7] COPY static/ /opt/imageview/static/                                                                      0.1s
 => exporting to image                                                                                             0.8s
 => => exporting layers                                                                                            0.8s
 => => writing image sha256:ffb52eb57d17c0fd2b911892bac09a6470f0e40a19656f0304e7b1adc03e950f                       0.0s
 => => naming to docker.io/library/chap07_webserver                                                                0.0s
WARNING: Image for service webserver was built because it did not already exist. To rebuild this image you must use `docker-compose build` or `docker-compose up --build`.
Creating chap07_redis_1 ... done
Creating chap07_webserver_1 ... done
Attaching to chap07_redis_1, chap07_webserver_1
redis_1      | 1:C 19 Mar 14:57:37.394 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
redis_1      | 1:C 19 Mar 14:57:37.395 # Redis version=4.0.14, bits=64, commit=00000000, modified=0, pid=1, just started
redis_1      | 1:C 19 Mar 14:57:37.395 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
redis_1      | 1:M 19 Mar 14:57:37.399 * Running mode=standalone, port=6379.
redis_1      | 1:M 19 Mar 14:57:37.399 # Server initialized
redis_1      | 1:M 19 Mar 14:57:37.399 # WARNING overcommit_memory is set to 0! Background save may fail under low memory condition. To fix this issue add 'vm.overcommit_memory = 1' to /etc/sysctl.conf and then reboot or run the command 'sysctl vm.overcommit_memory=1' for this to take effect.
redis_1      | 1:M 19 Mar 14:57:37.399 # WARNING you have Transparent Huge Pages (THP) support enabled in your kernel. This will create latency and memory usage issues with Redis. To fix this issue run the command 'echo never > /sys/kernel/mm/transparent_hugepage/enabled' as root, and add it to your /etc/rc.local in order to retain the setting after a reboot. Redis must be restarted after THP is disabled.
redis_1      | 1:M 19 Mar 14:57:37.399 * Ready to accept connections
webserver_1  |  * Serving Flask app "app" (lazy loading)
webserver_1  |  * Environment: production
webserver_1  |    WARNING: Do not use the development server in a production environment.
webserver_1  |    Use a production WSGI server instead.
webserver_1  |  * Debug mode: on
webserver_1  |  * Running on all addresses.
webserver_1  |    WARNING: This is a development server. Do not use it in a production deployment.
webserver_1  |  * Running on http://172.18.0.3:80/ (Press CTRL+C to quit)
webserver_1  |  * Restarting with stat
webserver_1  |  * Debugger is active!
webserver_1  |  * Debugger PIN: 465-738-733
webserver_1  | 172.18.0.1 - - [19/Mar/2023 14:57:58] "GET / HTTP/1.1" 200 -
webserver_1  | 172.18.0.1 - - [19/Mar/2023 14:57:58] "GET /static/css/bootstrap.css HTTP/1.1" 200 -
webserver_1  | 172.18.0.1 - - [19/Mar/2023 14:57:58] "GET /static/images/docker-machine-02.jpg HTTP/1.1" 200 -
webserver_1  | 172.18.0.1 - - [19/Mar/2023 14:57:58] "GET /favicon.ico HTTP/1.1" 404 -
```



## docker-compose.yml

+ Docker compose는 docker-compose.yml이라는 Compose 정의 파일에 시스템 안에서 가동하는 여러 서버들의 구성을 모아서 정의
+ YAML
  + 구조화된 데이터를 표현하기 위한 데이터 포맷

```
version: '3.3'
services:
  # WebServer config
  webserver:
    image: ubuntu
    ports:
     - "80:80"
    depends_on:
     - webnet

  # Redis config
  redis:
    image: redis:4.0
    networks:
    	- webnet

#네트워크 정의
networks:
	webnet:

#데이터 볼륨 정의
volumes:
	data-volume:
```



### 이미지 지정(image)

+ 도커 컨테이너 바탕이 되는 베이스 이미지 지정을 위해서는 image 사용
+ 위의 경우 webserver라는 이름의 이미지 베이스를 'ubuntu'로 지정
  + 태그가 없다면 latest



### 이미지 빌드(build)

+ 이미지의 작성을 Dockerfile에 기술하고 그것을 자동으로 빌드하여 베이스 이미지로 지정가능

+ 같은 폴더안에 Dockerfile과 docker-compose.yml을 같이 배치

  + ```
    services:
    	webserver:
    		build: .   #피리어드로 커런트 디렉토리를 나타냄
    ```

+ 임의의 이름으로 된 Dockerfile을 빌드할때는 dockerfile을 지정

+ Dockerfile이 있는 디렉토리의 경로나 Git 레포지토리의 URL을 'context'로 지정(상대경로로 지정가능)

+ /data에 저장되어있는 'Dockerfile-alternate'라는 이름의 Dockerfile을 빌드

  + ```
    services:
    	webserver:
    		build:
    			context: /data
    			dockerfile: Dockerfile-alternate
    ```

+ 이미지 빌드 시 인수를 args로 지정가능

+ 인수값은 Docker Compose를 실행하는 머신 위에서만 유효

  + ```
    services:
    	webserver:
    		build:
    			args:
    				projectno: 1
    				user: asa
    ```



### 컨테이너 안에서 작동하는 명령 지정(command/entrypoint)

+ 컨테이너에서 작동하는 명령은 command로 지정

+ 베이스 이미지에서 지정되었을 때는 그 명령을 덮어씀

+ ```
  command: /bin/bash
  ```

+ entrypoint를 덮어쓸 수 있음

+ ```
  entrypoint:
  	-php
  	- -d
  	- memory_limit=-1
  ```



### 컨테이너 간 연결(links)

+ 다른 컨테이너에 대한 링크기능을 사용하여 연결

+ logserver라는 이름의 컨테이너와 링크시키고 싶을때

+ 또한 컨테이너명과는 별도로 앨리어스명을 붙이고 싶을때 '서비스명:앨리어스명'

+ ```
  links:
  	- logserver
  	- logserver:log01
  ```

+ 서비스간의 의존관계는 depends_on을 사용해 지정가능

```
Docker Compose에서 alias는 컨테이너 간 통신을 위해 사용되는 이름입니다. alias를 사용하면 컨테이너의 IP 주소와 포트 번호를 직접 입력하지 않고도 다른 컨테이너에 연결할 수 있습니다. 예를 들어, 웹 애플리케이션 컨테이너와 데이터베이스 컨테이너를 연결할 때, 데이터베이스 컨테이너에 "db"라는 alias를 지정하면 웹 애플리케이션 컨테이너에서는 "db"라는 이름으로 데이터베이스 컨테이너에 접근할 수 있습니다. 이를 통해 컨테이너 간의 의존성을 관리하고, 확장성을 높일 수 있습니다.
```





### 컨테이너 간 통신(ports/expose)

+ 컨테이너가 공개하는 포트는 ports로 지정(호스트머신의 포트번호: 컨테이너의 포트번호)

+ 컨테이너의 포트번호만 지정가능(이때는 호스트머신의 포트는 랜덤한 값으로 설정)

+ YAML은 XX:YY 형식을 시간으로 해석하므로 포트번호를 설정할때는""로 둘러싸서 문자열로 정의

+ ```
  ports:
  	- "3000"
  	- "8000:8000"
  	- "49100:22"
  	- "127.0.0.1:8001:8001"
  ```

+ 호스트 머신에 대한 포트는 공개하지 않고 링크기능을 사용하여 연결하는 컨테이너에게만 포트를 공개할 때는 expose 지정

+ 로그 서버와 같이 호스트 머신에서 직접 액세스 하지 않고 웹 애플리케이션 서버기능을 갖고 있는 컨테이너를 경유해서 액세스하고 싶은 경우 등

+ ```
  expose:
  	- "3000"
  	- "8000"
  ```

```
Docker Compose에서 expose는 컨테이너가 외부에 노출할 포트를 지정하는 역할을 합니다. expose를 사용하면 컨테이너 내부에서 실행 중인 프로세스가 지정한 포트에 바인딩되어 외부에서 접근할 수 있습니다. 

expose는 컨테이너를 외부 네트워크에서 보호하기 위한 보안 기능을 제공하지 않습니다. 따라서, 외부에서 접근 가능한 포트를 지정할 때는 반드시 보안을 고려하여 적절한 인증 및 암호화 방법을 사용해야 합니다.

expose는 컨테이너 간 통신을 위한 포트를 지정하는 것과는 다릅니다. 컨테이너 간 통신을 위해서는 Docker Compose에서 links 또는 networks를 사용하여 컨테이너를 연결해야 합니다.
```





### 서비스의 의존관계 정의(depends_on)

+ 여러 서비스의 의존관계를 정의할때는 depends_on 지정

+ webserver 컨테이너 시작 전 db컨테이너와 redis 컨테이너를 시작하고 싶을때 아래와 같이 작성

+ ```
  services:
  	webserver:
  		build: .
  		depends_on:
  			- db
  			- redis
      redis:
      	image: redis
      dp:
      	image: postgres
  ```

+ depends_on은 컨테이너 시작 순서만 제어할 뿐 애플리케이션이 이용 가능해질때까지 기다리고 제어하진 않음

+ 의존관계에 있는 DB 서비스의 준비가 끝날때 까지 기다리는 것은 아니기에 대책이 필요



### 컨테이너 환경변수 지정(environment/env_file)

```
#배열 형식으로 지정
environment:
	- HOGE=fuga
	- FOO

#해시 형식으로 지정
environment:
	HOGE: fuga
	FOO:
```



```
#envfile
HOGE=fuga
FOO=bar


#Docker Compose
env_file : envfile # 단 같은 폴더에 있어야함

# 여러개도 가능
env_file:
	- ./envfile1
	- ./app/envfile2
	- ./tmp/envfile3
```



### 컨테이너 정보 설정

```
#컨테이너 명 지정
container_name : web-container
```



```
#배열형식 지정
labels:
	- "com.example.description=Accounting webapp"
	- "com.example.department=Finance"
#해시형식으로 지정
labels:
	com.example.description: "Accounting webapp"
	com.example.department: "Finance"
```



### 컨테이너 데이터 관리(volumes/volumes_from)

+ 컨테이너에 볼륨을 마운트할 때는 volumes 지정

+ ````
  Docker Compose에서 volume은 호스트와 컨테이너 간 파일 공유를 위한 방법 중 하나입니다. volume을 사용하면 컨테이너에서 생성된 파일을 호스트에 저장하거나, 호스트에서 생성된 파일을 컨테이너에 마운트할 수 있습니다. 이를 통해 컨테이너의 데이터를 영속적으로 보존하고, 여러 컨테이너 간 데이터를 공유할 수 있습니다.
  
  volume은 Docker Compose에서 다음과 같이 지정할 수 있습니다.
  ```
  version: "3"
  services:
    app:
      image: myapp
      volumes:
        - /path/on/host:/path/in/container
  ```
  위 예시에서 `/path/on/host`는 호스트의 경로를, `/path/in/container`는 컨테이너의 경로를 나타냅니다. 이렇게 지정된 volume은 컨테이너가 종료되어도 보존되며, 다른 컨테이너에서도 마운트하여 사용할 수 있습니다. 또한, Docker Compose에서 지정한 volume은 `docker volume ls` 명령어를 통해 확인할 수 있습니다.
  ````



```
volumes:
	- /var/lib/mysql
	- cache/:/tmp/cache # 호스트의 디렉터리 경로 : 컨테이너 디렉터리 경로
```

```
#읽기 전용 볼륨
volumes:
	- ~/configs:/etc/configs/:ro  # 볼륨지정뒤에 ro를 지정하면 읽기전용으로 마운트
```

```
volumes_from:
	- log # 다른 컨테이너들로 부터 모든 볼륨을 마운트 할때(log라는 이름의 컨테이너로 마운트)
```



## Docker Compose를 활용한 컨테이너 운용

### 도커 컴포즈 버전 확인

```
docker-compose --version


docker-compose version 1.29.2, build 5becea4c
```



### 컴포즈 파일 지정

> 커런트 디렉토리 안에 docker-compose.yml이 찾을수 없다면 오류 발생

```
docker-compose up
ERROR:
        Can't find a suitable configuration file in this directory or any
        parent. Are you in the right directory?

        Supported filenames: docker-compose.yml, docker-compose.yaml, compose.yml, compose.yaml
```



| 서브 명령 | 설명                         |
| --------- | ---------------------------- |
| up        | 컨테이너 생성/시작           |
| ps        | 컨테이너 목록 표시           |
| logs      | 컨테이너 로그 출력           |
| run       | 컨테이너 실행                |
| start     | 컨테이너 시작                |
| stop      | 컨테이너 정지                |
| restart   | 컨테이너 재시작              |
| pause     | 컨테이너 일시정지            |
| unpause   | 컨테이너 재개                |
| port      | 공개 포트번호 표시           |
| config    | 구성확인                     |
| kill      | 실행 중인 컨테이너 강제 정지 |
| rm        | 컨테이너 삭제                |
| down      | 리소스 삭제                  |



### 파일 위치 지정해서 컨테이너 생성/시작

```
docker-compose -f ./sample/docker-compose.yml up
```



### 특정 컨테이너 조작

```
docker-compose stop webserver
```



### 여러 컨테이너 생성

```
docker-compose up [옵션] [서비스명 .]

옵션
-d : 백그라운드 실행
--no-deps : 링크 서비스를 시작하지 않음
--build : 이미지 빌드
--no-build : 이미지 빌드x
-t, --timeout : 컨테이너의 타임아웃을 초로 지정(기본 10초)
--scale SERVICE=서비스 수 : 서비스 수를 지정
```



```
services:
	server_a:
		image: nginx
    
    server_b:
    	image: redis
    	
docker-compose up --scale server_a=10 --scale server_b = 20

server_a는 10개의 컨테이너, server_b는 20개의 컨테이너가 돌아감
```



### 여러 컨테이너 확인

```
#컨테이너 상태 확인
docker-compose ps

# 컨테이너 확인
docker conatiner ls

#로그 확인
docker-compose logs
```



### 컨테이너에서 명령 실행(run)

```
docker-compose run server_a /bin/bash

server_a의 /bin/bash 실행 예

#시작 / 정지 / 재시작
docker-compose start

docker-compose stop

docker-compose restart

#특정 컨테이너만 재시작
docker-compose restart server_a
```



### 여러 컨테이너 일시 정지/재개

```
docker-compose pause

docker-compose unpause
```



### 서비스의 구성 확인

```
docker-compose port [옵션] <서비스명> <프라이빗 포트 번호>

옵션
--protocol=proto : 프로토콜, tcp or udp
--index=index : 컨테이너의 인덱스 수

# webserver 서비스의 80번 포트에 할당되어있는 설정 확인
docker-compose port webserver 80

#docker-compose 구성파일이 나옴(cat dockerfile했을때와 똑같이 나옴)
docker-compose config
```

