FROM ubuntu:xenial
MAINTAINER <Chris Hubbard> "chris_hubbard@sil.org"

ENV REFRESHED_AT 2017-05-02

RUN apt-get update && apt-get install -y\
  wget\
  lsb-release\
  software-properties-common\
  python-software-properties

RUN wget -qO - http://packages.sil.org/sil.gpg | apt-key add -
RUN add-apt-repository "deb http://packages.sil.org/ubuntu $(lsb_release -sc) main"
RUN add-apt-repository "deb http://packages.sil.org/ubuntu $(lsb_release -sc)-experimental main"
RUN apt-get update 
