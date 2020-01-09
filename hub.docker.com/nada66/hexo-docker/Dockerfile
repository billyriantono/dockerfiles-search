FROM node:latest
MAINTAINER NadaLiu <lzj12530@sina.com>
RUN npm install
# install hexo
RUN npm install hexo-cli -g
# install hexo server
RUN npm install hexo-server
RUN npm install hexo-deployer-git
# 挂载 volume
VOLUME ["/hexo"]
# set home dir
WORKDIR /hexo
EXPOSE 4000