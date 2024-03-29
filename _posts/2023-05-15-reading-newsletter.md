---
title: 2023-05-15 뉴스레터 요약하기
author: billy_goo
date: 2023-05-15 15:50:00 +0900
categories: [Summary, Daily Newsletter]
tags: [newletter, tech-news]
---

> 이 페이지는 그날 그날 구독한 뉴스레터에서 기록하고 싶은 글들을 정리하는 페이지 입니다.
{: .prompt-info }

## Science & Future

[실험을 통한 췌장암 백신의 가능성](https://news.yahoo.com/pancreatic-cancer-vaccine-shows-promise-181909301.html?utm_source=tldrnewsletter)
: 암 과학자 그룹이 췌장암에 대한 새로운 백신을 개발했다. 이 백신은 환자에 개인화된 백신을 통해 면역 체계가 종양을 공격하도록 설계되었다. 비용도 $350,000에서 $100,000 민만으로 낮춤. mRNA 기반임. 


## IT Tech

[Stable Animation SDK](https://stability.ai/blog/stable-animation-sdk)
: [stability.ai](https://stability.ai/)가 Stable Diffusion 모델을 사용하여 애니메이션을 만들기 위한 도구 세트인 Stable Animation SDK를 출시함. 무엇보다 [오픈소스](https://github.com/Stability-AI/stablediffusion)로 공개했기 때문에 이를 활용해 직접 무언가를 만들어 볼 수 있다. 
{% include embed/youtube.html id='xsoMk1EJoAY' %}

[Datadog’s $65M/year customer mystery solved](https://blog.pragmaticengineer.com/datadog-65m-year-customer-mystery)
: Datadog에서 년간 65만불을 지출한 고객사 코인베이스에 대해 알아낸 사실을 글로 풀었음. 결론적으로 급격한 성장으로 인해 Datadog을 사용하며 많은 비용을 지불함. 그러나 코인 시장 냉각에 따른 비용 절감을 위해 `Grafana/Prometheus/Clickhouse` Stack으로 전환함. 또한 Datadog도 완전히 없애지 않고 같이 활용하고 있음. 

[Brex의 Prompt 엔지니어링 가이드](https://github.com/brexhq/prompt-engineering)
: 지출관리를 하나의 플랫폼에서 제공하는 [Brex](https://www.brex.com/)에서 LLMs에서 사용하는 프롬프트에 대해 어떻게 사용할지에 대해 가이드를 작성해 제공함. 

[당근마켓 검색 엔진, 쿠버네티스로 쉽게 운영하기](https://medium.com/daangn/%EB%8B%B9%EA%B7%BC%EB%A7%88%EC%BC%93-%EA%B2%80%EC%83%89-%EC%97%94%EC%A7%84-%EC%BF%A0%EB%B2%84%EB%84%A4%ED%8B%B0%EC%8A%A4%EB%A1%9C-%EC%89%BD%EA%B2%8C-%EC%9A%B4%EC%98%81%ED%95%98%EA%B8%B0-bdf2688df267)
: 제목 그대로 당근 마켓에서 검색 인프라를 쿠버네티스로 이관하는 작업을 공유한 글 
 - AWS에서 ELK 스택을 Terraform을 통해 관리하고 있었음
 - 각 컴포넌트의 업데이트과정에 수동 배포 및 배포 시간이 길었음
 - 이를 EKS와 ArgoCD, GithubAction을 이용해 구축 및 배포 자동화 구성함
 - 글은 이 과정을 진행하면서 수행한 Task들을 시간순으로 정리해 설명
 

## 구독 중인 뉴스레터

- [TL;DR Newletter](https://tldr.tech/)
- [GeekNews](https://news.hada.io/)
- [미라클 레터](https://page.stibee.com/)
