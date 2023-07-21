---
title: jekyll 사용시 블로그 중복 URL 이슈 
categories: [Tech, jekyll]
tags: [blog, jekyll, configuration]
---
jeklly을 이용해 문서를 작성하게 되면 URL 노출을 설정할 수 있다. 이때 설정과 블로그 포스트 파일을 작성할때 파일
이름 명명 규칙에 따라 URL이 중복해서 만들어질 수 있다. 


## 이슈 
아래와 같이 [날짜]+[영문제목] 형태로 문서를 작성하게 된다. 이때 Jekyll에서는 날짜를 인식해 문서 생성일자와 
영문 제목을 이용해 URL을 노출 시킨다. 만약 날짜만 다르고 문서 제목이 같다면 어떻게 될까? 전체 주소 형태가 
날짜를 기준으로 하지 않는다면 동일한 문서 링크를 생성하게 된다. 

![My blog list](/assets/img/post/20230721/post-list.png)

즉 아래와 같이 매칭 된다. 
```
2023-05-15-reading-newsletter.md -> /post/reading-newsletter.md
2023-05-16-reading-newsletter.md -> /post/reading-newsletter.md
...
...
```

이렇게 된 이유는 설정 파일(`_config.yml`)에 다음과 같은 형태로 블로그 URL을 설정했기 때문이다. 
```yaml
defaults:
  - scope:
      path: "" # An empty string here means all files in the project
      type: posts
    values:
      layout: post
      comments: true # Enable comments in posts.
      toc: true # Display TOC column in posts.
      permalink: /post/:title/                      ## <<--- 여기 
```

## 해결 방법 
그러면 어떻게 변경해 볼까? 

내 블로그의 글은 동일한 타이틀을 가진 경우가 종종 생긴다. 그래서 메뉴얼을 확인해 생성 날짜를 URL에 포함시키도록
변경했다.
```yaml
defaults:
  - scope:
      path: "" # An empty string here means all files in the project
      type: posts
    values:
      layout: post
      comments: true # Enable comments in posts.
      toc: true # Display TOC column in posts.
      permalink: /post/:year/:month/:day/:title/     ## <<--- 여기 
```

이렇게 변경하니 Title 이름이 같더라도, 생성 날짜가 다르기 때문에 각 페이지가 독립적은 URL을 갖게되었다. 
```
2023-05-15-reading-newsletter.md -> /post/2023/05/15/reading-newsletter.md
2023-05-16-reading-newsletter.md -> /post/2023/05/16/reading-newsletter.md
...
...
```

## 참고 사이트 
- [Jekyll Permalinks](https://jekyllrb.com/docs/permalinks/){:target="_blank"} : 여기 상세 설명을 보면 다양하게 설정을 변경할 수 있다. 
- [Duplicated page generation](https://talk.jekyllrb.com/t/duplicated-page-generation/2759/4){:target="_blank"}
