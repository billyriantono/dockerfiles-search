FROM ubuntu:trusty

WORKDIR /app

RUN apt-get update
RUN apt-get install -y software-properties-common
RUN add-apt-repository -y ppa:builds/sphinxsearch-rel22
RUN apt-get update
RUN apt-get install -y sphinxsearch

EXPOSE 9312
