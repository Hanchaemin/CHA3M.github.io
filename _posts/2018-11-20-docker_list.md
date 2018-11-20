---
title: ! "Docker 명령어"
date: 2018-11-20
tags:
  - docker
  - container
  - chaem
categories:
  - docker
---

# install  
sudo apt install docker.io  

# build  
docker build -t overflow1 .  

# run
docker run -d -it -p 9999:9999 --name test1 test1  
docker run --name test1 -d -p 9999:9999 test1  

# manange  
docker exec -i -t test1 /bin/bash  
차이는 run은 새로 컨테이너를 만들어서 실행하고 exec는 실행중인 컨테이너에 명령을 내린다.  

docker stop test1 test2 test3  
컨테이너를 중지한다.  

docker restart test1 test2 test3  
해당 컨테이너를 다시 시작한다. (여러 컨테이너의 이름을 한번에 써서 이용할 수 있다.)   

docker images  
이미지 목록을 확인한다.  

docker ps -a  
컨테이너 목록을 확인한다.  

# remove  
docker rm test1  
컨테이너를 제거한다.  

docker rmi test1  
이미지를 제거한다.  

docker system prune -a  
컨테이너와 이미지들을 한번에 모두 정리하는 명령어이다.  
