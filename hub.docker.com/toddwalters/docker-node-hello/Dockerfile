# Originally forked from: git@github.com:gasi/docker-node-hello.git

FROM node:0.10

#ENV http_proxy http://40.0.40.10:9000
#ENV https_proxy http://40.0.40.10:9000

MAINTAINER Todd Walters <junk4walters@gmail.com>

#USER root

ENV AP /data/app
ENV SCPATH /etc/supervisor/conf.d

RUN apt-get -y update

# The daemons
RUN apt-get -y install supervisor
RUN mkdir -p /var/log/supervisor

# Supervisor Configuration
ADD ./supervisord/conf.d/* $SCPATH/

# Application Code
ADD *.js* $AP/

WORKDIR $AP

RUN npm install

CMD ["supervisord", "-n"]

EXPOSE 8080
