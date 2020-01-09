FROM debian:buster-slim
LABEL maintainer="Mattia Monga <monga@debian.org>"
USER root
ENV DEBIAN_FRONTEND=noninteractive
ENV REPO=http://cdn-fastly.deb.debian.org
RUN echo "deb $REPO/debian buster main\
  deb $REPO/debian-security buster/updates main" > /etc/apt/sources.list &&\
  apt-get -yq update && apt-get install -yq eatmydata &&\
  eatmydata apt-get -yq upgrade &&\
  eatmydata apt-get -yq install texlive-full python3-pygments xindy \
  git emacs elpa-org auctex pandoc &&\
  eatmydata apt-get clean && rm -rf /var/lib/apt/*
RUN useradd -ms /bin/bash knuth
USER knuth
WORKDIR /home/knuth
