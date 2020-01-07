FROM library/debian:wheezy
MAINTAINER Radha Montell <radha.montell@gmail.com>
#El canvi de nameserver només ens cal a l'Esteve Terradas
RUN apt-get update && \
apt-get -y upgrade && \
apt-get install -y funny-manpages man-db manpages && \
apt-get clean && apt-get autoclean && \
  rm -rf /var/lib/apt/lists/* 

