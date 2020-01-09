FROM centos:latest
MAINTAINER Koi "akillcool@live.com"

RUN yum update && \
    yum install -y \
    unzip \
    wget

ENV MOTHUR_VERSION 1.38.1

RUN mkdir /mothur
WORKDIR /mothur

RUN wget https://github.com/mothur/mothur/releases/download/v$MOTHUR_VERSION.1/Mothur.linux_64.zip \
     -O /mothur/mothur.zip && \
    unzip /mothur/mothur.zip && rm /mothur/mothur.zip

WORKDIR /mothur/mothur

ENTRYPOINT ["/mothur/mothur/mothur"]

