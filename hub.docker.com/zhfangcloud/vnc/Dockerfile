FROM dorowu/ubuntu-desktop-lxde-vnc
MAINTAINER Zhihao Fang <zhfang@dataman-inc.com>

COPY sources.list /etc/apt/sources.list

RUN apt-get update \
    && apt-get install -y vim git wget \
    && easy_install robotframework \
    && easy_install robotframework-selenium2library \
    && cd /usr/local/bin \
    && wget https://github.com/mozilla/geckodriver/releases/download/v0.10.0/geckodriver-v0.10.0-linux64.tar.gz \
    && tar -xzvf geckodriver-v0.10.0-linux64.tar.gz \
    && rm -rf geckodriver-v0.10.0-linux64.tar.gz \
    && apt-get autoclean \
    && apt-get autoremove \
    && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && rm -rf /var/lib/apt/lists/*

ENV DISPLAY=localhost:1

