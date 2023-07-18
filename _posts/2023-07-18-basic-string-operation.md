---
title: Shell - String 처리 관련 예제
categories: [Tech, Shell]
tags: [shell, string-operation]
---

## Shell에서 String 처리 기초 
이 페이지에서는 Shell에서 문자열을 처리하는 기초 예제를 정리한 페이지이다. 

### String 길이 출력하기 

```bash
#       123456789012345678901
STRING="This is a test string"
echo ${#STRING}

21   # Result
```

### index 
`STRING`문자열에서 `SUBSTRING`에 있는 문자들 중 하나라도 포함되는 시작 위치를 찾는다. 이 때 `expr`명령을 사용한다. (시작은 1부터 시작한다.)

```bash
STRING="This is a test string"
SUBSTRING="gnh"
expr index "$STRING" "$SUBSTRING"

2     # Result : gnh 중에 h가 제일 먼저 나오기 때문에 2 결과를 표시한다.
```

### 일부 문자열 추출하기 
특정 위치(index)부터 길이를 지정하면 해당 문자열을 반환한다. 시작은 0부터 시작한다. 

```bash
STRING="This is a test string"
POS=1
LEN=3
echo ${STRING:$POS:$LEN}

his    # Result 

echo ${STRING:$POS}

his is a test string    # Result : 추출 길이를 전달하지 않으면 시작 위치부터 끝까지 반환함
```

### 일부 문자열 교체하기 
문자열에서 일부 문자열만 교체하기 위한 2가지 방법을 사용할 수 있다. 

아래와 같이 처음 만나는 문자열만 교체 된다. 
```bash
STRING="hello world, this is new world"
echo ${STRING/world/my world}

hello my world, this is new world    # Result
```

다음은 일치하는 모든 문자열이 교체 된다. 
```bash
STRING="hello world, this is new world"
echo ${STRING//world/billy}

hello billy, this is new billy    # Result
```

아래와 같이 지정하면 문자열을 삭제할 수 있다. 
```bash
STRING="hello world, this is new world"
echo ${STRING//new/}

hello world, this is world    # Result
```

검색 문자열을 시작(`#`) 문자와 끝(`%`) 문자를 같이 사용하면 검색 위치 지정할 수 있다. 
```bash
STRING="hello, this is new world, this is new world"
echo ${STRING/#world/World}   

hello, this is new world, this is new world # Result : -_-;; 특정 조건에서 잘 동작하지 않음. 왠지 모르겠음. 

echo ${STRING/%world/World}

hello, this is new world, this is new World  # Result : 뒤에부터 검색된 문자열 교체 
```

이러한 것들을 활용하면 문자열을 다음과 같이 날짜를 삽입할 수 있다. 
```bash
STRING="hello, this is new world, this is new world"
echo ${STRING/%world/World on $(date +%Y-%m-%d)}

hello, this is new world, this is new World on 2023-07-18 # Result
```

## 참고 사이트 
- [Manipulating Strings](https://tldp.org/LDP/abs/html/string-manipulation.html){:target="_blank"}
- [Unix / Linux - Shell Substitution](https://www.tutorialspoint.com/unix/unix-shell-substitutions.htm){:target="_blank"}
- [Basic String Operations](https://www.learnshell.org/en/Basic_String_Operations){:target="_blank"}
