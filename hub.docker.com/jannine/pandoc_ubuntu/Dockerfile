FROM ubuntu:16.04

# https://docs.docker.com/engine/reference/builder/#label
LABEL maintainer="william" version="v0.2" description="this is ubunut and pandoc for markdown and latex env"

ENV TZ="Asia/Taipei"
# switch mirror site to nchc
RUN sed -i 's/archive.ubuntu.com/free.nchc.org.tw/g' /etc/apt/sources.list
# set timezone
RUN apt update && apt install tzdata -y && rm /etc/localtime && echo $TZ > /etc/timezone  && \
    ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && \
    dpkg-reconfigure --frontend noninteractive tzdata
RUN apt update && apt install -y -o Acquire::Retries=10 --no-install-recommends pandoc \
    texlive-latex-base \
    texlive-xetex latex-xcolor \
    texlive-math-extra \
    texlive-latex-extra \
    texlive-fonts-extra \
    texlive-bibtex-extra \
    fontconfig \
    lmodern fonts-arphic-ukai texlive-xetex

# define dir path that available to mount
VOLUME ["/data"]

WORKDIR /data
