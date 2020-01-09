FROM ubuntu:14.04
MAINTAINER Ping Dong (ping.dong@live.com)

RUN apt-get update
RUN apt-get -y dist-upgrade

RUN apt-get -y install apache2
RUN apt-get -y install openssh-server
RUN apt-get -y install supervisor

copy supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 22 80

CMD ["/user/bin/supervisord"]