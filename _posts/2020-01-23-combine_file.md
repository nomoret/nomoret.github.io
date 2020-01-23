---
title: "여러개 텍스트 파일 하나로 합치기"
date: 2020-01-23 16:02:00 -0000
categories: jekyll update
---

## 
## 여러개의 텍스트 파일을 하나로 합치고 싶은 경우 
* 아래 링크된 사이트를 예제로 리눅스에서 해보겠습니다.
* [https://wikidocs.net/21690](https://wikidocs.net/21690) 참고
* 딥러닝을 이용한 자연어처리 입문 10-5 4) 훈련 데이터 만들기 

```shell

# 우선 AA 디렉토리 안의 모든 파일인 wiki00 ~ wiki90에 대해서 wiki_data.txt로 통합해보겠습니다. 프롬프트에서 아래의 커맨드를 수행합니다. (리눅스 환경 기준)
foo@bar:~ cat ./wiki_result/A*/wiki* >> wiki_data.txt

#이제 모든 텍스트 파일을 하나로 만든 훈련 데이터가 완성되었습니다. 

```
