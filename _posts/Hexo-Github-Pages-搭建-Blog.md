---
title: Hexo Github Pages 搭建 Blog
date: 2020-03-28 18:32:52
tags: [Hexo, Github Pages, Blog]
categorys: [Hexo]
---

### 安装工具

1. install nodejs `brew install node`
2. install hexo `npm i hexo -g`

### 查看 hexo 版本

```
 mz@Mz  ~  node --version
v13.11.0
 mz@Mz  ~  npm --version
6.14.4
 mz@Mz  ~  hexo -verison
hexo-cli: 3.1.0
os: Darwin 19.3.0 darwin x64
node: 13.11.0
v8: 7.9.317.25-node.29
uv: 1.34.2
zlib: 1.2.11
brotli: 1.0.7
ares: 1.15.0
modules: 79
nghttp2: 1.40.0
napi: 6
llhttp: 2.0.4
openssl: 1.1.1d
cldr: 35.1
icu: 64.2
tz: 2019a
unicode: 12.1
```

### 常用命令

1. hexo clean
2. hexo g
3. hexo s
4. hexo d

### 本地调试

1. hexo g #生成
2. hexo s #启动本地服务，进行文章预览调试
3. hexo d -g #或者直接作用组合命令
