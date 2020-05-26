---
title: "vscode를 이용한 도커(docker) 안에 c++ 앱 디버깅(gdb-server) 방법"
date: 2020-05-26 16:02:00 -0000
categories: docker environment vscode
---

# 개요
* 도커에서 c/c++을 디버깅 해보고 싶은 경우.
* vscode와 gdb-server를 이용한다
* centos 기준으로 설명

## 참고 링크 
* https://medium.com/@aharon.amir/develop-c-on-docker-with-vscode-98fb85b818b2

## 보충 설명
* 참고링크의 방법 그대로 필자는 centos 이미지에서 확인
* centos인 경우 아래 패키지를 설치
```Dockerfile
# RUN apt-get install gcc-4.9 g++-4.9 cmake gdb gdbserver -y  && \
RUN yum install -y gcc gcc-c++ gdb-gdbserver
```
* docker-compoes.yml 안에 privileged 옵션은 없어도 된다.
* launch.json 설명 
```json
{
	"version": "0.2.0",
	"configurations": [

  {
			"name": "C++ Launch (GDBSERVER)",
			"type": "cppdbg",
			"request": "launch",
			"miDebuggerServerAddress": "localhost:2000", // gdbserver의 호스트
			"preLaunchTask": "start-gdbserver", //tasks.json에 같은 이름의 task가 실행된다
			"miDebuggerPath": "/usr/bin/gdb",
			"targetArchitecture": "x64",
			"program": "${workspaceRoot}/build/bin/your_app", // 디버깅 실행할 앱
			"args": [],
			"stopAtEntry": false,
			"cwd": "${workspaceRoot}", //로컬에서 앱의 실행 기준 패스
			"sourceFileMap":{
				"/home/develop/project": "${workspaceRoot}" // 디버깅을 위한 소스 위치
			},
			"environment": []
	}
 ]
}
```
* tasks.json 설명
    * 앱의 cwd가 로컬과 서버가 다른 경우. Dockerfile을 다시 만들던가 실행 패스로 이동해서 실행하자
```json
...
        {
            "label": "start-gdbserver", //launch.json의 preLaunchTask
            "type": "shell",
            // "command": "docker exec -d devenv  gdbserver :2000 build/bin/your_app",            
            "command": "docker exec -d devenv  bash -c 'cd build/bin && gdbserver :2000 build/bin/your_app'",            
            "problemMatcher": []
        }
```

## 사용 환경
* suse tumbleweed
* docker
    - version 19.03.5
    - base image - centos7.8 
