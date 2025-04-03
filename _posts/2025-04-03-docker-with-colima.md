---
title: 애플실리콘에서 colima를 이용해 docker 조합 활용 하기 
categories: [DevOps, Container]
tags: [docker, colima, apple-silicon]
---
## 이 글의 시작 
매일같이 워드와 엑셀과 씨름하다가 오랜만에 맥북으로 오픈소스 시스템을 실행해 보고 싶어졌다. 
오랜만에 터미널을 켜서 'docker' 명령어를 치니, 프로그램 설치도 안되어 있는 현실을 마주쳐 부랴 부랴 실리콘 맥에서는 
어떻게 쓰는지 찾아보녀 정리한 글이다. 
   
## 요즘은 실리콘 맥에서 어떻게 쓸까? 
기술 자료들을 찾아보니 제일 많이 나오는게 colima + docker 조합을 많이 글 이었다. 

> colima??? docker desktop은 안쓰나? 

### Docker Desktop의 한계
보통 Docker Desktop 제품을 이용하면 docker를 손쉽게 이용할 수 있었다. 다만 애플 실리콘이라는 장벽을 넘어가기 위해서
docker desktop에서 가상 리눅스 VM을 실행하고, docker 명령어는 해당 VM에서 실행되는 구조로 동작했다. 
이러한 동작 방식 때문에 성능이 발을 잡았다. VM을 계속 실행다는 것은 CPU 점유율과 그로 인해 배터리가 많이 소모하는 구조!

개발자는 노트북 성능 이슈는 못참는 민족! 

그리고 한가지 더 이슈가 Docker Desktop의 유료화 이슈!! 
> 직원이 250명 이상 또는 회사 매출이 1000만 이상인 경우 유료 라이선스 필수

성능과 유료화 이슈가 있어 Docker Desktop은 버려졌...다... 
   
## 그들이 찾은 대안은?   
> `colima + docker cli` 조합

`lima`라고 CNCF 샌드박스 프로젝트로 리눅스 VM을 생성해 파일 공유와 포트 포워딩을 자동으로 해주는 어플리케이션 이다.
이걸 조금 더 단순하게 쓸 수 있도록 사용자 편의 기능을 추가한 `colima`이 개발 되었고, 이를 활용해 docker desktop에서 
수행하던 가상 VM을 경량화해 docker cli와 함께 쓰는 조합이 주로 이용 한다. 

## 어떻게 쓸까? 
단순하다. `brew`를 이용해 설치하고 VM을 실행 후 docker 명령어를 바로 실행하면 된다. 

"""bash
$ brew install docker
$ brew install colima 

$ docker ps 
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?

$ colima start
INFO[0000] starting colima
INFO[0000] runtime: docker
INFO[0000] creating and starting ...                     context=vm
INFO[0000] downloading disk image ...                    context=vm
INFO[0108] provisioning ...                              context=docker
INFO[0109] starting ...                                  context=docker
INFO[0109] done

$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
"""

## Apple Silicon에서 Docker 사용 조합들 

| 조합 | 구성 설명 | 장점 | 단점 |
|------|-----------|------|------|
| **1. Docker Desktop (Apple Silicon 지원)** | Docker 공식 앱. ARM 지원 포함. GUI 있음. | 설치 간편, 공식 지원, GUI 친숙 | 비교적 무거움, 기업 유료 라이선스 |
| **2. Docker + Colima** | 경량 VM 기반으로 Docker 데몬 실행 (CLI 전용) | 빠름, 가벼움, 무료, 개발 친화적 | GUI 없음, 설정 필요 |
| **3. Docker + Lima** | Colima보다 더 로우레벨. Lima로 직접 가상머신 구성 | 유연한 설정, 가볍고 빠름 | 난이도 높음, 수작업 설정 많음 |
| **4. Docker + Multipass (Canonical)** | Ubuntu VM 위에 Docker 설치 | Ubuntu 기반 개발에 좋음 | 일반적이지 않음, 설정 복잡 |
| **5. Docker + UTM** | ARM/Linux VM 위에서 Docker 직접 설치 | 완전한 리눅스 환경 사용 가능 | 무겁고 번거로움 |


## 선호도 요약 (개발자 설문/커뮤니티 트렌드 기준)

| 조합 | 선호도 (★ 5점 기준) | 추천 사용자 |
|------|----------------------|-------------|
| Docker Desktop | ★★★★☆ | 입문자, GUI가 필요한 사람 |
| Docker + Colima | ★★★★★ | 백엔드/DevOps 개발자, 자원 아끼고 싶은 사용자 |
| Docker + Lima | ★★☆☆☆ | 커스터마이징 매니아 |
| Docker + UTM/Multipass | ★☆☆☆☆ | 실험적 목적, 특정 OS가 필요할 때만 |
