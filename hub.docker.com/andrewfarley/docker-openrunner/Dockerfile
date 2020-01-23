FROM ubuntu:latest
ENV LC_ALL C
ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN true

RUN apt-get update 
RUN apt-get install -y software-properties-common curl
RUN add-apt-repository ppa:ubuntu-mozilla-daily/ppa -y
RUN apt-get update 
RUN apt-get install -y firefox-trunk 
RUN rm -rf /var/lib/apt/lists/*
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs
RUN npm install --global openrunner
