FROM mongo:latest
LABEL maintainer "Satoshi Murashige <murashige.satoshi.mi1 [at] is.naist.jp"

RUN apt-get -y update --fix-missing && apt-get -y upgrade
RUN apt-get install -y sudo wget bzip2 git vim cmake xserver-xorg-dev libgl1-mesa-dev unzip && \
    apt-get install -y python3 python3-pip && \
    update-alternatives --install /usr/bin/python python /usr/bin/python3 10 &&\
    update-alternatives --install /usr/bin/pip    pip    /usr/bin/pip3    10

