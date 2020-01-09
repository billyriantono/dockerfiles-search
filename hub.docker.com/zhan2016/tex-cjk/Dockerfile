FROM ubuntu:16.04
MAINTAINER Zhan.Shi <g.shizhan.g@gmail.com>
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -q && apt-get install -qy python-software-properties software-properties-common
RUN apt-add-repository ppa:texlive-backports/ppa
RUN apt-get install -qy texlive-base texlive-xetex texlive-lang-cjk cjk-latex latex-cjk-all
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

VOLUME /documents
WORKDIR /documents

CMD ["/sbin/init"]
