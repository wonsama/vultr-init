# vultr-init

클라우드 서버인 [vultr](https://www.vultr.com/?ref=8812497) 에서 서버를 관리 하는 방법

## 회원 가입하기

[vultr](https://www.vultr.com/?ref=8812497)

- 위 링크로 가입 시 최초 100$를 줌 :)

## 인스턴스 생성

Deploy New Server 를 눌러 생성

## 저렴한 서버 생성하기

> 간단한 웹서버 구동 가능 ( 월 6$ + 1.2$ (백업) )

- Choose Server
  - Cloud Compute
- CPU & Storage Technology
  - Amd
- Server Location
  - Seoul ( South Korea )
- Server Image
  - Ubuntu 22.04 LTS x64
- Server Size
  - 1vCPU / 1 GB Memory / 2 TB Bandwidth
- Add Auto Backups
  - 선택

위 설정으로 기본 선택하면 약 월 7.2 $ 에 클라우드 서버를 운용할 수 있다.

## 접속하기

vultr 에 instance 추가 후 products - overview 에 접속하면 생성된 서버를 확인 할 수 있다. ( 약 5-10 분 정도 기다리면 서버가 생성됨 )

이후 터미널 프로그램을 통해 ( puttry, iterm, git-bash 등 ) 접속을 하면 됨

`ssh xxx.xxx.xxx.xxx -l root`

- 기본적으로 root 계정으로 생성됨
- products - overview 에서 생성된 password 를 통해 암호 확인 후 접속하면 됨

## 초기 설치 요약

빠른 개발 및 배포를 위해 아래와 같이 설치하도록 한다

- docker
- nvm : nodejs version manager

### 1 docker 설치

참조링크 - [docker - install ubuntu](https://docs.docker.com/engine/install/ubuntu/)

```sh
# GPG 키 추가하기
sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" |  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# 최신 정보로 업데이트
sudo apt-get update

# docker 및 docker compose 설치
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# 설치 확인
# 23.03.26 기준 Docker version 23.0.1, build a5ee5b1
docker --version
```

### 2. nvm 설치

참조링크 - [github - nvm](https://github.com/nvm-sh/nvm)

```sh
# 자동설치 URL
# 버전 정보는 바뀔 수 있으니 위 참조링크에서 최신 버전을 확인한다
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash

# 설치 완료 후
`source ~/.bashrc` 를 입력하여 바로 사용할 수 있도록 한다.

# 기본 명령어

## 설치 가능 목록 확인하기
nvm ls-remote

## 16버전 설치
nvm install 16

## 16버전 사용하기
nvm use 16
```

## subdomain 설정하기

`npx degit https://github.com/wonsama/p-dc-subdomain subdomain`

자세한 내용은 [github - p-dc-subdomain](https://github.com/wonsama/p-dc-subdomain) 를 참조하기 바랍니다.

## ssh key 생성하기

> 암호 없이 로그인 하기

1. 접속하려는 PC - `ssh-keygen -t rsa` 을 실행
2. `~/.ssh/id_rsa.pub` 파잃의 내용을 원격지 PC의 `~/.ssh/authorized_keys` 에 복사하여 넣어주면 된다.

## port 열기

> 기본적으로 22번 포트만 열려 있다.

`sudo ufw status` : 포트 상태 보기
`sudo ufw allow 80` : 포트번호 80번 오픈하기

- 보통 80, 443, 기타 서비스포트를 open 하면 좋은 것 같다.
- 22번 포트를 열어두면 보통 무작위 대입공격을 많이 받는다.
- 이를 방지하기 위해 22번 포트를 다른 포트로 변경하는 것도 좋음
- root의 비번은 반드시 복잡하는 것을 사용한다 (최초 자동생성한 된 것만 봐도 우수함)

## docs 빠르게 만들기

> docsify 를 사용하면 좋음

## 최종 업데이트

- 23.03.26 : 최초 작성
