FROM centos:6
LABEL maintainer="Mario David <mariojmdavid@gmail.com>"

RUN yum -y update && \
    yum -y install epel-release && \
    mkdir -p /home/udocker 

RUN yum -y update && \
    yum -y install curl git wget tar python34 && \
    curl -O https://bootstrap.pypa.io/get-pip.py && \
    python3 get-pip.py && \
    pip install setuptools && \
    pip install pyinstaller && \
    pip install click

WORKDIR /home/udocker

