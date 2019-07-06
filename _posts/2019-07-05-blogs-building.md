---
layout: post
title: Jekyll 搭建 Github Pages 个人博客

date: 2019-07-05 21:11:11.000000000 +09:00
tags: Jekyll Github 
---

***
## Git commands to update online pages:


```
git add --all
git commit -m "First Push"
git push -u origin master
```

***
## Local repository sets & edits:

### 1. Install jekyll
```
brew install ruby
gem install jekyll bundler
```

### 2. Init the repository & start local web pages

#### 2.1 cd to github pages path & init:
```
jekyll new . --force
```
#### 2.2 then start local web pages:
```
bundle exec jekyll serve
```
#### 2.3 visit the blogs locally at 127.0.0.1:4000 .

### 3. Markdown files 
#### 3.1 file name:
```
年-月-日-标题.markdown
```
#### 3.2 page head:
```
---
layout: post
title: Blogging Like a Hacker
date: 2019-07-05 20:11:11.000000000 +09:00
tags: Jekyll Github 
---
```
