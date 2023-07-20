---
title: LLM과 Prompt Engineering
categories: [Tech, ChatGPT]
tags: [ai, llm, github, copilot, chat-gpt]
---

> 이 글은 [2023-07-19 뉴스레터 요약하기](/post/2023/07/19/reading-newsletter/#it-tech)에서 봤던 블로그 글을 보며 느낀 점을 정리한 글입니다. 
{: .prompt-info }

> 블로그 링크 : [A developer’s guide to prompt engineering and LLMs](https://github.blog/2023-07-17-prompt-engineering-guide-generative-ai-llms/){:target="_blank"}
{: .prompt-tip }

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
![process to using LLMs](/assets/img/post/20230720/inside-how-llms-work.webp){: width="600" }

지난 몇 년 동안 Copilot을 개발하기 위해 Github에서 Prompt Pipeline을 만들고 개선하는 작업들을 수행해왔다고 한다. 그  Pipeline 동작을 살펴 보면 다음과 같이 6 단계를 거친다. 

1. 전후 사정 정보 수집하기(Gathering context)
    - VS Code를 사용할 경우 파일 언어 정보 
    - 열려진 파일 내용 또는 탭 정보 (일부만 활용) 등
2. 질의 맥락에 맞는 정보 발췌하기(Snippeting)
    - 맥락에 맞지 않는 정보를 활용하면 LLM의 정확도를 떨어뜨림
    - 그래서 단편적인 정보(Snippet, 실제 코드 정보)에 대한 점수를 매겨 좋은 점수만 추려 활용 
    - 점수를 매기기 위해 [Jaccad 유사도](https://ko.wikipedia.org/wiki/%EC%9E%90%EC%B9%B4%EB%93%9C_%EC%A7%80%EC%88%98){:target="_blank"}를 활용함
3. 전후 사정 정보 다듬기(Dressing them up)
    - AI 처리 모델인 Codex 및 다른 모델에 파일을 업로드하거나 문서 언어나 파일 이름을 지정할 API가 없다. 
    - 그래서 전후 사정 정보를 전달하기 위해 주석과 같은 형태로 메타 정보들을 추가한다.

    ```python
    # compare this snippet from utils/concatenate.py:

    # def crazy_concat(a, b):

    # return str(a) + str(b)[::-1]
    ```
4. 우선순위 지정(Prioritization)
    - 다양한 정보를 수집함 : 커서 바로 위/아래 텍스트, 다른 파일의 텍스트, 언어 및 파일 경로 같은 메타데이터 등
    - 여기서 우선순위를 지정해 중요한 정보를 알려준다. 
5. AI가 Prompt 정보를 처리(The AI does its thing)
    - 좋은 품질의 답을 제공하기 위해 OpenAI와 Github 공동으로 모델을 개발함([Codex](https://openai.com/blog/openai-codex){:target="_blank"})
6. 사용자에게 생성된 문자열 전달하기(Now, over to you!)

위와 같이 LLMs를 활용한 서비스를 제공하기 위해 Propmt Engineering 활동, 즉 4번까지의 LLMs에 전후 사정 정보를 
전달하기 위한 작업을 서비스 개발자가 해야할 활동으로 이해했다. 더 나아가 모델이 효율적이지 못하다면, 그 모델을
직접 만드는 활동까지 할 수 있겠지만, 그 경우에는 AI/ML 엔지니어가 필요하다는 생각이 들었다. 

> 위 정보는 LLMs에 익숙치 않은 지식과 영어 자료를 이해하면서 작성하다 보니 틀릴 수 있습니다.
> 그래서 새롭게 알게되거나, 고쳐야할 사항들은 다시 업데이트 하겠습니다. 
{: .prompt-warning }

## 그래서 일반 개발자는 무엇에 집중해야 할까? 
나와 같은 평범한 Software Engineer인 경우에는 새로운 모델을 개발하는 것보다 앞단에 사용자 인터페이스부터 
다양한 맥락 정보(Context)를 정리하는 Prompt Engineering 단에 집중해야 한다. 추가적으로 
미세 조정([Fine-tuning](https://platform.openai.com/docs/guides/fine-tuning){:target="_blank"}) 작업을 통해서 
데이터 모델을 업데이트해 원하는 결과를 만드는데 집중해야 할 것같다. 

> 2023/07 기준으로 Chat GPT-3, GPT-4에 대한 Fine-tuning에 지원은 안되고 있음. 추후 열릴듯. 
{: .prompt-info }

## 참고 사이트 
- [A developer’s guide to prompt engineering and LLMs](https://github.blog/2023-07-17-prompt-engineering-guide-generative-ai-llms/#step-2-snippeting){:target="_blank"}
- [ChatGPT 용어 - 파인튜닝(Fine-tuning)이란 무엇인가?](https://m.blog.naver.com/mynameistk/223036912084){:target="_blank"}
- [OpenAI/Fine-tuning](https://platform.openai.com/docs/guides/fine-tuning){:target="_blank"}
