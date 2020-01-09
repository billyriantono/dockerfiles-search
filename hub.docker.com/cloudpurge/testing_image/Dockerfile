FROM ubuntu:xenial
MAINTAINER Anatoly Litovsky <anatolylit@gmail.com>
MAINTAINER Yair Zaslavsky <yair.zaslavsky@gmail.com>
ENV container docker

RUN apt-get clean && apt-get update
RUN apt-get install -y git npm python python3 python-pip python3 python3-pip pyflakes3 pyflakes
RUN ln -s /usr/bin/nodejs /usr/bin/node
RUN pip install pep8 ansible-lint
RUN npm install -g dockerlint
