FROM ubuntu:xenial
MAINTAINER Douglas De Rizzo Meneghetti <douglasrizzom@gmail.com>
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -q && apt-get install -qy \
    make git \
    texlive-full biber texlive-publishers texlive-lang-portuguese texlive-latex-extra texlive-fonts-recommended \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get autoclean
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /data
VOLUME ["/data"]
