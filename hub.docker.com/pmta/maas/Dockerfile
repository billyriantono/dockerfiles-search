FROM ubuntu:18.04

ENV LC_ALL=C.UTF-8 
# ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Europe/Helsinki

WORKDIR /

RUN ln -snf /usr/share/zoneinfo/${TZ} /etc/localtime && echo ${TZ} > /etc/timezone

RUN DEBIAN_FRONTEND=noninteractive apt-get update -y
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y maas


CMD sh

EXPOSE 5240

