---
title: vue-disqus를 이용해 Gridsome 블로그에 댓글 시스템을 달아보자
date: 2021-07-02
tags:
  - gridsome
  - vue-disqus
published: true
category: blog
---

조금씩 블로그 세팅을 덧붙여가고 있다.  
이번에는 [VueDisqus](https://github.com/ktquez/vue-disqus)를 이용해 블로그에 댓글을 달아보았다.

## vue-disqus
Gridsome 공식 문서에 보면, vue-disqus를 이용해 댓글 시스템을 다는 방법에 대한 설명이 잘 나와있다.  
https://gridsome.org/docs/guide-comments/  ← 참고한 Gridsome 문서이다. 보며 설치할 것을 추천.

사실 vue-disqus 넣는 것도 방식이 어렵지 않고 아주 깔끔하다!

## 설치하기
### 1. Disqus 가입하기.
먼저 **Disqus**에 가입해야 한다.   
https://disqus.com/ 에 들어간 뒤, 가입하면 된다. 가입 후   
- 'Get Started' 버튼을 누르고, 
- 'I want to install Disqus on my site'를 누른 뒤 
- Website Name을 입력해주고 
- 'Create Site' 버튼까지 눌러주면
기본적으로 필요한 준비가 모두 끝난다.

이 과정에 대해 https://devinlife.com/howto%20github%20pages/blog-disqus/ 이 글이 아주 상세하게 설명하고 있어 참고하였다.

### 2. vue-disqus 설치하기
내 블로그 프로젝트에 `vue-disqus`를 설치한다.

    npm install vue-disqus

### 3. 프로젝트에 vue-disqus 임포트하기
프로젝트 내의 `main.js` 로 간다. 아래의 코드를 추가한다.

    import VueDisqus from 'vue-disqus'

    export default function (Vue, { head }) {
    Vue.use(VueDisqus)
    }

그러면 사용할 준비도 끝났다! 😊

## Disqus를 레이아웃에 넣어보자
위의 과정을 마치면 프로젝트 어디에서든 Disqus 컴포넌트를 삽입해 사용할 수 있다.  
컴포넌트의 사용법은 아래와 같다.

    <Disqus shortname="mygridsomesite" :identifier="$page.post.title" />

shortname에는 Disqus에서 Website Name을 적었을 때 만들어진 단어를 넣으면 된다.  
아래에 'Your unique disqus URL will be: ...' 라고 친절하게 알려준다.

나의 경우는 글의 레이아웃 컴포넌트인 Post.vue 파일의 템플릿 내에 아래와 같이 추가했다.


    <div class="post-comments">
        <Disqus 
          shortname="https-makepin2r-github-io-blog" 
          :identifier="$page.post.title" 
        />
    </div>

조금씩 블로그 형태를 갖춰나가는 게 아주 재밌다.