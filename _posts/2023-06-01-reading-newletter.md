---
title: 2023-06-01 뉴스레터 요약하기
author: billy_goo
date: 2023-06-01 11:46:00 +0900
categories: [Summary, Daily Newsletter]
tags: [newletter, tech-news]
---

> 이 페이지는 그날 그날 구독한 뉴스레터에서 기록하고 싶은 글들을 정리하는 페이지 입니다.
{: .prompt-info }

## IT Tech
[Apple Reality Pro 유출](https://www.macworld.com/article/1935837/apple-reality-headset-display-leak-resolution-brightness.html){:target="_blank"}
: 애플에서 새로 출시할 AR 헤드셋이 유출되었다. 
  ![APPLE AR Headset](/assets/img/post/20230601/joseraphael_1-4.webp){: width="950"}
- 마이크로 OLED, 1.41 인치, 4,000 ppi, 5000니트 이상 밝기
- 참고로 PS VR2는 850 ppi, HoloLens는 최대 밝기가 500 니트
- 현재 예측 가격은 3000 달러(한화로 약 400만원임)
- 6/5 애플 WWDC에서 발표 예정임 

[AI 광풍에 NVIDIA 1조 달러 기업 되다](https://www.theverge.com/2023/5/30/23742123/nvidia-stock-ai-gpu-1-trillion-market-cap-price-value){:target="_blank"}
: 펜데믹 기간 암호화폐 및 게임용 PC 열기가 식었지만 AI 광풍이 불면서 주식 가치가 1조 달러 규모가 되었다. 
- ChatGPT로 촉발된 AI 경쟁이 [Google I/O](https://io.google/2023/intl/ko/){:target="_blank"} 및 [Microsoft Build](https://news.microsoft.com/build-2023/){:target="_blank"} 발표에 AI 도구가 경쟁적으로 도입 발표됨
- AI 도구들은 연산을 위해 수많은 NVIDIA 칩을 사용함
- 이로 인해 주가가 급등함


## Science & Futuristic Technology
[독일 스타트업이 핵융합 장치 개발을 위한 초기 투자 확보](https://archive.md/XKpBg){:target="_blank"}
: 1월에 설립된 독일의 스타트업 `Proxima Fusion`이 스텔라레이터(`stellarator`)로 알려진 핵융합 에너지 장치 개발을 목표로 하고 있음 
- 700만 유로 투자금 유치 
- 독일 막스플랑크 플라즈마 물리학 연구소에 분사한 최초의 핵융합 기업 
- [스텔라레이터](https://ko.wikipedia.org/wiki/%EC%8A%A4%ED%85%94%EB%9D%BC%EB%A0%88%EC%9D%B4%ED%84%B0){:target="_blank"}는 [토카막](https://ko.wikipedia.org/wiki/%ED%86%A0%EC%B9%B4%EB%A7%89){:target="_blank"} 장치의 대안임 
   - 참고 자료
    {% include embed/youtube.html id='NA1PEwbZ8Is' %}

[스키니 잽을 맞은 어린이 절반이 비만이 개선된 임상 연구 결과](https://www.theguardian.com/society/2023/may/17/half-of-children-given-skinny-jab-no-longer-clinically-obese-us-study){:target="_blank"}
: 제2형 당뇨병 치료제로 사용하던 Semaglutide를 투약한 어린이들의 약 45%가 임상적으로 비만으로 분류되지 않을 만큼의 체중 감량 효과가 있었음
  - 전례없는 효과를 가짐
  - 체중 관리용으로 `Wegovy` 브랜드 제품이 승인됨
  - 국내에는 23년 5월 기준으로 허가됨 
    - [참고기사](http://www.monews.co.kr/news/articleView.html?idxno=322653){:target="_blank"}


## Programming 
[fastgron](https://github.com/adamritter/fastgron){:target="_blank"}
: Json 데이터를 Grep을 사용해 빠르게 검색할 수 있게 도와주는 툴로 손쉽게 API를 탐색할 수 있음
- 기존 [gron](https://github.com/tomnomnom/gron){:target="_blank"} 대비 50배 속도 향상되었고, 역방향 변환도 지원함
- 손쉽게 거대한 양의 API를 검색할 수 있게 도와줌 
  ```bash
  > fastgron "https://api.github.com/repos/adamritter/fastgron/commits?per_page=1" | fgrep commit.author
  json[0].commit.author = {};
  json[0].commit.author.name = "adamritter";
  json[0].commit.author.email = "58403584+adamritter@users.noreply.github.com";
  json[0].commit.author.date = "2023-05-30T18:04:25Z";
  ```
- 역방향으로 다시 Json으로 변환도 가능함 
  ```bash
  > fastgron "https://api.github.com/repos/adamritter/fastgron/commits?per_page=1" | fgrep commit.author | fastgron --ungron
  [
    {
      "commit": {
        "author": {
          "date": "2023-05-30T18:11:03Z",
          "email": "58403584+adamritter@users.noreply.github.com",
          "name": "adamritter"
        }
      }
    }
  ]
  ```
- 참고 자료 
  - [gron](https://github.com/tomnomnom/gron){:target="_blank"}은 json 데이터를 grep할 수 있도록 만드는 유틸리티

[Apache Baremaps](https://github.com/apache/incubator-baremaps){:target="_blank"}
: 온라인 지도를 생성, 발행, 운영하기 위한 인프라 구성 및 툴킷 


## 읽어 볼 만한 기사나 블로그
[빅 테크 기업들의 가장 큰 베팅들](https://www.matthewball.vc/all/bigtechbiggestbets){:target="_blank"}
: 빅 테크 기업들이 다음으로 유망하다는 기술을 선택하고 투자하고 있는 현황 및 방향을 설명한 글 

- Meta와 Apple의 AR Headset 투자 및 출시
- Amazon 제프 베조스의 Prime video와 Alexa 강조
  - 하지만 실적이 좋지 않음. 또한 Alexa는 단순 질의 대응으로 AI가 크게 불필요
- 아마존이 구매 목록과 배송 정보를 이메일로 보내지 않는다.
  - 구글이 이를 분석해 활용하기 때문에 Amazon 비즈니스에 위협이 되기 때문

[Stop being a junior](https://kentcdodds.com/blog/stop-being-a-junior){:target="_blank"}
: 시니어로 넘어가기 위해 필자가 한 경험 및 조언 


## 구독 중인 뉴스레터
- [TL;DR Newletter](https://tldr.tech/)
- [GeekNews](https://news.hada.io/)
- [미라클 레터](https://page.stibee.com/)
