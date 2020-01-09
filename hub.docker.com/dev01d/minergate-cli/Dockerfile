FROM ubuntu:16.04

LABEL Description="Containerized crypto miner based on Ubuntu and the minergate cli" \
  tags="latest 1.0.0" \
  maintainer='dev01d <http://github.com/dev01d>'

ENV MINER_BIN="https://minergate.com/download/ubuntu-cli"

RUN \
  echo "**** Install Packages ****" \
  && apt-get update -qq > /dev/null \
  && apt-get upgrade -qq -y > /dev/null \ 
  && apt-get install -qq -y curl libxcb1 libpcre16-3 > /dev/null 

RUN \
  echo "**** Install Miner Binary ****" \
  && curl -o /tmp/minergate.deb -L "${MINER_BIN}" \ 
  && dpkg -i /tmp/minergate.deb

RUN \
  echo "**** Clean Up install ****" \
  rm -rf /tmp/*

ENTRYPOINT ["minergate-cli"]
