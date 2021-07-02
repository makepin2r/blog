---
title: Gridsome과 Github Pages를 이용해 블로그 만들기
date: 2021-07-02
tags:
  - gridsome
  - gh-pages
published: true
category: blog
---

Gridsome을 이용해서 블로그를 개설해보았다.

## Gridsome 알아보기
[Gridsome 홈페이지 바로가기](https://gridsome.org/)

Gridsome은 간단히 말하자면 Vue.js로 만들어진 정적 사이트 생성기이다.  
마치 Gatsby가 React를 이용해 만들어진 것처럼, Vue에는 Gridsome이 있다. (Gridsome 자체가 Gatsby에서 많은 영향을 받았다고 한다.)

### Gridsome을 알게 된 & 사용하게 된 이유
이번에 프론트엔드 개발을 시작하면서 배우는 것들이 너무 많아 기술 블로그를 쓰기로 했다.  
깃허브 블로그를 쓰고 싶어 Jekyll로 세팅하려 했는데 팀장님이 Vue로 된 정적 사이트 생성기가 있다고 소개해주셨다.
아직 만들어진지 오래 되진 않았지만 (2018년인가..로 알고 있다) 문서도 훌륭하고 초기 세팅을 돕는 Starter도 너무 잘 되어있었다.
덕분에 쾌적하게 블로그를 만들었다 😊

---

## Gridsome으로 블로그를 세팅해보자
### 1. Gridsome을 설치
일단 Gridsome을 설치한다.  

    npm install --global @gridsome/cli

### 2. Gridsome Blog Starter 이용해 프로젝트 생성
Gridsome에서는 아주 깔끔한 starter를 제공한다.
프로젝트를 생성할 경로로 가서, (폴더 형태로 생성되니 현재 있는 경로가 최종 경로의 상위 경로가 될 것이다.)

    gridsome create my-blog https://github.com/gridsome/gridsome-starter-blog.git

    
`my-blog`는 생성될 프로젝트의 폴더명이므로, 원하는 대로 바꾸면 된다.
뒤의 git url은 Gridsome Blog Starter에서 제공하는 가장 기본 테마이다. 

나는 [Gridsome Starters](https://gridsome.org/starters/flex-markdown-starter/)에 가서 다른 테마를 골랐다.
바로 [이것!](https://gridsome.org/starters/flex-markdown-starter/)

<!-- ![screenshot_flex-markdown-starter](../src/assets/post-images/210702_01.PNG) -->

여기까지 하면 Blog Starter 세팅은 끝이다! 
`package.json` 파일에 가보면 scripts에 이 명령이 있는 것을 알 수 있다.

    "develop": "gridsome develop",

콘솔창에 `npm run develop` 을 입력해주면 (그 전에 `npm install` 하는 걸 잊지 말자), 로컬에 페이지가 구동된다.

### 3. 내 Github 리파지토리 연결
프로젝트 세팅이 끝나면, Github에 새 리파지토리를 만들어 연결해준다.
    
    git remote add origin [새 리파지토리 url]

## gh-pages를 이용해 Github Pages에 프로젝트 연결하기
Github Pages에 만든 블로그 프로젝트를 올리려면, 추가 세팅이 필요하다.

### 1. gh-pages 설치
npm에 `gh-pages`를 설치한다.

    npm install gh-pages

### 2. url 연결
`gridsome.config.js` 파일에 가면, **siteUrl** 이라는 항목이 있다.   
siteUrl을 다음과 같이 수정하고, 하단에 **pathPrefix** 항목도 추가한다.
(siteUrl은 기본 경로, pathPrefix는 기본 경로 다음에 붙는 추가 경로이다.)

    siteUrl: 'https://my-name.github.io',
    pathPrefix: '/my-blog'

위와 같이 수정하면 블로그의 최종 경로는 https://my-name.github.io/my-blog/ 가 된다.  

### 3. deploy 명령어 추가
`package.json`에 가면 scripts 항목이 있다. 그곳에 아래 명령어를 추가한다.

    "deploy": "gridsome build && gh-pages -d dist"

해당 명령어를 실행하면,

    npm run deploy

dist 폴더가 생성되고 프로젝트가 빌드된다.  
빌드 결과물은 gh-pages 에 자동으로 푸쉬, 연결된다.

배포 후 몇 초 기다린 다음 설정한 2에서 설정한 url로 이동하면 반영된 화면을 볼 수 있다.

---

세팅하면서, [아주 정리가 잘 되어있는 블로그 글](https://perade.github.io/blog/make-blog-with-gridsome-2nd/)이 있어 큰 도움을 받았다. 감사합니다...😍
