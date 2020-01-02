---
title: "도커(docker) 이미지, 컨테이너 저장 경로 변경 "
date: 2020-01-02 16:02:00 -0000
categories: docker environment
---

# 도커(docker) 이미지, 컨테이너 저장 경로 변경
* 도커 사용시 root 레벨의 경로가 기본이라 용량 부족을 경험해봤을것이다.
* 아래처럼 저장되는 경로를 변경해주면 된다.

## 주의 사항
* docker를 사용중이고 기존의 이미지,컨테이너를 복원시 /var/lib/docker를 rsync 또는 다시 패스를 변경한다. 
* 아래 작업시 sudo systemctl stop docker, sudo server docker stop 등을 하고 해야 한다.

## 환경
* tumbleweed suse

## 설정 파일
* /etc/sysconfig/docker 파일 emacs, vi로 수정
* 다시 쉘에서 sudo systemctl restart docker

```

DOCKER_OPTS="-g /data/my_docker" 

```
