FROM ubuntu:14.04

MAINTAINER Daniel Holzmann <daniel@codelovers.at>

RUN apt-get update -qq
RUN apt-get upgrade -y -qq
RUN apt-get install -y -qq tar

# install Symfony app
COPY www.tar.gz /
WORKDIR /
RUN tar -xvzf www.tar.gz
RUN rm -f /www.tar.gz

RUN chmod -R 777 /www/app/cache
RUN chmod -R 777 /www/app/logs

ADD info.php /www/web/info.php
RUN chmod 777 /www/web/info.php

VOLUME /www
