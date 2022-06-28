# CI/CD 란?

- CI

CI는 지속적 통합(Continuous Integration)으로,
모든 개발이 끝난 이후에 코드 품질을 관리하는 고전적 방식의 단점을 해소하기위해 나타난 개념이다.
말그대로 개발을 하면서 ‘코드에대한 통합’을 ‘지속적’으로 진행함으로써 품질을 유지하자는 것이다.

조금은 극단적인 예를 들어보자.
10명의 개발자가 참여하는 프로젝트가 있다고 가정해보자.
git에 기본 틀이 잡혀있는 코드가 올라와있고, 각 개발자가 자신의 로컬환경에 clone 받아서 작업을 시작한다.
그런데 개발이 끝날때까지 모든 개발자가 한 번도 중앙저장소에 코드를 올리지 않았고,
개발이 끝난 이후에 10명의 개발자의 코드를 한 번에 통합해야하는 상황이라면?
상상만해도 끔찍하니 더 말하진 않겠다.

적절한 예시일지 모르겠지만, 이해를 돕기위해 다른 예를 들어보자.
건물을 전부 다 지어놓고 마지막에 다시 돈을들여 대규모 보수공사를 하는 것보다,
층을 하나씩 쌓을때마다 올바르게 지어지고있는지 체크해주는것이 질적, 비용적 측면에서 모두 유리할 것이다.
햄버거를 다 만들어놓고 모든 재료가 제대로 들어갔는지, 유통기한이 지나지 않았는지 확인하는 것보다,
재료 하나를 올릴때마다 유통기한이나 재료의 양 등을 체크하는게 더욱 유리한 것처럼 말이다.

그렇다면 지속적 통합을 이루기 위해서는 어떻게 해야할까?
첫 번째 예제의 상황에서, 이런 규칙을 정하면 어떨까?

1. 모든 개발자는 퇴근하기 전에 자신의 코드를 중앙 코드와 통합한다.
2. 통합된 코드에서 본인의 코드가 제대로 동작하는지 테스트한다.
3. 통합된 코드가 제대로 빌드되는지 테스트한다.
4. 결과를 정리하고. 버그가 있다면 다음날 업무 목록에 적어둔다.

쉽게 말하면, 매일 퇴근하기 전에 git에 코드를 올리고 문제가 없는지 테스트하라는 것이다.
이러한 과정이 프로젝트 시작부터 종료까지 잘 지켜진다면 코드의 품질을 어느정도는 유지할 수 있을 것 같다.
그리고 막판에가서 모든 개발자의 코드를 통합하겠다고 난리법석(?)을 떨지 않아도 될 것 같다.

근데 왜 “~하다.” 라고 표현하지 않고, “~ 것 같다.” 라고 표현했을까?
이 방식은 개념만 놓고보면 아주 이상적으로 보인다.
하지만 CI의 단점이 있는데, 이미 눈치챈 사람도 있겠지만 ‘너무 귀찮다’는 것이다.
git에 코드를 올리는 것 까지는 그렇다고 쳐도,
코드가 커질수록 테스트 양은 물론이거니와 테스트 시간도 점점 길어질 것이다.
게다가 이것은 굳이 사람이 일일이 돌리지 않아도 되는 매우 지루한 반복 작업이다.

이렇게 되면 어떨까?

git에 코드만 올려놓으면 알아서 테스트와 빌드를 수행하고,
그 결과를 잘 정리해 개발자에게 자동으로 알려주는 프로그램이 있다면 좋지 않을까?
그렇기에 CI를 설명할때 항상 자동화라는 키워드가 따라다니는 것이다.

그럼 CI 자동화가 잘 이루어졌을때, 위의 규칙이 얼마나 단순화되는지 확인해보자.
1. 모든 개발자는 퇴근하기 전에 자신의 코드를 중앙 코드와 통합한다.
2. 다음날 출근시 메일로 발송된 결과 리포트를 확인하고 버그가 있으면 수정한다.
테스트나 빌드등 복잡한 절차가 모두 생략되고,
그냥 퇴근전에 코드를 git에 올리고 가면 되는 것이다.
이정도의 의지도 없다면 사실상 CI를 통한 코드 품질 개선 의지가 없다고 보는게 맞다.

- CD

그렇다면 CI/CD에서 CD는 무엇일까?
CD란 지속적 배포(Continuous Deploy 또는 Delivery)로써,
소프트웨어가 항상 신뢰 가능한 수준에서 배포될 수 있도록 지속적으로 관리하자는 개념이다.

사실 어려울 것 없이 그냥 CI의 연장선으로 생각하면 된다.
배포 이전에 테스트와 빌드는 필수적이기 때문에,
사실상 CD가 되려면 항상 CI가 선행되어야 한다고 봐도 무방하다.

즉, CI 프로세스를 통해 개발중에 지속적으로 빌드와 테스트를 진행하고,
이를 통과한 코드에 대하여 테스트서버와 운영서버에 곧바로 그 내용을 배포해 반영하는 것이다.
이상적인 환경이라면 테스트와 빌드가 ‘지속적’으로 이루어지기 때문에,
배포 또한 자연스럽게 ‘지속적’으로 이루어지게 된다.

사실상,
CI = 빌드 및 테스트 자동화
CD = 배포 자동화
라고 기억해도 무방하다.

중요한 것은,
코드 품질관리에 있어서 CI/CD 자동화가 ‘왜’ 필요하며,
이러한 시스템을 구축하는 것이 ‘왜’ 중요한지에 대해 이해하는 것이다.

# 젠킨스

서버에 기능을 추가 하려면 개발자가 개발자 노트북에서 개발을 하고 테스트까지 한 다음에 이상이 없으면 사용자가 사용할 수 있게 수정된 내용을 서버에 반영해야 한다.

## Build란?

빌드는 `서버에 올릴 수 있는 상태로 만드는 것`을 빌드라고 한다.
서버에 올려서 `사용자가 사용 할 수 있게 하는 것`은 배포(Deploy)라고 한다.

## Build를 자동화 해야하는 이유

빌드는 하루에 한번을 할 수도 있고 안할수도 있지만 1주일, 1달로 따지면 꽤 많이 한다. 그리고 이게 1년이면 꽤 많은 시간이라고 할 수 있다.
예를들면 옛날에는 자바를 빌드 할 때 javac라는 커맨드를 직접 사용 했지만 지금은 IDEA를 쓰면 main()메소드를 실행하면 javac를 하고 java가 실행이 된다.
이렇게 반복되는 과정은 버튼 하나 또는 단축키로 자동화 시킬 필요가 있다.
왜냐하면 이 작업을 하는데도 집중력, 긴장감 등이 소모 되기 때문이다. 그리고 빌드는 시간이 꽤 걸리는 작업인데(30초 이상 걸림) 빌드를 실행 시키고 나서 빌드가 될 때까지 기다리는 시간도 모아보면 엄청 길 것이다.
개발자의 시간은 소중하기 때문에 최대한 반복작업은 자동화 할 필요가 있다.
수정하고 빌드하고 dev에 올리고 하는데 너무 시간을 많이 잡아먹기 때문이다.

## Jenkins란?

위에서 이야기한 빌드를 자동화 해주는 툴이다.
Jenkins는 빌드를 자동화 시키기 위해 사용한다.

1. 대쉬보드 제공
- 여러가지 배포 작업의 상황을 모니터링 할 수 있음

2. 배포 스크립트를 실행해주기
- 배포 스크립트를 개발자 로컬에서도 실행 할 수 있는데 젠킨스라는 프로그램을 띄워놓으면 걔가 스케쥴링을 해줌

젠킨스를 통해 지속적인 통합 (CI: Continuous Integration)을 행할 수 있다.

# Jenkins 설치 & Gradle

Jenkins 는 Java 8 and 11 에서 동작하므로 두버전 중 하나가 있어야 합니다.

http://mirrors.jenkins-ci.org/osx-stable/
주소에서 Jenkins 설치 파일을 다운로드 받아 설치하면 localhost:8080 으로 구동됩니다.

설치가 왼료되면 프로젝트를 생성하기 전에

1. 관련 플러그인 다운로드
  - Jenkins 관리 => 플러그인 관리 에서 가능
    : Gradle Plugin
    : Post build task Plugin => 빌드로그를 판단해 batch/shell 를 실행하는 플러그인

Jenkins 관리 => 플러그인 관리 에 들어갑니다.
설치가능에 검색하여 설치합니다.

2. 툴 관리에서 Gradle 등록 
  - Jenkins 관리 => Global Tool Configuration 이동
  - Gradle 등록

제가 설치한 서버는 Gradle 4.9 를 설치했습니다.
그래서 GRADLE_HOME 에 설치위치를 등록합니다.
그리고 install automatically 의 체크를 해제합니다.

3. 빌드할 아이템 등록

대시보드로 이동한 후에 새로운 Item 을 클릭하여 생성합니다.
Item 이름을 입력하고 Freestyle project를 선택한 후 하단에 OK를 누릅니다.

소스 코드 관리에서 Git 서버에 올린 코드주소를 입력합니다.

그리고 Credentials 를 등록해야 하는데 ADD버튼을 눌러 등록을 합니다.
Git 자신의 계정 Username 과 Password를 입력하여 계정등록을 해둡니다.

Build 에서는 Invoke Gradle를 체크한 후 위에서 등록한 Gradle 버전을 등록합니다.
Task 에는

> --project-dir=/Users/kimminseok/git-repository/jjunpro-portfolio-ecommerce/project bootJar --stacktrace

등록합니다.

--project-dir 는 프로젝트 root 경로입니다.

mac 의 경우 jenkins 권한이 root 폴더 변경 권한이 없으므로 project 폴더의 권한 수정을 해줘야합니다.

> sudo chmod -R 777 /Users/kimminseok/git-repository/jjunpro-portfolio-ecommerce/project

빌드 후에 shell 입력을 통해 실행되도록 할 것입니다.
빌드 후 조치 에서 '빌드 후 조치 추가'를 클릭하면  위에서 설치한 'Post build task'이 있습니다.
클릭해서 Log text 에는 BUILD SUCCESSFUL  를 입력합니다.
빌드에 실패했는데 서버를 다시 띄우면 위험하니 꼭 성공한 후에만 실행하도록 합니다.

그리고 스크립트 내용에는 다음을 추가합니다.

> nohup java -jar build/libs/[jar이름] &

이제 모든설정이 끝났습니다. 
생성한 아이템으로 들어가서 Build Now 를 클릭해 실행합니다.

# Docker Install

~~~
sudo su
yum update -y
yum install docker -y
service docker start
systemctl status docker.service
~~~

# Jenkins Docker 설치 - AWS Linux 환경
~~~
docker pull jenkins/jenkins:lts

docker run --name jenkins 
-d 
--restart always 
-p 8081:8080
-p 50000:50000 
-e TZ=Asia/Seoul  
-v $PWD/jenkins_home:/var/jenkins_home
-u root 
-v /var/run/docker.sock:/var/run/docker.sock  
-v /usr/bin/docker:/usr/bin/docker 
jenkins/jenkins
~~~

# Jenkins Docker 설치 - Oracle Linux 환경
~~~
1. 설치에 필요한 패키지를 설치하고 리포지토리를 추가한다.
dnf install -y dnf-utils zip unzip
dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo

2. 도커를 설치한다.
dnf remove -y runc
dnf install -y docker-ce --nobest

3. 도커 서비스를 시작한다.
systemctl enable docker.service
systemctl start docker.service
~~~

## 만약 설치 오류생기면 jenkins 최신 버전으로 Update

~~~
docker exec -it -u 0 jenkins bash
apt-get update
apt-get install wget
wget http://updates.jenkins-ci.org/download/war/${newVersion}/jenkins.war
mv ./jenkins.war /usr/share/jenkins/
chown jenkins:jenkins /usr/share/jenkins/jenkins.war
exit
~~~

## 실행 포트 확인

> netstat -antp

# Git WebHook 연동

Jenkins와 Github을 연동하기 위해 Github Access Token을 생성합니다.
우측 상단 초상화 클릭
Settings 선택
Developer settings 선택
Personal access tokens 선택
Generate new token 선택
이름 입력 (ex: Jenkins-Local)
Select scopes - repo, admin:repo_hook 선택
Generate token 선택
생성한 토큰 복사 (복사 아이콘 선택)

Jenkins에서 방금 생성한 Token을 등록합니다.
Manage Jenkins 선택
Manage Credentials 선택
global 선택
Add credentials 선택
Kind - Secret text 선택
Secret - Secret 입력 (1.1에서 복사한 토큰 붙여넣기)
ID - GitHub ID 입력
OK 선택

연동
Manage Jenkins 선택
Configure System 선택
Add GitHub Server 선택
Name - GitHub ID 입력
Credentials - 1.2에서 생성한 Credentials 선택
Test Connection 선택 - 정상적으로 연결 됐는지 확인
Manage hooks 선택 (Checked)
Save 선택

연동할 Github repository 접속
Settings 선택
Webhooks 선택
Add webhook 선택

Payload URL 입력 - 2.1에서 복사한 주소 + /github-webhook/ 추가
Content type - application/json 선택
Add webhook 추가

https://www.comtec.kr/2021/07/22/jenkins-webhook-설정/ 참고

# Node 프로젝트

## 플러그인 설치 항목

NodeJS
Maven IntegrationVersion
Publish Over SSHVersion
GIT serverVersion

## Node JS 플러그인 설치

Jenkins 관리 -> Plugin Manager (플러그인 관리) -> 설치 가능 -> Nodejs
Global Tool Configuration -> NodeJS Add

# SSH Over 플로그인 설치

Jenkins 관리 -> Plugin Manager (플러그인 관리) -> 설치 가능 -> publish over ssh

# Git SSH 연결하기 위한 작업

~~~
sudo mkdir $PWD/jenkins_home/.ssh
sudo chmod 700 $PWD/jenkins_home/.ssh
sudo ssh-keygen -t rsa
cat $PWD/jenkins_home/.ssh/id_rsa.pub

$PWD/jenkins_home/.ssh/id_rsa
/home/ec2-user/jenkins_home/.ssh/id_rsa
~~~
값 복사 후 git ssh 에 등록
https://github.com/settings/keys

# Publish over SSH 설정

Jenkins 홈페이지 구성 설정에 [Publish over SSH] -> [SSH Servers] 설정

Key : ec2 혹은 접근하는 pem 키 등록

보안그룹에 22 포트로 연결 해주어야 합니다.

Name : [프로젝트 명]
Hostname : ec2 ip 주소
Username : ec2-user

# 새로운 EC2 에 Nginx Docker 설치

실 서버 EC2
~~~
docker pull nginx

docker run --name ${name}
-d 
--restart always 
-p 80:80
-v $PWD:/usr/share/nginx/html nginx
~~~

vim 설치 & UTF-8 설정
~~~
docker exec -it nginx /bin/bash
apt-get update
apt-get install vim nano -y

vim /etc/vim/vimrc
set encoding=utf-8
set fileencodings=utf-8,cp949
~~~

Nginx 커스텀 설정파일 적용
~~~
cp /etc/nginx/nginx.conf /etc/nginx/nginx.conf.back
vim /etc/nginx/conf.d/nginx.http.conf
~~~

> nginx.http.conf
~~~
server {
    listen       80;
    listen       [::]:80;

    root /usr/share/nginx/html/client/build;
    location / {
            try_files $uri /index.html;
    }

    server_name  chat.neodigm.com;
    return 301   https://$host$request_uri;

    error_page 404 /404.html;
    location = /404.html {
    }

    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
    }
}
~~~

~~~
vim /etc/nginx/conf.d/nginx.https.conf
~~~

> nginx.https.conf
~~~
# Settings for a TLS enabled server.
server {
    listen       443 ssl http2;
    listen       [::]:443 ssl http2;
    server_name  chat.neodigm.com;
    client_max_body_size 16M;

    ssl_protocols           TLSv1.2;
    ssl_certificate         "/usr/share/nginx/html/ssl/ssl-bundle.crt";
    ssl_certificate_key     "/usr/share/nginx/html/ssl/private.key";
    ssl_session_cache       shared:SSL:1m;
    ssl_session_timeout     10m;
    ssl_prefer_server_ciphers on;
    ssl_ciphers "ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384";

    proxy_cache off;
    proxy_store off;

    root /usr/share/nginx/html/client/build;
    index index.html index.htm;

    location / {
            try_files $uri $uri/ /index.html;
    }

    location /api {
            proxy_pass              https://localhost:8443;

            #proxy_redirect          http://localhost:3000 https://localhost:3000;
            proxy_set_header        Host                    $host;
            proxy_set_header        X-Real-IP               $remote_addr;
            proxy_set_header        X-Forwarded-Host        $host;
            proxy_set_header        X-Forwarded-Server      $host;
            proxy_set_header        X-Forwarded-For         $proxy_add_x_forwarded_for;
            proxy_set_header        X-NginX-Proxy true;

            # For WebSocket upgrade header
            proxy_http_version      1.1;
            proxy_set_header        Upgrade $http_upgrade;
            proxy_set_header        Connection "upgrade";

            # set all cookies to secure
            #proxy_cookie_path / "/; secure; SameSite=None";

            aio threads=default;
    }

    error_page 404 /404.html;
        location = /40x.html {
    }

    error_page 500 502 503 504 /50x.html;
        location = /50x.html {
    }
}
~~~

exit

만든 도커 이미지 화 하기

> docker commit nginx nginx_base

## Item 생성

GitHub project -> Project url -> https://github.com/alalstjr

### 그후 젠킨스 SSH Token 등록

소스 코드 관리 -> Repositories -> Repository URL -> git@github.com:alalstjr/neodigm-websocket-client.git
Credentials -> Add Credentials -> Private Key -> Enter directly

### 아래 경로의 Key 입력

cat /home/jenkins/.ssh/id_rsa

Check -> GitHub hook trigger for GITScm polling
Check -> Provide Node & npm bin/ folder to PATH

Build -> execute shell -> npm install -> npm run build

## 프로젝트 실행중인 EC2 Nginx Docker SH 파일 생성

vim docker.sh
~~~
#!/bin/bash
# Build N Run DB Container
# 2020. 09. 18 Zini

docker_username="nginx_c"
db_image_name="nginx_base"
db_container_name="nginx_base"
version="1.0.0"
port=80

echo "## Automation docker-database build and run ##"

# remove container
echo "=> Remove previous container..."
# docker rm -f ${db_container_name}
docker rm -f ${docker_username}

# remove image
# echo "=> Remove previous image..."
# docker rmi -f ${docker_username}/${db_image_name}:${version}

# new-build/re-build docker image
# echo "=> Build new image..."
# docker build --tag ${docker_username}/${db_image_name}:${version} .

# Run container
echo "=> Run container..."
docker run --name ${docker_username} -d --restart always -p ${port}:${port} -v $PWD:/usr/share/nginx/html ${db_container_name}
~~~
sudo chmod 755 ./docker.sh
./docker.sh 으로 실행

# 새로운 EC2 에 Nginx 설치

> sudo amazon-linux-extras install nginx1 -y
> cp /etc/nginx/nginx.conf /etc/nginx/nginx.conf.back
> vim /etc/nginx/nginx.conf

~~~
# For more information on configuration, see:
#   * Official English Documentation: http://nginx.org/en/docs/
#   * Official Russian Documentation: http://nginx.org/ru/docs/

user                    nginx;
worker_processes        auto;
worker_rlimit_nofile    204800;
worker_cpu_affinity     auto;
error_log               /var/log/nginx/error.log;
pid                     /run/nginx.pid;

# 스레드
thread_pool default threads=32 max_queue=65536;

# Load dynamic modules. See /usr/share/doc/nginx/README.dynamic.
include /usr/share/nginx/modules/*.conf;

events {
        # 동시에 8192개의 요청을 받을 수 있다.
        worker_connections      8192;
        # 순차적으로 요청을 받지 않고 동시에 요청을 접수합니다.
        multi_accept    on;
        # Linux 2.6+ 이상에서 사용하는 효율적인 이벤트 처리방식
        use                     epoll;
}

http {
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile            on;
    tcp_nopush          on;
    tcp_nodelay         on;
    keepalive_timeout   15;
    keepalive_requests  100000;
    types_hash_max_size 4096;

    reset_timedout_connection   on;
    client_body_timeout         10;
    send_timeout                2;

    include             /etc/nginx/mime.types;
    default_type        application/octet-stream;

    # Load modular configuration files from the /etc/nginx/conf.d directory.
    # See http://nginx.org/en/docs/ngx_core_module.html#include
    # for more information.
    include /etc/nginx/conf.d/*.conf;

    server {
        listen       80;
        listen       [::]:80;

        root /home/ec2-user/client/build;
        location / {
                try_files $uri /index.html;
        }

        server_name  chat.neodigm.com;
        return 301   https://$host$request_uri;

        include /etc/nginx/default.d/*.conf;

        error_page 404 /404.html;
        location = /404.html {
        }

        error_page 500 502 503 504 /50x.html;
        location = /50x.html {
        }
    }

    # Settings for a TLS enabled server.
    server {
        listen       443 ssl http2;
        listen       [::]:443 ssl http2;
        server_name  chat.neodigm.com;
        client_max_body_size 16M;

        ssl_protocols           TLSv1.2;
        ssl_certificate         "/home/ec2-user/ssl/ssl-bundle.crt";
        ssl_certificate_key     "/home/ec2-user/ssl/private.key";
        ssl_session_cache       shared:SSL:1m;
        ssl_session_timeout     10m;
        ssl_prefer_server_ciphers on;
        ssl_ciphers "ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384";

        proxy_cache off;
        proxy_store off;

        # 활동안하면 타임아웃 시키는 시간
        proxy_send_timeout          3600s;
        proxy_connect_timeout       3600s;
        proxy_read_timeout          3600s;

        root /home/ec2-user/client/build;
        index index.html index.htm;

        location / {
                try_files $uri $uri/ /index.html;
        }

        location /api {
                proxy_pass              https://localhost:8443;

                #proxy_redirect          http://localhost:3000 https://localhost:3000;
                proxy_set_header        Host                    $host;
                proxy_set_header        X-Real-IP               $remote_addr;
                proxy_set_header        X-Forwarded-Host        $host;
                proxy_set_header        X-Forwarded-Server      $host;
                proxy_set_header        X-Forwarded-For         $proxy_add_x_forwarded_for;
                proxy_set_header        X-NginX-Proxy true;

                # For WebSocket upgrade header
                proxy_http_version      1.1;
                proxy_set_header        Upgrade $http_upgrade;
                proxy_set_header        Connection "upgrade";

                # set all cookies to secure
                #proxy_cookie_path / "/; secure; SameSite=None";

                aio threads=default;
        }

        include /etc/nginx/default.d/*.conf;

        error_page 404 /404.html;
            location = /40x.html {
        }

        error_page 500 502 503 504 /50x.html;
            location = /50x.html {
        }
    }
}
~~~

~~~
chmod 711 /
chmod 711 /bin
chmod 711 /boot
chmod 711 /dev
chmod 711 /etc
chmod 711 /home
chmod 711 /mnt
chmod 711 /opt
chmod 711 /proc
chmod 711 /usr
chmod 711 /usr/local
chmod 711 /var
~~~

권한 설정을 해주어야 ec2-user 폴더에 접근할 수 있다.
추가로 미리 client/build 폴더를 생성하면 안된다 권한으로 인해 접근을 못한다.

# 프로젝트 생성

- General
  - GitHub project
    - url : https://github.com/alalstjr/
- 소스 코드 관리
  - Git
    - Repository URL : git@github.com:alalstjr/neodigm-websocket-client.git
- 빌드 유발
  - GitHub hook trigger for GITScm polling
- 빌드 환경
  - Provide Node & npm bin/ folder to PATH
- Build
  - Execute shell
    - npm install 
    - npm run build
- 빌드 후 조치
  - Send build artifacts over SSH
    - Transfers
      - Source files : build/
      - Remote directory : ./client
      - Exec command
        - (만약 docker 로 nginx 를 돌리는 경우에만 넣는다) sudo ./docker.sh
    - 고급
      - Clean remote : 체크

# Spring Boot Maven 프로젝트

## Java 11 젠킨스 등록

Jenkins AWS EC2 에서 작업
~~~
docker exec -it {container_id} /bin/bash
apt-get update
apt-get install openjdk-11-jdk -y
~~~

System Configuration / Global tool configuration에 들어간다.
JDK를 찾고 경로를 지정해준다.

> /usr/lib/jvm/java-11-openjdk-arm64

## Maven 플러그인 설치

젠킨스 플러그인 Maven Integration 설치
새로운 Item -> Maven project 으로 생성
Build > Goals and options > clean package
빌드 후 조치 -> SSH Publishers -> Source files -> target/
Exec command -> 아래 코드를 삽입
~~~
$NAME = Neodigm-websocket-restapi
sudo yum install java-11-amazon-corretto -y
pid=$(ps -eaf | grep $NAME.jar | grep -v "grep" | awk '{print $2}')

if [ "$pid" == "" ]; then
    echo "demo web application is not running."
else
    kill -9 $pid
    echo "demo web application process killed forcefully. (pid : $pid)"
fi

nohup  java -jar ./target/*.jar 2>> /dev/null >> /dev/null &
~~~

## 프로젝트 실행중인 EC2 run SH 파일 생성

SSL 프로젝트이 경우 인증서 [keystore.p12] 파일은 최상위 폴더 [/home/ec2-user] 에 위치한다

spring.sh
~~~
#!/bin/bash

sudo yum update -y
#sudo yum install -y java-1.8.0-openjdk-devel.x86_64
sudo yum install java-11-amazon-corretto -y
sudo rm /etc/localtime
sudo ln -sf /usr/share/zoneinfo/Asia/Seoul /etc/localtime
REPOSITORY=/home/ec2-user/target
PROJECTNAME=Neodigm-amazon-seller

echo "> 현재 구동중인 애플리케이션 pid 확인"
echo "$(pgrep -f $PROJECTNAME)"
if [ -z $(pgrep -f $PROJECTNAME) ]; then
    echo "> 현재 구동중인 애플리케이션이 없으므로 종료하지 않습니다."
else
    echo "> kill -2 $(pgrep -f $PROJECTNAME)"
    sudo kill -9 $(pgrep -f $PROJECTNAME)
    sleep 5
fi
echo "> 새 어플리케이션 배포"
JAR_NAME=$(ls $REPOSITORY/ |grep $PROJECTNAME | tail -n 1)
echo "> JAR Name: $PROJECTNAME"
nohup sudo java -jar $REPOSITORY/*.jar &
~~~
sudo chmod 755 ./spring.sh
./spring.sh 으로 실행

# AWS S3, CodeDeploy 연동하기

## IAM 사용자

각자의 iam을 사용하는 것을 권장(han, park, song): 누가 어떤 작업을 했는지 추적할 수 있음.
- jenkins-user 사용자 추가
- jenkins에서 S3와 CodeDeploy에 접근하기 위한 IAM 유저 추가, Access key 파일은 따로 보관.
  - <권한>
  - AmazonS3FullAccess
  - AWSCodeDeployFullAccess

## IAM 역할이란 무엇입니까?

- IAM 역할은 신뢰하는 개체에 권한을 부여하는 안전한 방법입니다. 개체의 예는 다음을 포함합니다.
  - 다른 계정의 IAM 사용자
  - AWS 리소스에서 작업을 수행해야 하는 EC2 인스턴스에서 실행 중인 애플리케이션 코드
  - 계정 내 리소스에서 작업을 수행하여 기능을 제공해야 하는 AWS 서비스
  - SAML을 통해 인증 연동을 사용하는 사내 디렉토리의 사용자
  - IAM 역할은 권한을 부여하는 더욱 안전한 방법으로 짧은 기간 동안 유효한 키를 발행합니다.

- 역할
  - AWS 서비스에만 할당할 수 있는 권한
  - EC2, CodeDeploy, SQS 등

- 사용자
  - AWS 서비스 외에 사용할 수 있는 권한
  - 로컬PC, IDC서버 등

## 역할 만들기

1. 유형의 개체 선택
지금 만들 권한은 EC2에서 사용할 것이기 때문에 사용자가 아닌 역할로 처리합니다.

2. 권한 정책 연결 
EC2RoleForA정도까지 검색하여 AmazonEC2RoleforAWS-CodeDeploy를 선택합니다.

## 역할을 EC2 서비스에 등록

해당 EC2 인스턴스 설정에서 [IAM 역할 연결/바꾸기]를 선택합니다.
생성한 역할을 선택합니다.

## CodeDeploy 에이전트 설치

재부팅이 완료되었으면 CodeDeploy의 요청을 받을 수 있에 에이전트를 설치해야합니다.
Amazon Linux 2 AMI (centos)환경에서 작업하였습니다.
EC2에 접속해서 다음 명령어를 입력합니다.

> aws s3 cp s3://aws-codedeploy-ap-northeast-2/latest/install . --region ap-northeast-2

다음과 같은 메시지가 콘솔창에 출력됩니다.

> download: s3://aws-codedeploy-ap-northeast-2/latest/install to ./install

install 파일에 실행 권한을 추가하고 설치를 진행하는데, 설치가 안된다면 ruby를 설치하시면 됩니다.

> chmod +x ./install && sudo ./install auto

Agent가 정상적으로 실행되고 있는지 상태 검사를 합니다.
다음과 같이 나오면 정상입니다.

~~~
sudo service codedeploy-agent status
The AWS CodeDeploy agent is running as PID 3530
~~~

내부에 nginx 설정 혹은 SSL 설정은 맞추어 놓아야 한다.

그 후 생성된 EC2 AMI 로 만들어 저장합니다.

## 시작 템플릿 생성

이름: jenkins-template
AMI: jenkins-ami
스토리지: EBS 범용 SSD(gp3) 30GB
IAM 역할: jenkins-codedeploy
보안 그룹: ec2-security-group -> 인바운드 허용 포트: 22(ssh), 80(http), 9000(운영)

## CodeDeploy를 위한 권한 생성

CodeDeploy에서 EC2에 접근하려면 마찬가지로 권한이 필요합니다.
AWS의 서비스이니 조금전과 마찬가지로 IAM역할을 생성합니다.

1. 유형의 개체 선택
사용 사례 선택 -> codeDeploy

2. 권한 선택
CodeDeploy는 권한이 하나뿐이라서 선택 없이 바로 다음으로 넘어가면 됩니다.

## CodeDeploy 생성

CodeDeploy는 AWS의 배포 삼형제 중 하나입니다.
- Code Commit
  - 깃허브와 같은 코드 저장소의 역할 (거의 사용되지 않음)
- Code Build
  - Travis CI, Circle CI와 마찬가지로 빌드용 서비스(역시 거의 사용되지 않음)
- CodeDeploy
  - AWS의 배포 서비스
  - Commit이나 Build는 대체제가 있어 AWS서비스를 사용하지 않지만, CodeDeploy는 대체제가 없음
  - 오토 스케일링 그룹 배포, 블루 그린 배포, 롤링 배포, EC2 단독 배포 등 많은 기능을 지원

현재 프로젝트에서 Commit은 github, build는 Circle CI 또는 Travis CI가 하고 있기 때문에 추가로 사용할 서비스는 CodeDeploy입니다.

## 1. 애플리케이션 생성

CodeDeploy서비스로 이동해서 [애플리케이션 생성] 버튼을 클릭하여 CodeDeploy의 이름과 컴퓨팅 플랫폼을 선택합니다.
컴퓨팅 플랫폼에선 [EC2/온프레미스]를 선택합니다.

## 2. 배포 그룹 생성

생성이 완료되면 배포 그룹을 생성하라는 메시지를 볼 수 있습니다. 
배포 그룹을 생성할 때 서비스 역할은 좀 전에 생성한 CodeDeploy용 IAM역할을 선택합니다.

배포 유형에서는 1대의 EC2에만 배포하므로 현재 위치를 선택합니다. 
배포할 서비스가 2대 이상이라면 블루/그린을 선택하면 됩니다.

환경 구성은 [Amazon EC2 인스턴스]에 체크합니다.

배포 설정과 로드밸런서를 선택합니다. 
배포 구성이란 한번 배포할 때 몇 대의 서버에 배포할지를 결정합니다.
2대 이상이라면 1대씩 배포할지, 30% 혹은 50%로 나눠서 배포할지 등등 여러 옵션이 있지만, 1대 서버다 보니 전체 배포하는 옵션으로 선택합니다.
CodeDeployDefaultAllAtOnce는 한 번에 다 배포하는 것을 의미합니다.

## Jenkins S3 CodeDeploy 배포

### 플러그인 설치 

AWS CodeDeploy 

## 새로운 Item 생성

### React 빌드 조치

1. 빌드 후 조치
2. Deploy an application to AWS CodeDeploy
3. AWS CodeDeploy Application Name
   1. neodigm-websocket-client-app (git 저장소 이름으로 기준 잡았다.)
4. AWS CodeDeploy Deployment Group
5. AWS CodeDeploy Deployment Config
6. CodeDeployDefault.AllAtOnce
7. AWS Region
8. 서울 리전
9. S3 Bucket
10. {버킷 이름}
11. S3 Prefix
12. {폴더 명}
13. Include Files
    1. appspec.yml, sh/**, build/**
14. Exclude Files
    1. node_modules
15. Use Access/Secret keys
16. 위에서 만든 jenkins-user 사용자 보안 자격증명 정보 입력

### Spring 빌드 조치

1. 빌드 후 조치
2. Deploy an application to AWS CodeDeploy
3. AWS CodeDeploy Application Name
4. AWS CodeDeploy Deployment Group
5. AWS CodeDeploy Deployment Config
   1. CodeDeployDefault.AllAtOnce
6. AWS Region
   1. 서울 리전
7. S3 Bucket
   1. {버킷 이름}
8. S3 Prefix
   1. {폴더 명}
9. Include Files
   1. appspec.yml, sh/**, target/*.jar, ssl/**
10. Use Access/Secret keys
    1. 위에서 만든 jenkins-user 사용자 보안 자격증명 정보 입력

## appspec.yml 파일 생성 

codedeploy 에서 실행할 수 있도록 파일 생성 프로젝트 최상위 내부에 넣습니다.

> appspec.yml
~~~
version: 0.0
os: linux
files:
  - source:  /
    destination: /home/ec2-user/api/
    overwrite: yes

permissions:
  - object: /
    pattern: "**"
    owner: root
    group: root

hooks:
  AfterInstall:
    - location: stop.sh
      timeout: 60
      runas: root
  ApplicationStart:
    - location: start.sh
      timeout: 60
      runas: root
  ValidateService:
    - location: health.sh
      timeout: 60
      runas: root
~~~

> stop.sh
~~~
#!/bin/bash

sudo yum update -y
sudo yum install java-11-amazon-corretto -y
sudo rm /etc/localtime
sudo ln -sf /usr/share/zoneinfo/Asia/Seoul /etc/localtime

PROJECT_NAME=Neodigm-websocket-restapi
PROJECT_ROOT="/home/ec2-user/api"
JAR_FILE="$PROJECT_ROOT/target/$PROJECT_NAME.jar"

DEPLOY_LOG="$PROJECT_ROOT/deploy.log"

TIME_NOW=$(date +%c)

# 현재 구동 중인 애플리케이션 pid 확인
CURRENT_PID=$(pgrep -f $JAR_FILE)

# 프로세스가 켜져 있으면 종료
if [ -z $CURRENT_PID ]; then
  echo "$TIME_NOW > 현재 실행중인 애플리케이션이 없습니다" >> $DEPLOY_LOG
else
  echo "$TIME_NOW > 실행중인 $CURRENT_PID 애플리케이션 종료 " >> $DEPLOY_LOG
  kill -15 $CURRENT_PID
fi
~~~
sudo chmod 755 ./stop.sh

> start.sh
~~~
#!/bin/bash

PROJECT_NAME=Neodigm-websocket-restapi
PROJECT_ROOT="/home/ec2-user/api"
JAR_FILE="$PROJECT_ROOT/target/$PROJECT_NAME.jar"

#APP_LOG="$PROJECT_ROOT/application.log"
#ERROR_LOG="$PROJECT_ROOT/error.log"
DEPLOY_LOG="$PROJECT_ROOT/deploy.log"

TIME_NOW=$(date +%c)

# build 파일 복사
#echo "$TIME_NOW > $JAR_FILE 파일 복사" >> $DEPLOY_LOG

# jar 파일 실행
#nohup java -Dspring.profiles.active=deploy -jar $JAR_FILE > $APP_LOG 2> $ERROR_LOG &
echo "$TIME_NOW > $JAR_FILE 파일 실행" >> $DEPLOY_LOG
nohup java -Dspring.profiles.active=deploy -jar $JAR_FILE > $PROJECT_ROOT/nohup.out 2>&1 &

CURRENT_PID=$(pgrep -f $JAR_FILE)
echo "$TIME_NOW > 실행된 프로세스 아이디 $CURRENT_PID 입니다." >> $DEPLOY_LOG
~~~
sudo chmod 755 ./start.sh

-Dspring.profiles.active=deploy 설정을 주는 이유는 spring properties 절대경로 구분위해서
예시로 logging.file.path = /home/ec2-user/api/logs 이런식이다.

nohup 실행에 [ $PROJECT_ROOT/nohup.out 2>&1 & ] 을 넣은 이유는 sh 종료 시점을 확인해야하는데
nohup.out 출력을 하지 않으면 무한 루프에 빠지기 때문에 넣어주었다.

> health.sh
~~~
#!/bin/bash
IP=$(curl ifconfig.me)
echo "> Health check 시작"
echo "> curl -s https://chat.neodigm.com/api/health"
#echo "> curl -s https://$IP:8443/api/health"

for RETRY_COUNT in {1..15}
do
  RESPONSE=$(curl -s https://chat.neodigm.com/api/health)
  UP_COUNT=$(echo $RESPONSE | grep 'UP' | wc -l)

  if [ $UP_COUNT -ge 1 ]
  then # $up_count >= 1 ("UP" 문자열이 있는지 검증)
      echo "> Health check 성공"
      rm -rf "/opt/codedeploy-agen/deployment-root"
      break
  else
      echo "> Health check의 응답을 알 수 없거나 혹은 status가 UP이 아닙니다."
      echo "> Health check: ${RESPONSE}"
  fi

  if [ $RETRY_COUNT -eq 10 ]
  then
    echo "> Health check 실패. "
    exit 1
  fi

  echo "> Health check 연결 실패. 재시도..."
  sleep 10
done
exit 0
~~~
sudo chmod 755 ./health.sh

배포 이전에 api 폴더를 ec2 에 생성해준다.

## codedeploy 덤프 파일 제거

aws codedeploy 를 진행하다보면 dump 파일이 쌓이고 용량이 꽉차 오류가 출력되는 문제 확인

> find / -xdev -name core -ls -o -path "/lib*" -prune

로그 확인하여 덤프파일 확인 본인 같은 경우에는 codedeploy-agent 폴더에 빌드 파일이 쌓여 오류가 출력되었다.

> rm -rf "/opt/codedeploy-agen/deployment-root"

health 체크 완료 후 덤프파일을 바로 지우도록 수정했다.

## Auto Scaling 

ALB 생성 후 Auto Scaling 연결 
일단 간단한 Nginx + codedeploy 가 생성 연결되어있는 ec2 생성
health check 만 될 수 있도록 공간만 마련한다
나머지는 build 후 자동으로 체워진다.

codedeploy 애플리케이션 배포 그룹의 설정

1. 배포 유형
   1. 현재 위치
2. 환경 구성
   1. Amazon EC2 Auto Scaling 그룹 체크
   2. 생성한 Auto Scaling 그룹 추가
      1. 추가로 ec2 를 따로 넣고싶다면 체크하고 추가
3. 배포 설정
   1. All
4. 로드 밸런서
   1. None Check
5. 젠킨스에서 각각 client / backend 빌드 해주어 공간을 체워준다

# 참고

https://itholic.github.io/qa-cicd/ - [CI/CD 란?]
https://lemontia.tistory.com/660 - [Jenkins, SpringBoot, Gradle 사용 Jar로 빌드, 배포]
https://miiingo.tistory.com/171 - [Jenkins Docker]
https://velog.io/@minholee_93/Jenkins-Springboot-Gradle-Github-CodeDeploy-ELB-9ck5x7mt4q - [Jenkins AWS 배포]
https://velog.io/@minholee_93/Jenkins-Springboot-Gradle-Github-CodeDeploy-ELB-2-1yk5ze6ky0 - [Jenkins AWS 배포]
https://blog.mint-soft.com/entry/mac-jenkins-%EC%8B%A4%ED%96%89-%EC%97%90%EB%9F%AC - [mac jenkins 실행 에러]
https://gksdudrb922.tistory.com/200 - [Auto scaling]