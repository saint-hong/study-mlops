# Docker 정리

## 1. 설치
- docker 공식 문서 : https://docs.docker.com/engine/install/ubuntu/
   - docker engine을 설치하는 방식은 여러가지가 있음
- apt repository를 사용해서 설치하는 방식
   - docker engine을 설치하기 전에 docker 저장소(repository)를 설정해야함
   - 그 후 레포지토리에서 docker를 설치하고 업데이트 한다.
- apt 패키지 업데이트 기본 : sudo apt-get update
   - root 유저 아닌 host 기본 유저도 docker 권한 추가해야 sudo 명령어 안 쓰고 사용가능

#### facamp 방식
- docs의 방식은 약간다름
```
<prerequisite packge install>

$ sudo apt-get install \
   apt-transport-https \
   ca-certificates \
   curl \
   gnupg \
   lsb-release

<docker의 CPG key 추가>

$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmo r -o /usr/share/keyrings/docker-archcive-keyring.png

<gpg 키가 stable버전의 레포지토리를 바라보도록 설정>

$ echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

<docker engine 설치>

$ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

- 설치 후 정상 작동 확인
   - sudo docker run hello-world   
   - hello-world 라는 docker image가 작동함 

```
<docker engine 시작>

$ sudo docker run hell-world
```
##









