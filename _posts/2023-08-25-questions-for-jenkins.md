---
title: 질문으로 Jenkins Deep Dive 시작하기
categories: [DevOps, Jenkins]
tags: [newletter, tech-news]
---
![jenkins-worldwide-logo](/assets/img/post/20230825/jenkins-logo-worldwide.png)

## 들어가며
[Jenkins](https://www.jenkins.io/)는 최고의 오픈소스 CI/CD 도구이다. 개발자 친화적이고, 수많은 사용자가 있어 
문제가 발생했을때, 해결할 수 있는 참조 사례도 많다.

나 조차도 이 도구를 잘 쓰고, 활용하고 있다. 그런데 내가 얼만큼 알고 있을까? 하는 
스스로의 궁금함이 떠올랐다. 곰곰히 생각해보니 내가 알고 있는 지식들은 활용 방법이
중심이었던 것 같다. 예를 들면 아래와 같다. 

- Jenkins Pipeline을 활용한 CI/CD 시각화 
- Shard Library를 개발해 자신만의 Custom Pipeline 구성하기 
- 다양한 도구들과 통합해, Seamless한 연결 구성하기 

그래서 활용 사례대신 조금 더 Jenkins를 깊이 있게 학습해 추후 기술 지식을 활용하고자 한다. 
목적은 다음과 같다. 

1. 내부 모델 구조를 이해해, 앞으로 필요한 내용이 있다면 빠르게 Plugin을 개발할 수 있는 역량을 키운다. 
2. Jenkins의 오픈소스 개발 Life Cycle을 이해하고, 오픈소스에 기여할 수 있는 기회를 확보한다. 


## 호기심 
1. [Jenkins는 왜 File System을 Backend로 활용하나?](/post/2023/08/25/why-dose-jenkins-use-filesystem/)
2. Jenkins가 시작할 때 어떤 동작을 수행하는가? 
3. Jenkins에 나만의 Job Type을 추가하려면 어떻게 해야하나? 

> 호기심은 그때 그때 생각나면 추가하면서 정리한다. 그리고 그 질문별로 글타래를 하나씩 작성한다.
{: .prompt-info }

## 잡담 
Jenkins에도 다른 오픈소스처럼 의사결정기구인 
[SIG(Special Interest Group)](https://www.jenkins.io/sigs/){:target="_blank"}이 있다. 
꾸준히 활동은 이루어 지지만, 활발한 활동은 이루어지지 않은것 같다. 그래서 조금 더 Jenkins를 이해하고, 
기여한다면 손쉽게 SIG에 참여할 기회가 많아 보인다. 
