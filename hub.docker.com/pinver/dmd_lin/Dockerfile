FROM ubuntu:16.04

RUN apt-get update && apt-get install -y wget \
  && wget http://master.dl.sourceforge.net/project/d-apt/files/d-apt.list -O /etc/apt/sources.list.d/d-apt.list \
  && apt-get update \
  && apt-get -y --allow-unauthenticated install --reinstall d-apt-keyring \
  && apt-get update

RUN apt-get update && apt-get install -y dmd-bin

CMD ["dmd"]
