FROM python:slim

MAINTAINER WANG XIAOWEI & LI YANZHE

WORKDIR /usr/src/app

ADD ./IOC ./IOC

WORKDIR IOC

RUN apt -y update \
    && apt -y upgrade \
    && apt -y install nodejs \
    && pip install -U pip \
    && pip install -U requests[socks] \
    && pip install -r requirements.txt

