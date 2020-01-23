FROM debian:buster-slim

MAINTAINER EgoFelix <docker@egofelix.de>

COPY cleanup.sh /root/cleanup.sh
COPY adduser.sh /root/adduser.sh
COPY package.sh /root/package.sh
COPY supervisor.sh /root/supervisor.sh

RUN /root/package.sh supervisor
#RUN /root/package.sh software-properties-common
#RUN apt-add-repository non-free
#RUN apt-add-repository contrib
RUN rm -rf /etc/supervisor
RUN rm -rf /etc/supervisor.d
RUN mkdir -p /etc/supervisor.d

COPY supervisord.conf /etc/supervisord.conf

RUN rm -rf /var/lib/apt/lists/*

ENTRYPOINT /usr/bin/supervisord --nodaemon --configuration /etc/supervisord.conf
