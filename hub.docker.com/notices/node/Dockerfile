from node:8.11
MAINTAINER hushuang<hushuang123a@gmail.com>

RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    #yarn config set registry http://registry.npm.taobao.org && \
    #yarn config set disturl https://npm.taobao.org/dist && \
    #yarn config set sass_binary_site https://npm.taobao.org/mirrors/node-sass/ && \
    #yarn config set electron_mirror https://npm.taobao.org/mirrors/electron/ && \
    #yarn config set phantomjs_cdnurl http://cnpmjs.org/downloads && \
    mv /etc/apt/sources.list /etc/apt/sources.list.bak && \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo "deb http://mirrors.163.com/debian/ jessie main non-free contrib" >/etc/apt/sources.list && \
    echo "deb http://mirrors.163.com/debian/ jessie-proposed-updates main non-free contrib" >>/etc/apt/sources.list && \
    echo "deb-src http://mirrors.163.com/debian/ jessie main non-free contrib" >>/etc/apt/sources.list && \
    echo "deb-src http://mirrors.163.com/debian/ jessie-proposed-updates main non-free contrib" >>/etc/apt/sources.list && \
    apt-get update && apt-get install -y vim curl && \
    yarn global add pm2 webpack
