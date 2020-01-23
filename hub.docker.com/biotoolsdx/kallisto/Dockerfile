FROM ubuntu:16.04
MAINTAINER CHEN, Yuelong <yuelong.chen.btr@gmail.com>

ARG kallisto_version=v0.46.1

RUN apt update && apt install -y wget

RUN cd /tmp/ \
    && wget https://github.com/pachterlab/kallisto/releases/download/${kallisto_version}/kallisto_linux-${kallisto_version}.tar.gz \
    && tar -zxvf kallisto_linux-${kallisto_version}.tar.gz \
    && cp kallisto/kallisto /usr/local/bin

RUN rm -rf /tmp/*

CMD bash