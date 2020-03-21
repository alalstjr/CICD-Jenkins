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

# Mac Os 설치방법

https://www.youtube.com/watch?v=HjfrsAChjzA

# Jenkins 실행 중지

$ sudo launchctl unload /Library/LaunchDaemons/org.jenkins-ci.plist
$ sudo launchctl load /Library/LaunchDaemons/org.jenkins-ci.plist

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

# 에러발생시 조치

현상
launchdaemon으로 등록되어 있어서 자동으로 실행이된다(컴터 켤때마다)
근데 갑자기 페이지를 띄울수 없다고 나온다.
ERR_CONNECTION_REFUSED브라우져에서 이런 에러를 내보낸다. 

추적
각종로그참고
1.jenkins 로그  /var/log/jenkins/jenkins.log

Dec 17 00:30:00 Mac-mini newsyslog[3784]: logfile turned over

아무 정보도 얻을수 없어서 다른 로그를 분석햇다.

2.system.log /var/log/system.log
com.apple.xpc.launchd[1] (org.jenkins-ci[965]): Service could not initialize: 14B25: xpcproxy + 14045 [1344][1016C726-9ACF-3A24-9C51-A279F5C6B167]: 0xd

구글로 검색해본결과

http://stackoverflow.com/questions/26483089/launchd-is-not-starting-jenkins-server-on-os-x-yosemite
스택오버플로어에 자세히 나와있다.
shutdown하거나 systemerror가 있을때 로그에 기록해야 하는데 퍼미션이 문제라고 한다.
그래서 퍼미션을 고쳐주면 된다. 

# 참고

https://itholic.github.io/qa-cicd/ - [CI/CD 란?]

https://lemontia.tistory.com/660 - [Jenkins, SpringBoot, Gradle 사용 Jar로 빌드, 배포]
https://miiingo.tistory.com/171 - [Jenkins Docker]
https://velog.io/@minholee_93/Jenkins-Springboot-Gradle-Github-CodeDeploy-ELB-9ck5x7mt4q - [Jenkins AWS 배포]
https://velog.io/@minholee_93/Jenkins-Springboot-Gradle-Github-CodeDeploy-ELB-2-1yk5ze6ky0 - [Jenkins AWS 배포]

https://blog.mint-soft.com/entry/mac-jenkins-%EC%8B%A4%ED%96%89-%EC%97%90%EB%9F%AC - [mac jenkins 실행 에러]