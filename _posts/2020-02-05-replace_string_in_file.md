---
title: "sed를 이용한 대용량 텍스트 파일 다루기"
date: 2020-02-05 16:02:00 -0000
categories: shell linux tip
---

# sed(stream editor)
* 대용량 파일을 다루기 좋다.
* 검색, 치환(삭제)에 사용
* find, cat, xargs, wc와 결합한 예제들을 찾아보자

## 유용한 예
* 파일 안 특정 라인만 보고 싶은 경우
```bash
sed -n '200,300p' ./dummy.txt
```
* 파일안 문자열 치환(정규식 지식 필요)
```bash
sed 's/hello/good/g' ./dummy.txt
```
