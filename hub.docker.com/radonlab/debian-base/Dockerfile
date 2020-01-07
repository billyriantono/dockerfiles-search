FROM debian:stretch-slim

LABEL maintainer="skyler.ac.lee@gmail.com"

RUN sed -i.save "s@http://[a-z]*.debian.org@http://mirrors.aliyun.com@g" /etc/apt/sources.list \
    && apt-get update \
    && apt-get install -y apt-transport-https \
    && rm -rf /var/lib/apt/lists/* \
    && sed -i "s@http:@https:@g" /etc/apt/sources.list
