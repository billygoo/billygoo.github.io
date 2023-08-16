---
title: 2023-08-16 뉴스레터 요약하기
categories: [Summary, Daily Newsletter]
tags: [newletter, tech-news]
---
> 이 페이지는 그날 그날 구독한 뉴스레터에서 기록하고 싶은 글들을 정리하는 페이지 입니다.
{: .prompt-info }

[Amazon의 수백만개의 택배가 포장 없이 배송된다.](https://www.entrepreneur.com/business-news/amazon-trims-packaging-offers-ships-in-own-container/457329){:target="_blank"}
: 아마존 주문의 11%가 포장없이 택배 배송이 이루어지고 있다. 
- 소비자는 추가 포장 여부를 선택 가능함 
- 포장 제거로 비용 절감 및 환경 개선 목표 달성 목표 
- 포장 자체가 가지는 제품 보호에 대한 것이 잘 이루어 지는지 지속 확인 필요함 
- 제품 노출로 인한 절도 이슈 대응도 필요 (SNS에 부정적인 이슈 노출 되고 있는 중)

[Amazon이 Custom Chip을 활용해 생성형 AI에서 MS와 Google을 따라잡기 위한 방법](https://www.cnbc.com/2023/08/12/amazon-is-racing-to-catch-up-in-generative-ai-with-custom-aws-chips.html){:target="_blank"}
: Amazon에서 AI 경쟁에서 MS와 구글을 따라 잡기 위해 자체 설계 칩을 만들고 있다. 
- MS에서는 OpenAI에 투자하고 발빠르게 Bing에 통합
- Google에서는 자체 생성형 AI Bard 출시 후 OpenAI 라이벌 Anthropic에 3억 달러 투자 
- 메타에서는 자체 생성형 AI Llama2 cnftl 
- Amazon에서는 `Trainium`과 `Inferentia` 자체 칩을 개발해 LLM 학습할 수 있도록 제공 중
    - 2013년부터 Nitro라는 Custom HW를 만들어, 사용하고 있었음 
    - 2015년 이스라엘 칩 스타트업 [Annapurna Labs](https://en.wikipedia.org/wiki/Annapurna_Labs){:target="_blank"}를 인수함
    - 2018년 Arm 기반 서버칩 Graviton 출시 
    - 2018년 [AI Chip 출시](https://www.cnbc.com/2018/11/28/aws-launches-inferentia-ai-chip.html){:target="_blank"}
    - 2019년 Inferentia 출시 
    - 2021년 Trainium 출시 
- AWS Cloud가 가진 시장 장악력을 활용해 AI 관련 도구들을 지원해 영향력을 넓히고 있음 

[선언형 API개발 플랫폼 - metatype](https://github.com/metatypedev/metatype){:target="_blank"}
: `Metatyp`은 선언형 API 개발 플랫폼이다. 
- 프로그래밍 가능한 가상 그래프인 `Typegraph`를 사용
- 플러그인과 재사용 가능한 구성 요소를 지원 
- [투토리얼](https://metatype.dev/docs/tutorials/getting-started)
- [Use cases](https://metatype.dev/use-cases/automatic-crud-validation)
    - BFF, FaaS Runner, GraphQL server 등 사례 제공

[소스 코드 가독성의 근원](https://loup-vaillant.fr/articles/source-of-readability){:target="_blank"}
: 코드 가독성을 위한 규칙을 정리한 블로그 
- 클린아키텍처와 같이 코드 가독성의 원칙과 개인의 변경을 기록한 글 
- 기존 기본 룰과 다를 수 있지만, 개인의 원칙을 기록하는 것은 도움이 될거라 생각다는 글이다. 
