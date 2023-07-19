---
title: LLM과 Prompt Engineering
categories: [Tech, LLM]
tags: [ai, llm, github, copilot]
---

> 이 글은 [2023-07-19 뉴스레터 요약하기](/post/2023/07/19/reading-newsletter)에서 봤던 다음 글을 보며 느낀 점을 정리한 글입니다. 
{: .prompt-info }

[A developer’s guide to prompt engineering and LLMs](https://github.blog/2023-07-17-prompt-engineering-guide-generative-ai-llms/){:target="_blank"}
: LLM이 작동하는 방식과 LLM 기반 애플리케이션을 구축하는 방법을 설명한 후 실 사례인 Github Copilot을 가지고 설명함.

## Github Copilot에서의 Prompt Engineering 
블로그 내용에서는 사용자 입력을 통해 어떻게 소스코드를 생성하는지 설명한다. 
글을 읽으면서 내가 알게 된 것이 있다면, `Prompt Engineering` 개념을 확장 할 수
있었다는 것이다. 단순히 사용자가 LLM 질문을 잘 작성하는 것으로 한정적인 생각을 
어떻게 하면 더 잘 응답하게 할 수 있을지 연관 정보를 모아 전달하는 과정이라는 것을
말이다.  
- Prompt Engineering
    - 글을 읽기 전 : 사용자가 LLM에 질의하기 위해 글을 잘 쓰는 것 
    - 글을 읽은 후 : LLM이 최대한 정답에 가까운 응답을 할 수 있도록 정보를 구성하는 것 

## WIKI 백과에선 뭐라고 하지? 
> 프롬프트 엔지니어링 ( Prompt Engineering ) 은 인공지능의 한 개념으로 특히 자연어 처리 부분에 해당된다. 주요 업무는 인공지능의 역량을 발휘하도록 120%지시어를 적합하게 내려주는 것이다. ([WIKI](https://ko.wikipedia.org/wiki/%ED%94%84%EB%A1%AC%ED%94%84%ED%8A%B8_%EC%97%94%EC%A7%80%EB%8B%88%EC%96%B4%EB%A7%81))

## 그럼 Github Copilot에서는 어떻게 Prompt Engineering을 구성했을까? 


