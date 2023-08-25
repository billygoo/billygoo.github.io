---
title: Jenkins는 왜 File System을 Backend로 활용하나?
categories: [DevOps, Jenkins]
tags: [newletter, tech-news]
---
## 호기심
Jenkikns는 왜 File system을 활용할까? 


## 탐색
### Jenkins 히스토리 확인
일단 Jenkins [공식 홈페이지](https://www.jenkins.io/)와 [가이드](https://www.jenkins.io/doc/book/)를 확인했다. 

큰 소득은 없었다. 확인한 것은 Jenkins 아키텍처 2개의 그림과 파일 시스템(Persistent Objects)에 대한 내용만 
확인할 수 있었다. 

### SIG에서 논의 기록을 찾기
그렇다면 주요 개발자나 기여자들의 논의 공간에는 이야기 나눈 기록은 없을까? 하는 생각에 [SIG](https://www.jenkins.io/sigs/)에 
들어가 논의한 내용들을 살펴봤다. SIG들은 크게 아래와 같이 5개 그룹으로 나뉘어져 있었고, 나는 Platform을 먼저 
뒤져봤다. 

1. Advocacy and Outreach : Jenkins 기여를 위한 프로세스나 이벤트들을 협의하는 공간
2. Documentation : 말 그대로 문서 기여를 위한 논의 
3. Google Summer of Code : 특이하게 GSoC를 위한 공간이 있다. 
4. Platform : 플랫폼 지원 정책을 정의하고 논의 하는 공간
5. User Experience : 사용자 인터페이스와 사용자 경험 개선 논의 공간 

기록들이 3~6년 정도 밖에 없었고, File system에 논의는 검색 조차 안됐다. 
왠지 Backend에 대한 암묵적인 동의가 있는 것처럼 당연하게 생각하는 느낌이 든다. 그래서 
아무도 Backend를 바꾸자는 이야기가 없는 것일까? 

### ChatGpt에 물어보기 
```
Q > hudson이 저장소를 파일시스템으로 선정한 이유가 뭐야? 

Hudson은 Jenkins의 이전 이름으로, 지속적인 통합(CI)을 위한 자동화 도구입니다. 
Hudson이 파일 시스템을 저장소로 선택한 이유는 몇 가지 이유로 설명할 수 있습니다:

1. 간단한 구현: 초기 버전의 Hudson이 개발되었을 때에는 다양한 데이터베이스 시스템과의 
통합이 추가 비용과 복잡성을 초래할 수 있었습니다. 파일 시스템은 기본적으로 모든 
운영체제에서 지원되기 때문에 구현이 단순하고 호환성이 좋았습니다.

2. 실시간 변경 추적: CI 도구에서는 설정 파일, 빌드 스크립트 및 작업 정보와 같은 변경 
사항을 실시간으로 추적하고 저장해야 합니다. 파일 시스템은 이러한 변경 사항을 비교 
및 추적하기에 적합한 구조를 제공합니다.

3. 단순한 백업 및 복구: 파일 시스템을 사용하면 백업 및 복구 작업이 비교적 간단합니다. 
설정 파일이나 작업 정보를 복사하거나 이동하여 백업을 만들거나 이전한 뒤 문제가 
발생한 경우 복구할 수 있습니다.

4. 동기화와 공유의 용이성: 파일 시스템을 사용하면 여러 서버나 개발자 간에 설정 정보나 
작업 정보를 동기화하거나 공유하기가 비교적 용이합니다.

그러나 파일 시스템을 사용하는 방식은 몇 가지 단점도 가지고 있습니다. 분산된 환경에서의 
데이터 무결성 문제, 성능 저하, 확장성의 한계 등이 있을 수 있습니다. 따라서 점차적으로 
많은 CI/CD 도구들이 데이터베이스나 다른 저장소 시스템과의 통합을 강화하여 더 
유연하고 안정적인 시스템을 구축하도록 발전해왔습니다.
```

- 뭔가 간단성과 단순성을 위해서 이지 않았을까?하고 추측 정도는 할 수 있겠다.  


## 알아낸 것들 
### Jenkins Dataflow 아키텍처
[https://www.jenkins.io/doc/developer/architecture/](https://www.jenkins.io/doc/developer/architecture/)
![jenkins-dataflow](/assets/img/post/20230825/jenkins-dataflow.png)

- Jenkins와 외부와 소통하는 아키텍처이다. 
- 방화벽 설정시 해당 화면을 참조해 필요한 Port들을 확보해야한다. 

### Jenkins High level view
[https://www.jenkins.io/doc/developer/architecture/model/](https://www.jenkins.io/doc/developer/architecture/model/)
```
  ┌─────────────────────────────────────────┐   ┌─────────────────────┐   ┌─────────────┐
  │    Automation, machine to machine       │   │ End users/Browsers  │   │    Agents   │
  │    command line prompt (curl, wget..)   │   │                     │   │             │
  └─────────▲─────────────────────▲─────────┘   └───────────▲─────────┘   └───────▲─────┘
            │                     │                         │                     │
            │                     │                         │                     │
            │                     │                         │                     │
┌───────────▼───────────┬─────────▼───────────┬─────────────▼───────────┬─────────▼──────┐
│   Command line CLI    │   HTTP Endpoints    │  Web user interface     │    Remoting    │
├───────┬───────────────│                     │                         │                │
│  SSH  │   websocket   │                     │  (Jelly /Groovy views)  │                │
│       │   or HTTP     │                     │                         │                │
│       ├───────────────┴─────────────────────┴─────────────────────────┤                │
│       │                                                               │                │
│       │       Stapler: security, routing, requests processing         │                │
│       │                                                               │                │
├───────┴───────────────────────────────────────────────────────────────┴────────────────┤
│                                                                                        │
│                       Business layer: models, processing, scheduling                   │
│                                                                                        │
├────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                        │
│                      Storage layer: XML files on JENKINS_HOME                          │
│                                                                                        │
└────────────────────────────────────────────────────────────────────────────────────────┘
```
- Jenkins 내부 컴포넌트들을 확인할 수 있다. 
    - Web UI : [jelly](https://en.wikipedia.org/wiki/Apache_Jelly)/groovy views를 활용해 사용자에게 Web UI 제공
    - Remoting : Agent와 통신하기 위한 모듈
    - Stapler : 내부 클래스 객체와 URL 매핑하기 위한 모듈
- 컴포넌트 단위로 보면 단순하게 구조를 확인할 수 있다. 


## 결론 
- 여러 탐색을 했지만 정확한 이유는 모르겠다. 
- 이 글을 작성하는 시점에 [Google Groups](https://groups.google.com/g/jenkinsci-dev) 있는 개발자 공간을 발견했다. 
    - Google Groups를 탐색해 보고, 이유를 업데이트 해봐야겠다. 

