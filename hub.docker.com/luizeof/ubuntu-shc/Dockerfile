FROM ubuntu:latest

RUN apt-get update

RUN apt-get install -y sudo software-properties-common gcc

RUN sudo add-apt-repository -y ppa:neurobin/ppa

RUN sudo apt-get update

RUN sudo apt-get install shc

COPY build-shc.sh /usr/local/bin/build-shc

RUN chmod +x /usr/local/bin/build-shc

RUN mkdir /shc-data

VOLUME /shc-data

WORKDIR /shc-data

CMD tail -f
