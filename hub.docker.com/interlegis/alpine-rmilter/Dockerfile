FROM rawmind/alpine-monit:0.5.20-4
MAINTAINER Fabio Rauber <fabiorauber@gmail.com>

RUN echo "@testing http://nl.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories \
 && apk add --no-cache rmilter@testing rsyslog

COPY rmilter.conf /etc/rmilter.conf
COPY rsyslog.conf /etc/rsyslog.conf
COPY monit-service.conf /opt/monit/etc/conf.d 

EXPOSE 9900
