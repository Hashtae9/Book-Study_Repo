## Docker 명령어



### 도커 버전

```
docker -v
docker version

Docker는 클라/서버 아키텍쳐 채택, Docker 클라와 Docker 서버가 Remote API를 경유하여 연결(서버에서 처리)
```



### 도커 실행 환경 확인

```
docker system info
```



### 도커 디스크 이용 현황 확인

```
docker system df
```



### 도커 이미지 검색

```
docker search 찾고싶은 이미지(ex ubuntu)
```



### 원하는 이미지 다운

```
docker image pull 옵션 이미지명[:태그명]

docker (image) pull ubuntu:18.04   (이미지명:태그명)

이미지 확인
docker image ls [옵션] [리포지토리명]

옵션
-a : 모든 태그 받아오기
--digests : 다이제스트를 표시할지 말지
--no-trunc : 결과를 모두 표시
--quiet, -q : Docker 이미지 ID만 표시
```



### 도커 컨테이너 정지

```
docker stop 특정컨테이너
```



### 도커 컨테이너 작동 확인

```
=> nginx 서버 상태 확인(ps는 컨테이너 리스트를 반환)
docker container ps

=> 특정 컨테이너 가동 확인
docker container stats webserver
```



### 도커 컨테이너 생성 및 실행

```
docker run -d -p 80:80 docker/getting-started
docker run -it --name 컨테이너명 이미지명+tag /bin/bash

-d : detachedd 모드(백그라운드에서 실행, 분리모드로 컨테이너 실행)
-p 80:80 : 호스트의 포트 80을 컨테이너 포트 80와 매핑
docker/getting-started
```



### 도커 컨테이너 어떤게 있는지 확인

```
docker ps -a
```



### 뒤에 붙는 말들

+ -a, --all=false : 모든 이미지 표시
+ --digests=false : digest 표시
+ --no-trunc=false : 모든 결과 표시
+ -q, -quiet=false : Docker 이미지 id만 표시



### 도커의 이미지 목록

```
docker images
docker image ls [옵션] [리포지토리명]
```

+ Repository : Docker 이미지명
+ Tag : Docker 이미지 태그명
+ IMAGE ID : 도커 이미지 ID
+ created : 생성일
+ virtual size : 사이즈



**📌이미지 위장 변조 막기**

+ export DOCKER_CONTENT_TRUST=1
  + DCT 기능 유효화
    + 이미지 업로드 전 로컬 환경에서 이미지 작성자의 비밀키를 사용하여 이미지 서명
    + 서명이 된 이미지를 다운로드 할 때 이미지 작성자의 공개키를 사용해 이미지가 진짜인지 아닌지 확인



### 이미지 세부정보 확인

```
docker image inspect [옵션] <컨테이너 또는 이미지 이름, ID>

-결과
C:\Users\LG>docker inspect ubuntu
[
    {
        "Id": "sha256:74f2314a03de34a0a2d552b805411fc9553a02ea71c1291b815b2f645f565683",
        "RepoTags": [
            "ubuntu:latest"
        ],
        "RepoDigests": [
            "ubuntu@sha256:2adf22367284330af9f832ffefb717c78239f6251d9d0f58de50b86229ed1427"
        ],
        "Parent": "",
        "Comment": "",
        "Created": "2023-03-01T04:38:49.239257335Z",
        "Container": "298f60554671ae2f5bf43b9892526aaa221e8093c9cee1ca68ef65fc3ac67600",
        "ContainerConfig": {
            "Hostname": "298f60554671",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/sh",
                "-c",
                "#(nop) ",
                "CMD [\"/bin/bash\"]"
            ],
            "Image": "sha256:6088cf91777e3b0190e579c7c7cab9c65626f5ff625373bcdb02ae877a9118d8",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {
                "org.opencontainers.image.ref.name": "ubuntu",
                "org.opencontainers.image.version": "22.04"
            }
        },
        "DockerVersion": "20.10.12",
        "Author": "",
        "Config": {
            "Hostname": "",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/bash"
            ],
            "Image": "sha256:6088cf91777e3b0190e579c7c7cab9c65626f5ff625373bcdb02ae877a9118d8",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {
                "org.opencontainers.image.ref.name": "ubuntu",
                "org.opencontainers.image.version": "22.04"
            }
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 77810712,
        "VirtualSize": 77810712,
        "GraphDriver": {
            "Data": {
                "MergedDir": "/var/lib/docker/overlay2/1f7e2723b9851109e2bfa206bc902a6cb145ade1575229cf3eb13699087e2423/merged",
                "UpperDir": "/var/lib/docker/overlay2/1f7e2723b9851109e2bfa206bc902a6cb145ade1575229cf3eb13699087e2423/diff",
                "WorkDir": "/var/lib/docker/overlay2/1f7e2723b9851109e2bfa206bc902a6cb145ade1575229cf3eb13699087e2423/work"
            },
            "Name": "overlay2"
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:202fe64c3ce39b94d8beda7d7506ccdfcf7a59f02f17c915078e4c62b5c2ed11"
            ]
        },
        "Metadata": {
            "LastTagTime": "0001-01-01T00:00:00Z"
        }
    }
]
```

+ 이미지 id
+ 생성일
+ Docker 버전
+ 이미지 생성자
+ cpu



```
docker inspect --format="{{ .Os}}" ubuntu
해당 이미지의 os 찾기
```



### 이미지 태그 설정(docker tag)

```
<Docker Hub 사용자명>/이미지명:[태그명]

docker tag 이미지 사용자명/이미지명
=> 태그 설정
```



### 도커 이미지 삭제

```
docker rmi [옵션] <이미지명>

-f, --force=false : 이미지 강제 삭제
--no-prune=false : 태그가 없는 부모 이미지를 삭제하지 않음
```



### 도커 허브 로그인 & 로그아웃

```
docker login [옵션][서버명]

-u,--username="" 사용자명
-p,--password="" 페스워드
-e,--email="" 이메일주소

docker logout [서버명]
```



### 이미지 업로드

```
docker push <이미지명>[:태그명]

도커 허브에 업로드시 이미지명 양식
<Docker Hub 사용자명>/이미지명:[태그명]
```



### 이미지 삭제

```
docker image rm [옵션] 이미지명 [이미지명]

옵션
--force, -f : 이미지를 강제로 삭제
--no-prune : 중간 이미지를 삭제하지 않음


사용하지 않는 이미지 삭제
docker image prune [옵션]

옵션
--all, -a : 사용하지 않은 이미지를 모두 삭제
--force, -f : 이미지를 강제로 삭제
```







## Docker 컨테이너 생성 구동 중지

+ 이미지가 생성되면 이미지를 기반으로 컨테이너를 생성



### 컨테이너 라이프 사이클

![image](https://user-images.githubusercontent.com/101400894/222661330-f5e7d20f-da31-4c35-a4bb-24ef5d5ab29d.png)



#### 컨테이너 생성

<img src="https://user-images.githubusercontent.com/101400894/222661872-8743f980-04a8-4167-b9b4-70b03322b995.png" alt="image" style="zoom:67%;" />

+ 이미지 : 'Docker에서 서버를 동작시키기 위해 필요한 디렉터리 및 파일의 집합'
+ 즉, 리눅스동작에 필요한 /etc와 /bin등의 디렉터리 및 파일의 집합
+ docker create 커맨드 실행 시 이미지에 포함된 linux 디렉터리 및 파일 집합의 스냅샷을 만듦
  + 스냅샷 : 특정 시간에 스토리지 내부에 존재하는 파일과 디렉터리를 저장한 것

+ 컨테이너 시작할 준비

```
docker container create
```



#### 컨테이너 확인

```
docker container ls [옵션]

옵션
-all, -a : 모든 컨테이너 표시
--filter, -f : 표시할 컨테이너의 필터링
--format : 표시 포맷을 지정
--last, -n : 마지막으로 실행된 n건의 컨테이너만 표시
--latest, -l : 마지막으로 실행된 컨테이너만 표시
--no-trunc : 정보를 생략하지 않고 표시
--quiet, -q : 컨테이너 id만 표시
--size, -s : 파일 크기 표시

컨테이너 세부정보
docker container inspect
```



#### 컨테이너 생성 및 시작

<img src="https://user-images.githubusercontent.com/101400894/222662219-96763705-1d91-4c79-8439-cc6805eda40f.png" alt="image" style="zoom:67%;" />

+ 이미지에서 컨테이너를 생성하여 컨테이너상에서 프로세스 구동
+ 포트번호 등 네트워크 설정을 통해 외부에서 컨테이너 프로세스에 액세스 가능

```
docker container run [옵션] 이미지명[:태그명] [인수]

옵션
-attach, -a : 표준입력, 표준출력, 표준오류출력에 어태치
--cidfile : 컨테이너 ID를 파일로 출력
--detach, -d : 컨테이너를 생성하고 백그라운드에서 실행
--interactive, -I : 컨테이너의 표준 입력을 염
--tty, -t : 단말기 디바이스를 사용

예시
docker container run -it --name "test1" centos /bin/cal

centos라는 이름의 이미지를 바탕으로 test1이라는 이름의 컨테이너 실행
컨테이너 안에서는 /bin/cal 명령 실행(리눅스 표준명령으로 달력을 콘솔에 표시)
-i : 컨테이너의 표준 출력을 연다
-t : tty(단말 디바이스)를 확보

예시
docker container run -it --name "test2" centos /bin/bash

컨테이너 안에서 쉘 실행

예시
docker container run -d centos /bin/ping localhost

centos라는 이름의 이미지를 바탕으로 컨테이너 생성, localhost에 대해 ping 명령 실행
-d : 백그라운드 실행

------------------------------------------------------------
restart 옵션

no : 재시작하지 않음
on-failure : 종료 스테이터스가 0이 아닐 때 재시작
on-failure:횟수n : 종료 스테이터스가 0이 아닐 때 n번 재시작
always : 항상 재시작
unless-stopped : 최근 컨테이너가 정지상태가 아니라면 항상 재시작

예시
docker container run -it --restart=always centos /bin/bash

--rm옵션과 --restart 옵션은 동시에 못씀

--------------------------------------------------------------------
docker container run [네트워크 옵션] 이미지명[:태그명] [인수]

네트워크 옵션
--add-host = [호스트명:IP주소]              		컨테이너의 /etc/hosts에 호스트명과 IP주소를 정의
--dns=[IP주소]                             					컨테이너용 DNS 서버의 IP주소 지정
--expose                                  						지정한 범위의 포트 번호를 할당
--max-address=[MAC 주소]                   						   컨테이너의 MAC 주소 지정
--net = [bridge|none|container:<name|id> | host | NETWORK]           컨테이너 네트워크를 지정
--hostname, -h                                                   컨테이너 자신의 호스트명 지정
--publish, -p[호스트의 포트번호]:[컨테이너의 포트번호]                  호스트와 컨테이너의 포트 매핑
--publish-all, -P   									  호스트의 임의의 포트를 컨테이너에 할당

예시
docker container run -d -p 8080:80 nginx

nginx라는 이름의 이미지를 바탕으로 컨테이너 생성, 백그라운드에서 실행
이때 호스트의 8080과 컨테이너 포트 80을 매핑(호스트의 8080포트에 액세스하면 컨테이너의 Ngnix 80번포트와 액세스)
지정한 범위로 포트번호를 할당하고싶다면 --expose
호스트 머신의 임의의 포트를 할당할 때는 -P

예시
docker container run -d --dns 192.168.1.1 nginx

dns를 192.168.1.1로 지정

예시
docker container run -d --mac-address="92:d0:c6:0a:29:33"

예시
docker container run -it --hostname www.test.com --add-host node1.test.com:192.168.1.1 centos

호스트명 : www.test.com과 node1.test.com(192.168.1.1)로 정의
-----------------------------------------------------------------------------
docker container run [자원 옵션] 이미지명[:태그명] [인수]

--cpu-shares, -c : CPU의 사용 배분(비율)
--memory, -m : 사용할 메모리를 제한하여 실행
--volume=[호스트의 디렉토리]:[컨테이너의 디렉토리], -v : 호스트와 컨테이너의 디렉토리를 공유

예시
docker container run --cpu-shares=512 --memory=1g centos

cpu 시간을 512로 설정
--------------------------------------------------------------------------------
docker container run [환경설정 옵션] 이미지명[:태그명] [인수]

--env=[환경변수], -e : 환경변수 설정
--env-file=[파일명] : 환경변수를 파일로 부터 설정
--read-only=[true | false] : 컨테이너의 파일 시스템을 읽기 전용으로 만듦
--workdir=[패스], -w : 컨테이너의 작업 디렉토리를 지정
-u, --user=[사용자명] : 사용자명 또는 UID를 지정
```

📌 **프롬프트**

+ 명령을 입력할 수 있는 표시

+ [$] 마크가 프롬프트

+ ```
  docker@default:~$
  
  사용자명@호스트명:작업디렉토리 사용자권한
  ~ : 작업하고 있는 사용자 홈디렉터리
  일반사용자 : $
  루트사용자 : #
  ```



#### 컨테이너 로그 확인

```
docker container logs [옵션] 이미지명

-t : 타임스탬프를 표시
```



#### 컨테이너 기동 확인

```
docker container stats [컨테이너 식별자]
```







#### **컨테이너 시작(docker container start 명령)**
+ 정지 중인 컨테이너를 시작할 때 사용합니다. 
+ 컨테이너에 할당된 컨테이너 식별자를 지정하여 컨테이너를 시작합니다.

```
docker container start [옵션] <컨테이너 식별자> [컨테이너 식별자]

옵션
--attach, -a : 표준 출력, 표준오류 출력을 염
--interactive, -l : 컨테이너 표준 입력을 염
```





#### **컨테이너 정지(docker container stop 명령)**

+ 실행 중인 컨테이너를 정지시킬 때 사용합니다. 컨테이너에 할당된 컨테이너 식별자를 지정하여 컨테이너를 정지합니다. 또한 컨테이너를 삭제할 때는 docker container stop 명령을 사용하여 실행 중인 컨테이너를 정지시켜 둘 필요가 있습니다. 컨테이너를 재시작하고 싶을 때는 docker container restart 명령을 사용합니다.

```
docker container stop [옵션] <컨테이너 식별자> [컨테이너 식별자]

--time, -t : 컨테이너의 재시작 시간을 지정(기본값 10초)
```





#### **컨테이너 삭제(docker container rm 명령)**

+ 컨테이너를 삭제할 때 사용합니다. docker container rm 명령을 사용하여 정지 중인 컨테이너 프로세스를 삭제합니다.
+ 그 외에도 컨테이너의 상태를 확인하기 위한 docker container ps 명령이나 일시 정지를 하는 docker container pause 명령 등이 있습니다.

```
docker container rm [옵션] <컨테이너 식별자> [컨테이너 식별자]: 컨테이너 지우기

옵션
--force, -f : 실행중인 컨테이너 강제로 삭제
--volumes, -v : 할당한 볼륨 삭제

docker container ps : 컨테이너 상태확인

docker container pause : 일시정지
```



### 컨테이너 네트워크

#### 도커 컨테이너 네트워크 목록 표시

```
docker network ls [옵션]

옵션
-f, --filter=[] : 출력을 필터링
--no-trunc : 상세 정보 출력
-q, --quiet : 네트워크 ID만 표시

예시
docker network ls -q --filter driver = bridge
```



#### 네트워크 작성

```
docker network create [옵션] 네트워크

옵션
--driver, -d : 네트워크 브리지 또는 오버레이
--ip-range : 컨테이너에 할당하는 IP 주소의 범위 지정
--subnet : 서브넷을 CIDR 형식으로 지정
--ipv6 : IPv6 네트워크를 유효화할지 말지(true/false)
-label : 네트워크에 설정하는 라벨

예시
docker network create --driver=bridge web-network
```

