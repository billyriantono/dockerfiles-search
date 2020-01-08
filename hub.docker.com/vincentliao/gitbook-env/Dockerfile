FROM ubuntu:16.04
MAINTAINER vincentliao@gmail.com

RUN apt-get -y update
RUN apt-get -y install default-jre
RUN apt-get -y install nodejs
RUN apt-get -y install graphviz
RUN apt-get -y install npm
RUN apt-get -y install curl
RUN apt-get -y install git

RUN apt-get -y install language-pack-zh-hant
ENV LC_ALL zh_TW.utf8

ENV TZ Asia/Taipei

RUN npm install -g n
RUN n stable
RUN npm install -g gitbook-cli
RUN npm install -g gitbook-plugin-plantuml-svg
RUN npm install -g binwin20/gitbook-plugin-plantuml.git
RUN gitbook install latest




CMD ["/bin/bash"]
