FROM ubuntu:14.04
MAINTAINER Perlan Cloud <perlancloud@gmail.com>

RUN apt-get -qyy update
RUN apt-get -qyy install rsyslog

CMD rsyslogd -n

VOLUME /dev
VOLUME /var/log

