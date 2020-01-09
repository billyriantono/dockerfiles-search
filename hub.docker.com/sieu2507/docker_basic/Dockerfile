FROM ubuntu:18.04
MAINTAINER DoSieu<duongdosieu@gmail.com>
# Update ubuntu
RUN apt-get update

# Install nginx
RUN apt-get install -y nginx

# Set time zone
ENV TZ=Asia/Ho_Chi_Minh
RUN set -x \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && echo $TZ > /etc/timezone
    
# Install php
RUN apt-get install -y php

WORKDIR /venv

COPY start.sh /venv

RUN chmod a+x /venv/*

ENTRYPOINT ["/venv/start.sh"]

EXPOSE 80