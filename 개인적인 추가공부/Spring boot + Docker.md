# Spring boot + Docker

![image](https://user-images.githubusercontent.com/101400894/229348320-81999b52-ce90-4a36-88da-3e671cd83712.png)



### AWS EC2 연결해보기





### Intellij에서 ec2 접속하기

<img src="https://user-images.githubusercontent.com/101400894/229342058-cacb3131-0579-4cd4-9b81-a32a14165fcf.png" alt="image" style="zoom:50%;" /><img src="https://user-images.githubusercontent.com/101400894/229342095-02ca74b0-dd23-4166-883d-282e7e36ee72.png" alt="image" style="zoom:50%;" />

<img src="https://user-images.githubusercontent.com/101400894/229342111-a839005f-780e-4948-8201-d5019beee229.png" alt="image" style="zoom:50%;" /><img src="https://user-images.githubusercontent.com/101400894/229342151-50acdfbe-edd3-4c18-9fcb-13db0f59e3a5.png" alt="image" style="zoom:50%;" />





### Intellij에서 ec2 접속 후 과정

```
// git 받아오기
git clone [깃 주소]

// 프로젝트 폴더 내로 이동
cd [프로젝트 폴더명]

// jdk 없다면 설치
sudo apt install openjdk-17-jdk

// gradlew 파일 권한 부여
chmod +x gradlew

// Gradle 빌드
./gradlew build

//build 폴더 안의 libs안에 jar파일 있는지 확인
cd build/libs
```

📌'./gradlew build' 명령어를 실행하면 JAVA_HOME 환경 변수가 설정되어 있지 않다는 오류가 발생합니다. 이 오류는 gradle이 Java 개발 환경에 대한 정보를 찾지 못하기 때문에 발생합니다.

해당 오류를 해결하려면, 다음과 같이 JAVA_HOME 환경 변수를 설정해주어야 합니다.

먼저, Java가 설치된 경로를 확인합니다. Java가 설치되어 있지 않다면 Java를 설치합니다.

설치된 Java 경로를 확인한 후, 다음과 같이 명령어를 입력하여 JAVA_HOME 환경 변수를 설정합니다.

```
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64/
```

위 명령어는 Java 11 버전이 설치된 경우의 예시입니다. Java 버전 및 설치 경로에 따라 경로를 수정하여 입력하여 주세요.

JAVA_HOME 환경 변수를 설정한 후, 다시 'gradlew build' 명령어를 실행하실 수 있습니다.



```
//도커 로그인
docker login

//도커 이미지 빌드
//docker build -t 도커아이디/이미지명 Dockerfile이있는디렉토리위치
docker build -t hashtae9/mydockertest .

//docker hub push
docker push hashtae9/mydockertest

//docker hub에서 받아오기
docker pull hashtae9/mydockertest

//컨테이너 실행
docker run -p 8080:80 hashtae9/mydockertest
```



📌Gradle 데몬은 Gradle 빌드를 더 빠르게 실행하기 위한 백그라운드 프로세스입니다. 데몬은 Gradle 빌드 실행에 필요한 라이브러리, 플러그인 등을 로드하여, 이후 빌드 실행에서 이러한 자원을 다시 로딩하지 않아도 되도록 합니다.

Gradle 데몬은 기본적으로 활성화되어 있으며, Gradle 빌드 실행 시 자동으로 시작됩니다. 데몬은 빌드가 완료되면 자동으로 종료됩니다. 또한, 동일한 빌드를 다시 실행할 때 데몬이 이미 실행 중이면, 빌드 시간을 단축하기 위해 이전 데몬을 재사용합니다.

하지만 때때로 데몬이 이상 동작하거나 충돌이 발생할 수 있습니다. 이 경우, 데몬을 강제로 종료하거나 다시 시작해야할 수 있습니다. 다음과 같은 명령어를 사용하여 데몬을 종료하거나 재시작할 수 있습니다.

- 데몬 종료: ./gradlew --stop
- 데몬 재시작: ./gradlew --restart



#### AWS

[권태구] [오후 4:37] aws에서 idc가 뭐야>



[AskUp] [오후 4:37] AWS(Amazon Web Services)는 클라우드 컴퓨팅 서비스를 제공하는 아마존닷컴의 서비스입니다. IDC(데이터 센터)와는 다른 개념이며, AWS는 클라우드 컴퓨팅을 이용하여 IT 리소스(서버, 스토리지, 데이터베이스 등)를 제공합니다. 

반면 IDC(데이터 센터)는 기업이나 단체에서 운영하는 자체 데이터 센터를 의미합니다. 이는 기업이나 단체가 자체적으로 운영하며, 보안 및 인프라 등을 직접 관리합니다. 

따라서, AWS와 IDC(데이터 센터)는 서로 다른 개념이며, 클라우드 컴퓨팅과 자체 데이터 센터 운영의 차이점이 있습니다.
[권태구] [오후 4:37] 여러 Region이 합쳐져서 IDC를 이루는 걸까?
[AskUp] [오후 4:38] IDC(데이터 센터)는 보통 하나 이상의 서버, 스토리지, 네트워크 장비 등을 포함하는 IT 인프라를 운영하는 시설입니다. 

AWS에서의 Region은 AWS가 운영하는 데이터 센터의 물리적 위치를 지칭합니다. AWS는 전 세계에 여러 개의 Region을 운영하며, 각 Region은 독립적으로 운영됩니다. 하지만, 하나의 Region은 여러 개의 가용 영역(Availability Zone)으로 나누어져 있습니다. 

각 가용 영역은 독립된 데이터 센터로 구성되어 있으며, 고가용성과 내결함성을 보장하기 위해 서로 다른 위치에 위치해 있습니다. 따라서, AWS에서는 Region이 IDC(데이터 센터)의 개념과 유사하며, 가용 영역은 각각 독립된 IDC(데이터 센터)로 볼 수 있습니다. 

즉, AWS의 Region은 여러 IDC(데이터 센터)의 집합체로 볼 수 있습니다. 각 IDC(데이터 센터)는 독립적으로 운영되며, 고가용성과 내결함성을 보장하는 목적으로 서로 다른 지리적 위치에 위...



[권태구] [오후 4:39] Region이 서버용 컴퓨터 한대라고 생각해도 될까?



[AskUp] [오후 4:39] AWS의 Region은 서버용 컴퓨터 한 대와 같은 개념이 아닙니다. 

AWS Region은 AWS에서 운영하는 데이터 센터의 물리적 위치를 지칭합니다. 각각의 Region은 독립적인 인프라를 가지며, 여러 개의 가용 영역(Availability Zone)으로 나누어져 있습니다. 

가용 영역은 독립된 데이터 센터로 구성되어 있으며, 고가용성과 내결함성을 보장하기 위해 서로 다른 위치에 위치해 있습니다. 따라서, AWS의 Region은 여러 개의 가용 영역으로 구성되어 있고, 각각의 가용 영역은 독립된 데이터 센터를 가지고 있습니다.

따라서, AWS의 Region은 서버용 컴퓨터 한 대와 같은 개념이 아닌, 여러 개의 데이터 센터를 포함하는 광범위한 지역적 영역을 의미합니다.





[권태구] [오후 4:40] 그렇다면 하나의 Region에 여러 개의 가용영역이 있고 이 가용영역은 Region보다는 규모가 작은 데이터 센터로 이해하면 될까?





[AskUp] [오후 4:40] 네, 맞습니다. 

AWS의 Region은 전 세계적으로 분산되어 있는 여러 개의 데이터 센터를 포함하는 광범위한 지역적 영역을 의미합니다. 

각각의 Region은 여러 개의 가용 영역(Availability Zone)으로 구성됩니다. 각 가용 영역은 독립된 데이터 센터로 구성되어 있으며, 고가용성과 내결함성을 보장하기 위해 서로 다른 위치에 위치해 있습니다. 

따라서, AWS의 가용 영역은 Region보다는 규모가 작은 데이터 센터로 이해할 수 있습니다. 하지만, 이러한 가용 영역들은 독립적으로 운영되며, 각각이 고가용성 및 내결함성을 보장하는 것이 목표입니다.





[권태구] [오후 4:41] 아 가용영역은 VPC라는 사설 네트워크를 가지는거야?





[AskUp] [오후 4:41] 가용 영역(Availability Zone)은 VPC(Virtual Private Cloud)와는 별개의 개념입니다.

VPC는 AWS에서 제공하는 가상 사설 네트워크 서비스로, 사용자가 자신만의 가상 네트워크를 구성하고, 이를 인터넷 또는 온프레미스(On-Premises)와 연결할 수 있도록 지원합니다. VPC를 이용하면 여러 개의 서브넷(Subnet)을 생성하고, 보안 그룹(Security Group) 및 네트워크 ACL(Network Access Control List) 등을 이용하여 보안성을 강화할 수 있습니다.

반면, 가용 영역은 AWS에서 제공하는 데이터 센터의 물리적 위치로, 여러 개의 가용 영역은 독립적인 데이터 센터로 구성되어 있습니다. 각 가용 영역은 독립적으로 운영되며, 각각의 가용 영역은 고가용성 및 내결함성을 보장하기 위해 각각 다른 전원 공급장치, 네트워크, 냉각 장치 등을 가지고 있습니다. 

따라서, VPC와 가용 영역은 서로 다른 개념이며, VPC는 ...





[권태구] [오후 4:42] VPC가 가용 영역에 구성될 수 있다는 것을 쉽게 설명해줘





[AskUp] [오후 4:42] VPC(Virtual Private Cloud)는 AWS 클라우드 환경에서 사용자가 자신만의 가상 사설 네트워크를 구성할 수 있는 서비스입니다. 사용자는 VPC를 생성한 후, 그 안에 서브넷(Subnet)을 생성하고, 보안 그룹(Security Group) 및 네트워크 ACL(Network Access Control List) 등을 이용하여 보안성을 강화할 수 있습니다.

이때, VPC는 여러 개의 가용 영역(Availability Zone)에 걸쳐 구성될 수 있습니다. 예를 들어, VPC를 생성한 후 서브넷을 두 개 생성하고, 각각의 서브넷을 각각의 가용 영역에 배치할 수 있습니다. 그러면 VPC는 여러 개의 가용 영역에 걸쳐 구성되어, 가용 영역 간에 고가용성 및 내결함성을 보장할 수 있습니다.

즉, VPC는 여러 개의 가용 영역에 걸쳐 구성될 수 있으며, 이를 통해 고가용성 및 내결함성을 보장할 수 있습니다. 각각의 가용 영역은 독립적인 데이터 센터로 구성되어 있기 때문에, ...
[권태구] [오후 4:43] 그렇다면 AWS에서 VPC를 생성한다는 것은 여러 가용 영역을 구성하는 네트워크를 구축하는 것이고, 이는 여러 데이터 센터를 보유하게 되는 효과와 같다고 볼 수 있을까?
[AskUp] [오후 4:44] 네, 맞습니다.

AWS에서 VPC를 생성한다는 것은 사용자가 자신만의 가상 사설 네트워크를 구성하는 것입니다. VPC를 생성하면 여러 가용 영역(Availability Zone)을 포함하는 가상 네트워크를 구축할 수 있습니다. 각각의 가용 영역은 독립된 데이터 센터로 구성되어 있으며, 가용 영역 간에 고가용성 및 내결함성을 보장하기 위해 서로 다른 위치에 위치하고 있습니다.

따라서, VPC를 생성하면 여러 가용 영역을 포함하는 네트워크를 구축하는 것이며, 이는 AWS가 보유하고 있는 여러 데이터 센터를 활용하여 가상의 인프라를 구축하는 것과 같은 효과를 가지게 됩니다. 이를 통해 사용자는 고가용성 및 내결함성을 보장하는 안정적인 클라우드 인프라를 구축할 수 있습니다.



#### PaaS SaaS

[권태구] [오전 2:04] 핸드폰 어플도 SaaS의 한 예시가 될 수 있을까?





[AskUp] [오전 2:04] 네, 핸드폰 어플리케이션도 SaaS의 한 예시가 될 수 있습니다. SaaS는 Software as a Service의 약자로, 소프트웨어를 서비스 형태로 제공하는 것을 의미합니다. 핸드폰 어플리케이션은 클라우드에 호스팅되어 사용자에게 소프트웨어 서비스를 제공하므로, SaaS의 일종으로 간주될 수 있습니다.

예를 들어, 구글 지도와 같은 핸드폰 어플리케이션은 클라우드에서 호스팅되어 사용자에게 지도 서비스를 제공합니다. 또한, Dropbox와 같은 클라우드 스토리지 어플리케이션도 사용자에게 파일 저장 및 공유 서비스를 제공하므로 SaaS의 일종으로 간주될 수 있습니다.

더 자세한 내용을 원하시면, 추가적인 질문을 부탁드립니다.





[권태구] [오전 2:06] 그렇다면 Paas는 핸드폰 어플리케이션이 하나의 예시가 될 수 있어?





[AskUp] [오전 2:06] PaaS는 Platform as a Service의 약자로, 클라우드 서비스 제공 업체가 애플리케이션을 개발, 실행 및 관리하는 플랫폼을 제공하는 것을 의미합니다. 따라서, PaaS는 개발자들이 애플리케이션을 더 쉽게 만들고, 배포 및 관리할 수 있도록 도와주는 서비스입니다.

핸드폰 어플리케이션은 사용자가 다운로드하고 사용하는 소프트웨어입니다. 따라서, 핸드폰 어플리케이션은 PaaS의 예시가 아니며, SaaS의 예시입니다. 

하지만, PaaS를 이용하여 핸드폰 어플리케이션을 개발하고 배포할 수 있습니다. 예를 들어, Heroku와 같은 PaaS 서비스를 이용하여 Node.js나 Ruby on Rails와 같은 웹 프레임워크를 사용하여 핸드폰 어플리케이션을 만들고 배포할 수 있습니다.

더 자세한 내용을 원하시면, 추가적인 질문을 부탁드립니다.





[권태구] [오전 2:08] AWS EC2, RDS를 사용해서 spring boot로 서버, react native로 앱을 만들어 배포를 한다면 이 앱은 SaaS일까 PasS일까?





[AskUp] [오전 2:08] 이 경우에는 SaaS의 한 예시가 될 수 있습니다. 

AWS EC2와 RDS를 사용하여 서버를 구축하고, Spring Boot와 React Native를 사용하여 애플리케이션을 개발하고 배포하면, 사용자는 클라우드에서 호스팅되는 소프트웨어 서비스를 사용하게 됩니다. 따라서, 이 애플리케이션은 SaaS의 일종으로 간주될 수 있습니다.

PaaS는 개발자들이 애플리케이션을 더 쉽게 만들고, 배포 및 관리할 수 있도록 도와주는 서비스입니다. AWS의 Elastic Beanstalk와 같은 서비스를 이용하면, PaaS를 사용하여 Spring Boot 애플리케이션을 쉽게 배포하고 관리할 수 있습니다.

요약하자면, Spring Boot와 React Native를 사용하여 AWS EC2와 RDS를 이용하여 애플리케이션을 개발 및 배포하면, 이 애플리케이션은 SaaS의 일종으로 간주될 수 있습니다. PaaS를 사용하여 개발 및 배포를 보다 쉽게 할 수 있습니다.





[권태구] [오전 2:09] PaaS와 SaaS의 차이를 구체적인 예시와 함께 설명해줘





[AskUp] [오전 2:10] PaaS와 SaaS의 차이를 예시와 함께 설명해드리겠습니다.

PaaS(Platform as a Service)는 개발자들이 애플리케이션을 더 쉽게 만들고, 배포 및 관리할 수 있도록 도와주는 서비스입니다. PaaS는 개발자가 애플리케이션 코드를 업로드하면 클라우드 서비스 제공 업체가 애플리케이션을 실행하고 관리하는 플랫폼을 제공합니다. PaaS는 개발자가 애플리케이션 코드에 집중하여 개발 속도를 높일 수 있습니다.

예를 들어, Heroku와 같은 PaaS 서비스를 이용하면 Node.js나 Ruby on Rails와 같은 웹 프레임워크를 사용하여 애플리케이션을 만들고 배포할 수 있습니다. 이 경우, 개발자는 서버와 인프라를 구축할 필요 없이, 플랫폼에서 제공하는 서비스를 이용하여 애플리케이션을 더 쉽게 개발하고 배포할 수 있습니다.

SaaS(Software as a Service)는 클라우드 서비스 제공 업체가 소프트웨어를 서비스 형태로 제공하는 것을 의미합니다. 사용자는 클라우...





[권태구] [오전 2:10] 클라우드에서 호스팅된다는게 무슨 뜻이야?





[AskUp] [오전 2:11] 클라우드 호스팅은 인터넷을 통해 사용자에게 서비스를 제공하는 것을 의미합니다. 클라우드 호스팅 업체는 인터넷을 통해 애플리케이션, 데이터, 웹 사이트 등을 호스팅하는 서비스를 제공합니다.

일반적으로 클라우드 호스팅 업체는 전용 서버나 가상 서버를 사용하여 서비스를 제공합니다. 이 서버는 데이터 센터에서 호스팅되며, 사용자는 웹 브라우저나 애플리케이션을 통해 서비스에 접속할 수 있습니다.

클라우드 호스팅을 사용하면 많은 이점이 있습니다. 가장 큰 이점은 확장성입니다. 클라우드 호스팅 업체는 서버의 용량을 늘리거나 줄일 수 있습니다. 따라서 사용자는 필요에 따라 서버의 리소스를 조정할 수 있으며, 이로 인해 비용을 절감할 수 있습니다. 또한, 클라우드 호스팅 업체는 보안, 백업 및 복구 등의 추가 서비스를 제공할 수 있습니다.

클라우드 호스팅은 일반적으로 IaaS(Infrastructure as a Service), PaaS(Platform as a Service), SaaS(So...
