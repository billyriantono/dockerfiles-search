# FROM node:11.7.0-alpine
FROM node:10.15.3-alpine
LABEL maintainer "jiashuai <leaderjs@live.com>"

# chromedriver
ENV CR_E5 2.46

# node_sass 
ENV NS_E5 4.9.0

# ENV NS_A 4.11.0

RUN mkdir /tmp/${CR_E5} \
    mkdir /tmp/${NS_E5}

# mkdir /tmp/${NS_A}

# ADD为什么不解压？？？ 
# nodejs version 11.7 对应 node module 为 67
# nodejs 和 node module 对应关系
# https://nodejs.org/zh-cn/download/releases/#ref-1
ADD http://cdn.npm.taobao.org/dist/chromedriver/${CR_E5}/chromedriver_linux64.zip /tmp/${CR_E5}
ADD https://github.com/sass/node-sass/releases/download/v${NS_E5}/linux-x64-67_binding.node /tmp/${NS_E5}
# ADD https://github.com/sass/node-sass/releases/download/${NS_A}/linux-x64-47_binding.node /tmp/${NS_A}
# ADD https://github.com/sass/node-sass/releases/download/${NS_5}/linux-x64-47_binding.node /tmp/${NS_5}