---
title: ! "git branch 사용하기"
date: 2018-10-03
tags:
  - git
  - branch
  - chaem
categories:
  - git
---
## branch 생성 및 제거

로컬 PC에서 원하는 브랜치를 생성하고 이동
- git checkout -b test

원격 저장소에 자신이 만든 브랜치와 동일한 브랜치를 생성  
- git push origin test

로컬 PC에서 브랜치 제거
- git branch -d test

원격 브랜치 제거
- git push origin :test

## branch 관리

브랜치 로컬 목록 보기
git branch

브랜치 원격 목록 보기
git branch -r

브랜치 전체 목록 보기
git branch -a
